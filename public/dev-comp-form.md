## button

**Buttons**

| Attribute name   | Type    | Default value | Description                                                  | Minimum version      |
| ---------------- | ------- | ------------- | ------------------------------------------------------------ | -------------------- |
| size             | String  | default       | Button size                                                  |                      |
| type             | String  | default       | Button style type                                            |                      |
| plain            | Boolean | false         | Whether button is hollow and background color is transparent |                      |
| disabled         | Boolean | false         | Whether disabled                                             |                      |
| loading          | Boolean | false         | Whether there is a loading icon before the name              |                      |
| form-type        | String  |               | Used for `<form/>` component, tapping will trigger a submit/reset event respectively |                      |
| open-type        | String  |               | Valid value: contact; opens Service Center session           | {%version('1.1.0')%} |
| hover-class      | String  | button-hover  | Specifies style type when button pressed. When `hover-class="none"`, there are no tap status effects. |                      |
| hover-start-time | Number  | 20            | How long it takes for tap status to appear after holding down, unit milliseconds |                      |
| hover-stay-time  | Number  | 70            | Amount of time tap status is maintained after finger is released, unit milliseconds |                      |

**Note: button-hover default is {background-color: rgba(0, 0, 0, 0.1); opacity: 0.7;}**

**size valid values:**

| Value   | Description |
| ------- | ----------- |
| default |             |
| mini    |             |

**type valid values:**

| Value   | Description |
| ------- | ----------- |
| primary |             |
| default |             |
| warn    |             |

**form-type valid values:**

| Value  | Description  |
| ------ | ------------ |
| submit | Submits form |
| reset  | Resets form  |

**open-type valid values:**

| Value   | Description                  | Minimum version |
| ------- | ---------------------------- | --------------- |
| contact | Opens Service Center session |                 |

**Sample code:**

```css
/** wxss **/
/** Modifies default button tap status and style type**/
.button-hover {
  background-color: red;
}
/** Adds custom button tap status and style type**/
.other-button-hover {
  background-color: blue;
}
<button type="default" size="{{defaultSize}}" loading="{{loading}}" plain="{{plain}}"
        disabled="{{disabled}}" bindtap="default" hover-class="other-button-hover"> default </button>
<button type="primary" size="{{primarySize}}" loading="{{loading}}" plain="{{plain}}"
        disabled="{{disabled}}" bindtap="primary"> primary </button>
<button type="warn" size="{{warnSize}}" loading="{{loading}}" plain="{{plain}}"
        disabled="{{disabled}}" bindtap="warn"> warn </button>
<button bindtap="setDisabled">Click to set the above button's disabled attribute</button>
<button bindtap="setPlain">Click to set the above button's plain attribute</button>
<button bindtap="setLoading">Click to set the above button's loading attribute</button>
<button open-type="contact">Enter Service Center session</button>
var types = ['default', 'primary', 'warn']
var pageObject = {
  data: {
    defaultSize: 'default',
    primarySize: 'default',
    warnSize: 'default',
    disabled: false,
    plain: false,
    loading: false
  },
  setDisabled: function(e) {
    this.setData({
      disabled: !this.data.disabled
    })
  },
  setPlain: function(e) {
    this.setData({
      plain: !this.data.plain
    })
  },
  setLoading: function(e) {
    this.setData({
      loading: !this.data.loading
    })
  }
}

for (var i = 0; i < types.length; ++i) {
  (function(type) {
    pageObject[type] = function(e) {
      var key = type + 'Size'
      var changedData = {}
      changedData[key] =
        this.data[key] === 'default' ? 'mini' : 'default'
      this.setData(changedData)
    }
  })(types[i])
}

Page(pageObject)
```

![button](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/button.png)



## checkbox-group

Multi selector, composed of multiple `checkboxes` internally.

| Attribute name | Type        | Default value | Description                                                  |
| -------------- | ----------- | ------------- | ------------------------------------------------------------ |
| bindchange     | EventHandle |               | Changes to a selected item in `<checkbox-group/>` trigger a change event, detail = {value:[selected checkbox value array]} |

