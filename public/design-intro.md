### Outline

We have drawn up interface design guidelines and recommendations for WeChat Mini Programs that reflect their emphasis on speed and ease of use. The design guidelines have been developed based on respect for the user's right to know and action rights. They are aimed at creating a friendly, efficient and consistent user experience within the WeChat ecosystem. Every effort has been made to cater to a range of needs, and ensure that both the user and service provider benefit from the Mini Program platform.

### Be Friendly and Polite

To keep the user from getting distracted by the surrounding environment during use of the WeChat Mini Program service, take care when designing the Mini Program to minimize irrelevant design elements that interfere with the user's experience. Politely show to the user the services provided by the Mini Program, and guide them through actions in a friendly manner.

#### Highlight Key Points

Each screen should have a clear focus, so that the user is able to quickly grasp the key points every time they arrive at a new screen. Once the key points have been determined, try to avoid introducing other interfering elements onto the screen that are irrelevant to the decisions or actions of the user.

##### Example of Problematic Design

This screen is designed for queries, but has been augmented with numerous entry points for services that have nothing to do with querying. These are irrelevant to the user's objective and may lead them astray.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/1emphasis.dont.png)

##### Correct Design

All content irrelevant to the user's objective has been removed, clarifying the theme of the screen. Content helpful for user decisions and actions, such as recent search terms, has been provided where permitted by technical and screen controls.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/1emphasis.do.png)

##### Example of Problematic Design

Primary and secondary actions are not distinguished, bewildering the user with choice.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/1emphasis.dont2.png)

##### Correct Design

Where possible, avoid listing too many actions for the user to choose from. If multiple options are absolutely necessary, be sure to distinguish between primary and secondary actions to make the choice easier for the user.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/2flow.dont.png)

#### Keep Processes Well-defined

To facilitate easy use of a screen, when a user is engaged in an action process, avoid interrupting the user with content unrelated to that process.

##### Example of Problematic Design

A user intending to make a search is interrupted by a modal pop-up prize draw window upon entering the search screen. This is an extremely unwelcome distraction for users not interested in prize draws, and even if a proportion of users are actually tempted by the "attractive" prize draw offer, when they leave the main process to go to the draw they may forget their original intention and end up missing out on the true value of the product.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/2flow.dont.png)

### Be Clear and Explicit

Once a user has entered the Mini Program screen, you have a responsibility and obligation to clearly inform the user where they are and where they can go. The user must be able to move around the screen with ease if we are to provide them with a safe and pleasant experience.

#### Provide Clear Navigation and Freedom of Movement

Navigation is the most crucial element in ensuring that the user does not get lost when browsing and flipping between web pages. Navigation needs to tell the user where they are at the moment, where they can go, and how to get back. A navigation bar provided by WeChat is built in to all the screens of every Mini Program in the WeChat system so that the user always knows where they are and how to go back. This preserves the consistency of experience at the WeChat level, and helps the user enjoy standardized experiences and interactions within WeChat. There is then no need to expend effort on learning or change established use habits when switching between different Mini Programs and other WeChat screens.

##### WeChat Navigation Bar

The WeChat navigation bar is inherited directly from the the client. Other than the bar color, there is no need for developers to customize any content in the navigation bar. However, developers do need to define the navigation relationships between the screens of the Mini Program so that the navigation system works properly.

The WeChat navigation bar is split into a navigation area, a title area, and an action area. The navigation area controls the screen processes in the program. Currently the navigation bar comes in two different basic color shades of light and dark.

##### Navigation Area (iOS)

The first screen when entering a Mini Program in WeChat, the navigation area typically contains just one action - "Back", i.e. return to the WeChat screen where the user was before entering the Mini Program. In the sub-screen after entering the Mini Program, the actions available in the navigation area are "Back" and "Close". "Back" returns the user to the previous Mini Program interface or WeChat interface. "Close" directly exits out of the Mini Program from the current interface and returns to the WeChat screen from which the user came.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/3navigation.iOS.png)

##### Navigation Area (Android)

Only one action is available in the navigation area - direct exit out of the Mini Program to return to the WeChat or system desktop where the user was before entering the Mini Program. The back button built into the hardware on Android mobiles executes a return to the previous screen.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/3navigation.android.png)

A special situation occurs in Android navigation: when a user adds a Mini Program to their Android desktop via the menu on the action area, and then opens the Mini Program from their Android desktop, the navigation button is not displayed on the home page of the Mini Program. Only the title and action areas of the Mini Program are displayed. The Mini Program sub-screens and navigation area only allow the user to return to the previous screen, while tapping on the back button provided in the Android mobile also has the same function.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/3navigation.android.special.png)

##### Customizing the Color of the WeChat Navigation Bar (iOS and Android)

The Mini Program navigation bar supports customization of the primary background color. The color chosen must ensure usability while matching harmoniously with the two main navigation bar icons provided by WeChat. The following color effects are recommended:

Color Scheme Example

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/3navigation.color.png)

##### In-Screen Navigation

