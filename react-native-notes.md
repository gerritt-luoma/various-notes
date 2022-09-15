# React Native
These notes are based on the [Learn React Native](https://www.codecademy.com/learn/learn-react-native) course on codecademy.

- [React Native](#react-native)
  - [Intro](#intro)
  - [React Native Overview](#react-native-overview)
  - [Expo](#expo)
  - [Core Components](#core-components)
    - [View Component](#view-component)
    - [Text Component](#text-component)
    - [Image Component](#image-component)
    - [ScrollView Component](#scrollview-component)
    - [Button Component](#button-component)
    - [TextInput Component](#textinput-component)
  - [Accessiblity](#accessiblity)
    - [Accessible Properties](#accessible-properties)
    - [Design](#design)
  - [Styling](#styling)
    - [Stylesheets](#stylesheets)
    - [Combining Styles](#combining-styles)
    - [Width and Height](#width-and-height)

## Intro
- There are over 5.7 **billion** users on mobile devices
- Normally if you are going to develop an app for a device you would need to do so in the native language for the device
  - Java/Kotlin for android
  - Objective C/Swift for iOS
- Android and iOS make up 99.4% of all mobile devices
- React native is cross platform meaning you write all of your code in one language and it gets compiled into the native language of the devices at runtime

## React Native Overview
- React native is built with the same API as react
- Uses the same declarative UI paradigm but renders as native components
- This is not pure native development
- Uses components

## Expo
- Expo is a development platform to make universal react native apps
- It helps build, deploy, and iterate on mobile apps
- Expo isn't required to make a react native app but it makes it much easier to do so
- Expo tools:
  - `Expo Go` is an app downloaded on your phone that allows you to view your development app on your actual device
  - `Expo CLI` is a command line tool that helps you run, initialize, and build your app
  - `Expo SDK` is a set of APIs that give you better access to native APIs
  - `Expo Snack` is a web based program that allows you to write react native snippits and run them on the web


## Core Components
- Instead of using html like you do in regular react, you use `core components`
- These core components are rendered into native components on the device
- These core components include:
  - View
  - Text
  - Image
  - Button
  - TextInput
  - ScrollView
- These components are used in every react native app and are essential for development

### View Component
- The main component used in react native is the `view` component
- Views are similar to that of a `div` in html
- You are able to make responsive layouts in views by using `flexbox` or basic styling for nested components
- View components are not visible unless some sort of styling is applied to them

### Text Component
- The text component is used to render actual text to the screen
- On the web you can just wrap text in a div and it will render.  In react native, all text needs to be within text tags
- You can style the text using the style property of the text tag

### Image Component
- Image components work the same way as `img` tags in html
- You provide them a path to an image (in the form of a url) and they will download the image and render them to the screen
- You can also import an image directly from your project and set it to the image with the `source` tag

### ScrollView Component
- Since `view` components are fixed in size, you will need a bit more to make scrollable content
- `ScrollView` components allow for overflow and make the view scrollable
- `ScrollView` allows for you to customize how the view actually scrolls

### Button Component
- One of the most frequent things done on an app is pressing on parts of the UI
- Most of the core components in react native have support for press interactions
- Buttons are designed for simple presses
- Buttons have very limited styling options and customization.  This makes them very good for quick iteration and prototyping
- To capture a user press, you use the `onPress` event handler

### TextInput Component
- Most if not all apps require user text input
- This component is used to capture text/numeric input from users
- You are able to listen to changes in input from the user by using the `onChangeText` event handler

## Accessiblity
- Roughly 13% of American adults have difficulty seeing
- Applications that are inaccessible due to sight or other disabilities can cause a lot of frustration and reduce your userbase
- Inclusive apps are good for business and good for morals

### Accessible Properties
- Android and iOS have built in assistive functionalities for users with disabilities
  - Talkback
  - Voiceover
- React native has built in accessibility properties as well
- You can add textual descriptions to components without having the text appear on screen
- This is done with:
  - Setting the `accessible` property to true
  - Adding an `accessibilityLabel` to be the description of the component
  - Adding an `accessibilityHint` to provide additional detail as to what will happen after they take the action

### Design
- Another large part of accessibility is the actual design of your app
- You need to keep contrast in mind when dealing with foreground/background colors
- When someone has blurry vision, they may not be able to read what is on the screeen if it doesn't contrast well

## Styling
- Every core component (except for buttons) come with a `style` property
- Style properties are added as javascript objects
- React native styling is very similar to that of CSS

### Stylesheets
- When adding your styles directly into your components, your code readability can decrease greatly
- Thankfully, react native has the `Stylesheet API` that you can import into your projects
- This makes it so we can create our stylesheets separately from our components to produce clean, readable code
  ```
  import { StyleSheet } from 'react-native';

  const styles = StyleSheet.create({
    styleName: {
        prop1: val1,
        prop2: val2,
        ...
    },
  });
  ```
- Unfortunately, stylesheets are static meaning we can't change properties of styling based on user input

### Combining Styles
- Despite stylesheets being static, the style property has a way to handle dynamic styling
- Within the style property of components we can include a list of properties
- This list allows us to provide a stylesheet style along with conditional single properties combining static and dynamic styles
- Any styles inlined in the list will override the styles defined in the stylesheet

### Width and Height