#### checkbox

Select multiple items.

| Attribute name | Type    | Default value | Description                                                  |
| -------------- | ------- | ------------- | ------------------------------------------------------------ |
| value          | String  |               | `<checkbox/>` ID, triggers `<checkbox-group/>` change event when selected and brings `<checkbox/>` value |
| disabled       | Boolean | false         | Whether disabled                                             |
| checked        | Boolean | false         | Whether currently selected, can be used to set the default selection |
| color          | Color   |               | checkbox color, same as css color                            |

**Example:**

```html
<checkbox-group bindchange="checkboxChange">
  <label class="checkbox" wx:for="{{items}}">
    <checkbox value="{{item.name}}" checked="{{item.checked}}"/>{{item.value}}
  </label>
</checkbox-group>
Page({
  data: {
    items: [
      {name: 'USA', value: 'USA'},
      {name: 'CHN', value: 'China', checked: 'true'},
      {name: 'BRA', value: 'Brazil'},
      {name: 'JPN', value: 'Japan'},
      {name: 'ENG', value: 'England'},
      {name: 'TUR', value: 'France'},
    ]
  },
  checkboxChange: function(e) {
    console.log('when a checkbox change event occurs, the value brought is:', e.detail.value)
  }
})
```

![checkbox](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/checkbox.png)



#### form

A form submitting `<switch/>`, `<input/>`, `<checkbox/>`, `<slider/>`, `<radio/>`, and `<picker/>`entered by users in components.

When the formType submit `<button/>` component in `<form/>` is tapped, the values in the form component will be submitted. The name needs to be added to the form component to serve as a key.

| Attribute name | Type        | Description                                                  |
| -------------- | ----------- | ------------------------------------------------------------ |
| report-submit  | Boolean     | Whether to return formId used to send [templated message](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/notice) |
| bindsubmit     | EventHandle | Brings data in form to trigger a submit event, event.detail = {value : {'name': 'value'} , formId: ''} |
| bindreset      | EventHandle | A reset event will be triggered when the form is reset       |

**Sample code:**

```html
<form bindsubmit="formSubmit" bindreset="formReset">
  <view class="section section_gap">
    <view class="section__title">switch</view>
    <switch name="switch"/>
  </view>
  <view class="section section_gap">
    <view class="section__title">slider</view>
    <slider name="slider" show-value ></slider>
  </view>

  <view class="section">
    <view class="section__title">input</view>
    <input name="input" placeholder="please input here" />
  </view>
  <view class="section section_gap">
    <view class="section__title">radio</view>
    <radio-group name="radio-group">
      <label><radio value="radio1"/>radio1</label>
      <label><radio value="radio2"/>radio2</label>
    </radio-group>
  </view>
  <view class="section section_gap">
    <view class="section__title">checkbox</view>
    <checkbox-group name="checkbox">
      <label><checkbox value="checkbox1"/>checkbox1</label>
      <label><checkbox value="checkbox2"/>checkbox2</label>
    </checkbox-group>
  </view>
  <view class="btn-area">
    <button formType="submit">Submit</button>
    <button formType="reset">Reset</button>
  </view>
</form>
Page({
  formSubmit: function(e) {
    console.log('form experienced submit event, data brought is: ', e.detail.value)
  },
  formReset: function() {
    console.log('form experienced reset event')
  }
})
```

![form](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/form.png)



## input

**Input box**

