## audio

**Audio**

| Attribute name | Type        | Default value  | Description                                                  |
| -------------- | ----------- | -------------- | ------------------------------------------------------------ |
| id             | String      |                | audio component unique identifier                            |
| src            | String      |                | Resource address for audio that needs to be played           |
| loop           | Boolean     | false          | Whether loop playback                                        |
| controls       | Boolean     | true           | Whether default control displayed                            |
| poster         | String      |                | Audio cover image resource address on default control, if controls attribute value is false, then setting poster will be ineffective |
| name           | String      | Unknown audio  | Audio name on default control, if controls attribute value is false, then setting name will be ineffective |
| author         | String      | Unknown author | Author name on default control, if controls attribute value is false, then setting author will be ineffective |
| binderror      | EventHandle |                | error event triggered when an error occurs, detail = {errMsg: MediaError.code} |
| bindplay       | EventHandle |                | play event triggered when starting/continuing playback       |
| bindpause      | EventHandle |                | pause event triggered when playback paused                   |
| bindtimeupdate | EventHandle |                | timeupdate event triggered when playback progress changes, detail = {currentTime, duration} |
| bindended      | EventHandle |                | ended event triggered when playback ends                     |

**MediaError.code**

| Error return code            | Description                        |
| ---------------------------- | ---------------------------------- |
| MEDIA_ERR_ABORTED            | Getting resources disabled by user |
| MEDIA_ERR_NETWORD            | Network error                      |
| MEDIA_ERR_DECODE             | Decode error                       |
| MEDIA_ERR_SRC_NOT_SUPPOERTED | Inappropriate resource             |

**Sample code:**

```html
<!-- audio.wxml -->
<audio poster="{{poster}}" name="{{name}}" author="{{author}}" src="{{src}}" id="myAudio" controls loop></audio>

<button type="primary" bindtap="audioPlay">Play</button>
<button type="primary" bindtap="audioPause">Pause</button>
<button type="primary" bindtap="audio14">Set current play time as 14 seconds</button>
<button type="primary" bindtap="audioStart">Return to start</button>
// audio.js
Page({
  onReady: function (e) {
    // Use wx.createAudioContext to get audio context
    this.audioCtx = wx.createAudioContext('myAudio')
  },
  data: {
    poster: 'http://y.gtimg.cn/music/photo_new/T002R300x300M000003rsKF44GyaSk.jpg?max_age=2592000',
    name: 'At The Moment',
    author: 'Xu Wei',
    src: 'http://ws.stream.qqmusic.qq.com/M500001VfvsJ21xFqb.mp3?guid=ffffffff82def4af4b12b3cd9337d5e7&uin=346897220&vkey=6292F51E1E384E06DCBDC9AB7C49FD713D632D313AC4858BACB8DDD29067D3C601481D36E62053BF8DFEAF74C0A5CCFADD6471160CAF3E6A&fromtag=46',
  },
  audioPlay: function () {
    this.audioCtx.play()
  },
  audioPause: function () {
    this.audioCtx.pause()
  },
  audio14: function () {
    this.audioCtx.seek(14)
  },
  audioStart: function () {
    this.audioCtx.seek(0)
  }
})
```

![audio](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/audio.png)

