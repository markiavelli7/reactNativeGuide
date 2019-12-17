# State Management in React Native

**State:** System to track a piece of data that will change over time. If that data changes, our app will 'rerender'

### useState()

useState is a hook, a hook is a function that adds some new functionality to a function component.

## Showing an Array With FlatList

```javascript
import React, { useState } from "react"
import { View, Text, Button, FlatList } from "react-native"
import styled, { css } from "@emotion/native"

var Container = styled.View``

function ColorGenerator() {
  var [colors, setColors] = useState([])
  return (
    <Container>
      <Text>This is your new color picker.</Text>
      <Button
        title="Add a Color"
        onPress={() => {
          setColors([...colors, randomRgbGenerator()])
        }}
      />
      <FlatList
        data={colors}
        keyExtractor={item => item}
        renderItem={({ item }) => {
          // item === 'rgb(0,0,0)'
          return (
            <View
              style={{
                height: 100,
                width: 100,
                backgroundColor: item,
              }}
            ></View>
          )
        }}
      />
    </Container>
  )
}

export default ColorGenerator

function randomRgbGenerator() {
  var red = Math.floor(Math.random() * 256)
  var blue = Math.floor(Math.random() * 256)
  var green = Math.floor(Math.random() * 256)

  return `rgb(${red}, ${green}, ${blue})`
}
```

## useReducer()

```javascript
import React, { useReducer } from "react"
import { View, Text, Button } from "react-native"
import styled, { css } from "@emotion/native"

import ColorCounter from "../components/ColorCounter"

function reducer(state, action) {
  if (action.type == "") {
    return state
  }

  switch (action.type) {
    case "CHANGE_RED":
      if (state.red + action.amount > 255 || state.red + action.amount < 0) {
        return state
      }
      return { ...state, red: state.red + action.amount }
    case "CHANGE_GREEN":
      if (
        state.green + action.amount > 255 ||
        state.green + action.amount < 0
      ) {
        return state
      }
      return { ...state, green: state.green + action.amount }

    case "CHANGE_BLUE":
      if (state.blue + action.amount > 255 || state.blue + action.amount < 0) {
        return state
      }
      return { ...state, blue: state.blue + action.amount }
    default:
      return state
  }
}

var initialState = {
  red: 0,
  green: 0,
  blue: 0,
}

function ColorPickerScreen() {
  var [state, dispatch] = useReducer(reducer, initialState)
  var colorString = `rgb(${state.red}, ${state.green}, ${state.blue})`
  const COLOR_INCREMENT = 20

  console.log(colorString)
  return (
    <View>
      <Text>Custom Color Generator</Text>
      <ColorCounter
        incrementColor={() => {
          dispatch({
            type: "CHANGE_RED",
            amount: COLOR_INCREMENT,
          })
        }}
        decrementColor={() => {
          dispatch({
            type: "CHANGE_RED",
            amount: -COLOR_INCREMENT,
          })
        }}
        color="Red"
      />
      <ColorCounter
        color="Blue"
        incrementColor={() => {
          dispatch({
            type: "CHANGE_BLUE",
            amount: COLOR_INCREMENT,
          })
        }}
        decrementColor={() => {
          dispatch({
            type: "CHANGE_BLUE",
            amount: -COLOR_INCREMENT,
          })
        }}
      />
      <ColorCounter
        color="Green"
        incrementColor={() => {
          dispatch({
            type: "CHANGE_GREEN",
            amount: COLOR_INCREMENT,
          })
        }}
        decrementColor={() => {
          dispatch({
            type: "CHANGE_GREEN",
            amount: -COLOR_INCREMENT,
          })
        }}
      />

      <View
        style={{
          height: 100,
          width: 100,
          backgroundColor: colorString,
        }}
      />
    </View>
  )
}

export default ColorPickerScreen
```

