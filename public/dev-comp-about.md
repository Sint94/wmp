# Base components

The framework has provided a series of base components for developers. Developers can make rapid developments by combining these base components.

What are components?

- Components are the basic constituent units of the view layer.

- Components come with some functions and WeChat styles.

- A component usually includes a `start tag` and `end tag`. `Attributes` are used to modify the component, the `content` is within the two tags.

  ```html
  <tagname property="value">
    Content goes here ...
  </tagename>
  ```

  **Note: All components and attributes use lowercase letters and are linked by a hyphen symbol -.**

### Attribute types

| Type         | Description                    | Notes                                                        |
| ------------ | ------------------------------ | ------------------------------------------------------------ |
| Boolean      | Boolean value                  | The component writes this attribute. Its value is always `true`, regardless of what the attribute is equal to. The attribute value will only be `false` when the attribute is not written on the component. If the attribute value is variable, the variable value will be converted into Boolean type. |
| Number       | Number                         | `1`, `2.5`                                                   |
| String       | String                         | `"string"`                                                   |
| Array        | Array                          | `[ 1, "string" ]`                                            |
| Object       | Object                         | `{ key: value }`                                             |
| EventHandler | Event processing function name | The `"handlerName"` is the event processing function name defined in [Page](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/app-service/page) |
| Any          | Any attribute                  |                                                              |

### Common attribute type

Attributes that all components possess:

| Attribute name | Type         | Description                   | Notes                                                        |
| -------------- | ------------ | ----------------------------- | ------------------------------------------------------------ |
| id             | String       | Component unique identifier   | Maintains uniqueness of entire page                          |
| class          | String       | Component style type          | Style type defined in corresponding WXSS                     |
| style          | String       | Component internal stylesheet | Internal styles that can be dynamically set                  |
| hidden         | Boolean      | Whether component displayed   | Default display for all components                           |
| data-*         | Any          | Custom attribute              | Will be sent to the event processing function when an event is triggered on the component |
| bind* / catch* | EventHandler | Component event               | Refer to [Events](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/framework/view/wxml/event) for more details |

### Special attributes

Almost all components have their own respective custom attributes that can modify the component's functions or styles. Please refer to the definitions for each [component](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/index#component-list).

### Component list

Base components are divided into the following seven categories:

**View container:**

| Component name                                               | Description               |
| ------------------------------------------------------------ | ------------------------- |
| [view](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/view) | View container            |
| [scroll-view](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/scroll-view) | Scrollable view container |
| [swiper](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/swiper) | Sliding view container    |

**Basic content:**

| Component name                                               | Description  |
| ------------------------------------------------------------ | ------------ |
| [icon](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/icon) | Icon         |
| [text](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/text) | Text         |
| [progress](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/progress) | Progress bar |

**Form:**

| Tag name                                                     | Description            |
| ------------------------------------------------------------ | ---------------------- |
| [button](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/button) | Button                 |
| [form](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/form) | Form                   |
| [input](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/input) | Input box              |
| [checkbox](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/checkbox) | Multi selector         |
| [radio](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/radio) | Single selector        |
| [picker](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/ker) | List selector          |
| [picker-view](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/ker-view) | Built-in list selector |
| [slider](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/slider) | Scroll selector        |
| [switch](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/switch) | Switch selector        |
| [label](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/label) | Tag                    |

**Navigation:**

| Component name                                               | Description      |
| ------------------------------------------------------------ | ---------------- |
| [navigator](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/navigator) | Application link |

**Multimedia:**

| Component name                                               | Description |
| ------------------------------------------------------------ | ----------- |
| [audio](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/audio) | Audio       |
| [image](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/image) | Image       |
| [video](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/video) | Video       |

**Map:**

| Component name                                               | Description |
| ------------------------------------------------------------ | ----------- |
| [map](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/map) | Map         |

**Canvas:**

| Component name                                               | Description |
| ------------------------------------------------------------ | ----------- |
| [canvas](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/canvas) | Canvas      |

**Service Center session:**

| Component name                                               | Description                         |
| ------------------------------------------------------------ | ----------------------------------- |
| [contact-button](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/contact-button) | Enter Service Center Session button |