## View

**View container**

| Attribute name   | Type   | Default value | Description                                                  |
| ---------------- | ------ | ------------- | ------------------------------------------------------------ |
| hover-class      | String | none          | Specifies style type when pressed. When `hover-class="none"` there are no tap status effects. |
| hover-start-time | Number | 50            | How long it takes for tap status to appear after holding down, unit milliseconds |
| hover-stay-time  | Number | 400           | Amount of time tap status is maintained after finger is released, unit milliseconds |

**Example:**

```html
<view class="section">
  <view class="section__title">flex-direction: row</view>
  <view class="flex-wrp" style="flex-direction:row;">
    <view class="flex-item bc_green">1</view>
    <view class="flex-item bc_red">2</view>
    <view class="flex-item bc_blue">3</view>
  </view>
</view>
<view class="section">
  <view class="section__title">flex-direction: column</view>
  <view class="flex-wrp" style="height: 300px;flex-direction:column;">
    <view class="flex-item bc_green">1</view>
    <view class="flex-item bc_red">2</view>
    <view class="flex-item bc_blue">3</view>
  </view>
</view>
```

![view](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/view.png)

#### Bugs & Tips

1. `tip`: Please use [scroll-view](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/scroll-view) if you need to use the scroll view.



## scroll-view

**A scrollable view area**

| Attribute name        | Type        | Default value | Description                                                  |
| --------------------- | ----------- | ------------- | ------------------------------------------------------------ |
| scroll-x              | Boolean     | false         | Allows horizontal scrolling                                  |
| scroll-y              | Boolean     | false         | Allows vertical scrolling                                    |
| upper-threshold       | Number      | 50            | A scrolltoupper event is triggered when far from the top/left (unit px) |
| lower-threshold       | Number      | 50            | A scrolltolower event is triggered when far from the bottom/right (unit px) |
| scroll-top            | Number      |               | Sets vertical scroll bar position                            |
| scroll-left           | Number      |               | Sets horizontal scroll bar position                          |
| scroll-into-view      | String      |               | Value should be a child element id (id cannot begin with a number), then the top of the element is aligned at the top of the scroll area when this element is scrolled to, only supports vertical scrolling |
| scroll-with-animation | Boolean     | false         | Uses animated transition when scroll bar position is set     |
| enable-back-to-top    | Boolean     | false         | Scroll bar returns to top when the top status bar is tapped in iOS, or the title bar is tapped in Android, only supports vertical |
| bindscrolltoupper     | EventHandle |               | Scrolling to the top/left will trigger a scrolltoupper event |
| bindscrolltolower     | EventHandle |               | Scrolling to the bottom/right will trigger a scrolltolower event |
| bindscroll            | EventHandle |               | Triggered when scrolling, event.detail = {scrollLeft, scrollTop, scrollHeight, scrollWidth, deltaX, deltaY} |

`<scroll-view/>` needs to be given a fixed height when using vertical scrolling. The height is set using WXSS.

**Sample code:**

```html
<view class="section">
  <view class="section__title">vertical scroll</view>
  <scroll-view scroll-y="true" style="height: 200px;" bindscrolltoupper="upper" bindscrolltolower="lower" bindscroll="scroll" scroll-into-view="{{toView}}" scroll-top="{{scrollTop}}">
    <view id="green" class="scroll-view-item bc_green"></view>
    <view id="red"  class="scroll-view-item bc_red"></view>
    <view id="yellow" class="scroll-view-item bc_yellow"></view>
    <view id="blue" class="scroll-view-item bc_blue"></view>
  </scroll-view>

  <view class="btn-area">
    <button size="mini" bindtap="tap">click me to scroll into view </button>
    <button size="mini" bindtap="tapMove">click me to scroll</button>
  </view>
</view>
<view class="section section_gap">
  <view class="section__title">horizontal scroll</view>
  <scroll-view class="scroll-view_H" scroll-x="true" style="width: 100%">
    <view id="green" class="scroll-view-item_H bc_green"></view>
    <view id="red"  class="scroll-view-item_H bc_red"></view>
    <view id="yellow" class="scroll-view-item_H bc_yellow"></view>
    <view id="blue" class="scroll-view-item_H bc_blue"></view>
  </scroll-view>
</view>
var order = ['red', 'yellow', 'blue', 'green', 'red']
Page({
  data: {
    toView: 'red',
    scrollTop: 100
  },
  upper: function(e) {
    console.log(e)
  },
  lower: function(e) {
    console.log(e)
  },
  scroll: function(e) {
    console.log(e)
  },
  tap: function(e) {
    for (var i = 0; i < order.length; ++i) {
      if (order[i] === this.data.toView) {
        this.setData({
          toView: order[i + 1]
        })
        break
      }
    }
  },
  tapMove: function(e) {
    this.setData({
      scrollTop: this.data.scrollTop + 10
    })
  }
})
```