| Attribute name    | Type        | Default value       | Description                                                  | Minimum version      |
| ----------------- | ----------- | ------------------- | ------------------------------------------------------------ | -------------------- |
| value             | String      |                     | Initial content of input box                                 |                      |
| type              | String      | "text"              | input type                                                   |                      |
| password          | Boolean     | false               | Whether is password type                                     |                      |
| placeholder       | String      |                     | Placeholder when input box is empty                          |                      |
| placeholder-style | String      |                     | Specified placeholder style                                  |                      |
| placeholder-class | String      | "input-placeholder" | Specified placeholder style type                             |                      |
| disabled          | Boolean     | false               | Whether disabled                                             |                      |
| maxlength         | Number      | 140                 | Maximum input length, maximum length not restricted when set as -1 |                      |
| cursor-spacing    | Number      | 0                   | Specified distance between cursor and keyboard, unit px. The minimum value obtained for the distance between the input and the bottom and the specified cursor-spacing distance serves as the distance between cursor and keyboard. |                      |
| auto-focus        | Boolean     | false               | (About to become obsolete, please use focus directly) Automatic focus, pull keyboard up |                      |
| focus             | Boolean     | false               | Gets focus                                                   |                      |
| confirm-type      | String      | "done"              | Sets text on button in bottom right corner of keyboard       | {%version('1.1.0')%} |
| confirm-hold      | Boolean     | false               | Whether keyboard remains unhidden when button in bottom right corner of keyboard is tapped |                      |
| bindinput         | EventHandle |                     | input event triggered during keyboard input, event.detail = {value: value }, processing function can return a string directly, input box content will be replaced |                      |
| bindfocus         | EventHandle |                     | Triggered during input box focus, event.detail = {value: value} |                      |
| bindblur          | EventHandle |                     | Triggered when input box loses focus, event.detail = {value: value} |                      |
| bindconfirm       | EventHandle |                     | Triggered when Done button tapped, event.detail = {value: value} |                      |

**type valid values:**

| Value  | Description                        |
| ------ | ---------------------------------- |
| Text   | Text input keyboard                |
| number | Number input keyboard              |
| idcard | ID card input keyboard             |
| digit  | Digit keyboard with decimal points |

**confirm-type valid values:**

| Value  | Description                             |
| ------ | --------------------------------------- |
| send   | Button in bottom right corner is Send   |
| search | Button in bottom right corner is Search |
| next   | Button in bottom right corner is Next   |
| go     | Button in bottom right corner is Go     |
| done   | Button in bottom right corner is Done   |

**Sample code:**

```html
<!--input.wxml-->
<view class="section">
  <input placeholder="This is an input that can be automatically focused" auto-focus/>
</view>
<view class="section">
  <input placeholder="这个只有在按钮点击的时候才聚焦" focus="{{focus}}" />
  <view class="btn-area">
    <button bindtap="bindButtonTap">Make input box get focus</button>
  </view>
</view>
<view class="section">
  <input  maxlength="10" placeholder="最大输入长度10" />
</view>
<view class="section">
  <view class="section__title">You have inputted: {{inputValue}}</view>
  <input  bindinput="bindKeyInput" placeholder="输入同步到view中"/>
</view>
<view class="section">
  <input  bindinput="bindReplaceInput" placeholder="连续的两个1会变成2" />
</view>
<view class="section">
  <input  bindinput="bindHideKeyboard" placeholder="输入123自动收起键盘" />
</view>
<view class="section">
  <input password type="number" />
</view>
<view class="section">
  <input password type="text" />
</view>
<view class="section">
  <input type="digit" placeholder="带小数点的数字键盘"/>
</view>
<view class="section">
  <input type="idcard" placeholder="身份证输入键盘" />
</view>
<view class="section">
  <input placeholder-style="color:red" placeholder="Placeholder font is red" />
</view>
//input.js
Page({
  data: {
    focus: false,
    inputValue: ''
  },
  bindButtonTap: function() {
    this.setData({
      focus: true
    })
  },
  bindKeyInput: function(e) {
    this.setData({
      inputValue: e.detail.value
    })
  },
  bindReplaceInput: function(e) {
    var value = e.detail.value
    var pos = e.detail.cursor
    if(pos != -1){
      //Cursor is in the middle
      var left = e.detail.value.slice(0,pos)
      //Calculates cursor position
      pos = left.replace(/11/g,'2').length
    }

    //Directly returns objects, can filter input at the same time as controlling cursor position
    return {
      value: value.replace(/11/g,'2'),
      cursor: pos
    }

    //Or directly returns strings, cursor is at the very end
    //return value.replace(/11/g,'2'),
  },
  bindHideKeyboard: function(e) {
    if (e.detail.value === '123') {
      //Hide keyboard
      wx.hideKeyboard()
    }
  }
})
```