Related api: [wx.createAudioContext](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/api-audio#wx-createaudiocontext-audioid-)



## image

**Images**

| Attribute name | Type        | Default value | Description                                                  |
| -------------- | ----------- | ------------- | ------------------------------------------------------------ |
| src            | String      |               | Image resource address                                       |
| mode           | String      | 'scaleToFill' | Image cropping and zoom modes                                |
| binderror      | HandleEvent |               | The event name released on AppService when an error occurs, event object event.detail = {errMsg: 'something wrong'} |
| bindload       | HandleEvent |               | Event name released to AppService when image loading is complete, image object event.detail = {height: 'image height px', width: 'image width px'} |

**Note: Image component default width is 300px, default height is 225px.**

**mode valid values:**

There are 13 modes, of which 4 are zoom modes and 9 are crop modes.

| Mode | Value        | Description                                                  |
| ---- | ------------ | ------------------------------------------------------------ |
| Zoom | scaleToFill  | Image zoom that does not maintain aspect ratio, stretches height and width of image to completely fill image element |
| Zoom | aspectFit    | Image zoom that maintains aspect ratio, enables long edge of image to be fully displayed. In other words, the image can be fully displayed. |
| Zoom | aspectFill   | Image zoom that maintains aspect ratio, only ensures that short edge of image can be fully displayed. In other words, an image that is normally horizontal or vertical will be complete, but it will be cut if it faces the other direction. |
| Zoom | widthFix     | Width is fixed while height changes automatically, original image aspect ratio remains unchanged |
| Crop | top          | Does not zoom image, only displays top area of image         |
| Crop | bottom       | Does not zoom image, only displays bottom area of image      |
| Crop | center       | Does not zoom image, only displays center area of image      |
| Crop | left         | Does not zoom image, only displays left area of image        |
| Crop | right        | Does not zoom image, only displays right area of image       |
| Crop | top left     | Does not zoom image, only displays top left area of image    |
| Crop | top right    | Does not zoom image, only displays top right area of image   |
| Crop | bottom left  | Does not zoom image, only displays bottom left area of image |
| Crop | bottom right | Does not zoom image, only displays bottom right area of image |

**Example:**

```html
<view class="page">
  <view class="page__hd">
    <text class="page__title">image</text>
    <text class="page__desc">Image</text>
  </view>
  <view class="page__bd">
    <view class="section section_gap" wx:for="{{array}}" wx:for-item="item">
      <view class="section__title">{{item.text}}</view>
      <view class="section__ctn">
        <image style="width: 200px; height: 200px; background-color: #eeeeee;" mode="{{item.mode}}" src="{{src}}"></image>
      </view>
    </view>
  </view>
</view>
Page({
  data: {
    array: [{
      mode: 'scaleToFill',
      text: 'scaleToFill: Image zoom that does not maintain aspect ratio and completely adapts image'
    }, { 
      mode: 'aspectFit',
      text: 'aspectFit: Image zoom that maintains aspect ratio, enables long edge of image to be fully displayed'
    }, { 
      mode: 'aspectFill',
      text: 'aspectFill: Image zoom that maintains aspect ratio, only ensures that short edge of image can be fully displayed'
    }, { 
      mode: 'top',
      text: 'top: Does not zoom image, only displays top area of image' 
    }, {      
      mode: 'bottom',
      text: 'bottom: Does not zoom image, only displays bottom area of image'
    }, { 
      mode: 'center',
      text: 'center: Does not zoom image, only displays center area of image'
    }, { 
      mode: 'left',
      text: 'left: Does not zoom image, only displays left area of image'
    }, { 
      mode: 'right',
      text: 'right: Does not zoom image, only displays right area of image'
    }, { 
      mode: 'top left',
      text: 'top left: Does not zoom image, only displays top left area of image 
    }, { 
      mode: 'top right',
      text: 'top right: Does not zoom image, only displays top right area of image'
    }, { 
      mode: 'bottom left',
      text: 'bottom left: Does not zoom image, only displays bottom left area of image'
    }, { 
      mode: 'bottom right',
      text: 'bottom right: Does not zoom image, only displays bottom right area of image'
    }],
    src: '../../resources/cat.jpg'
  },
  imageError: function(e) {
    console.log('image3 has experienced an error event, the value brought is', e.detail.errMsg)
  }
})
```

##### Original image

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/0.jpg)

##### scaleToFill

Image zoom that does not maintain aspect ratio and completely adapts image

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/1.png)

##### aspectFit

Image zoom that maintains aspect ratio, enables long edge of image to be fully displayed

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/2.png)

##### aspectFill

Image zoom that maintains aspect ratio, only ensures that short edge of image can be fully displayed

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/3.png)

##### top

Does not zoom image, only displays top area of image

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/4.png)

##### bottom

Does not zoom image, only displays bottom area of image

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/5.png)

##### center

Does not zoom image, only displays center area of image

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/6.png)

##### left

Does not zoom image, only displays left area of image

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/7.png)

##### right

Does not zoom image, only displays right area of image

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/8.png)

##### top left

Does not zoom image, only displays top left area of image

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/9.png)

##### top right

Does not zoom image, only displays top right area of image

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/10.png)

##### bottom left

Does not zoom image, only displays bottom left area of image

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/11.png)

