# View layer

The framework's view layer has been written using WXML and WXSS. Components are used for display.

Logical layer data is sent to the view, while view layer events are sent to the logical layer.

WXML (WeiXin Markup language) is used to describe page structure.

WXSS (WeiXin stylesheet) is used to describe page style.

Components are the basic constituent units of the view.



## WXML

WXML (WeiXin Markup Language) is a tag language designed by the framework that integrates [base components](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/index) and the [event system](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event). It is able to build a page structure.

We will use the following simple examples to see what capabilities WXML possesses:

### [Data binding](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/data)

```html
<!--wxml-->
<view> {{message}} </view>
// page.js
Page({
  data: {
    message: 'Hello MINA!'
  }
})
```

### [List rendering](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/list)

```html
<!--wxml-->
<view wx:for="{{array}}"> {{item}} </view>
// page.js
Page({
  data: {
    array: [1, 2, 3, 4, 5]
  }
})
```

### [Conditional rendering](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/conditional)

```html
<!--wxml-->
<view wx:if="{{view == 'WEBVIEW'}}"> WEBVIEW </view>
<view wx:elif="{{view == 'APP'}}"> APP </view>
<view wx:else="{{view == 'MINA'}}"> MINA </view>
// page.js
Page({
  data: {
    view: 'MINA'
  }
})
```

### [Template](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/template)

```html
<!--wxml-->
<template name="staffName">
  <view>
    FirstName: {{firstName}}, LastName: {{lastName}}
  </view>
</template>

<template is="staffName" data="{{...staffA}}"></template>
<template is="staffName" data="{{...staffB}}"></template>
<template is="staffName" data="{{...staffC}}"></template>
// page.js
Page({
  data: {
    staffA: {firstName: 'Hulk', lastName: 'Hu'},
    staffB: {firstName: 'Shang', lastName: 'You'},
    staffC: {firstName: 'Gideon', lastName: 'Lin'}
  }
})
```

### [Events](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event)

```html
<view bindtap="add"> {{count}} </view>
Page({
  data: {
    count: 1
  },
  add: function(e) {
    this.setData({
      count: this.data.count + 1
    })
  }
})
```

The specific capabilities and usage methods can be viewed in the following sections:

- [Data Binding](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/data)
- [List Rendering](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/list)
- [Conditional Rendering](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/conditional)
- [Templates](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/template)
- [Events](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event)
- [Referencing](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/import)



## Data binding

The dynamic data in WXML all comes from the corresponding Page data.

### Simple binding

Data binding uses Mustache syntax (double brace) to package variables. It can act on:

#### Content

```html
<view> {{ message }} </view>
Page({
  data: {
    message: 'Hello MINA!'
  }
})
```

#### Component properties (need to be in double quotes)

```html
<view id="item-{{id}}"> </view>
Page({
  data: {
    id: 0
  }
})
```

#### Control properties (need to be in double quotes)

```html
<view wx:if="{{condition}}"> </view>
Page({
  data: {
    condition: true
  }
})
```

#### Keywords (need to be in double quotes)

`True`: if boolean type is true, a true value is represented.

`false`： If boolean type is false, a false value is represented.

```html
<checkbox checked="{{false}}"> </checkbox>
```

**Pay special attention: Do not directly write checked="false", its calculation result is a string. A true value is represented after conversion to boolean type.**

### Mathematical operations

Simple mathematical operations can be performed within `{{}}`, the following methods are supported:

#### Ternary operations

```html
<view hidden="{{flag ? true : false}}"> Hidden </view>
```

#### Arithmetic operations

```html
<view> {{a + b}} + {{c}} + d </view>
Page({
  data: {
    a: 1,
    b: 2,
    c: 3
  }
})
```

Content in view is `3 + 3 + d`.

#### Logical judgment

```html
<view wx:if="{{length > 5}}"> </view>
```

#### String operations

```html
<view>{{"hello" + name}}</view>
Page({
  data:{
    name: 'MINA'
  }
})
```

#### Data path operations

```html
<view>{{object.key}} {{array[0]}}</view>
Page({
  data: {
    object: {
      key: 'Hello '
    },
    array: ['MINA']
  }
})
```

