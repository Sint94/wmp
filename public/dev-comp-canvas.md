# canvas

**Canvas**

| Attribute name  | Type        | Default value | Description                                                  |
| --------------- | ----------- | ------------- | ------------------------------------------------------------ |
| canvas-id       | String      |               | canvas component unique identifier                           |
| disable-scroll  | Boolean     | false         | Disables screen scrolling and pull down refresh when moved in canvas |
| bindtouchstart  | EventHandle |               | Started by finger touch action                               |
| bindtouchmove   | EventHandle |               | Moved after finger touch                                     |
| bindtouchend    | EventHandle |               | Ended by finger touch action                                 |
| bindtouchcancel | EventHandle |               | Finger touch action interrupted, by call reminder or pop-up window, for example |
| bindlongtap     | EventHandle |               | Triggered after finger presses and holds for 500ms, movement after press and hold event triggered will not trigger screen scrolling |
| binderror       | EventHandle |               | error event triggered when an error occurs, detail = {errMsg: 'something wrong'} |

**Note:**

1. **canvas tag default width is 300px, default height is 225px.**
2. **canvas-ids on the same page cannot be duplicated. If a canvas-id that has already appeared is used, the canvas corresponding to the canvas tag will be hidden and will no longer work normally.**

**Sample code: Download**

```html
<!-- canvas.wxml -->
<canvas style="width: 300px; height: 200px;" canvas-id="firstCanvas"></canvas>
<!-- When using absolute positioning, the display level of the canvas after the document stream is higher than that of the preceding canvas-->
<canvas style="width: 400px; height: 500px;" canvas-id="secondCanvas"></canvas>
<!-- Because the canvas-id is a duplicate of the previous canvas, the canvas will not be displayed and an error will be sent to AppService -->
<canvas style="width: 400px; height: 500px;" canvas-id="secondCanvas" binderror="canvasIdErrorCallback"></canvas>
// canvas.js
Page({
  canvasIdErrorCallback: function (e) {
    console.error(e.detail.errMsg)
  },
  onReady: function (e) {
    // Use wx.createContext to get drawing context
    var context = wx.createCanvasContext('firstCanvas')

    context.setStrokeStyle("#00ff00")
    context.setLineWidth(5)
    context.rect(0, 0, 200, 200)
    context.stroke()
    context.setStrokeStyle("#ff0000")
    context.setLineWidth(2)
    context.moveTo(160, 100)
    context.arc(100, 100, 60, 0, 2 * Math.PI, true)
    context.moveTo(140, 100)
    context.arc(100, 100, 40, 0, Math.PI, false)
    context.moveTo(85, 80)
    context.arc(80, 80, 5, 0, 2 * Math.PI, true)
    context.moveTo(125, 80)
    context.arc(120, 80, 5, 0, 2 * Math.PI, true)
    context.stroke()
    context.draw()
  }
})
```

Related api: [wx.createCanvasContext](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/canvas/create-canvas-context#canvas_create-canvas-context)

#### Bugs & Tips

1. `tip`: The `canvas` component is a native component created by the client, its level is the highest.
2. `tip`: Please do not use the `canvas` component in `scroll-view`.
3. `tip`: `css` animation is ineffective on the `canvas` component.