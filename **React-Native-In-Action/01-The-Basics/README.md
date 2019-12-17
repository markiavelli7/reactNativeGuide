# Basic Config

### index.js

```javascript
import React from 'react';
import {AppRegistry} from 'react-native';
import App from './App';
import {name as appName} from './app.json';

function TodoApp() {
  return <App />;
}

AppRegistry.registerComponent(appName, () => TodoApp);
```

We brought in **AppRegistry** from react-native. We also bring in the main *App* component.

In the *AppRegistry* method, we initiate the application. *AppRegistry* is the JS entry point to running all React Native apps. It takes two arguments: the **appKey**, or the name of the application we defined when we initialized the app; and a function that returns the React Native component we want to use as the entry point of the app. In this case, we're returning the *TodoApp* component.

### App.js

```javascript
import React from 'react';
import {View, Text, ScrollView, StyleSheet} from 'react-native';

function App() {
  return (
    <View style={styles.container}>
      <ScrollView keyboardShouldPersistTaps="always" style={styles.content}>
        <View />
        <Text>This is my app. Lol.</Text>
      </ScrollView>
    </View>
  );
}

var styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f5f5f5',
  },
  content: {
    flex: 1,
    paddingTop: 60,
  },
});

export default App;
```

We import a new component called *ScrollView*, which wraps the platform *ScrollView* and is basically a scrollable View component. A *keyboardShouldPersistTaps* prop of always is added: this prop will dismiss the keyboard if it's open and allow the UI to process any *onPress* events. We make sure both the *ScrollView* and the parent *View* have a *flex:1* value. *flex:1* is a style value that makes the component fill the entire space of its parent container.