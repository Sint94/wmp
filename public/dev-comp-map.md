# map

**Map**

| Attribute name   | Type        | Default value | Description                                       |
| ---------------- | ----------- | ------------- | ------------------------------------------------- |
| longitude        | Number      |               | Central longitude                                 |
| latitude         | Number      |               | Central latitude                                  |
| scale            | Number      | 16            | Zoom level, range is 5-18                         |
| markers          | Array       |               | Markers                                           |
| covers           | Array       |               | **About to be removed, please use markers**       |
| polyline         | Array       |               | Line                                              |
| circles          | Array       |               | Circles                                           |
| controls         | Array       |               | Controls                                          |
| include-points   | Array       |               | All given coordinate points included in zoom view |
| show-location    | Boolean     |               | Shows current anchor point with direction         |
| bindmarkertap    | EventHandle |               | Triggered when marker tapped                      |
| bindcontroltap   | EventHandle |               | Triggered when control tapped                     |
| bindregionchange | EventHandle |               | Triggered when field of view changed              |
| bindtap          | EventHandle |               | Triggered when map tapped                         |

**Note: The covers attribute is about to be removed, please use markers instead.**

##### markers

Markers are used to display a marked location on the map.

| Attribute | Description         | Type   | Required | Remarks                                                      |
| --------- | ------------------- | ------ | -------- | ------------------------------------------------------------ |
| id        | Marker id           | Number | No       | marker tap event callbacks will return this id               |
| latitude  | Latitude            | Number | Yes      | Floating-point number, range is -90 to 90                    |
| longitude | Longitude           | Number | Yes      | Floating-point number, range is -180 to 180                  |
| title     | Marker name         | String | No       |                                                              |
| iconPath  | Displayed icon      | String | Yes      | The image path under the project directory, supports being written as a relative path, a '/’ at the beginning indicates the relative Mini Program root directory; also supports temporary paths |
| rotate    | Angle of rotation   | Number | No       | An angle rotating clockwise, the range is 0 to 360, the default is 0 |
| Alpha     | Marker transparency | Number | No       | Default is 1, not transparent                                |
| width     | Marker icon width   | Number | No       | Default is actual width of image                             |
| height    | Marker icon height  | Number | No       | Default is actual height of image                            |

##### polyline

Specifies a series of coordinate points, a connecting line from the first item in an array to the last.

| Attribute  | Description                  | Type    | Required | Remarks                                                      |
| ---------- | ---------------------------- | ------- | -------- | ------------------------------------------------------------ |
| points     | Latitude and longitude array | Array   | Yes      | [{latitude: 0, longitude: 0}]                                |
| color      | Line color                   | String  | No       | 8-digit hexadecimal expression, last 2 digits indicate alpha value, for example: #000000AA |
| width      | Line width                   | Number  | No       |                                                              |
| dottedLine | Whether dotted line          | Boolean | No       | Default is false                                             |

##### circles

Circles displayed on map.

| Attribute   | Description  | Type   | Required | Remarks                                                      |
| ----------- | ------------ | ------ | -------- | ------------------------------------------------------------ |
| latitude    | Latitude     | Number | Yes      | Floating-point number, range is -90 to 90                    |
| longitude   | Longitude    | Number | Yes      | Floating-point number, range is -180 to 180                  |
| color       | Stroke color | String | No       | 8-digit hexadecimal expression, last 2 digits indicate alpha value, for example: #000000AA |
| fillColor   | Fill color   | String | No       | 8-digit hexadecimal expression, last 2 digits indicate alpha value, for example: #000000AA |
| radius      | Radius       | Number | Yes      |                                                              |
| strokeWidth | Stroke width | Number | No       |                                                              |

##### controls

Controls displayed on map. Controls do not move with the map.

| Attribute | Description                | Type    | Required | Remarks                                                      |
| --------- | -------------------------- | ------- | -------- | ------------------------------------------------------------ |
| id        | Control id                 | Number  | No       | Control tap event callbacks will return this id              |
| position  | Position of control on map | Object  | Yes      | Relative map position of control                             |
| iconPath  | Displayed icon             | String  | Yes      | The image path under the project directory, supports being written as a relative path, a '/' at the beginning indicates the relative Mini Program root directory; also supports temporary paths |
| clickable | Whether clickable          | Boolean | No       | Default is not clickable                                     |

##### position

| Attribute | Description                             | Type   | Required | Remarks                 |
| --------- | --------------------------------------- | ------ | -------- | ----------------------- |
| left      | How far from the left border of the map | Number | No       | Default is 0            |
| top       | How far from the top border of the map  | Number | No       | Default is 0            |
| width     | Control width                           | Number | No       | Default is image width  |
| height    | Control height                          | Number | No       | Default is image height |

The latitude and longitude of map components must be filled in. If they are not filled in, the default values are the latitude and longitude of Beijing.

**Example:**

```html
<!-- map.wxml -->
<map id="map" longitude="113.324520" latitude="23.099994" scale="14" controls="{{controls}}" bindcontroltap="controltap" markers="{{markers}}" bindmarkertap="markertap" polyline="{{polyline}}" bindregionchange="regionchange" show-location style="width: 100%; height: 300px;"></map>
// map.js
Page({
  data: {
    markers: [{
      iconPath: "/resources/others.png",
      id: 0,
      latitude: 23.099994,
      longitude: 113.324520,
      width: 50,
      height: 50
    }],
    polyline: [{
      points: [{
        longitude: 113.3245211,
        latitude: 23.10229
      }, {
        longitude: 113.324520,
        latitude: 23.21229
      }],
      color:"#FF0000DD",
      width: 2,
      dottedLine: true
    }],
    controls: [{
      id: 1,
      iconPath: '/resources/location.png',
      position: {
        left: 0,
        top: 300 - 50,
        width: 50,
        height: 50
      },
      clickable: true
    }]
  },
  regionchange(e) {
    console.log(e.type)
  },
  markertap(e) {
    console.log(e.markerId)
  },
  controltap(e) {
    console.log(e.controlId)
  }
})
```

#### Bugs & Tips

1. `tip`: The `map` component is a native component created by the client, its level is the highest.
2. `tip`: Please do not use the `map` component in `scroll-view`.
3. `tip`: `css` animation is ineffective on the `map` component.
4. `tip`: The `map` component uses the Mars coordinate system for latitude and longitude. The `type` needs to be specified as `gcj02` when calling the `wx.getLocation` interface.