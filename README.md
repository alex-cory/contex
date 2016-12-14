# contex
Helpers for React to make your life a little easier

How to use
==========

```javascript
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

Built In React Attributes
-------------------------
| Attributes            | Description                                                    | Status      |
| --------------------- | ---------------------------------------------------------------------------- | ----------- |
| hide         | boolean value that will render or not render a component |  |
| show         | boolean value that will render or not render a component |  |
| href         | allows any DOM element to be clickable |  |
| hideOnMobile | hides the element when screen size is on a mobile device |  |
| columnOnMobile | changes the current element to a flex-box column on mobile |  |

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

#### Old Syntax
```javascript
...
componentDidMount(x,y,z){
 this.setState({
   height: window.innerHeight + 'px',
   width: window.innerWidth + 'px'
 })
}
render () {
  const { height, width } = this.state
  if (width <= 320) {
    // do something for Mobile
  }
  return (
    <div show={false} href='//google.com' hideOnMobile >
      <div hide={true}>Cool</div>
    </div>
  )

}
...
```
#### New Syntax
```javascript
...
@viewPort
render ({ mobile, tablet, width, iphone4 }, { start, end }, { now }) {
  if (mobile) {
    // do something
  }
  return (
    <div show={false} href='//google.com' hideOnMobile >
      <div hide={true}>Cool</div>
    </div>
  )
}
...
```