![input](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/input.png)

#### Bugs & Tips

1. `bug`: focus attribute settings are ineffective in WeChat version `6.3.30`.
2. `bug`: Ghosting problem occurs when placeholder is being focused in WeChat version `6.3.30`.
3. `tip`: The input component is a native component. It uses the system font, so font-family cannot be set.
4. `tip`: Avoid using css animation while input is being focused.



## label

Used to improve the availability of form components. The `for` attribute is used to find the corresponding `id`, or the control is placed under this tag. The corresponding control will be triggered when tapped.

`for` has higher priority than the internal control. The first control is triggered by default when there are multiple internal controls.

The controls that can currently be bound are: `<button/>`, `<checkbox/>`, `<radio/>`, and `<switch/>`.

| Attribute name | Type   | Description      |
| -------------- | ------ | ---------------- |
| for            | String | Bound control id |

**Sample code:**

```html
<view class="section section_gap">
<view class="section__title">Form component is in label</view>
<checkbox-group class="group" bindchange="checkboxChange">
  <view class="label-1" wx:for="{{checkboxItems}}">
    <label>
      <checkbox hidden value="{{item.name}}" checked="{{item.checked}}"></checkbox>
      <view class="label-1__icon">
        <view class="label-1__icon-checked" style="opacity:{{item.checked ? 1: 0}}"></view>
      </view>
      <text class="label-1__text">{{item.value}}</text>
    </label>
  </view>
</checkbox-group>
</view>

<view class="section section_gap">
<view class="section__title">label uses for to identify form component</view>
<radio-group class="group" bindchange="radioChange">
  <view class="label-2" wx:for="{{radioItems}}">
    <radio id="{{item.name}}" hidden value="{{item.name}}" checked="{{item.checked}}"></radio>
    <view class="label-2__icon">
      <view class="label-2__icon-checked" style="opacity:{{item.checked ? 1: 0}}"></view>
    </view>
    <label class="label-2__text" for="{{item.name}}"><text>{{item.name}}</text></label>
  </view>
</radio-group>
</view>
Page({
  data: {
    checkboxItems: [
      {name: 'USA', value: 'USA'},
      {name: 'CHN', value: 'China', checked: 'true'},
      {name: 'BRA', value: 'Brazil'},
      {name: 'JPN', value: 'Japan', checked: 'true'},
      {name: 'ENG', value: 'England'},
      {name: 'TUR', value: 'France'},
    ],
    radioItems: [
      {name: 'USA', value: 'USA'},
      {name: 'CHN', value: 'China', checked: 'true'},
      {name: 'BRA', value: 'Brazil'},
      {name: 'JPN', value: 'Japan'},
      {name: 'ENG', value: 'England'},
      {name: 'TUR', value: 'France'},
    ],
    hidden: false
  },
  checkboxChange: function(e) {
    var checked = e.detail.value
    var changed = {}
    for (var i = 0; i < this.data.checkboxItems.length; i ++) {
      if (checked.indexOf(this.data.checkboxItems[i].name) !== -1) {
        changed['checkboxItems['+i+'].checked'] = true
      } else {
        changed['checkboxItems['+i+'].checked'] = false
      }
    }
    this.setData(changed)
  },
  radioChange: function(e) {
    var checked = e.detail.value
    var changed = {}
    for (var i = 0; i < this.data.radioItems.length; i ++) {
      if (checked.indexOf(this.data.radioItems[i].name) !== -1) {
        changed['radioItems['+i+'].checked'] = true
      } else {
        changed['radioItems['+i+'].checked'] = false
      }
    }
    this.setData(changed)
  }
})
.label-1, .label-2{
    margin-bottom: 15px;
}
.label-1__text, .label-2__text {
    display: inline-block;
    vertical-align: middle;
}

.label-1__icon {
    position: relative;
    margin-right: 10px;
    display: inline-block;
    vertical-align: middle;
    width: 18px;
    height: 18px;
    background: #fcfff4;
}

.label-1__icon-checked {
    position: absolute;
    top: 3px;
    left: 3px;
    width: 12px;
    height: 12px;
    background: #1aad19;
}


.label-2__icon {
    position: relative;
    display: inline-block;
    vertical-align: middle;
    margin-right: 10px;
    width: 18px;
    height: 18px;
    background: #fcfff4;
    border-radius: 50px;
}

.label-2__icon-checked {
    position: absolute;
    left: 3px;
    top: 3px;
    width: 12px;
    height: 12px;
    background: #1aad19;
    border-radius: 50%;
}

.label-4_text{
    text-align: center;
    margin-top: 15px;
}
```

