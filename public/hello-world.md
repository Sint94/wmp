### Brief Tutorial

This document will take you through creating a WeChat Mini Program step by step. You will also be able to experience the actual results of this Mini Program on a phone. The homepage of this Mini Program will display a welcome message and the WeChat profile photo of the current user. Click on the profile photo to view the current Mini Program's boot log on a new page.   [Download source code](https://mp.weixin.qq.com/debug/wxadoc/dev/demo/quickstart.zip)

### 1. Get AppID for WeChat Mini Program

If you log in to [https://mp.weixin.qq.com](https://mp.weixin.qq.com/), you will be able to view the WeChat Mini Program's AppID in Settings (设置) - Developer Settings (开发者设置). Note that you cannot use Service Account or Subscription Account AppIDs directly.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/setting.png)

**Note: If you want to experience the Mini Program on a phone using a non-administrator WeChat ID, then we will also need to run Bind Developer (绑定开发者). Namely, the WeChat IDs that need to experience the Mini Program are bound in the User Identity (用户身份) - Developer (开发者) module. An administrator WeChat ID is used for both the default registered account and experience for this tutorial.**

### 2. Create a project

We need to use [Developer Tools](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/devtools) to complete the Mini Program's creation and code editing.

After the developer tools have been installed, open and use a WeChat QR code login. Select Create Project (创建项目), enter the AppID obtained as described above, set a local project name (not a Mini Program name), for example, "My First Project", and select a local folder to serve as the code storage directory. Click on New Project (新建项目).

To make it easier for beginners to understand the basic code structure of WeChat Mini Programs, if an empty folder is selected as the local folder during the creation process, Developer Tools will show whether the creation of a quick start project is required. If Yes is selected, the developer tools will help us to generate a simple demo in the development directory.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/new_project.png)

After the project has been created successfully, we can click on the project to enter and view the complete Developer Tools interface, then click on the navigation bar on the left hand side to view and edit our code in Edit (编辑). We can test code and simulate the results of the Mini Program on the WeChat client in Debug (调试). We can send a preview of the actual results to a phone in Project (项目).

### 3. Write code

#### Create a Mini Program instance

If we click on Edit (编辑) in the left hand navigation bar in Developer Tools, we can see that this project has been initialized and contains a few simple code files. The most important ones, which are also indispensable, are these three: app.js, app.json, and app.wxss. The file with the `.js` suffix is a script file, the file with the `.json` suffix is a configuration file, and the file with the `.wxss` suffix is a stylesheet file. The WeChat Mini Program will read these files and generate a [Mini Program instance](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/app).

Next we will gain a simple understanding of the functions of these three files, which make it easier to modify your WeChat Mini Programs and develop them from scratch.