Developers can add their own navigation tools to screens as required by functional and design needs. This navigation can be made consistent across different screens. However, given the limitations imposed by the size of mobile phone screens, navigation in Mini Program screens should be as simple as possible. For screens using ordinary linear browsing only, we suggest that the WeChat navigation bar will suffice.

Developers can choose to add tabs to Mini Program screens for navigation. Tab bars may be fixed in place at the top or bottom of the screen to make it easier for the user to switch between tabs. The number of tabs used must be at least two, and not more than five. To ensure that tap zones are well-defined, no more than four tabs are recommended. No more than one set of tab bars should appear on the same screen.

The native bottom tab style provided by WeChat may be chosen for the home page of the Mini Program, but this option is only available for the home page. Icon styles, tab text, and text color may be customized during development. Refer to the Developer Guide and WeUI basic control library for specific settings such as icon size.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/3navigation.page.bottom.png)

The color of top tab bars is customizable. In selecting customized colors, be sure to pay attention to preserving the usability, visibility, and operability of tab bars.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/3navigation.page.top.png)

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/3navigation.page.top.dont.png)

#### Less Waiting Time and Prompt Feedback

Overly long waiting times in a screen will result in a bad user experience. Use of the technology provided for WeChat Mini Programs already shortens waiting times considerably. Nevertheless, when loading and waiting are unavoidable, timely feedback needs to be given so as to mitigate a negative user reaction that would result from a long waiting.

##### Loading of Start-up Screen

The Mini Program start-up screen is one of the screens that can really showcase a Mini Program's branding within WeChat. This screen will highlight the brand features and loading status of the Mini Program. Apart from the display of the brand logo, all elements on the start-up screen, such as the loading progress indicator, are provided by default by WeChat and cannot be altered by the developer.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/4miniapp.loading.png)

##### Sliding Down to Refresh Loading

WeChat provides a standardized feature for sliding down in the screen to refresh loading within Mini Programs, absolving developers of the need to develop their own refresh tool.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/4pull-to-refresh.png)

##### Examples of Incorrect Use of Slide Down Refresh

Please avoid making the errors shown below to ensure the coherence of information and usability of the interface.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/4pull-to-refresh.dont.png)

##### In-screen Loading Feedback

Developers can customize the loading style of screen content within the Mini Program. It is recommended that customized loading styles be as plain as possible both for local and global loading, using simple animation to keep the user informed of the loading progress. Developers can also use the generic screen loading styles supplied by WeChat, as shown in the image.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/4loading.page.feedback.png)

##### Modal Loading

Modal loading styles will cover the entire screen. Since they are unable to clearly communicate the exact position and content of loading and may provoke a negative reaction from the user, they should be used with caution. Please do not use modal loading for anything other than certain important global actions.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/4loading.png)

##### Local Loading Feedback

Local loading feedback refers to feedback only shown on the screen which triggered the loading. This type of feedback mechanism is more targeted and involves minimal screen disruption. This is the form of feedback recommended by WeChat. For example:

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/4loading.feedback.png)

##### Precautions for Loading Feedback

- If the loading time is too long, a cancel option should be provided, and a progress bar used to display the progress of loading.
- Animation effects should be maintained throughout the loading process. Loading without any animation can easily give the false impression that the interface has frozen.
- Do not use more than one loading animation simultaneously on the same screen.

##### Outcome Feedback

In addition to providing timely feedback during user waiting times, clear feedback also needs to be given on the outcome of actions. Different outcome feedback styles may be chosen depending on the situation. For actions localized to a screen, feedback can be provided directly in the action area. For the outcome of screen-level actions, a pop-up toast, modal dialog box or outcome screen may be used.

##### Outcome Feedback for Screen-Specific Actions

For actions localized to a screen, feedback can be provided directly in the action area, such as by tapping on a checkbox as shown below. The WeChat Design Center provides a control library for common controls. The controls in this library all come with full action feedback.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/5local.feedback.png)

##### Feedback for Global Actions - Toasts

Toasts are suited to lightweight prompts indicating success and will automatically disappear after 1.5 seconds. They do not interrupt the current flow and have minimal impact on the user, making them useful for action reminders that do not need to be emphasized, such as prompts indicating success. Note that this format is not suited for error prompts. As error prompts need to be clearly indicated to the user, the transient nature of a toast makes them inappropriate.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/5global.toast.png)

##### Outcome of Global Actions - Modal Dialog Boxes

The outcome status of actions which users need to know about can be communicated in the form of a modal dialog box, which may come with guidance for the next action.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/5global.popup.png)

##### Outcome of Global Actions - Outcome Screens

For situations where the action outcome represents the end of the current process, an action outcome screen may be used for feedback. This method is the most emphatic and explicit way of informing a user of the completion of an action. Depending on the situation, the screen may give directions for the next action.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/5global.result.png)

#### Contingency Planning for Error States

Error states and processes are often easily overlooked when designing a task or process, and more often that not it is these error scenarios which leave the user most frustrated and in need of help. Therefore, it is important to take particular care in the design of error states to provide the user with necessary status information and inform them how to resolve the situation so that they have an exit route.