![label](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/label.png)



## picker

A scroll selector that pops up from the bottom. Three selectors are currently supported, these are differentiated by mode and are the ordinary selector, time selector, and date selector respectively. The default is the ordinary selector.

**Ordinary selector: mode = selector**

| Attribute name | Type                 | Default value | Description                                                  |
| -------------- | -------------------- | ------------- | ------------------------------------------------------------ |
| range          | Array / Object Array | []            | range is effective when mode is selector                     |
| range-key      | String               |               | When range is an Object Array, the key value specified in Object by range-key acts as the selector display content |
| value          | Number               | 0             | The value indicates the ordinal within the selected range (subscript starts from 0) |
| bindchange     | EventHandle          |               | A change event triggered when the value changes, event.detail = {value: value} |
| disabled       | Boolean              | false         | Whether disabled                                             |

**Time selector: mode = time**

| Attribute name | Type        | Default value | Description                                                  |
| -------------- | ----------- | ------------- | ------------------------------------------------------------ |
| value          | String      |               | Indicates selected time, format is "hh:mm"                   |
| start          | String      |               | Indicates start of effective time range, string format is "hh:mm" |
| end            | String      |               | Indicates end of effective time range, string format is "hh:mm" |
| bindchange     | EventHandle |               | A change event triggered when the value changes, event.detail = {value: value} |
| disabled       | Boolean     | false         | Whether disabled                                             |

**Date selector: mode = date**

| Attribute name | Type        | Default value | Description                                                  |
| -------------- | ----------- | ------------- | ------------------------------------------------------------ |
| value          | String      | 0             | Indicates selected date, format is "YYYY-MM-DD"              |
| start          | String      |               | Indicates start of effective date range, string format is "YYYY-MM-DD" |
| end            | String      |               | Indicates end of effective date range, string format is "YYYY-MM-DD" |
| fields         | String      | day           | Valid values are year, month, and day, indicates selector granularity |
| bindchange     | EventHandle |               | A change event triggered when the value changes, event.detail = {value: value} |
| disabled       | Boolean     | false         | Whether disabled                                             |

**fields valid values:**

| Value | Description                   |
| ----- | ----------------------------- |
| year  | Selector granularity is year  |
| month | Selector granularity is month |
| day   | Selector granularity is day   |

**Note:** Development tools temporarily only support mode = selector.

**Sample code:**

