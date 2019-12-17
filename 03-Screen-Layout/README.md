# Screen Layout

## Box Object Model System

Similar to content, padding, border, margin in web development.

**Shortcuts**
- *margin*: Set the margin on all sides
- *marginVertical*: Set the margin on the top and bottom
- *marginHorizontal*: Set the margin on the left and right
- *padding*: Set the padding on all sides
- *paddingVertical*: Set the padding on top and bottom
- *paddingHorizontal*: Set the padding on the left and right
- *borderWidth*: Set the border width on all sides

## Flexbox

**Properties**
- *Align Items* Left to Right
- *Flex Direction* Default is column
- *Justify Content* Position vertically
- *Flex* Set two 1 to take as much space as possible. *flex: 1;*

# Showing Icons

By using Expo, we have access to the Vector Icons package, which has a resource set of included icons.

To use the icon, we import the **icon library** as a named export and then use the actual icon name that we are looking for inside of the component as the name prop.

```javascript
import { Ionicons } from "@expo/vector-icons";

function SearchBar() {
  return (
    <View style={styles.background}>
      <Ionicons size={30} name="ios-search" />
      <Text>Search Bar</Text>
    </View>
  );
}
```

### The Text Input

```javascript
import React from "react";
import { View, StyleSheet, TextInput } from "react-native";
import { Ionicons } from "@expo/vector-icons";

function SearchBar() {
  return (
    <View style={styles.backgroundStyle}>
      <Ionicons style={styles.iconStyle} name="ios-search" />
      <TextInput style={styles.inputStyle} placeholder="Search" />
    </View>
  );
}

var styles = StyleSheet.create({
  backgroundStyle: {
    backgroundColor: "#F0EEEE",
    height: 50,
    borderRadius: 7.5,
    marginHorizontal: 15,
    marginTop: 10,
    flexDirection: "row"
  },
  inputStyle: {
    flex: 1,
    fontSize: 18
  },
  iconStyle: {
    fontSize: 35,
    alignSelf: "center",
    marginHorizontal: 15
  }
});

export default SearchBar;
```

## Search Bar Functionality

**HomeScreen.js**
```javascript
import React, { useState } from "react";
import { View, Text, StyleSheet } from "react-native";
import SearchBar from "../components/SearchBar";

function HomeScreen() {
  var [term, setTerm] = useState("");

  return (
    <View>
      <SearchBar
        onTermSubmit={() => console.log(`Search term submitting: ${term}`)}
        term={term}
        onTermChange={newTerm => setTerm(newTerm)}
      />
      <Text>Search Screen</Text>
    </View>
  );
}

var styles = StyleSheet.create({});

export default HomeScreen;
```

**SearchBar.js**
```javascript
import React from "react";
import { View, StyleSheet, TextInput } from "react-native";
import { Ionicons } from "@expo/vector-icons";

function SearchBar({ term, onTermChange, onTermSubmit }) {
  return (
    <View style={styles.backgroundStyle}>
      <Ionicons style={styles.iconStyle} name="ios-search" />
      <TextInput
        value={term}
        onChangeText={userInputText => onTermChange(userInputText)}
        style={styles.inputStyle}
        placeholder="Search"
        autoCapitalize="none"
        autoCorrect={false}
        onEndEditing={() => onTermSubmit()}
      />
    </View>
  );
}

var styles = StyleSheet.create({
  backgroundStyle: {
    backgroundColor: "#F0EEEE",
    height: 50,
    borderRadius: 7.5,
    marginHorizontal: 15,
    marginTop: 10,
    flexDirection: "row"
  },
  inputStyle: {
    flex: 1,
    fontSize: 18
  },
  iconStyle: {
    fontSize: 35,
    alignSelf: "center",
    marginHorizontal: 15
  }
});

export default SearchBar;
```