app.js is the Mini Program script code. We can monitor and process Mini Program lifecycle functions and declare global variables in this file. We can also call the considerable APIs provided by the framework, such as synchronous storage and reading of local data in this example. You can refer to the [API Document](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/index#api_index) to learn more about available APIs

```javascript
//app.js
App({
  onLaunch: function () {
    //Call API from local cache to get data
    var logs = wx.getStorageSync('logs') || []
    logs.unshift(Date.now())
    wx.setStorageSync('logs', logs)
  },
  getUserInfo:function(cb){
    var that = this;
    if(this.globalData.userInfo){
      typeof cb == "function" && cb(this.globalData.userInfo)
    }else{
      //Call login interface
      wx.login({
        success: function () {
          wx.getUserInfo({
            success: function (res) {
              that.globalData.userInfo = res.userInfo;
              typeof cb == "function" && cb(that.globalData.userInfo)
            }
          })
        }
      });
    }
  },
  globalData:{
    userInfo:null
  }
})
```

app.json is the global configuration for the entire Mini Program. In this file, we can configure which pages the Mini Program consists of, its window background, its navigation bar style, and its default title. Note that no comments may be added to this file. You can refer to [Configuration Details](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/config) for more configurable items

```json
{
  "pages":[
    "pages/index/index",
    "pages/logs/logs"
  ],
  "window":{
    "backgroundTextStyle":"light",
    "navigationBarBackgroundColor": "#fff",
    "navigationBarTitleText": "WeChat",
    "navigationBarTextStyle":"black"
  }
}
```

app.wxss is the public stylesheet for the entire Mini Program. We can directly use the style rules declared in app.wxss on the class attribute in the page component.

```css
/**app.wxss**/
.container {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 200rpx 0;
  box-sizing: border-box;
}
```

#### Create a page

We have two pages in this tutorial, an index page and a logs page, that is, a welcome page and a Mini Program boot log display page. They are both under the pages directory. All of the paths and page names for every page in a WeChat Mini Program need to be written in the app.json pages. The first page within the pages is the Mini Program homepage.

Every [Mini Program page](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/page) is composed of files with four different suffixes after the same name under the same path, for example: index.js, index.wxml, index.wxss, and index.json. The file with the `.js` suffix is a script file, the file with the `.json` suffix is a configuration file, the file with the `.wxss` suffix is a stylesheet file, and the file with the `.wxml` suffix is a page structure file.

index.wxml is the page structure file:

```html
<!--index.wxml-->
<view class="container">
  <view class="userinfo">
    <block wx:if="{{hasUserInfo}}">
      <image bindtap="bindViewTap" class="userinfo-avatar" src="{{userInfo.avatarUrl}}" background-size="cover"></image>
      <text class="userinfo-nickname">{{userInfo.nickName}}</text>
    </block>
    <button wx:else open-type="getUserInfo" bindgetuserinfo="getUserInfo"> 获取头像昵称 </button>
  </view>
  <view class="usermotto">
    <text class="user-motto">{{motto}}</text>
  </view>
</view>
```

In this example, [``](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/view), [``](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/image), and [``](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/text) have been used for page structure construction, data binding, and interactive processing functions.

index.js is the page script file. In this file, we can monitor and process page lifecycle functions, get Mini Program instances, declare and process data, and respond to page interaction events.

```javascript
//index.js
//Get application instance
var app = getApp()
Page({
  data: {
    motto: 'Hello World',
    userInfo: {}
  },
  //Event processing function
  bindViewTap: function() {
    wx.navigateTo({
      url: '../logs/logs'
    })
  },
  onLoad: function () {
    console.log('onLoad')
    var that = this
    //Call application instance method to get global data
    app.getUserInfo(function(userInfo){
      //Update data
      that.setData({
        userInfo:userInfo
      })
    })
  }
})
```

index.wxss is the page stylesheet:

```css
/**index.wxss**/
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 200px;
}
```

The page stylesheet is non-essential. When there is a page stylesheet, the style rules in the page stylesheet will cascade and overwrite the style rules in app.wxss. If no page stylesheet has been specified, the style rules specified in app.wxss can also be used directly in the page structure file.

index.json is the page configuration file:

The page configuration file is non-essential. When there is a page configuration file, the configuration items on this page will overwrite the same configuration items in the app.json window. If no page configuration file has been specified, the default configuration in app.json is used directly on this page.

Logs page structure

```html
<!--logs.wxml-->
<view class="container log-list">
  <block wx:for="{{logs}}" wx:for-item="log">
    <text class="log-item">{{index + 1}}. {{log}}</text>
  </block>
</view>
```

The logs page uses the [``](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/list#black-wx-for) control tag to organize code, uses [`wx:for`](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/list#wx-for) to bind `logs` data on `<block/>`, and expands nodes for `logs` data circulation.

```js
//logs.js
var util = require('../../utils/util.js')
Page({
  data: {
    logs: []
  },
  onLoad: function () {
    this.setData({
      logs: (wx.getStorageSync('logs') || []).map(function (log) {
        return util.formatTime(new Date(log))
      })
    })
  }
})
```

The run result is as follows:

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/start_result.png)

### 4. Phone preview

Select Project (项目) in the left menu bar in Developer Tools and click on Preview (预览). After scanning the QR code you can experience this in the WeChat client.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/start_preview.png)