```html
<view class="section">
  <view class="section__title">Region selector</view>
  <picker bindchange="bindPickerChange" value="{{index}}" range="{{array}}">
    <view class="picker">
      Current selection: {{array[index]}}
    </view>
  </picker>
</view>
<view class="section">
  <view class="section__title">Time selector</view>
  <picker mode="time" value="{{time}}" start="09:01" end="21:01" bindchange="bindTimeChange">
    <view class="picker">
      Current selection: {{time}}
    </view>
  </picker>
</view>

<view class="section">
  <view class="section__title">Date selector</view>
  <picker mode="date" value="{{date}}" start="2015-09-01" end="2017-09-01" bindchange="bindDateChange">
    <view class="picker">
      Current selection: {{date}}
    </view>
  </picker>
</view>
Page({
  data: {
    array: ['USA', 'China', 'Brazil', 'Japan'],
    objectArray: [
      {
        id: 0,
        name: 'USA'
      },
      {
        id: 1,
        name: 'China'
      },
      {
        id: 2,
        name: 'Brazil'
      },
      {
        id: 3,
        name: 'Japan'
      }
    ],
    index: 0,
    date: '2016-09-01',
    time: '12:01'
  },
  bindPickerChange: function(e) {
    console.log('picker sent selection change, the value brought is', e.detail.value)
    this.setData({
      index: e.detail.value
    })
  },
  bindDateChange: function(e) {
    this.setData({
      date: e.detail.value
    })
  },
  bindTimeChange: function(e) {
    this.setData({
      time: e.detail.value
    })
  }
})
```

![picker](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/picker.png)



## picker-view

**An embedded page scroll selector**

| Attribute name  | Type        | Description                                                  | Minimum version |
| --------------- | ----------- | ------------------------------------------------------------ | --------------- |
| value           | NumberArray | The order of the numbers in the array indicates the ordinal item selected in the picker-view-column in picker-view (subscript starts from 0). If the number is greater than the length of the selectable items in the picker-view-column, the last item is selected. |                 |
| indicator-style | String      | Sets style for check box in middle of selector               |                 |
| indicator-class | String      | Sets class name for check box in middle of selector          |                 |
| bindchange      | EventHandle | When scrolling selection, a change event triggered when the value changes, event.detail = {value: value}; value is an array, indicates the ordinal item currently selected in the picker-view-column in picker-view (subscript starts from 0) |                 |

**Note**: Of these, only the `<picker-view-column/>` component can be placed. Other nodes will not be displayed.

#### picker-view-column

Can only be placed in `<picker-view />`. The height of its child nodes will automatically be set to the same height as the picker-view check box.

**Sample code:**

```html
<view>
  <view>{{year}}year{{month}}month{{day}}day</view>
  <picker-view indicator-style="height: 50px;" style="width: 100%; height: 300px;" value="{{value}}" bindchange="bindChange">
    <picker-view-column>
      <view wx:for="{{years}}" style="line-height: 50px">{{item}}年</view>
    </picker-view-column>
    <picker-view-column>
      <view wx:for="{{months}}" style="line-height: 50px">{{item}}月</view>
    </picker-view-column>
    <picker-view-column>
      <view wx:for="{{days}}" style="line-height: 50px">{{item}}日</view>
    </picker-view-column>
  </picker-view>
</view>
const date = new Date()
const years = []
const months = []
const days = []

for (let i = 1990; i <= date.getFullYear(); i++) {
  years.push(i)
}

for (let i = 1 ; i <= 12; i++) {
  months.push(i)
}

for (let i = 1 ; i <= 31; i++) {
  days.push(i)
}

Page({
  data: {
    years: years,
    year: date.getFullYear(),
    months: months,
    month: 2,
    days: days,
    day: 2,
    year: date.getFullYear(),
    value: [9999, 1, 1],
  },
  bindChange: function(e) {
    const val = e.detail.value
    this.setData({
      year: this.data.years[val[0]],
      month: this.data.months[val[1]],
      day: this.data.days[val[2]]
    })
  }
})
```

![picker_view](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/picker_view.png)



## radio-group

Single selector, composed of multiple `<radio/>`s internally.

| Attribute name | Type        | Default value | Description                                                  |
| -------------- | ----------- | ------------- | ------------------------------------------------------------ |
| bindchange     | EventHandle |               | A change event triggered when a selected item in `<radio-group/>` changes, event.detail = {value: value of selected item radio} |

#### radio

Radio item

