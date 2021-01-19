---
layout: post
title:      "Props and State"
date:       2021-01-19 19:57:49 +0000
permalink:  props_and_state
---


**For Dummies

Initially I was very confused about this topic. However, thanks to a LOT of medium and stackoverflow posts on the topic, i was able to get a better grasp of the concept, allowing me to go on and coplete my final Project. 

```
Basically:  Props + State = React.js 
```

## Props={properties}

It handles the transfer of data between Components. 

What is a Component you ask? A Component is an independent and reusable bit of code. It serves the same purpose as a JavaScript function, but returns HTML via a render() function.

As seen above, Props stands for Properties.  The example below aims to highlight what a prop and as well as how it can be transferred between components.

```
import React from 'react';
import ReactDOM from 'react-dom';

class Car extends React.Component {
  render() {
    return <h2>I am a {this.props.brand}!</h2>;
  }
}

class Garage extends React.Component {
  render() {
    return (
      <div>
      <h1>Who lives in my Garage?</h1>
      <Car brand="Ford" />
      </div>
    );
  }
}
ReactDOM.render(<Garage />, document.getElementById('root'));
```

In the example above We are passing the value of the *brand* props from **Garage to Car**. The Car Component has a property called brand,returned via a render function with ```{this.props.brand}```. In the Garage Component, we can see that after returning the Car component, it receives an argument of brand which sets the value of Car's property: brand to "Ford'  with this line of code ```<Car brand="Ford"/>```

The example above assumes both Components are within the same file. However, In reality, for ease, we try to seperate Components into different files and types as much as we can so we can keep track of which component is doing what. In cases like that, to gain access to props of a component in a different file, in this case Garage will gain access to the properties of Car; we want to make sure to export and import it. (see below):

```
export default class Car extends React.Component {
  render() {
    return <h2>I am a {this.props.brand}!</h2>;
  }
}
```

```
import Car from './src/components/car'

class Garage extends React.Component {
  render() {
    return (
      <div>
      <h1>Who lives in my Garage?</h1>
      <Car brand="Ford" />
      </div>
    );
  }
}
ReactDOM.render(<Garage />, document.getElementById('root'));
```



## State

It is a built in object within React that allows us to store property values that belongs to the component. When the state object changes, the component re-renders.

In order to set the state of a component, we initialize it using a constructor method. (see example below)

```
class Car extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      brand: "Ford",
      model: "Mustang",
      color: "red",
      year: 1964
    };
  }
  render() {
    return (
      <div>
        <h1>My {this.state.brand}</h1>
        <p>
          It is a {this.state.color}
          {this.state.model}
          from {this.state.year}.
        </p>
      </div>
    );
  }
}
ReactDOM.render(<Car />, document.getElementById('root'));
```

In the example above, Super(props) - allows us to use 'this' to set initial state and then store props(which is passed in as an argument) within the state. Here, we have 4 properties stored in state that are returned via the render function. e.d ```{this.state.color}``` will output *Ford* and so on. 

We do not always need to explicilty use a constructor method or call on super(). Alternatively we can directly set state within the component(see below)

```
class Car extends React.Component {
  state = {
      brand: "Ford",
      model: "Mustang",
      color: "red",
      year: 1964
    };
	}
 ```
 
 If you ask me i think it makes our code look a lot cleaner.


This is often how props are transferred between components. Also keep in mind that initial state can only be set once. However, thanks to react and its built in method called **setState()** to update the current state with new properties. This will cause the component to re-render, updating everywhere state has been called, and properties if changed, to display the freshly update set information.  It's a tricky concept to grasp at first, so i would say definitely take time to grasp this very deeply and this would make creating a React project a thousand times easier, becuase most of the time, you're just going to be passing props and updating state.

*I hope this helps and i didn't confuse you some more. Suggestions on improving this write up are welcome :)*




