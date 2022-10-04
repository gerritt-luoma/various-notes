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
    - [Flexbox](#flexbox)
      - [Flex Direction](#flex-direction)
      - [Flex Justify Content](#flex-justify-content)
  - [Navigation](#navigation)
    - [Navigation Patterns](#navigation-patterns)
    - [Navigation Planning](#navigation-planning)
    - [React Navigation](#react-navigation)
      - [Stack Navigation](#stack-navigation)
      - [Tab Navigation](#tab-navigation)
      - [Programmatic Navigation](#programmatic-navigation)
      - [Nested Navigation](#nested-navigation)
      - [Authentication Flow](#authentication-flow)

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
- React native doesn't always use units like pixels when dealing with size/offset
- This is due to the fact that pixels on mobile apps causes a lot of deviation due to the difference in screen sizes
- Older phones typically have a lower pixels per inch (`PPI`) than newer phones so if you use pixels for sizing, it will cause images or text to be much larger than intended
- Mobile development uses `Density-independent Pixels` or `dp` for sizing.  `dp` takes the screen `PPI` into account when setting the actual number of pixels and this is actually default in react native

### Flexbox
- Screen sizes and shapes differ between phones that your app will be supported on
- Screens also "change shape" due to rotating the device or unfolding the device
- When designing a layout, you should make your app responsive to the layout changes to account for these different sizes and shapes
- The easiest way to make a responsive design is by using `flexbox`
- The following example makes 3 colored boxes that take up the full width of the screen and an even amount of space:
  ```
  import React, { useState } from 'react';
  import { Dimensions, StyleSheet, View } from 'react-native';

  const App = () => (
    <View style={styles.layout}>
      <View style={[styles.box, { backgroundColor: 'red' }]} />
      <View style={[styles.box, { backgroundColor: 'green' }]} />
      <View style={[styles.box, { backgroundColor: 'blue' }]} />
    </View>
  );

  export default App;

  const MAX_WIDTH = Dimensions.get('window').width;
  const MAX_HEIGHT = Dimensions.get('window').height;

  export const styles = StyleSheet.create({
    layout: {
      flex: 1,
      backgroundColor: '#e5e5e5',
    },
    box: {
      flex: 1,
      backgroundColor: 'black',
    },
  });
  ```

#### Flex Direction
- Flexbox can also control the direction that children elements move within flexbox
- The default direction that flexbox moves in react native is vertically (as opposed to horizontally on the web)
- There are 4 directions for flexbox:
  - `row` renders the child elements from left to right
  - `row-reverse` renders the child elements from right to left
  - `column` renders the child elements from top to bottom (default)
  - `column-reverse` renders the child elements from bottom to top

#### Flex Justify Content
- We can also control how child elements are positioned within the parent flexbox
- This is done with the `justifyContent` property
- There are 6 total options available for `justifyContent`:
  - `center` renders the children within the center of the parent
  - `flex-start` renders the children at the start of the parent (default)
  - `flex-end` renders them at the end of the parent box
  - `space-around` renders the children with remaining space around the elements
  - `space-between` renders the children with remaining space between the elements without a space at the start or the end
  - `space-evenly` renders the children with remaining space evenly divided with space at the start and end


## Navigation

### Navigation Patterns
- There are 3 common types of navigation patterns on mobile:
  - `Tab Navigation` is when an app uses a tab bar to allow users to switch between screens.  These different screens usually contain different functionality.  These tabs typically contain the primary functionality of the app like the main post feed and a user profile
  - `Stack Navigation` is when an app makes a user swipe from screen to screen to navigate through them.  When a user navigates through the screens, a new screen is pushed or popped off the stack.  This type of navigation is for when these screens are functionally related
  - `Drawer Navigation` uses a pane that can be opened either by swiping or pressing a button.  This provides a menu where users can switch between screens.  Similar to the tab bar but can be hidden.

### Navigation Planning
- It is good practice to plan out your navigation ahead of time to group related screens together in an organized manner
- Planning also allows us to spot issues early and correct them before the need to refactor code arises
- You should sketch out a "navigation heirarchy" to get a better picture of what your navigation will look like

### React Navigation
- The library `react-navigation` is very helpful in managing navigation throughout a react native app
- This library is able to hold together multiple screens of the app and determines what screen should be rendered next
- `react-navigation` ships with out main three navigation types out of the box

#### Stack Navigation
```
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';

const Stack = createStackNavigator();

const App = () => (
  <NavigationContainer>
    <Stack.Navigator>
      <Stack.Screen name="Feed" component={FeedScreen}/>
    </Stack.Navigator>
  </NavigationContainer>
);

const FeedScreen = () => (
  <View style={styles.layout}>
    <Text style={styles.title}>First screen</Text>
  </View>
)

export default App;

const styles = StyleSheet.create({
  layout: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  title: {
    fontSize: 32,
    marginBottom: 16,
  },
});
```

#### Tab Navigation
```
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';

const FeedScreen = () => (
  <View style={styles.layout}>
    <Text style={styles.title}>Feed</Text>
  </View>
);

const CatalogScreen = () => (
  <View style={styles.layout}>
    <Text style={styles.title}>Catalog</Text>
  </View>
)

const Stack = createBottomTabNavigator();

export const AppNavigator = () => (
  <Stack.Navigator>
    <Stack.Screen name="Feed" component={FeedScreen} />
    <Stack.Screen name="Catalog" component={CatalogScreen} />
  </Stack.Navigator>
);

const App = () => (
  <NavigationContainer>
    <AppNavigator />
  </NavigationContainer>
);

export default App;

const styles = StyleSheet.create({
  layout: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  title: {
    fontSize: 32,
    marginBottom: 16,
  },
});
```

#### Programmatic Navigation
- With the built in navigators you get a cutomizable menu that users can use to navigate between the app screens
- `react-navigation` allows us to interact with the navigators programmatically which lets us move to different screens when needed
- Every screen receives a `navigation` property which is an object with many useful methods
  - **OR** you can instead use the `useNavigation` hook to get the nav object


#### Nested Navigation
- When developing an app it is very common to use multiple types of navigation to allow users to do everything you intend for them to do
- You will need to be very careful when using multiple navigators at once since you will need to account for their combined functionality


#### Authentication Flow
- When authentication is needed on an app, we need to dynamically remove screens from our navigation depending on the status of authentication
- React native will automatically move users to the correct screen once configured