### Composition

New objects or arrays can be composed or configured directly in Mustache.

#### Arrays

```html
<view wx:for="{{[zero, 1, 2, 3, 4]}}"> {{item}} </view>
Page({
  data: {
    zero: 0
  }
})
```

Final array composition `[0, 1, 2, 3, 4]`。

#### Object

```html
<template is="objectCombine" data="{{for: a, bar: b}}"></template>
Page({
  data: {
    a: 1,
    b: 2
  }
})
```

The final object composition is `{for: 1, bar: 2}`

The extension operator `...` expands an object

```html
<template is="objectCombine" data="{{...obj1, ...obj2, e: 5}}"></template>
Page({
  data: {
    obj1: {
      a: 1,
      b: 2
    },
    obj2: {
      c: 3,
      d: 4
    }
  }
})
```

The final object composition is `{a: 1, b: 2, c: 3, d: 4, e: 5}`。

If the object key and value are the same, this can also be expressed indirectly.

```html
<template is="objectCombine" data="{{foo, bar}}"></template>
Page({
  data: {
    foo: 'my-foo',
    bar: 'my-bar'
  }
})
```

The final object composition is `{foo: 'my-foo', bar:'my-bar'}`。

**Note:** The methods above can be composed at random, but the front will overwrite the back if any variable names are the same, for example:

```html
<template is="objectCombine" data="{{...obj1, ...obj2, a, c: 6}}"></template>
Page({
  data: {
    obj1: {
      a: 1,
      b: 2
    },
    obj2: {
      b: 3,
      c: 4
    },
    a: 5
  }
})
```

The final object composition is `{a: 5, b: 3, c: 6}`。



## List rendering

### wx:for

`wx:for` is used on a component to control the binding of an array by an attribute, that is, the various data in the array can be used to repeatedly render the component.

The default subscript variable name for the current item in the default array is `index`, and the default variable name for the current item in the array is `item.`

```html
<view wx:for="{{array}}">
  {{index}}: {{item.message}}
</view>
Page({
  data: {
    array: [{
      message: 'foo',
    }, {
      message: 'bar'
    }]
  }
})
```

Using `wx:for-item` specifies the variable name for the current element in the array;

Using `wx:for-index` specifies the variable name for the current subscript in the array:

```html
<view wx:for="{{array}}" wx:for-index="idx" wx:for-item="itemName">
  {{idx}}: {{itemName.message}}
</view>
```

`Wx:for` can also perform nesting, a multiplication table is shown below:

```html
<view wx:for="{{[1, 2, 3, 4, 5, 6, 7, 8, 9]}}" wx:for-item="i">
  <view wx:for="{{[1, 2, 3, 4, 5, 6, 7, 8, 9]}}" wx:for-item="j">
    <view wx:if="{{i <= j}}">
      {{i}} * {{j}} = {{i * j}}
    </view>
  </view>
</view>
```

### block wx:for

Similarly to `block wx:if`, `wx:for` can also be used on a `<block/>` tag to render a block containing multiple nodes. For example:

```html
<block wx:for="{{[1, 2, 3]}}">
  <view> {{index}}: </view>
  <view> {{item}} </view>
</block>
```

### wx:key

If the position of an item on the list will dynamically change or a new item is added to the list, and you want items on the list to maintain their features and status (for example, the input content in `<input/>` or the selected status in `<switch/>`), you need to use `wx:key` to specify the unique identifiers for the items on the list.

`The value of wx:key` is provided in two forms:

1. A string representing a property of an item in a for loop array, the value of this property needs to be a unique string or number on the list and cannot change dynamically.
2. The reserved keyword `*this`, representing the item in the for loop array itself. This indicates that the item itself needs to be a unique string or number. For example:

When a data change triggers the re-rendering of the rendering layer, this will calibrate components with a key. The framework will ensure that they are reordered and not recreated, to ensure that the components maintain their status and to improve the efficiency of list rendering.

**A warning will be reported if wx:key is not provided. If it is understood clearly that the list is static, or that its order does not need to be paid attention to, Ignore can be selected.**

**Sample code:**

