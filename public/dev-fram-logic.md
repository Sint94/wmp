# Logical layer (App Service)

The logical layer of the Mini Program development framework has been written using JavaScript.

After the logical layer has processed data it sends it to the view layer, at the same time as receiving event feedback from the view layer. We have made a few modifications on a JavaScript base to make it easy to develop Mini Programs.

- The [App](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/app#app-) and [Page](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/page#page-) methods have been added to perform program and page registration.
- The getApp and getCurrentPages methods have been added, these are used to get App instances and the current page stack, respectively.
- A wide range of [APIs](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/index#api_index) have been provided, including unique WeChat capabilities such as WeChat user data, QR code scanning, and payment.
- Every page has an independent [scope](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/module#app-service_module%20and%20provides%20[modularization](/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/module#modularization) capabilities.
- As the framework does not run in the browser, some of JavaScript's web capabilities cannot be used, such as document and window.
- All code written by developers will ultimately be packaged in JavaScript and run from when the Mini Program is launched until it is removed. The logical layer is also known as App Service due to its similarity to ServiceWorker.

## App

### App()

The `App()` function is used to register a Mini Program. When it receives an object parameter, it specifies the Mini Program's lifecycle functions, etc.

**Object parameter descriptions:**

| Attribute | Type     | Description                                               | When triggered                                               |
| --------- | -------- | --------------------------------------------------------- | ------------------------------------------------------------ |
| onLaunch  | Function | Lifecycle function - monitors Mini Program initialization | onLaunch will be triggered when a Mini Program has completed initialization (only triggered once globally) |
| onShow    | Function | Lifecycle function - monitors Mini Program display        | onShow will be triggered when a Mini Program starts up, or enters the foreground from the background |
| onHide    | Function | Lifecycle function - monitors Mini Program hiding         | onHide will be triggered when a Mini Program enters the background from the foreground |
| onError   | Function | Error monitoring function                                 | onError will be triggered when a Mini Program script error occurs, or an api call is unsuccessful, and brings an error message |
| Other     | Any      |                                                           | Developers can add any functions or data to the object parameters and use `this` to access them |

**Foreground and background definitions:** When the user taps the top left corner to close WeChat, or presses the device's home button to leave WeChat, the Mini Program will not be removed directly but will enter the background. When WeChat is entered again or the Mini Program is opened again, the Mini Program will enter the foreground from the background. The following needs to be noted: a Mini Program will only really be removed if it enters the background for a certain amount of time, or too many system resources are being used.

**Closing Mini Programs (support beginnig with common library version 1.1.0):** When a user enters a Mini Program by scanning a QR Code or from shared access ([scene value](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/scene#app-service_scene) is 1007, 1008, 1011, or 1025), and exits when there is no Sticky on Top Mini Program situation, the Mini Program will be removed.

**Sample code:**

```js
App({
  onLaunch: function(options) {
    // Do something initial when launch.
  },
  onShow: function(options) {
      // Do something when show.
  },
  onHide: function() {
      // Do something when hide.
  },
  onError: function(msg) {
    console.log(msg)
  },
  globalData: 'I am global data'
})
```

### onLaunch and onShow parameters

| Field       | Type   | Description                                                  |
| ----------- | ------ | ------------------------------------------------------------ |
| path        | String | Opens Mini Program path                                      |
| query       | Object | Opens Mini Program query                                     |
| scene       | Number | Opens Mini Program scene value                               |
| shareTicket | String | shareTicket, refer to [Get More Information on Forwarding](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/share#get-more-forwarding-information) for more details |

Scene value [Refer to](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/scene) for more details.

### getApp()

We have provided a global `getApp()` function that can get Mini Program instances.

```javascript
// other.js
var appInstance = getApp()
console.log(appInstance.globalData) // I am global data
```

**Note:**

`App()` must be registered in `app.js` and multiple apps cannot be registered.

Do not call `getApp()` from a function within the `App()`, you can use `this` to get app instances.

Do not call `getCurrentPage()` when in onLaunch, this page has not been generated yet.

After using `getApp()` to get an instance, do not call the lifecycle function without authorization.



## Scene values

The currently supported scene values are:

| Scene value ID | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| 1001           | Discovery bar Mini Program main access                       |
| 1005           | Top search box search results page                           |
| 1006           | Discovery bar Mini Program main access search box search results page |
| 1007           | Mini Program message card in single chat session             |
| 1008           | Mini Program message card in group chat session              |
| 1011           | Scan QR code                                                 |
| 1012           | Press and hold image to identify QR code                     |
| 1013           | QR code selected from phone album                            |
| 1014           | Mini Program template message                                |
| 1017           | Go to experience version entry page                          |
| 1019           | WeChat Wallet                                                |
| 1020           | Mini Program list related to official account profile page   |
| 1022           | Mini Program access at top of chat list                      |
| 1023           | Android system desktop icon                                  |
| 1024           | Mini Program profile page                                    |
| 1025           | Scan one-dimensional code                                    |
| 1028           | My card pack                                                 |
| 1029           | Card details page                                            |
| 1031           | Press and hold image to identify one-dimensional code        |
| 1032           | One-dimensional code selected from phone album               |
| 1034           | WeChat payment completion page                               |
| 1035           | Official account custom-defined menu                         |
| 1036           | App sharing message card                                     |
| 1042           | Add friends search box search results page                   |
| 1043           | Official account templated message                           |
| 1044           | Mini Program message card in group chat session (with shareTicket) |
| 1047           | Scan Mini Program code                                       |
| 1048           | Press and hold image to identify Mini Program code           |
| 1049           | Mini Program code selected from phone album                  |

Can be obtained in App's `onLaunch` and `onShow`. [More details](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/app)

**Tip:** Due to the limitations of the Android system, the home button currently cannot be used to exit to desktop, then re-enter the Mini Program scene values from the desktop. In this situation, the scene values from the previous time will be maintained.



## Page

### Page()

The `Page()` function is used to register a page. When it receives an object parameter, it specifies the initialization data, lifecycle functions, and event processing functions for a page.

**Object parameter descriptions:**

| Attribute                                                    | Type     | Description                                                  |
| ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| [data](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/page#initialization-data) | Object   | Page initialization data                                     |
| onLoad                                                       | Function | Lifecycle function - monitors page loading                   |
| onReady                                                      | Function | Lifecycle function - monitors completion of initial page rendering |
| onShow                                                       | Function | Lifecycle function - monitors page display                   |
| onHide                                                       | Function | Lifecycle function - monitors page hiding                    |
| onUnload                                                     | Function | Lifecycle function - monitors page unloading                 |
| onPullDownRefresh                                            | Function | Page-related event processing function - monitors user pull down actions |
| onReachBottom                                                | Function | Processing function for scrolling to bottom and pulling up events |
| onShareAppMessage                                            | Function | User taps top right corner to forward                        |
| Other                                                        | Any      | Developers can add any functions or data to the object parameters and use `this` to access them in the page functions |

**Sample code:**

```javascript
//index.js
Page({
  data: {
    text: "This is page data."
  },
  onLoad: function(options) {
    // Do some initialize when page load.
  },
  onReady: function() {
    // Do something when page ready.
  },
  onShow: function() {
    // Do something when page show.
  },
  onHide: function() {
    // Do something when page hide.
  },
  onUnload: function() {
    // Do something when page close.
  },
  onPullDownRefresh: function() {
    // Do something when pull down.
  },
  onReachBottom: function() {
    // Do something when page reach bottom.
  },
  onShareAppMessage: function () {
   // return custom share data when user share.
  },
  // Event handler.
  viewTap: function() {
    this.setData({
      text: 'Set some data for updating view.'
    })
  },
  customData: {
    hi: 'MINA'
  }
})
```

### Initialization data

The initialization data will be used for the first rendering of a page. The data will be transferred from the logical layer to the rendering layer in JSON form, so it must be able to be converted into JSON format: strings, numbers, booleans, objects, and arrays.

The rendering layer can use [WXML](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/index) to bind the data.

**Sample code:**

```html
<view>{{text}}</view>
<view>{{array[0].msg}}</view>
Page({
  data: {
    text: 'init data',
    array: [{msg: '1'}, {msg: '2'}]
  }
})
```

### Lifecycle function

- `onLoad`: Page loading
  - Will only be called once per page. The query parameters called to open the current page can be obtained in onLoad.
- `onShow`: Page display
  - Will be called once every time a page is opened.
- `onReady`: Completion of initial page rendering
  - Will only be called once per page. Indicates that the page is ready and can interact with the view layer.
  - Please set interface settings such as `wx.setNavigationBarTitle` after `onReady` has been called. Refer to [Lifecycle](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/page#lifecycle) for more details.
- `onHide`: Page hiding
  - Called when `navigateTo` or bottom `tab` are toggled.
- `onUnload`: Page unloading
  - Called when `redirectTo` or `navigateBack` are used.

[Refer to Routing](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/route) for more details on lifecycle calls and page route methods.

**onLoad parameters**

| Type   | Description                                                  |
| ------ | ------------------------------------------------------------ |
| Object | The query parameters called for other pages to open the current page |

### Page-related event processing functions

- ```
  onPullDownRefresh
  ```

  : Pull down refresh

  - Monitors user pull down refresh events.
  - `enablePullDownRefresh` needs to be activated from the `config` [`window`](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/config#window) option.
  - After the data refresh has been processed, [`wx.stopPullDownRefresh`](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/pulldown#wx-stoppulldownrefresh) can stop the pull down refresh on the current page.

- ```
  onShareAppMessage
  ```

  : User forwarding

  - The menu in the top right corner will only display the Forward button if the processing function for this event has been defined.
  - It will be called when a user clicks on the Forward button.
  - This event needs to return an object, the user can customize the content to be forwarded.

**Custom forwarding fields**

| Field | Description      | Default value                                                |
| ----- | ---------------- | ------------------------------------------------------------ |
| title | Forwarding title | Current Mini Program name                                    |
| path  | Forwarding path  | Current page path, must be a full path with a / at the beginning |

**Sample code**

```javascript
Page({
  onShareAppMessage: function () {
    return {
      title: 'Custom forwarding title',
      path: '/page/user?id=123'
    }
  }
})
```

### Event processing functions

In addition to initialization data and lifecycle functions, some special functions can also be defined in Page: event processing functions. [Event Binding](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event) can be added to components in the rendering layer. It will execute the event processing functions defined in Page when an event is triggered.

**Sample code:**

```html
<view bindtap="viewTap"> click me </view>
Page({
  viewTap: function() {
    console.log('view tap')
  }
})
```

### Page.prototype.setData()

`The setData` function is used to send data from the logical layer to the view layer, while changing the corresponding `this.data` values.

### setData() parameter formats

When an object received is expressed in key or value form, it changes the values corresponding to keys in this.data into values.

Keys can be very flexible and provided in data path form, such as `array[2].message` or `a.b.c.d`. They also do not need to be predefined in this.data.

**Note:**

1. **Directly modifying this.data without calling this.setData will not change the page status and will also cause data inconsistency.**
2. **The data set on a single occasion cannot exceed 1024kB, please try to avoid setting too much data at once**.

**Sample code:**

```html
<!--index.wxml-->
<view>{{text}}</view>
<button bindtap="changeText"> Change normal data </button>
<view>{{num}}</view>
<button bindtap="changeText"> Change normal num </button>
<view>{{array[0].text}}</view>
<button bindtap="changeItemInArray"> Change Array data </button>
<view>{{object.text}}</view>
<button bindtap="changeItemInObject"> Change Object data </button>
<view>{{newField.text}}</view>
<button bindtap="addNewField"> Add new data </button>
//index.js
Page({
  data: {
    text: 'init data',
    num: 0,
    array: [{text: 'init data'}],
    object: {
      text: 'init data'
    }
  },
  changeText: function() {
    // this.data.text = 'changed data'  // bad, it can not work
    this.setData({
      text: 'changed data'
    })
  },
  changeNum: function() {
    this.data.num = 1
    this.setData({
      num: this.data.num
    })
  },
  changeItemInArray: function() {
    // you can use this way to modify a danamic data path
    this.setData({
      'array[0].text':'changed data'
    })
  },
  changeItemInObject: function(){
    this.setData({
      'object.text': 'changed data'
    });
  },
  addNewField: function() {
    this.setData({
      'newField.text': 'new data'
    })
  }
})
```

**You do not need to fully understand the following content all at once, but it will be helpful later on.**

### Lifecycle

The figure below illustrates the lifecycle of a Page instance.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/framework/app-service/mina-lifecycle.png)



## Page routes

The routes for all pages in a Mini Program are managed by the framework.

### Page stacks

The framework maintains all current pages in stack form. When route switching occurs, the page stack will behave as follows:

| Route method   | Page stack behavior                                          |
| -------------- | ------------------------------------------------------------ |
| Initialization | New page is stacked                                          |
| Open new page  | New page is stacked                                          |
| Page redirect  | Current page popped from stack, new page is stacked          |
| Page back      | Pages are continuously popped from stack until the target page is returned to, new pages are stacked |
| Tab switch     | All pages are popped from stack with just a new tab page left behind |
| Reload         | All pages are popped from stack with just a new page left behind |

### getCurrentPages()

`The getCurrentPages()` function is used to get an instance of the current page stack, which is given in array form in stack order. The first element is the homepage and the last element is the current page.

**Tip: Do not try to modify the page stack, this will cause route and page status errors.**

### Route methods

The route trigger methods and page lifecycle functions are as follows:

| Route method   | When triggered                                               | First page of route | Last page of route                                     |
| -------------- | ------------------------------------------------------------ | ------------------- | ------------------------------------------------------ |
| Initialization | The first page of the Mini Program is opened                 |                     | onLoad, onShow                                         |
| Open new page  | API [`wx.navigateTo`](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/ui-navigate#wx-navigateto-object-) is called or component [``](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/navigator) is used | onHide              | onLoad, onShow                                         |
| Page redirect  | API [`wx.redirectTo`](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/ui-navigate#wx-redirectto-object-) is called or component [``](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/navigator) is used | onUnload            | onLoad, onShow                                         |
| Page back      | API [`wx.navigateBack`](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/ui-navigate#wx-navigateback) is called or component [``](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/navigator) is used, or user presses Back button in top left corner | onUnload            | onShow                                                 |
| Tab switch     | API [`wx.switchTab`](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/ui-navigate#wx-switchtab) is called or component [``](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/navigator) is used, or user switches Tab |                     | Please refer to the following table for each situation |
| Restart        | API [`wx.reLaunch`](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/ui-navigate#wx-relaunch) is called or component [``](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/navigator) is used | onUnload            | onLoad, onShow                                         |

Lifecycles corresponding to Tab switch (in the examples, pages A and B are the tab bar pages, C is a page opened from Page A, and page D is a page opened from page C):

| Current page             | Last page of route | Trigger lifecycle (in order)                       |
| ------------------------ | ------------------ | -------------------------------------------------- |
| A                        | A                  | Nothing happened                                   |
| A                        | B                  | A.onHide(), B.onLoad(), B.onShow()                 |
| A                        | B (reopened)       | A.onHide(), B.onShow()                             |
| C                        | A                  | C.onUnload(), A.onShow()                           |
| C                        | B                  | C.onUnload(), B.onLoad(), B.onShow()               |
| D                        | B                  | D.onUnload(), C.onUnload(), B.onLoad(), B.onShow() |
| D (entered from sharing) | A                  | D.onUnload(), A.onLoad(), A.onShow()               |
| D (entered from sharing) | B                  | D.onUnload(), B.onLoad(), B.onShow()               |

**Tips**:

- `navigateTo` and `redirectTo` can only open non-tab bar pages.
- `switchTab` can only open tab bar pages.
- `reLaunch` can open any page.
- The tab bar at the bottom of the page is determined by the page, that is, as long as a page is defined as a tab bar page, there will always be a tab bar at the bottom.
- The parameters brought when calling a page route can be obtained in `onLoad` on the target page.



## File scope

The variables and functions declared in JavaScript files are only effective in those files. Variables and functions with the same names can be declared in different files, but they will not affect each other.

The global function [`getApp()`](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/app#getapp-) can be used to get global application instances. If global data is required, it can be set in `App()`, for example:

```javascript
// app.js
App({
  globalData: 1
})
// a.js
// The localValue can only be used in file a.js.
var localValue = 'a'
// Get the app instance.
var app = getApp()
// Get the global data and change it.
app.globalData++
// b.js
// You can redefine localValue in file b.js, without interference with the localValue in a.js.
var localValue = 'b'
// If a.js it run before b.js, now the globalData should be 2.
console.log(getApp().globalData)
```

### Modularization

We can remove some public code and turn it into an independent js file to be used as a module. Modules can only expose interfaces externally via `module.exports` or `exports`.

The following needs to be noted:

- `exports` is a reference for `module.exports`, so making random modifications to the direction `exports` points towards inside a module will cause an unknown error. We therefore recommend that developers use `module.exports` to expose module interfaces, unless you already have a clear understanding of the relationship between `exports` and `module.exports`.
- Mini Programs currently do not support the introduction of `node_modules`, it is recommended that developers copy the relevant code to the Mini Program directory when they need to use `node_modules`.

```javascript
// common.js
function sayHello(name) {
  console.log(`Hello ${name} !`)
}
function sayGoodbye(name) {
  console.log(`Goodbye ${name} !`)
}

module.exports.sayHello = sayHello
exports.sayGoodbye = sayGoodbye
```

Using `require(path)` introduces public code into the files that need to use these modules.

```javascript
var common = require('common.js')
Page({
  helloMINA: function() {
    common.sayHello('MINA')
  },
  goodbyeMINA: function() {
    common.sayGoodbye('MINA')
  }
})
```



## API

The Mini Program development framework provides plenty of native WeChat APIs that make it easy to call the capabilities provided by WeChat, such as getting user information, local storage, and payment functions.

Please refer to the [API Document](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/index) for a detailed introduction.