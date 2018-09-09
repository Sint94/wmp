# contact-button

   Service Center session button, used to display a Service Center session button on the page. Users will enter a Service Center session after tapping this button.

   | Attribute name | Type   | Default value | Description                                                  |
   | -------------- | ------ | ------------- | ------------------------------------------------------------ |
   | size           | Number | 18            | Session button size, valid values are 18-27, unit: px        |
   | type           | String | default-dark  | Session button style type                                    |
   | session-from   | String |               | When a user enters a session from this button, the developer will receive a push event with this parameter. This parameter can be used to distinguish the origin of the user entering the Service Center session. |

   **type valid values:**

   | Value         | Description |
   | ------------- | ----------- |
   | default-dark  |             |
   | default-light |             |

   **Sample code**

   ```html
   <contact-button 
     type="default-light" 
     size="20"
     session-from="weapp"
   >
   </contact-button>
   ```

   Related API: Refer to [Service Center messaging interface document](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/api/custommsg/receive#receive-messages-and-events) for more details.
   Related component: the [button](https://open.wechat.com/cgi-bin/newreadtemplate?t=overseas_open/docs/mini-programs/development/component/button) component can also enter Service Center sessions by setting open-type="contact".