```html
<switch wx:for="{{objectArray}}" wx:key="unique" style="display: block;"> {{item.id}} </switch>
<button bindtap="switch"> Switch </button>
<button bindtap="addToFront"> Add to the front </button>

<switch wx:for="{{numberArray}}" wx:key="*this" style="display: block;"> {{item}} </switch>
<button bindtap="addNumberToFront"> Add to the front </button>
Page({
  data: {
    objectArray: [
      {id: 5, unique: 'unique_5'},
      {id: 4, unique: 'unique_4'},
      {id: 3, unique: 'unique_3'},
      {id: 2, unique: 'unique_2'},
      {id: 1, unique: 'unique_1'},
      {id: 0, unique: 'unique_0'},
    ],
    numberArray: [1, 2, 3, 4]
  },
  switch: function(e) {
    const length = this.data.objectArray.length
    for (let i = 0; i < length; ++i) {
      const x = Math.floor(Math.random() * length)
      const y = Math.floor(Math.random() * length)
      const temp = this.data.objectArray[x]
      this.data.objectArray[x] = this.data.objectArray[y]
      this.data.objectArray[y] = temp
    }
    this.setData({
      objectArray: this.data.objectArray
    })
  },
  addToFront: function(e) {
    const length = this.data.objectArray.length
    this.data.objectArray = [{id: length, unique: 'unique_' + length}].concat(this.data.objectArray)
    this.setData({
      objectArray: this.data.objectArray
    })
  },
  addNumberToFront: function(e){
    this.data.numberArray = [ this.data.numberArray.length + 1 ].concat(this.data.numberArray)
    this.setData({
      numberArray: this.data.numberArray
    })
  }
})
```



## Conditional rendering

### wx:if

In the framework, we use `wx:if="{{condition}}"` to determine whether the code block needs to be rendered:

```html
<view wx:if="{{condition}}"> True </view>
```

`wx:elif` and `wx:else` can also be used to add an else block:

```html
<view wx:if="{{length > 5}}"> 1 </view>
<view wx:elif="{{length > 2}}"> 2 </view>
<view wx:else> 3 </view>
```

### block wx:if

Because `wx:if` is a control property, it needs to have a tag added to it. However, if we want to determine multiple component tags all at once, we can use a `<block/>` tag to package multiple components and use `wx:if` above to control attributes.

```html
<block wx:if="{{true}}">
  <view> view1 </view>
  <view> view2 </view>
</block>
```

**Note:** `<block/>` is not a component, it is just a wrapper element. It will not do any rendering on a page, it just receives control properties.

### `wx:if` vs `hidden`

Because the templates in `wx:if` may also include data binding, the framework has a local rendering process when any `wx:if` condition values are switched, because it will ensure that the condition block is removed or re-rendered during switching.

`wx:if` is also **lazy**. If an initial rendering condition is `false`, the framework will not do anything. Local rendering will only begin when the condition first becomes true.

In comparison, `hidden` is a lot simpler. The component will always be rendered, it is just a simple control for display and hiding.

In general, `wx:if` has higher switching consumption but `hidden` has higher initial rendering consumption. Therefore, it is better to use `hidden` in situations where frequent switching is required. If conditions are not too likely to change during running then `wx:if` is better.



## Templates

WXML provides templates. Code snippets can be defined in templates, then called in different places.

### Definition templates

A name attribute is used as the template name. Then code snippets are defined in `<template/>`, for example:

```html
<!--
  index: int
  msg: string
  time: string
-->
<template name="msgItem">
  <view>
    <text> {{index}}: {{msg}} </text>
    <text> Time: {{time}} </text>
  </view>
</template>
```

### Using templates

The template that needs to be used is declared using the is attribute, then the data required by the template is imported. For example:

```html
<template is="msgItem" data="{{...item}}"/>
Page({
  data: {
    item: {
      index: 0,
      msg: 'this is a template',
      time: '2016-09-15'
    }
  }
})
```

The is attribute can use Mustache syntax to dynamically determine the specific template that requires rendering.

```html
<template name="odd">
  <view> odd </view>
</template>
<template name="even">
  <view> even </view>
</template>

<block wx:for="{{[1, 2, 3, 4, 5]}}">
    <template is="{{item % 2 == 0 ? 'even' : 'odd'}}"/>
</block>
```

