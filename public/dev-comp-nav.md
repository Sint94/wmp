# navigator

   **Page links**

   | Attribute name   | Type   | Default value   | Description                                                  |
   | ---------------- | ------ | --------------- | ------------------------------------------------------------ |
   | url              | String |                 | Jump link in application                                     |
   | open-type        | String | navigate        | Jump mode                                                    |
   | delta            | Number |                 | Effective when open-type is 'navigateBack', indicates number of layers to go back |
   | hover-class      | String | navigator-hover | Specifies the style type when tapped, there are no tap status effects when `hover-class="none"` |
   | hover-start-time | Number | 50              | How long it takes for tap status to appear after holding down, unit milliseconds |
   | hover-stay-time  | Number | 600             | Amount of time tap status is maintained after finger is released, unit milliseconds |

   **open-type valid values:**

   | Value        | Description                               | Minimum version      |
   | ------------ | ----------------------------------------- | -------------------- |
   | navigate     | Corresponds to `wx.navigateTo` function   |                      |
   | redirect     | Corresponds to `wx.redirectTo` function   |                      |
   | switchTab    | Corresponds to `wx.switchTab` function    |                      |
   | reLaunch     | Corresponds to `wx.reLaunch` function     | {%version('1.1.0')%} |
   | navigateBack | Corresponds to `wx.navigateBack` function | {%version('1.1.0')%} |

   **Note: navigator-hover default is {background-color: rgba(0, 0, 0, 0.1); opacity: 0.7;}, <navigator/> child node background color should be a transparent color.**

   **Sample code:**

   ```css
   /** wxss **/
   /** Modify default navigator tap status **/
   .navigator-hover {
       color:blue;
   }
   /** Customize other tap status style types **/
   .other-navigator-hover {
       color:red;
   }
   <!-- sample.wxml -->
   <view class="btn-area">
     <navigator url="/page/navigate/navigate?title=navigate" hover-class="navigator-hover">Jump to new page</navigator>
     <navigator url="../../redirect/redirect/redirect?title=redirect" open-type="redirect" hover-class="other-navigator-hover">Open on current page</navigator>
     <navigator url="/page/index/index" open-type="switchTab" hover-class="other-navigator-hover">Switch Tab</navigator>
   </view>
   <!-- navigator.wxml -->
   <view style="text-align:center"> {{title}} </view>
   <view> Tapping top left corner returns you to previous page </view>
   <!-- redirect.wxml -->
   <view style="text-align:center"> {{title}} </view>
   <view> Tapping top left corner returns you to parent page </view>
   // redirect.js navigator.js
   Page({
     onLoad: function(options) {
       this.setData({
         title: options.title
       })
     }
   })
   ```