| Attribute name | Type    | Default value | Description                                                  |
| -------------- | ------- | ------------- | ------------------------------------------------------------ |
| value          | String  |               | `<radio/>` ID. When this `<radio/>` is selected, a `<radio-group/>` change event will bring the `<radio/>`value. |
| checked        | Boolean | false         | Whether currently selected                                   |
| disabled       | Boolean | false         | Whether disabled                                             |
| color          | Color   |               | radio color, same as css color                               |

```html
<radio-group class="radio-group" bindchange="radioChange">
  <label class="radio" wx:for="{{items}}">
    <radio value="{{item.name}}" checked="{{item.checked}}"/>{{item.value}}
  </label>
</radio-group>
Page({
  data: {
    items: [
      {name: 'USA', value: 'USA'},
      {name: 'CHN', value: 'China', checked: 'true'},
      {name: 'BRA', value: 'Brazil'},
      {name: 'JPN', value: 'Japan'},
      {name: 'ENG', value: 'England'},
      {name: 'TUR', value: 'France'},
    ]
  },
  radioChange: function(e) {
    console.log('when a radio change event occurs, the value brought is:', e.detail.value)
  }
})
```

![radio](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/radio.png)



## slider

**Slide selector**

| Attribute name  | Type        | Default value | Description                                                  |
| --------------- | ----------- | ------------- | ------------------------------------------------------------ |
| min             | Number      | 0             | Minimum value                                                |
| max             | Number      | 100           | Maximum value                                                |
| step            | Number      | 1             | Step, value must be greater than 0 and be able to be divided exactly (max - min) |
| disabled        | Boolean     | false         | Whether disabled                                             |
| value           | Number      | 0             | Current value                                                |
| color           | Color       | #e9e9e9       | Background bar color (please use backgroundColor)            |
| selected-color  | Color       | #1aad19       | Selected color (please use activeColor)                      |
| activeColor     | Color       | #1aad19       | Selected color                                               |
| backgroundColor | Color       | #e9e9e9       | Background bar color                                         |
| show-value      | Boolean     | false         | Whether to show current value                                |
| bindchange      | EventHandle |               | An event triggered after completing a drag, event.detail = {value: value} |

**Sample code:**

```html
<view class="section section_gap">
  <text class="section__title">Set left/right icon</text>
  <view class="body-view">
    <slider bindchange="slider1change" left-icon="cancel" right-icon="success_no_circle"/>
  </view>
</view>

<view class="section section_gap">
  <text class="section__title">Set step</text>
  <view class="body-view">
    <slider bindchange="slider2change" step="5"/>
  </view>
</view>

<view class="section section_gap">
  <text class="section__title">Show current value</text>
  <view class="body-view">
    <slider bindchange="slider3change" show-value/>
  </view>
</view>

<view class="section section_gap">
  <text class="section__title">Set minimum/maximum value</text>
  <view class="body-view">
    <slider bindchange="slider4change" min="50" max="200" show-value/>
  </view>
</view>
var pageData = {}
for (var i = 1; i < 5; i++) {
  (function (index) {
    pageData['slider' + index + 'change'] = function(e) {
      console.log (if 'slider' + 'index' + 'change event occurs, the value brought is', e.detail.value)
    }
  })(i)
}
Page(pageData)
```

![slider](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/slider.png)



## switch

**Switch selector**

| Attribute name | Type        | Default value | Description                                                  |
| -------------- | ----------- | ------------- | ------------------------------------------------------------ |
| checked        | Boolean     | false         | Whether selected                                             |
| type           | String      | switch        | Style, valid values: switch, checkbox                        |
| bindchange     | EventHandle |               | A change event triggered when checked changes, event.detail={ value:checked} |
| color          | Color       |               | switch color, same as css color                              |

```html
<view class="body-view">
    <switch checked bindchange="switch1Change"/>
    <switch bindchange="switch2Change"/>
</view>
Page({
  switch1Change: function (e){
    console.log('switch1 has experienced a change event, the value brought is', e.detail.value)
  },
  switch2Change: function (e){
    console.log('switch2 has experienced a change event, the value brought is', e.detail.value)
  }
})
```