### Template scope

Templates have their own scope, they can only use imported data.



## Events

### What are events?

- Events are the method of communication between the view layer and the logical layer.
- Events can feed user actions back to the logical layer for processing.
- Events can be bound to components. When a trigger event is reached, the corresponding event processing function in the logical layer will be executed.
- Event objects can carry additional information, such as ids, datasets, or touches.

### Usage method for events

- An event processing function is bound to a component.

For example, `bindtap`. When a user taps on this component, it will find the relevant event processing function in the Page corresponding to the page.

```html
<view id="tapTest" data-hi="WeChat" bindtap="tapName"> Click me! </view>
```

- The parameter for the event processing function written in the corresponding Page definitions is event.

```js
Page({
  tapName: function(event) {
    console.log(event)
  }
})
```

- The information that comes out of the log is more or less as follows:

  ```json
  {
  "type":"tap",
  "timeStamp":895,
  "target": {
    "id": "tapTest",
    "dataset":  {
      "hi":"WeChat"
    }
  },
  "currentTarget":  {
    "id": "tapTest",
    "dataset": {
      "hi":"WeChat"
    }
  },
  "detail": {
    "x":53,
    "y":14
  },
  "touches":[{
    "identifier":0,
    "pageX":53,
    "pageY":14,
    "clientX":53,
    "clientY":14
  }],
  "changedTouches":[{
    "identifier":0,
    "pageX":53,
    "pageY":14,
    "clientX":53,
    "clientY":14
  }]
  }
  ```

### Event details

#### Event classification

Events are divided into bubble events and non-bubble events:

1. Bubble event: after a component event is triggered, this event will be passed to the parent node.
2. Non-bubble event: after a component event is triggered, this event will not be passed to the parent node.

WXML bubble event list:

| Type        | Trigger condition                                            |
| ----------- | ------------------------------------------------------------ |
| touchstart  | Started by finger touch action                               |
| touchmove   | Moved after finger touch                                     |
| touchcancel | Finger touch action interrupted, by call reminder or pop-up window, for example |
| touchend    | Ended by finger touch action                                 |
| tap         | Leaves immediately after finger touch                        |
| longtap     | Leaves after finger touch if 350ms exceeded                  |

**Note: Other custom component events not included in the above table, including non-specific statements, are all non-bubble events, such as <form/> submit events, <input/>input events, and <scroll-view/> scroll events (see each component for details).**

#### Event binding

Event writing is done in the same way as component attributes, in key or value form.

- A key begins with `bind` or `catch`, then the event type follows, for example, `bindtap` or `catchtouchstart.`
- A value is a string that needs a function with the same name defined in the corresponding Page, otherwise an error will be reported when an event is triggered.

`bind` event binding will not prevent bubble events from bubbling up. `catch` event binding can prevent bubble events from bubbling up.

In this example below, tapping on the inner view will trigger `handleTap3` and `handleTap2` in succession (because tap events will bubble to the middle view, the middle view has prevented the tap from bubbling and it will not be passed to the parent node again). Tapping on the middle view will trigger `handleTap2`, while tapping on the outer view will trigger `handleTap1`.

```html
<view id="outter" bindtap="handleTap1">
  outer view
  <view id="middle" catchtap="handleTap2">
    middle view
    <view id="inner" bindtap="handleTap3">
      inner view
    </view>
  </view>
</view>
```

#### Event objects

If there are no special instructions, when a component triggers an event, the processing function that the logical layer binds to this event will receive an event object.

**BaseEvent object attribute list:**