##### bottom right

Does not zoom image, only displays bottom right area of image

![image](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/12.png)



## video

**Video**

| Attribute name | Type         | Default value | Description                                                  | Minimum version      |
| -------------- | ------------ | ------------- | ------------------------------------------------------------ | -------------------- |
| src            | String       |               | Resource address for video that needs to be played           |                      |
| duration       | Number       |               | Duration of specified video                                  | {%version('1.1.0')%} |
| controls       | Boolean      | true          | Whether default playback controls displayed (Play/Pause buttons, playback progress, time) |                      |
| danmu-list     | Object Array |               | Danmu list                                                   |                      |
| danmu-btn      | Boolean      | false         | Whether Danmu button displayed, only effective during initialization, cannot be dynamically changed |                      |
| enable-danmu   | Boolean      | false         | Whether danmu displayed, only effective during initialization, cannot be dynamically changed |                      |
| autoplay       | Boolean      | false         | Whether playback is automatic                                |                      |
| bindplay       | EventHandle  |               | play event triggered when starting/continuing playback       |                      |
| bindpause      | EventHandle  |               | pause event triggered when playback paused                   |                      |
| bindended      | EventHandle  |               | ended event triggered when playback ends                     |                      |
| bindtimeupdate | EventHandle  |               | Triggered when playback progress changes, event.detail = {currentTime: 'current play time'}. Trigger frequency should be once every 250ms. |                      |
| objectFit      | String       | contain       | Video display mode when video size is inconsistent with video container size. Contain, fill, cover. |                      |
| poster         | String       |               | Audio cover image resource address on default control, if controls attribute value is false, then setting poster will be ineffective |                      |

Recognized video tag width 300px, height 225px. Width and height need to be set using wxss.

**Sample code:**

```html
<view class="section tc">
  <video src="{{src}}"   controls ></video>
  <view class="btn-area">
    <button bindtap="bindButtonTap">Get video</button>
  </view>
</view>

<view class="section tc">
  <video id="myVideo" src="http://wxsnsdy.tc.qq.com/105/20210/snsdyvideodownload?filekey=30280201010421301f0201690402534804102ca905ce620b1241b726bc41dcff44e00204012882540400&bizid=1023&hy=SH&fileparam=302c020101042530230204136ffd93020457e3c4ff02024ef202031e8d7f02030f42400204045a320a0201000400" danmu-list="{{danmuList}}" enable-danmu danmu-btn controls></video>
  <view class="btn-area">
    <button bindtap="bindButtonTap">Get video</button>
    <input bindblur="bindInputBlur"/>
    <button bindtap="bindSendDanmu">Send danmu</button>
  </view>
</view>
function getRandomColor () {
  let rgb = []
  for (let i = 0 ; i < 3; ++i){
    let color = Math.floor(Math.random() * 256).toString(16)
    color = color.length == 1 ? '0' + color : color
    rgb.push(color)
  }
  return '#' + rgb.join('')
}

Page({
  onReady: function (res) {
    this.videoContext = wx.createVideoContext('myVideo')
  },
  inputValue: '',
    data: {
        src: '',
    danmuList: [
      {
        text: 'Danmu that appears in 1st second',
        color: '#ff0000',
        time: 1
      },
      {
        text: 'Danmu that appears in 3rd second',
        color: '#ff00ff',
        time: 3
    }]
    },
  bindInputBlur: function(e) {
    this.inputValue = e.detail.value
  },
  bindButtonTap: function() {
    var that = this
    wx.chooseVideo({
      sourceType: ['album', 'camera'],
      maxDuration: 60,
      camera: ['front','back'],
      success: function(res) {
        that.setData({
          src: res.tempFilePath
        })
      }
    })
  },
  bindSendDanmu: function () {
    this.videoContext.sendDanmu({
      text: this.inputValue,
      color: getRandomColor()
    })
  }
})
```

![video](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/video.png)

Related api：[wx.createVideoContext](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/api-video#wx-createvideocontext-videoid-)

#### Bugs & Tips

1. `tip`: The `video` component is a native component created by the client, its level is the highest.
2. `tip`: Please do not use the `video` component in `scroll-view`.
3. `tip`: `css` animation is ineffective on the `video` component.