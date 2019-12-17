# Using React Navigation

## Install the Dependencies

```bash
yarn add react-navigation-stack react-native-gesture-handler react-native-reanimated
```

## Set Up Navigation in App.js

```javascript
import { createStackNavigator } from 'react-navigation-stack'
import {createAppContainer} from 'react-navigation'
import HomeScreen from "./src/screens/HomeScreen"
import AboutScreen from "./src/screens/AboutScreen"

var navigator = createStackNavigator({
  Home: HomeScreen,
  About: AboutScreen,
}, {
  initialRouteName: 'Home'
  defaultNavigationOptions: {
    title: "Business Search"
  }
});

export default createAppContainer(navigator)
```

*defaultNavigationOptions* lets us customize the header that is displayed at the top of every screen.

*createAppContainer()* is a higher order function that wraps our navigator and uses its content to decide what to render. Anything in the App.js file is taken by React Native and automatically shown on the screen of the device.

The *createAppContainer()* function creates a default React component and displays whatever content the navigator is producing inside of the component.