![scroll-view](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/scroll-view.png)

#### Bugs & Tips

1. `tip`: Please do not use the `textarea`, `map`, `canvas`, or `video` components in `scroll-view`.
2. `tip`: `scroll-into-view` has higher priority than `scroll-top.`
3. `tip`: The page will be prevented from bouncing when scrolling `scroll-view`, so `onPullDownRefresh` cannot be triggered when scrolling in `scroll-view`.
4. `tip`: If you want to use pull down refresh, please use page scrolling instead of `scroll-view`. This way, you can also return to the top of the page by tapping the status bar at the top.



## swiper

**Sliding view container**

| Attribute name         | Type        | Default value     | Description                                                  | Minimum version      |
| ---------------------- | ----------- | ----------------- | ------------------------------------------------------------ | -------------------- |
| indicator-dots         | Boolean     | false             | Whether panel indicator dots displayed                       |                      |
| indicator-color        | Color       | rgba(0, 0, 0, .3) | Color of indicator dots                                      | {%version('1.1.0')%} |
| indicator-active-color | Color       | #000000           | Color of currently selected indicator dot                    | {%version('1.1.0')%} |
| autoplay               | Boolean     | false             | Whether to switch automatically                              |                      |
| current                | Number      | 0                 | Current page index                                           |                      |
| interval               | Number      | 5000              | Automatic switching time interval                            |                      |
| duration               | Number      | 500               | Slide animation duration                                     |                      |
| circular               | Boolean     | false             | Whether to use cohesive sliding                              |                      |
| bindchange             | EventHandle |                   | A change event will be triggered when current changes, event.detail = {current: current} |                      |

**Note**: Only `<swiper-item/>` components can be placed in this component, otherwise this will lead to an undefined action.

#### swiper-item

Can only be placed in the `<swiper/>` component, height and width are automatically set at 100%.

**Sample code:**

```html
<swiper indicator-dots="{{indicatorDots}}"
  autoplay="{{autoplay}}" interval="{{interval}}" duration="{{duration}}">
  <block wx:for="{{imgUrls}}">
    <swiper-item>
      <image src="{{item}}" class="slide-image" width="355" height="150"/>
    </swiper-item>
  </block>
</swiper>
<button bindtap="changeIndicatorDots"> indicator-dots </button>
<button bindtap="changeAutoplay"> autoplay </button>
<slider bindchange="intervalChange" show-value min="500" max="2000"/> interval
<slider bindchange="durationChange" show-value min="1000" max="10000"/> duration
Page({
  data: {
    imgUrls: [
      'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
      'http://img06.tooopen.com/images/20160818/tooopen_sy_175866434296.jpg',
      'http://img06.tooopen.com/images/20160818/tooopen_sy_175833047715.jpg'
    ],
    indicatorDots: false,
    autoplay: false,
    interval: 5000,
    duration: 1000
  },
  changeIndicatorDots: function(e) {
    this.setData({
      indicatorDots: !this.data.indicatorDots
    })
  },
  changeAutoplay: function(e) {
    this.setData({
      autoplay: !this.data.autoplay
    })
  },
  intervalChange: function(e) {
    this.setData({
      interval: e.detail.value
    })
  },
  durationChange: function(e) {
    this.setData({
      duration: e.detail.value
    })
  }
})
```