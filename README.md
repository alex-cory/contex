# contex
Helpers for React to make your life a little easier

Features
--------------------

**[How to Use](#how-to-use)**  
**[Extended Render Function](#extended-render-function)**  
**[Custom React Attributes](#custom-react-attributes)**   
**[View Port Helper Decorator](#view-port-helper-decorator)**   


How to use
==========

```javascript
import { context } from 'context'
...
@contex
export default class Something extends Component {
....
}
```

Extended Render Function
------------------------

#### Regular Syntax
```javascript
...
render () {
  const { start, end } = this.props
  const { now } = this.state
  return (
    <div>{start} + {end} + {now}</div>
  )
}
...
```
#### New Syntax
```javascript
...
render (props, state) {
  const { start, end } = props
  const { now } = state
  return (
    <div>{start} + {end} + {now}</div>
  )
}
...
```
#### New Syntax Optimized
```javascript
...
render ({ start, end }, { now }) {
  return (
    <div>{start} + {end} + {now}</div>
  )
}
...
```

Custom React Attributes
-------------------------
| Attributes            | Description                                                    | Status      |
| --------------------- | ---------------------------------------------------------------------------- | ----------- |
| hide         | boolean value that will render or not render a component or string for devices such as `hide='mobile'`|  |
| show         | boolean value that will render or not render a component or string for devices such as `show='tablet and desktop only'` |  |
| href         | allows any DOM element to be clickable |  |
| hideOnMobile | hides the element when screen size is on a mobile device |  |
| columnOnMobile | changes the current element to a flex-box column on mobile |  |
| moment | if on an input of some kind, changes onChange argument to be a moment object |  |
| onEsc or onEscape | calls a function when element is focused and the escape key is hit. | |
| onEnter | calls a function when element is focused and the enter key is hit. | |
| onTab | calls a function when element is focused and the tab key is hit. | |
| truncate | takes arguments such as `1 line`, `2 lines`, etc. If no arguments are passed it defaults to `1 line`. Basically it just adds [css to the element that will truncate it](https://css-tricks.com/snippets/css/truncate-string-with-ellipsis/). | |
| row | takes a boolean or a string such as `row='mobile'` |
| row | takes a boolean or a string such as `column='desktop'` |

#### Regular Syntax
```javascript
...
render () {
  const { start, end } = this.props
  const { now } = this.state
  return (
    <div>
      {start > end && (
        <div>
          {end >= start && (
            <div>Cool</div>
          )}
        </div>
      )}
    </div>
  )
}
...
```

#### New Syntax
```javascript
...
render ({ start, end }, { now }) {
  return (
    <div show={start > end}>
      <div hide={end >= start}>Cool</div>
    </div>
  )
}
...
```

View Port Helper Decorator
--------------------------
Can also be used on regular React functions.

#### Regular Syntax
```javascript
...
componentDidMount(x,y,z){
 this.setState({
   height: window.innerHeight + 'px',
   width: window.innerWidth + 'px'
 })
}
render () {
  const { height, width, now } = this.state
  const { start, end } = this.props
  if (width <= 320) {
    // do something for Mobile
  }
  return (
    <div show={start > end} href='//google.com' hideOnMobile >
      <div hide={end >= start}>{now}</div>
    </div>
  )

}
...
```
#### New Syntax
```javascript
...
@viewPort
render (screenSize, props, state) {
  if (screenSize.mobile) {
    // do something
  }
  return (
    <div show={props.start > props.end} href='//google.com' hideOnMobile >
      <div hide={props.end >= props.start}>{state.now}</div>
    </div>
  )
}
...
```

#### New Syntax Optimized
```javascript
...
@viewPort
render ({ mobile, tablet, width, iphone4 }, { start, end }, { now }) {
  if (mobile) {
    // do something
  }
  return (
    <div show={start > end} href='//google.com' hideOnMobile >
      <div hide={end >= start}>{now}</div>
    </div>
  )
}
...
```
