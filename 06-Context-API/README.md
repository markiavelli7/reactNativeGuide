# App.js

The one requirement of App.js in React Native is that we have to export a React Component.

In order to wrap our Application with the Context API we want to create a variable that will hold our wrapped navigator. Then we want a function that will return some JSX:

```javascript
var App = createAppContainer(navigator);

export default function() {
  return <App />;
}
```

## Context

Context is very similar to props.

Setting up the Blog Context:

**context/BlogContext.js**

```javascript
import React from 'react'

var BlogContext = React.createContext();

export function BlogProvider({children}) {
  return <BlogContext.Provider>{children}</BlogContext.Provider>
}
```

We do not make BlogProvider a default export, the reason for this is that we are also going to export the BlogContext from this file, and we are going to make it the default export.

## Wrap the App Container in the BlogProvider

**App.js**

```javascript
import {BlogProvider} from './src/context/BlogContext';

var App = createAppContainer(navigator);

export default function() {
  return (
    <BlogProvider>
      <App />
    </BlogProvider>
  );
}
```

## Moving Data With Context

When we create a Context object like we did in the above code, we also get something inside of that object called the Provider. The Provider accepts information and makes the information available to all of the child components. It is the actual mechanism that moves information from the Blog Post Provider down to the individual Blog posts.

## Using Context

Let's say that we are passing an initial value of 5 into the BlogContext.Provider and we want to access it in our HomeScreen.js:

**BlogContext.js**
```javascript
import React from 'react';

var BlogContext = React.createContext();

export function BlogProvider({children}) {
  return <BlogContext.Provider value={5}>{children}</BlogContext.Provider>
}

export default BlogContext
```

In the above code, we have set up our Context object with *var BlogContext = React.createContext()*. Then we have created Provider that we have already used to wrap our entire App. Inside of the provider, we have declared a value of 5 for the context object.

Now, let's say that we want to use the value of our context object inside of our HomeScreen.js:

**HomeScreen.js**
```javascript
import React, {useContext} from 'react'
import {View, Text} from 'react-native'
import BlogContext from '../context/BlogContext';

function HomeScreen() {
  var value = useContext(BlogContext);

  return (
    <View>
      <Text>This is my HomeScreen: {`${value}`}</Text>
    </View>
  )
}

export default HomeScreen
```

The first thing that we do is import the useContext() hook from react. This will help us extract the Context Object. The next thing that we do is import the context object itself (BlogContext).

Then to access and re-use the value of the context object we call useContext() and pass in the context object (BlogContext). We assign the result to the variable *value* so that we can refer to this value in our code.