![switch](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/development/component/switch.png)



## textarea

**Multi-row input box**

| Attribute name    | Type        | Default value        | Description                                                  |
| ----------------- | ----------- | -------------------- | ------------------------------------------------------------ |
| value             | String      |                      | Input box content                                            |
| placeholder       | String      |                      | Placeholder when input box is empty                          |
| placeholder-style | String      |                      | Specified placeholder style                                  |
| placeholder-class | String      | textarea-placeholder | Specified placeholder style type                             |
| disabled          | Boolean     | false                | Whether disabled                                             |
| maxlength         | Number      | 140                  | Maximum input length, maximum length not restricted when set as -1 |
| auto-focus        | Boolean     | false                | Automatic focus, pull keyboard up                            |
| focus             | Boolean     | false                | Gets focus                                                   |
| auto-height       | Boolean     | false                | Whether to increase height automatically, style.height is ineffective when auto-height set |
| fixed             | Boolean     | false                | If textarea is in a `position:fixed` area, the specified attribute fixed needs to be displayed as true |
| cursor-spacing    | Number      | 0                    | Specified distance between cursor and keyboard, unit px. The minimum value obtained for the distance between the textarea and the bottom and the specified cursor-spacing distance serves as the distance between cursor and keyboard. |
| bindfocus         | EventHandle |                      | Triggered during input box focus, event.detail = {value: value} |
| bindblur          | EventHandle |                      | Triggered when input box loses focus, event.detail = {value: value} |
| bindlinechange    | EventHandle |                      | Called when the number of input box rows changes, event.detail = {height: 0, heightRpx: 0, lineCount: 0} |
| bindinput         | EventHandle |                      | input event triggered during keyboard input, event.detail = {value: value}, **the return value of the bindinput processing function will not be reflected on the textarea** |
| bindconfirm       | EventHandle |                      | A confirm event is triggered when Done is tapped, event.detail = {value: value} |

**Sample code:**

```html
<!--textarea.wxml-->
<view class="section">
  <textarea bindblur="bindTextAreaBlur" auto-height placeholder="自动变高" />
</view>
<view class="section">
  <textarea placeholder="placeholder颜色是红色的" placeholder-style="color:red;"  />
</view>
<view class="section">
  <textarea placeholder="This is a textarea that can be automatically focused" auto-focus />
</view>
<view class="section">
  <textarea placeholder="这个只有在按钮点击的时候才聚焦" focus="{{focus}}" />
  <view class="btn-area">
    <button bindtap="bindButtonTap">Make input box get focus</button>
  </view>
</view>
<view class="section">
  <form bindsubmit="bindFormSubmit">
    <textarea placeholder="form 中的 textarea" name="textarea"/>
    <button form-type="submit"> Submit </button>
  </form>
</view>
//textarea.js
Page({
  data: {
    height: 20,
    focus: false
  },
  bindButtonTap: function() {
    this.setData({
      focus: true
    })
  },
  bindTextAreaBlur: function(e) {
    console.log(e.detail.value)
  },
  bindFormSubmit: function(e) {
    console.log(e.detail.value.textarea)
  }
})
```

#### Bugs & Tips

1. `bug`: In WeChat version `6.3.30`, when `textarea` is rendered in a list, the location of the newly added `textarea` is miscalculated during automatic focus.
2. `tip`: `textarea` `blur` events will be later than `tap` events on the page. If you need to get the `textarea` in a `button` tap event, you can use `form` `bindsubmit`.
3. `tip`: Modifying user input in multiple rows of text is not recommended, therefore the `textarea`'s `bindinput` processing function will not reflect the return value on the `textarea`.
4. `tip`: `The textarea` component is a native component created by the client, its level is the highest.
5. `tip`: Please do not use the `textarea` component in `scroll-view`.
6. `tip`: `css` animation is ineffective on the `textarea` component.