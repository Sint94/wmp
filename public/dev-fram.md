# Framework

The objective of the Mini Program development framework is to use the simplest, most effective methods possible to enable developers to have native app experience services in WeChat's development tools.

The framework has provided its own view layer description languages, WXML and WXSS, as well as a logical layer framework based on JavaScript. It has also provided a data transfer and event system between the view layer and the logical layer which makes it easier for developers to focus on data and logic.

### Response data binding

The framework's core is a response data binding system.

The entire system is divided into two: the view layer (View) and the logical layer (App Service).

The framework is able to keep the data and views synchronized very easily. When performing data modification, the data only needs to be modified in the logical layer. The view layer will be updated accordingly.

This can be seen using this simple example:

```html
<!-- This is our View -->
<view> Hello {{name}}! </view>
<button bindtap="changeName"> Click me! </button>
// This is our App Service.
// This is our data.
var helloData = {
  name: 'WeChat'
}

// Register a Page.
Page({
  data: helloData,
  changeName: function(e) {
    // sent data change to view
    this.setData({
      name: 'MINA'
    })
  }
})
```

- The developer uses the framework to bind the `name` in the logical layer data with the view layer `name`, so that `Hello WeChat!` will be displayed when the page is opened.
- When the button is clicked on, the view layer will send a `changeName` event to the logical layer. The logical layer finds the corresponding event processing function.
- When the logical layer has executed the `setData` action, the name is changed from `WeChat` to `MINA`. Because this data has already been bound with the view layer, the view layer will automatically change to `Hello MINA!`

### Page management

The framework manages the page routes for the entire Mini Program. It can switch seamlessly between pages and give pages a complete lifecycle. Developers just need to register the page data, method, and lifecycle functions in the framework. All other complex actions are processed by the framework.

### Base components

The framework has provided a set of base components that come with WeChat's styles and specific logic. Developers can use a combination of base components to create a strong Mini Program.

### A wide range of APIs

The framework provides plenty of native WeChat APIs that can make it easy to call the capabilities provided by WeChat, such as getting user information, local storage and payment functions.

## File structure

Mini Programs contain a page that describes the overall program app and several pages that describe each page.

The main part of a Mini Program consists of the following three files, which must be put in the root directory of the project:

| File                                                         | Required | Function                       |
| ------------------------------------------------------------ | -------- | ------------------------------ |
| [app.js](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/app#app-service_app) | Yes      | Mini Program logic             |
| [app.json](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/config#framework_config) | Yes      | Mini Program public settings   |
| [app.wxss](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxss#view_wxss) | No       | Mini Program public stylesheet |

A Mini Program page consists of the following four files:

| File type                                                    | Required | Function           |
| ------------------------------------------------------------ | -------- | ------------------ |
| [js](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/page#app-service_page) | Yes      | Page logic         |
| [wxml](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/index#wxml_index) | Yes      | Page structure     |
| [wxss](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxss#view_wxss) | No       | Page stylesheet    |
| [json](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/config#page-json) | No       | Page configuration |

**Note:** To make it easier for developers to reduce the number of configuration items, the four files in our specified description pages must have the same path and filename.

## Configuration

We use an `app.json` file to perform the global configuration of WeChat Mini Programs, determine page file paths and window presentation, and set network timeouts and multiple tabs.

An `app.json` containing all the configuration options is shown below:

```json
{
  "pages": [
    "pages/index/index",
    "pages/logs/index"
  ],
  "window": {
    "navigationBarTitleText": "Demo"
  },
  "tabBar": {
    "list": [{
      "pagePath": "pages/index/index",
      "text": "Homepage"
    }, {
      "pagePath": "pages/logs/logs",
      "text": "Log"
    }]
  },
  "networkTimeout": {
    "request": 10000,
    "downloadFile": 10000
  },
  "debug": true
}
```

### app.json configuration item list

| Attribute                                                    | Type         | Required | Description                           |
| ------------------------------------------------------------ | ------------ | -------- | ------------------------------------- |
| [pages](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/config#pages) | String Array | Yes      | Sets page path                        |
| [window](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/config#window) | Object       | No       | Sets default page window presentation |
| [tabBar](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/config#tabbar) | Object       | No       | Sets bottom tab presentation          |
| [networkTimeout](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/config#networktimeout) | Object       | No       | Sets network timeout                  |
| [debug](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/config#debug) | Boolean      | No       | Sets whether to enable debug mode     |

### pages

Every item in an array that is received is a string that specifies which pages the Mini Program consists of. Each item represents the path and filename information for the corresponding page. **The first item in the array represents the first page of the Mini Program. Adding/reducing pages in the Mini Program requires the pages array to be modified.**

The filename does not need to be written in the file suffix because the framework will automatically find and integrate the path's four files: `.json`, `.js`, `.wxml`, and `.wxss`.

If the development directories are:

> pages/
>
> pages/index/index.wxml
>
> pages/index/index.js
>
> pages/index/index.wxss
>
> pages/logs/logs.wxml
>
> pages/logs/logs.js
>
> app.js
>
> app.json
>
> app.wxss

We then need to write the following in app.json

```json
{
  "pages":[
    "pages/index/index"
    "pages/logs/logs"
  ]
}
```

### window

Used to set the Mini Program's status bar, navigation bar, titles, and window background color.

| Attribute                    | Type     | Default value | Description                                                  |
| ---------------------------- | -------- | ------------- | ------------------------------------------------------------ |
| navigationBarBackgroundColor | HexColor | #000000       | Navigation bar background color, for example "#000000"       |
| navigationBarTextStyle       | String   | white         | Navigation bar title color, only supports black/white        |
| navigationBarTitleText       | String   |               | Navigation bar title text content                            |
| backgroundColor              | HexColor | #ffffff       | Window background color                                      |
| backgroundTextStyle          | String   | dark          | Pull down background font, loading image style, only supports dark/light |
| enablePullDownRefresh        | Boolean  | false         | Whether to enable pull down refresh, refer to [Page-Related Event Processing Functions](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/page#page-related-event-processing-functions) for more details. |

**Note: HexColor (hexadecimal color values), for example "#ff00ff"**

If app.json is as follows:

```json
{
  "window":{
    "navigationBarBackgroundColor": "#ffffff",
    "navigationBarTextStyle": "black",
    "navigationBarTitleText": "WeChat interface function demonstration",
    "backgroundColor": "#eeeeee",
    "backgroundTextStyle": "light"
  }
}
```

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/framework/config.jpg)

### tabBar

If our Mini Program is an application with multiple tabs (there are tab bars at the top or bottom of the client window that can switch pages), then we can use the tabBar configuration items to specify tab bar presentation and display the corresponding pages when the tabs are switched.

**Tip:** A page reached using page jump (wx.navigateTo) or page redirect (wx.redirectTo) will not display the bottom tab bar, even if it is defined in the tabBar configurations. **Tip:** Icons will not be displayed when the set position is at the top.

tabBar is an array that **can only configure a minimum of two or a maximum of five tabs**. Tabs are sorted by array.

**Attribute descriptions:**

| Attribute       | Type     | Required | Default value | Description                                                  |
| --------------- | -------- | -------- | ------------- | ------------------------------------------------------------ |
| color           | HexColor | Yes      |               | Default color for text on tab                                |
| selectedColor   | HexColor | Yes      |               | Color of text on tab when selected                           |
| backgroundColor | HexColor | Yes      |               | Tab background color                                         |
| borderStyle     | String   | No       | black         | Color of border on tab bar, only supports black/white        |
| list            | Array    | Yes      |               | Tab list, refer to list attribute descriptions, minimum of two and maximum of five tabs |
| position        | String   | No       | bottom        | Optional values top and bottom                               |

Among these, every item in an array received by list is an object. Their attributes are as follows:

| Attribute        | Type   | Required | Description                                                  |
| ---------------- | ------ | -------- | ------------------------------------------------------------ |
| pagePath         | String | Yes      | Page path, must be defined in pages first                    |
| text             | String | Yes      | Button text on tab                                           |
| iconPath         | String | No       | Image path, icon size is limited to 40kb, recommended size is 81px * 81px, this parameter is invalid when current position is at the top |
| selectedIconPath | String | No       | Selected image path, icon size is limited to 40kb, recommended size is 81px * 81px, this parameter is invalid when current position is at the top |

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/framework/tabbar.png)

### networkTimeout

Can set various network request timeouts.

**Attribute descriptions:**

| Attribute     | Type   | Required | Description                                                  |
| ------------- | ------ | -------- | ------------------------------------------------------------ |
| request       | Number | No       | [wx.request](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/network-request#wx-request-object-) timeout, unit milliseconds, default is 60,000 |
| connectSocket | Number | No       | [wx.connectSocket](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/network-socket#wx-connectsocket-object-) timeout, unit milliseconds, default is 60,000 |
| uploadFile    | Number | No       | [wx.uploadFile](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/network-file#wx-uploadfile-object-) timeout, unit milliseconds, default is 60,000 |
| downloadFile  | Number | No       | [wx.downloadFile](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/network-file#wx-downloadfile-object-) timeout, unit milliseconds, default is 60,000 |

### debug

Can enable debug mode in Developer Tools. Debug information is given in info form on the Developer Tools control panel, this information includes `page registration`, `page routes`, `data updates`, and `event triggers`. This can help developers to locate common problems quickly.

## page.json

Every Mini Program page can also use `.json` files to to configure the page window presentation. Page configuration is a lot simpler than `app.json` global configuration. You just set the content of the window configuration items in app.json and the configuration items in the page will overwrite the same configuration items in the app.json window.

The page's `.json` can only set `window`-related configuration items to determine the page's window presentation. Therefore, the `window` key does not need to be written. For example:

| Attribute                    | Type     | Default value | Description                                                  |
| ---------------------------- | -------- | ------------- | ------------------------------------------------------------ |
| navigationBarBackgroundColor | HexColor | #000000       | Navigation bar background color, for example "#000000"       |
| navigationBarTextStyle       | String   | white         | Navigation bar title color, only supports black/white        |
| navigationBarTitleText       | String   |               | Navigation bar title text content                            |
| backgroundColor              | HexColor | #ffffff       | Window background color                                      |
| backgroundTextStyle          | String   | dark          | Pull down background font, loading image style, only supports dark/light |
| enablePullDownRefresh        | Boolean  | false         | Whether to enable pull down refresh, refer to [Page-Related Event Processing Functions](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/page#page-related-event-processing-functions) for more details. |
| disableScroll                | Boolean  | false         | You cannot scroll up or down on the entire page if this is set as true; only effective in page.json, this item cannot be set in app.json |

```json
{
  "navigationBarBackgroundColor": "#ffffff",
  "navigationBarTextStyle": "black",
  "navigationBarTitleText": "WeChat interface function demonstration",
  "backgroundColor": "#eeeeee",
  "backgroundTextStyle": "light"
}
```