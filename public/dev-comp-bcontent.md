## icon

**Icons**

| Attribute name | Type   | Default value | Description                                                  |
| -------------- | ------ | ------------- | ------------------------------------------------------------ |
| type           | String |               | icon type, valid values: success, success_no_circle, info, warn, waiting, cancel, download, search, clear |
| size           | Number | 23            | icon size, unit px                                           |
| color          | Color  |               | icon color, same as css color                                |

**Example:**

```html
<view class="group">
  <block wx:for="{{iconSize}}">
    <icon type="success" size="{{item}}"/>
  </block>
</view>

<view class="group">
  <block wx:for="{{iconType}}">
    <icon type="{{item}}" size="40"/>
  </block>
</view>


<view class="group">
  <block wx:for="{{iconColor}}">
    <icon type="success" size="40" color="{{item}}"/>
  </block>
</view>
Page({
  data: {
    iconSize: [20, 30, 40, 50, 60, 70],
    iconColor: [
      'red', 'orange', 'yellow', 'green', 'rgb(0,255,255)', 'blue', 'purple'
    ],
    iconType: [
      'success', 'success_no_circle', 'info', 'warn', 'waiting', 'cancel', 'download', 'search', 'clear'
    ]
  }
})
```

![icon](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/icon.png)



## text

**Text**

| Attribute name | Type    | Default value | Description                | Minimum version      |
| -------------- | ------- | ------------- | -------------------------- | -------------------- |
| selectable     | Boolean | false         | Whether text is selectable | {%version('1.1.0')%} |

Supports the escape character "\".

`<text/>` nesting is only supported in the `<text/>` component.

Apart from text nodes, all other nodes are unable to be selected by being pressed and held.

**Example:**

```html
<view class="btn-area">
  <view class="body-view">
    <text>{{text}}</text>
    <button bindtap="add">add line</button>
    <button bindtap="remove">remove line</button>
  </view>
</view>
var initData = 'this is first line\nthis is second line'
var extraLine = [];
Page({
  data: {
    text: initData
  },
  add: function(e) {
    extraLine.push('other line')
    this.setData({
      text: initData + '\n' + extraLine.join('\n')
    })
  },
  remove: function(e) {
    if (extraLine.length > 0) {
      extraLine.pop()
      this.setData({
        text: initData + '\n' + extraLine.join('\n')
      })
    }
  }
})
```

![text](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/text.png)

#### Bugs & Tips

1. `tip`: The `text` press and hold copy function has still not been implemented.



## progress

**Progress bar**

| Attribute       | Type    | Default value | Description                                      |
| --------------- | ------- | ------------- | ------------------------------------------------ |
| percent         | Float   | No            | Percentage 0 to 100                              |
| show-info       | Boolean | false         | Display percentage on right side of progress bar |
| stroke-width    | Number  | 6             | Progress bar line width, unit px                 |
| color           | Color   | #09BB07       | Progress bar color (please use activeColor)      |
| activeColor     | Color   |               | Selected progress bar color                      |
| backgroundColor | Color   |               | Unselected progress bar color                    |
| active          | Boolean | false         | Animation from left to right of progress bar     |

**Example:**

```html
<progress percent="20" show-info />
<progress percent="40" stroke-width="12" />
<progress percent="60" color="pink" />
<progress percent="80" active />
```

![progress](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/progress.png)