# The Basic Layout

Inside of our *src* folder, there will be a sub-folder called *screens*. Inside of *screens*, we have one file right now called *HomeScreen.js*

```javascript
import React from 'react';
import { Text, StyleSheet } from 'react-native';

const HomeScreen = () => {
  return <Text style={styles.text}>Still DRE</Text>;
};

const styles = StyleSheet.create({
  text: {
    fontSize: 30
  }
});

export default HomeScreen;
```

Basic Setup

```javascript
import React from 'react';
import { Text, StyleSheet } from 'react-native';
```

1. We need React to use JSX
2. We import *Text* and *Stylesheet* from *react-native*.

The react-native library knows how to take some information from React components and use it to show some content on the mobile device.

### Adding a New Screen

**screens/ComponentScreen.js**

```javascript
import React from 'react'
import { Text, StyleSheet } from 'react-native'

function ComponentScreen() {
  return (
    <Text style={styles.text}>Picture Me Rollin'</Text>
  )
}

var styles = StyleSheet.create({
  text: {
    fontSize: 30
  }
})

export default ComponentScreen
```

## Adding a Newly Created Screen to the Project

In order to actually be able to see our screen, we have to edit our *App.js* file to let it know that we have added a screen and want to see it in our project:

**App.js**

```javascript
import { createStackNavigator, createAppContainer } from 'react-navigation';
import HomeScreen from './src/screens/HomeScreen';
import ComponentsScreen from './src/screens/ComponentsScreen'

const navigator = createStackNavigator(
  {
    Home: HomeScreen,
    Components: ComponentsScreen
  },
  {
    initialRouteName: 'Components',
    defaultNavigationOptions: {
      title: 'Still DRE'
    }
  }
);

export default createAppContainer(navigator);
```

*createStackNavigator* holds an object that defines the navigation options for our project.

Above, we switched the *initialRouteName* inside of *createStackNavigator* to 'Components', this sets the initial route to the project that we just created.

## Primitive React Elements

Elements that are provided by the React Native library. They allow us to show some amount of basic content to a user. A *<Text>* element is a primitive React element that shows some very basic text to a user.

#### Examples of Primitive Elements:

**Text** - Show some text to the user. *Any text placed outside of a <Text> will result in an error.*

**View** - General purpose element used for grouping other elements or styling

**Image** - Show an image

**Button** - Show a button the user can press. Gives us some feedback whenever the user presses it


## createStackNavigator and createAppContainer

These are named exports from the react-navigation package. This package lets us set up navigation between pages and show different screens to the user.


# Building Lists

## FlatList Element

- Turns an array into a list of elements
- We are required to pass in a 'prop' of 'data' - the array of data that we are going to create a bunch of elements out of
- Also required to pass in a 'renderItem' prop - function that will turn each individual item into an element
- Coming from React on the web, we might be used to 'mapping' an array of data to build a list - FlatList is better with RN.

```javascript
import { FlatList } from "react-native"

function ListScreen() {
  var friends = [{name: "Frank"}, {name: "Robert"}, {name: "Max"},]
  return (
    <View>
      <FlatList data={friends} renderItem={(element) => {
        
      }} />
      <Text style={styles.titleText}>This is the List Component!! 👹</Text>
    </View>
  )
}
```

When we use renderItem and pass in our function, the argument that we have to work with in our function (element in our case) really has two properties on it:

```javascript
{
  item: {name: "Frank"},
  index: 0
}
```

To make things a little bit simpler (instead of referencing element.item.name), we usually make use of destructuring:

```javascript
renderItem={({item}) => {
  return <Text>{item.name}</Text>
}}
```

**Note**: Just like mapping over a list of elements in React for web development, we have to give each list item a unique key so that it knows which items it should re-render. Without keys, React has no idea which elements it should re-render.

**Here's how we fix the no-key warning:**

*There are two different methods to implement the key prop*

### Method 1 - Add a key property to our data structure:

```javascript
var friends = [
  { name: "Frank", key: "1" },
  { name: "Robert" key: "2" },
  { name: "Max" key: "3" },
  { name: "Joe" key: "4" },
  { name: "Rick" key: "5" },
  { name: "Daniel" key: "6" },
  { name: "Mikey" key: "7" },
  { name: "Nick" key: "8" },
]

<FlatList
        data={friends}
        renderItem={({ item }) => {
          return <Text key={item.name}>{item.name}</Text>
        }}
      />
```

**Keys must be strings, consistent between renders, and they must be unique.**

### Method 2 - Add the key within the FlatList element using keyExtractor

```javascript
<FlatList
  keyExtractor={friend => friend.name}
  data={friends}
  renderItem={({ item }) => {
    return (
      <Text style={styles.listItemText} key={item.name}>
        {item.name}
      </Text>
    )
  }}
/>
```

The *keyExtractor* property takes a function as a value, we provide the function and our job is to return a unique piece of data that will be used as the unique key for each item. In our case, the names are all unique, so we can use them as the key.

## Additional FlatList Props

**horizontal**: If we add in *horizontal* as a prop to our JSX tag like this:

```javascript
<FlatList horizontal ... />
```
we are telling our list that we want it to scroll horizontally

**showsHorizontalScrollIndicator**: This prop will hide the scrollbar if we desire that behaviour

```javascript
<FlatList showsHorizontalScrollIndicator={false} ... />
```

# Navigating Users Between Screens

## Buttons with React Native

**Button**: Very simple component for showing a button and detecting a press

```javascript
<Button
  title="Go to Components Demo"
  onPress={e => console.log("Button pressed")}
/>
```

**TouchableOpacity**: Highly customizable component that can detect a press on just about any kind of element

```javascript
<TouchableOpacity onPress={e => console.log("Lol")}>
  <Text>Go to List Demo</Text>
</TouchableOpacity>
```