| Attribute                                                    | Type    | Description                                                  |
| ------------------------------------------------------------ | ------- | ------------------------------------------------------------ |
| [type](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event#type) | String  | Event type                                                   |
| [timeStamp](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event#timestamp) | Integer | Time stamp for when the event was generated                  |
| [target](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event#target) | Object  | Some attribute value sets for the component that triggered an event |
| [currentTarget](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event#currenttarget) | Object  | Some attribute value sets for the current component          |

**CustomEvent object attribute list (carried on from BaseEvent):**

| Attribute                                                    | Type   | Description            |
| ------------------------------------------------------------ | ------ | ---------------------- |
| [detail](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event#detail) | Object | Additional information |

**TouchEvent object attribute list (carried on from BaseEvent):**

| Attribute                                                    | Type  | Description                                                  |
| ------------------------------------------------------------ | ----- | ------------------------------------------------------------ |
| [touches](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event#touches) | Array | Touch event, a touch point information array that currently stays on the screen |
| [changedTouches](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event#changedtouches) | Array | Touch event, a currently changing touch point information array |

**Special events: <canvas/> Touch events in** 

#### type

Represents event type.

#### timeStamp

The number of milliseconds that pass from when the page is opened to when the event is triggered.

#### target

The source component for a trigger event.

| Attribute                                                    | Type   | Description                                                  |
| ------------------------------------------------------------ | ------ | ------------------------------------------------------------ |
| id                                                           | String | Event source component id                                    |
| tagName                                                      | String | Current component type                                       |
| [dataset](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event#dataset) | Object | Set on the event source component composed of custom properties beginning with `data-` |

#### currentTarget

Current event binding components.

| Attribute                                                    | Type   | Description                                                  |
| ------------------------------------------------------------ | ------ | ------------------------------------------------------------ |
| id                                                           | String | Current component id                                         |
| tagName                                                      | String | Current component type                                       |
| [dataset](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event#dataset) | Object | Set on the current component composed of custom properties beginning with `data-` |

**Instructions: You can refer to the above example for the target and currentTarget. When the inner view is tapped on, the event objects target and currentTarget received by handleTap3are both inner, while the event object target received by handleTap2 is inner and currentTarget is middle.**

##### dataset

Data can be defined in the component, this data will be passed to SERVICE via the event. Writing method: `data-` used at the beginning, multiple words are linked by a hyphen symbol `-`, and capital letters cannot be used (capital letters will automatically be converted into lowercase letters). For example, `data-element-type`. In the end, hyphens will be converted into camel case in event.target.dataset. For example, `elementType`.

**Example:**

```html
<view data-alpha-beta="1" data-alphaBeta="2" bindtap="bindViewTap"> DataSet Test </view>
Page({
  bindViewTap:function(event){
    event.target.dataset.alphaBeta === 1 // - will turn into camel case
    event.target.dataset.alphabeta === 2 // capital letters will turn into lowercase letters
  }
})
```

#### touches

touches is an array, every element is a Touch object (the touches within canvas touch events are the CanvasTouch array). Touches indicate the touch points currently staying on the screen.

##### Touch objects

| Attribute        | Type   | Description                                                  |
| ---------------- | ------ | ------------------------------------------------------------ |
| identifier       | Number | Touch point identifier                                       |
| pageX, pageY     | Number | The distance from the top left corner of the document, the top left corner of the document is the origin, the x-axis is horizontal and the y-axis is vertical |
| clientX, clientY | Number | The distance from the top left corner of the area of the page that can be displayed (the screen excluding the navigation bar), the x-axis is horizontal and the y-axis is vertical |

##### CanvasTouch objects

| Attribute  | Type   | Description                                                  | Special instructions |
| ---------- | ------ | ------------------------------------------------------------ | -------------------- |
| identifier | Number | Touch point identifier                                       |                      |
| x, y       | Number | The distance from the top left corner of the canvas, the top left corner of the canvas is the origin, the x-axis is horizontal and the y-axis is vertical |                      |

#### changedTouches

The changedTouches data format is the same as touches. It indicates that a touch point has changed, for example, from nothing to something (touchstart), a position change (touchmove), or from something to nothing (touchend, touchcancel).

#### detail

Data carried by custom events. For example, a form component submit event will carry user input and a media error event will carry the error information. See the definitions of each event in [component](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/index) definitions for more details.

The x, y and pageX, pageY brought by clicking on an event's `detail` represent the distance from the top left corner of the document.



## Referencing

WXML provides two file reference methods: `import` and `include`.

### import

`Import` can use a `template` defined by the target file in a file. For example:

A `template` called `item` has been defined in item.wxml:

```html
<!-- item.wxml -->
<template name="item">
  <text>{{text}}</text>
</template>
```

If item.wxml is referenced in index.wxml, then the `item` template can be used:

```html
<import src="item.wxml"/>
<template is="item" data="{{text: 'forbar'}}"/>
```

### import scope

import has a scope concept, that is, only templates defined in a target file will be imported. Templates imported by a target file will not be imported.

**For example: C imports B, B imports A. A template defined by B can be used in C, and a template defined by A can be used in B, but C cannot use a template** defined by A.

```html
<!-- A.wxml -->
<template name="A">
  <text> A template </text>
</template>
<!-- B.wxml -->
<import src="a.wxml"/>
<template name="B">
  <text> B template </text>
</template>
<!-- C.wxml -->
<import src="b.wxml"/>
<template is="A"/>  <!-- Error! Can not use template when not import A. -->
<template is="B"/>
```

### include

`include` can import the entire code for the target file excluding `<template/>`. It is equivalent to being copied to the `include` position. For example:

```html
<!-- index.wxml -->
<include src="header.wxml"/>
<view> body </view>
<include src="footer.wxml"/>
<!-- header.wxml -->
<view> header </view>
<!-- footer.wxml -->
<view> footer </view>
```

## WXSS

WXSS (WeiXin stylesheets) is a style language that is used to describe WXML component styles.

WXSS is used to determine how WXML components should be displayed.

Our WXSS possesses most of the features of CSS, to suit a large number of front-end developers. We have also expanded and modified CSS to make it more suitable for the development of WeChat Mini Programs.

Compared to CSS, we have expanded the following features:

- Units of measurement
- Style importation

### Units of measurement

- rpx (responsive pixel): can adapt according to screen width. Specified screen width is 750rpx. On the iPhone 6, if screen width is 375px and there are a total of 750 physical pixels, then 750rpx = 375px = 750 physical pixels, 1rpx = 0.5px = 1 physical pixel.

| Device        | rpx converted into px (screen width/750) | px converted into rpx (750/screen width) |
| ------------- | ---------------------------------------- | ---------------------------------------- |
| iPhone 5      | 1rpx = 0.42px                            | 1px = 2.34rpx                            |
| iPhone 6      | 1rpx = 0.5px                             | 1px = 2rpx                               |
| iPhone 6 Plus | 1rpx = 0.552px                           | 1px = 1.81rpx                            |

**Recommendation:** Designers can use the iPhone6 as the mockup standard when developing WeChat Mini Programs. **Note:** It is inevitable that there will be some glitches on smaller screens, please try to avoid these situations when developing.

### Style importation

External stylesheets can be imported using the `@import` statement. The relative path for the external stylesheet that needs to be imported that follows `@import` uses `;` to indicate the end of the statement.

**Sample code:**

```less
/** common.wxss **/
.small-p {
  padding:5px;
}
/** app.wxss **/
@import "common.wxss";
.middle-p {
  padding:15px;
}
```

### Internal styles

Framework components support the use of style and class attributes to control component style.

- style: static styles are written uniformly in class. When style receives a dynamic style, it will perform analysis while running. Please try to avoid writing static styles in style to prevent the rendering speed from being affected.

```html
<view style="color:{{color}};" />
```

- class: used to specify style rules, its attribute values are the selector name (style name) sets in the style rules. Style names do not need to include a `.`, they are separated by spaces.

```html
<view class="normal_view" />
```

### Selectors

The currently supported selectors are:

| Selector         | Example          | Example description                                          |
| ---------------- | ---------------- | ------------------------------------------------------------ |
| .class           | `.intro`         | Selects all components that contain class="intro"            |
| #id              | `#firstname`     | Selects all components that contain id="firstname"           |
| element          | `view`           | Selects all view components                                  |
| element, element | `view, checkbox` | Selects all document view components and all checkbox components |
| ::after          | `view::after`    | An insertion after a view component                          |
| ::before         | `view::before`   | An insertion before a view component                         |

### Global and local styles

The styles defined in app.wxss are global styles that act on every page. The styles defined in the Page WXSS file are local styles that only act on the corresponding page and will overwrite the same selector in app.wxss.