The aim here is to prevent the user from encountering an incomprehensible error situation where they get stuck in a particular screen with nowhere to go. Both the modal dialog boxes and outcome screens mentioned above can be used to prompt users of an error state. Apart from this, in form screens, particularly those with lots of input fields in the form, it is also advisable to explicitly point out invalid entry values so that the user can change them accordingly.

##### Error States - Form Entry Error

When an error is reported in the form, the reason for the error should be notified at the top of the form, and the erroneous section highlighted for the user to make changes.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/6error.png)

### Provide Convenience and Elegance

The move from the physical keyboard and mouse of the PC era to the screen taps and gestures in the mobile era era has greatly simplified device input, but the accuracy of finger actions falls well short of what can be achieved with a keyboard and mouse. Adapting to this change requires developers to make full use of the unique attributes of mobile phones during the design process and offer users a convenient and elegant control interface.

#### Reduce Manual Input

The keyboard on a mobile phone is small and constrained, not only making input more difficult but also increasing the chance of input errors. In designing the interface of Mini Programs, it is therefore important to minimize user input as far as possible, and make use of existing interfaces or other easy-to-use controls to improve the user's input experience.

For example in the following image, the camera recognition API is used during the addition of a bank card to help the user input the card's details. The WeChat team has also released a number of additional WeChat Mini Program APIs such as a geographic location API. Use of these APIs will considerably enhance the efficiency and accuracy of user input and thus help improve the overall user experience.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/7less-input.png)

In addition to using APIs, where manual input by the user is the only option, as far as possible the user should be offered choices to choose from rather than requiring input via keyboard. On one hand, recalling is easier than memorizing, so having the user choose from a finite set of options tends to make input completely reliant on memory. On the other hand, there remains the problem of the small mobile phone keyboard being highly prone to input errors. In the image below, for example, a user's search is assisted by providing quick options from their past search history, minimizing and avoiding unnecessary keyboard input.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/7less-input2.png)

#### Avoid Mistaken Input

Since the interface on a mobile phone is controlled via screen taps with our fingers, which are far less precise than a mouse, we need to keep this in mind when designing the area of tap zones on controls and avoid mistaken inputs occurring as a result of tap zones that are too small or crowded. This type of problem tends to occur when interfaces originally designed for use on a computer screen are appropriated straight on to a mobile phone without any adaptation. As mobile phone screens differ in their resolution, the most appropriate pixel sizes for tapping will also vary, but lie roughly between 7 mm to 9 mm when converted into physical dimensions. In the standardized component library provided by WeChat, the various control elements have all been developed in consideration of interface tapping effects and adaptation to different screen sizes. We therefore reiterate that use of these elements is recommended, or alternatively that the dimensions of the standard controls be adopted during design.

#### Enhance Performance with APIs

The WeChat Design Center has already released a set of standard web page control libraries, including the [Sketch design control library](https://wximg.gtimg.com/shake_tv/mina/WEUI_1_0_161226_Sketch.zip) and the [Photoshop design control library](https://wximg.gtimg.com/shake_tv/mina/WeUI1.0.psd.zip) and we intend to continue to update these Mini Program components. These controls have all been designed with the characteristics of mobile device screens in mind, and are fully capable of ensuring usability and operability on a mobile screen. The WeChat development team are also working hard to keep improving and expanding the WeChat Mini Program APIs and provide a WeChat common library. Use of these resources not only provides the user with faster service, but also contributes to improving screen performance and effortlessly enhances the user experience.

### Be Consistent

In addition to the various principles discussed above, it is also recommended that the consistency and continuity of different screens be kept in mind in accessing WeChat Mini Programs, trying as much as possible to use the same controls and methods of interaction throughout the program.

Both consistent screen experience and recurring interface elements will help users accomplish their objectives with the minimum effort expended on learning, and mitigate discomfort arising from flipping between screens. Because of this, standard controls provided by WeChat are available for Mini Programs to use as required for the purposes of consistency.

### Visual Specifications

#### Font Specifications

The use of fonts within WeChat should remain consistent with the fonts of the system being run. Common font sizes are 20, 18, 17, 16, 14, 13, and 11 (pt). The specific use cases are as follows:

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/8Font.png)

##### Font Color

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/8Font.color.png)

Use black for major content and gray for secondary content. Use light gray for timestamps and default values in forms, and semi black for longer descriptive paragraphs that also counts as major content.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/8Font.color2.png)

Blue is the color used for links, green for status text indicating success, and red for errors. For Press and Disable states reduce transparency by 20% and 10%, respectively.

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/8Font.color3.png)

#### Visual Specifications for Lists

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/9List.png)

#### Visual Specifications for Form Entries

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/10Input.png)

#### Usage of Buttons

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/11button.png)![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/11button2.png)![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/11button3.png)![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/11button4.png)

#### Usage of Icons

![img](https://open.wechat.com/zh_CN/htmledition/overseas_open/images/doc_assets/mini-programs/design/12icon.png)