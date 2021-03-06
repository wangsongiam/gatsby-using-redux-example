# Redux

https://using-redux.gatsbyjs.org/

Gatsby example site that shows use of redux.
### Original version
[https://github.com/gatsbyjs/gatsby/tree/master/examples/using-redux](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-redux)

### Diff
in `src/state/createStore.js`

original
```js
import { createStore as reduxCreateStore } from "redux"

const reducer = (state, action) => {
  if (action.type === `INCREMENT`) {
    return Object.assign({}, state, {
      count: state.count + 1,
    })
  }
  return state
}

const initialState = { count: 0 }

const createStore = () => reduxCreateStore(reducer, initialState)
export default createStore
```

in here
```js
import { combineReducers, createStore as reduxCreateStore } from "redux"

const initialState = { count: 0 }

const reducer = (state={}, action) => {
  if (action.type === `INCREMENT`) {
    return Object.assign({}, state, {
      count: state.count + 1,
    })
  }
  return state
}

const createStore = () => reduxCreateStore(combineReducers({reducer}), initialState)
export default createStore
```

final version
```js
import { combineReducers, createStore as reduxCreateStore } from 'redux'

const reducer = (state = 0, action) => {
  if (action.type === `INCREMENT`) {
    return state + 1
  }
  return state
}

const root = combineReducers({
  count: reducer,
})

const createStore = () => reduxCreateStore(root)

export default createStore

```
