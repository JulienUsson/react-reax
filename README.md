# Redux-reax

An another way to write your Redux app. 
Inspired by [Redux Sauce](https://github.com/infinitered/reduxsauce) and [Vuex](https://vuex.vuejs.org/en/).

[![npm version](https://badge.fury.io/js/redux-reax.svg)](https://badge.fury.io/js/redux-reax)

# Why?

Because i like the Vuex syntax and React. 

With Redux-reax you can write reducers and actions like this :

![example](./example.png)

# Installation

- Install and configure [redux](https://redux.js.org/) and [react-redux](https://github.com/reactjs/react-redux)
- Run `npm install --save redux-reax` to install redux-reax
- Install and configure [redux-thunk](https://github.com/gaearon/redux-thunk) to use Actions

# Usage

## Create a module

A module contains a state, mutations and actions.

```Javascript
import { createModule } from 'redux-reax'

const { reducer, creators } = createModule({
  state: {...},
  mutations: {...},
  actions: {...},
})

export const counterReducer = reducer
export const counterCreators = creators
```

## State

The state object contains the initial state of the module.

```Javascript
const state = {
    count: 0,
}
```

## Mutations

Mutations is the only way to change state. Each mutations must return a new state object.
:warning: Mutations must be synchronous.

```Javascript
const mutations = {
    increment(state) {
        return { count: state.count + 1 }
    },
}
```

## Actions 

Actions are asynchronous mutations. It can commit mutations or dispatch actions.

```Javascript
const actions = {
    incrementAsync({ commit, dispatch, getState }, timeout) {
        setTimeout(() => {
          commit('increment')
        }, timeout)
    }
}
```

## Usage with react-redux

```Javascript
import { counterCreators } from './store/counter'

const mapStateToProps = state => ({
  count: state.counter.count,
})

export default connect(mapStateToProps, counterCreators)(Component)
```

# Examples

- [Counter](https://github.com/JulienUsson/react-reax/tree/master/examples/counter)

Running the examples:

``` bash
$ npm install
$ npm start # serve examples at localhost:3000
```

# License

[MIT](http://opensource.org/licenses/MIT)