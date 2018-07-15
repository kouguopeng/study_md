#

# #

#

## 函数组件(Functional Components)

`class Email extends React.Component { render() { return (`

`<div>`
      `  {this.props.text}`
    `  </div>`

`); } };
`
`const Email = (props) => (

<div>
    {props.text}
  </div>

);`
以上写法效果相同

## 添加状态到一个组件（Add State To A Component）

通过组件的state来改变样式

class Email extends React.Component { state = { text:'ABC' } render() { return (

<div>
        {this.state.text}
      </div>

); } };

## 更新组件状态（Update state with setState）

通过function setState()来改变state

this.setState({ subject: 'Hello! This is a new subject' })

this.setState((prevState) => ({ count: prevState.count + 1 }))

## PropTypes

### Type checking a Component's Props with PropTypes（用PropTypes来检查组件内传送过来的props是否符合规范）

proptypes是一个软件包，让我们明确我们要看到从一开始就警告我们在开发过程中，如果道具的传递给组件不匹配的期望是什么，正确的数据类型。

npm install --save prop-types

## Controlled Components

npm install --save escape-string-regexp sort-by

## 生命周期（Lifecycle Events）

### componentWillMount()

invoked immediately before the component is inserted into the DOM

### componentDidMount()

invoked immediately after the component is inserted into the DOM 接受数据时候使用 import React, { Component } from 'react'; import fetchUser from '../utils/UserAPI';

class User extends Component { constructor(props) { super(props)

```
this.state = {
  name: '',
  age: ''
}
```

}

componentDidMount() { fetchUser().then((user) => this.setState({ name: user.name, age: user.age })) }

render() { return (

<div>
  <p>Name: {this.state.name}</p>
  <p>Age: {this.state.age}</p>
</div>

) } }

export default User;

### componentWillUnmount()

invoked immediately before a component is removed from the DOM

### componentWillReceiveProps()

invoked whenever the component is about to receive brand new props

## Lesson summary

### Adding to the DOM

constructor() componentWillMount() render() componentDidMount()

### Re-rendering

componentWillReceiveProps() shouldComponentUpdate() componentWillUpdate() render() componentDidUpdate()

### Removing from the DOM

componentWillUnmount()

# React router

## Introduction

React Router is a collection of navigational components that compose declaratively with your application.

## 动态路由（Dynamic Routing Recap）

Short-circuit Evaluation Syntax In this video and when we created the "Now showing" from earlier section, we used a somewhat odd looking syntax:

## Short-circuit Evaluation Syntax

{this.state.screen === 'list' && (

<listcontacts contacts="{this.state.contacts}" ondeletecontact="{this.removeContact}">
)}</listcontacts>

{this.state.screen === 'create' && (

<createcontact>
)}</createcontact>

## The BrowserRouter Component

npm install --save react-router-dom/npm install --save react-router-native

### BrowserRouter(未学)

1、Listens to changes in URL 2、Makes sure that the correct screen shows up

## The Link Component
### demo  
<Link to="/about">About</Link>

<Link to={{
  pathname: '/courses',
  search: '?sort=name',
  hash: '#the-hash',
  state: { fromDashboard: true }
}}>
  Courses
</Link>

## The Route Component

## Finishing The Contact Form

npm install --save form-serialize

concat

#REDUX
##What is Redux/Why does it exist?
官方注释：a predictable state container for JavaScript apps.
Summary
Redux is a JavaScript library used to manage an application’s front-end state. Redux isn’t a requirement for React apps, but as web apps become more complex, bugs may arise from mismanaging state. Global state in Redux apps is held within a single source of truth: the store. Since updates to state are tightly controlled, this makes Redux very predictable. In fact, one of the main reasons that developers love Redux is its predictability.

##How Redux Improves Predictability
Summary
Redux improves predictability in web apps in several ways:

data is consolidated to one centralized location
components have to request access to that data
data in the store flows in one direction
strict rules are set on how the store can be updated

## Redux Stores vs Component State
### Three Principles
Single source of truth
Redux State is Read-Only
Changes are made with pure functions

## Pure Functions
### What are Pure Functions?
Pure functions are integral to how state in Redux applications is updated. By definition, pure functions:

1、Return one and the same result if the same arguments are passed in
2、Depend solely on the arguments passed into them
3、Do not produce side effects

### Using Pure Functions
Pure functions are core elements in functional programming. Along with avoiding data mutation and side effects, pure functions tie in pretty nicely with the idea of composition as well. How?

For one, pure functions are inherently modular, making them easy to test. Since pure functions always produce the same result given the same arguments, you won’t have to worry about other parts of your app affecting output data. During debugging and inspection, this gives you additional, well-defined points of control in your app.

On top of that, pure functions also make maintaining code much simpler. Recall that pure functions do not produce side effects. This means that as you refactor your app, changes to a pure function will not adversely affect the world outside of it.

While the usage of pure functions in an app adds a lot of benefits, you can still have both pure and impure functions in apps that you build. Using impure functions isn’t necessarily “bad programming”. For example, a button with an event handler that updates the DOM wouldn’t be great use cases for pure functions because the event handler is updating the DOM (i.e., producing a side effect!). Pure functions lend themselves to better quality code, and having this in all in mind as you build your apps will make you a stronger programmer.

### Summary
Pure functions are not exclusive to Redux (or even JavaScript), but they do support predictability in an application

## Array's .reduce() Method
The central idea of .reduce() is that it takes in a large amount of data but returns a single value. .reduce() is a higher-order function, meaning that it takes in a function (i.e., a callback) as an argument.

### example:
const iceCreamStats = [
  {
    name: 'Amanda',
    gallonsEaten: 3.8
  },
  {
    name: 'Geoff',
    gallonsEaten: 5.2
  },
  {
    name: 'Tyler',
    gallonsEaten: 1.9
  },
  {
    name: 'Richard',
    gallonsEaten: 7923
  }
];

iceCreamStats.reduce( (accumulator, currentValue) => {
  return accumulator + currentValue.gallonsEaten;
}, 0);

# Redux At Its Core
## Introduction
This is the graphic we just looked at. As you can see, there are three main parts to Redux:

actions

reducers
the store

### Summary
The whole goal of Redux is to make state management in your application more manageable. Typically, you use Redux in combination with React. However, they don't have to be used together. Redux can really be used in any application that needs help managing state.

The main concepts of Redux are actions, reducers, and the store. The store is the source of truth for the state in your application, reducers specify the shape of and update the store, and actions are payloads of information which tell reducers which type of events have occurred in the app.

## Create Actions
The browser allows you to set up event listeners and respond to certain events. Redux does too -- but the events are called actions. These actions are payloads of information that you set up to describe any event in the application that should update that application’s state.

Actions are JavaScript objects that describe any event that should update the application’s state. These objects must have a type property in order to distinguish the specific type of action that occurred.

### demo

`const LOAD_PROFILE = 'LOAD_PROFILE';`

`const myAction = {`
`  type: LOAD_PROFILE`
`};`


💡 Action Recommendations 💡

A couple of things to keep in mind as you build action objects:

Prefer constants rather than strings as the values of type properties. Both work -- but when using constants, the console will throw an error rather than fail silently should there be any misspellings (e.g. LAOD_PROFILE vs. LOAD_PROFILE).
Keep the payload as small as possible. Have your resources only send the necessary data!

### Action Creators
While Redux actions are just JavaScript objects -- these objects are not very portable. In order to make actions more portable and easier to test, we can wrap these actions in functions. These functions are called actions creators. The term "action creator" makes sense, since it's really just a function that creates and returns an action.

`const submitUser = user => ({`
`type: SUBMIT_USER,`
`user`  
`});`

Now, whenever we need a SUBMIT_USER action, we can just call the submitUser() function, pass it a user, and it will generate the action!

### Summary
In this section, we looked at actions and action creators.

Actions in Redux are JavaScript objects that you set up to describe any event in your application that should update your application’s state.

`const LOAD_PROFILE = 'LOAD_PROFILE';`

`const loadProfileAction = {
  type: LOAD_PROFILE
};
`
Plain objects aren't very portable, so in order to make actions more portable and easy to test, they’re usually wrapped in functions called "action creators". These actions aren’t modifying the state themselves; instead, they’re just specifying that some event occurred which should update the state. It is important to keep actions as concentrated as possible, free of side effects.

`const loadProfile = user => ({
  type: LOAD_PROFILE,
  user
});`

Now the question is: what’s next? As of right now all we’ve done is talk about creating objects (actions) and wrapping those objects in functions (action creators). There are still two questions we need to answer. First, how does Redux know that invoking these action creators should modify the application’s state? Second, how do we specify how the application’s state should change, based off of these actions? These questions lead us to the topic of reducers in Redux.

## Create Reducers

>A reducer is just a function which receives the current state and the specific action which was returned from an action creator:

`function reducer (state, action) {`
`  switch (action.type) {`
`    case 'SUBMIT_USER' :`
`      return Object.assign({}, state, {`
`        user: action.user`
`      })`
`  }`
`}`


In the example above, whenever a submitUser action creator is invoked and passed to a reducer, our switch statement will match the 'SUBMIT_USER' case. Then a new state will be created and a user property will be added (or edited) to that new state whose value is the user we originally passed to the submitUser action creator.

### A Reducer is Pure
>Recall that pure functions:

>Return one and the same result if the same arguments are passed in
>Depend solely on the arguments passed into them
>Do not produce side effects
>For a refresher, feel free to review Pure Functions from Lesson 1: Why Redux?

The whole point of a reducer is that it takes in the current state, an action, and returns the new state. That’s it! If you’re doing anything more than that in your reducer, your code is probably doing something wrong. A reducer should not:

* Change its arguments
* Have side-effects (asynchronous requests, changing scope variables, etc.)
* Use other impure functions
In other words, a reducer needs to be a pure function!

### UIState

>A fundamental part of being able to construct a well-built React/Redux application is understanding when to have state live in Redux, and when to have state live in React components. Now, there isn’t a hard set rule for this and it’s something even the React community can’t come to an agreement on, so everything below will be my opinion.

>The first question I ask myself when deciding where a piece of state should live is, “Will two components rely on this same piece of state?” If that answer is yes, you’ll almost always want to have Redux manage that piece of state. The reason for that is if the piece of state lives in Redux, no matter what the relationship is between the two components, each can gain access to the needed state.

>The next question I ask myself is, “What does that caching story for this piece of state look like?” If the operation to get the data was expensive, it may be worth putting it in Redux so you don’t have to re-fetch it every time the component mounts. For any other scenarios, you’re probably fine just sticking to local component state as you’re used to.

### Summary
Reducers are just functions; they receive the current state and an action object, they must be a pure function, and they should always return either the new state or the previous state.

  `function myReducer (state = initialState, action) {`

    `if (action.type === CHANGE_NAME) {`
      `return {`
        `...state,`
        `name: 'Tyler'`
      `};`
    `}`
  `return state;`
`}`

Store your state in Redux if two components rely on the same piece of state, or if the operation to get that state was expensive.

## Create A Redux Store
In order to create a store, you pass a reducer function to Redux’s createStore() method as the first argument. What’s returned from createStore() is the store itself, which has three properties on it:

* getState()
>store.getState() doesn’t take any arguments and will return the current state of the store.

* dispatch()
>store.dispatch(action) takes in an action object and will call the reducer function, passing it the current state and the action which was dispatched. For example:


    `// store.js`

    `import { createStore } from 'redux';`
    `import reducer from '../reducers/reducer';`

    `let store = createStore(reducer);`

    `const receiveComment = comment => ({`
      `  type: 'RECEIVE_COMMENT',`
      `  comment`
      `});`

      `export default store;`
      `store.getState(); // []`
      `store.dispatch(receiveComment('Redux is great!'));`
      `store.getState(); // ['Redux is great!']`

* subscribe()

>store.subscribe(cb) takes in a listener callback function that will be invoked whenever the state of the store changes.
Now that we have our actions and we have our reducer,

### Summary
>Redux comes with a method called createStore(). It takes in a reducer function as its first argument and returns a store object which has these methods on it:

* getState()
* dispatch()
* subscribe()

## All Together Now!

### Summary
>Actions are dispatched into the store's reducer, telling it what information needs to be updated. Since all three of these core pieces are interconnected in helping manage an application’s state, it may be tricky to learn them individually the first time. Feel free to check out the previous sections again for a refresher if needed!

### Lesson Summary
>We covered a lot in this lesson. To recap:

* The reducer is responsible for deciding the shape and the initial state of the store and when an action is dispatched, the state it * * returns will become the new state of the store.
* The state of Redux is stored in the Store.
* An action is a payload of information describing state changing events that occur in the application.
* The store can be used to dispatch actions, get the current state of the store, and subscribe to any changes.

# React&Redux
## Introduction
>Up until this point, we’ve only used "vanilla" Redux. That is, everything so far has been agnostic in regards to any sort of framework or view library.

>To recap, earlier we created a store with createStore(), passing it a reducer function. Then we learned how to use dispatch(), getState(), and subscribe() to hook up Redux to a React app. As you probably noticed: it didn’t work out that well! We ended up passing the store down to the main component in order to get access to dispatch(), getState(), and subscribe(). This worked fine for a small application, but it doesn't scale well with additional components.

>This doesn’t mean Redux is ineffective; we just don’t have the right abstraction. Until this point we’ve been learning about low-level Redux methods and trying to use those with React. What if there were a better abstraction, one specifically for using Redux with React? Good news! There is, and it’s called react-redux, made by the creators of Redux itself.

>The biggest benefit of react-redux is when dispatching actions and accessing the Redux store from inside of your React components. This is all possible through react-redux's Provider component and the connect() method.

>connect() allows you to specify which components should receive which data from the store and Provider makes connect() work properly. Let’s dive into both of those a bit more.

## Provider
### setup
> npm install --save react-redux

### Using Provider
The magic behind Provider is React’s context feature. From the React docs:

>"In some cases, you want to pass data through the component tree without having to pass the props down manually at every level. You can do this directly in React with the powerful 'context' API"

The reason Provider makes connect() possible is because, just as the docs describe, Provider makes it possible to “pass data through the component tree without having to pass the props down manually at every level”.

### Provider Recap
>Provider makes it possible for Redux to pass data from the store to any React components that need it. It uses React’s context feature to make this work.

>Components that need access to the store, however, still need a way to “connect” to it. We mentioned the connect() function earlier, which utilizes a technique in functional programming called currying. Before we see connect() in action, let’s take a closer look at how currying works!

## Currying

Here we have a simple plate() function which takes in two arguments: avegetable and a fruit.

    function plate(vegetables, fruit) {
      return `I ate a plate of ${vegetables} and ${fruit}!`;
    }

    plate('corn', 'apples');




    function plate(vegetables) {
      return function fruitFunc (fruit) {
        return `I ate a plate of ${vegetables} and ${fruit}!`;
      }
    }

    const fruitFunc = plate('corn');



    function plate(vegetables) {
        return function fruitFunc (fruit) {
          return `I ate a plate of ${vegetables} and ${fruit}!`;
        }
      }

    const sentence = plate('corn')('apples');

💡 Function Calls 💡

>If you’re ever in doubt of how many functions need to be returned, take a look at the number of function calls! The general rule is that number of functions returned is one less than the number of functions called. For example, if you see three function calls, you need to return two functions.


### Currying Recap
Currying is the process of partially providing the input to a function that requires additional data. The part of the Redux API that uses currying is its connect() method. Let's take a look!

## Connect

### Installation

`npm install --save react-redux`

`import { connect } from 'react-redux';`

### Using Connect
>connect() is a function that makes it possible for a component to get both state and dispatch from the Redux store. Its signature is interesting. Fully used, it looks like this:

    connect(mapStateToProps, mapDispatchToProps)(MyComponent)

>As a preview, MyComponent is the component you want to receive store state, dispatch, or both. mapStateToProps() is a function that receives the current store, current props, and what it returns will be available to MyComponent as props. mapDispatchToProps() allows you wrap action creators inside of dispatch. Let's take a closer look at each of them!

* mapStateToProps()

>mapStateToProps() allows you to specify which data from the store you want passed to your React component. It takes in the store's state, an optional ownprops argument, and returns an object. Check out its complete signature:

    mapStateToProps(state, [ownProps])

As stated in the Redux docs:
>“If this argument is specified, the new component will subscribe to Redux store updates. This means that any time the store is updated, mapStateToProps will be called. The results of mapStateToProps must be a plain object, which will be merged into the component’s props.”

In other words: the properties of the object returned from mapStateToProps() will be passed to the component as props! You can think of mapStateToProps() as just a function that lets connect() know how to map specific parts of the store’s state into usable props.

    import { connect } from 'react-redux';

    const User = ({ name, age }) => {
      // ...
    };

    const mapStateToProps = (state, props) => ({
      name: state.user.name,
      age: state.user.age
    });

    export default connect(mapStateToProps)(User);

In the above example, both name and age will be available as props for the User component to access.

* ownProps (optional argument)
>mapStateToProps()'s optional argument, ownProps, gives us access to props passed into a connected component. Let's say we have a component with props passed directly down from a parent component:

    <ConnectedComponent firstName={'Harper'} lastName={'Lee'} />

These props can be merged along with other portions of state through ownProps:

    const mapStateToProps = (state, ownProps) => ({
      occupation: state.occupation,
      userInfo: `${ownProps.firstName} ${ownProps.lastName}: ${state.occupation}.`
    });

    export default connect(mapStateToProps)(MyComponent);

A great place to use ownProps is when filtering some data. Let's say we want to build a component MyPhotos that, upon login, renders an index of all the user's photos. The logged-in user is stored in another location in the application, and is passed down to the MyPhotos component as a prop. We can then leverage ownProps to access and display only what we need:

    const mapStateToProps = (state, ownProps) => ({
      photos: state.photos.filter(photo => photo.user === ownProps.user)
    });

    export default connect(mapStateToProps)(MyPhotos);

This way, we can quickly pass in a prop to a component (e.g., user) and return all of the photos authored by that user from the store's state.
Now, that we've wrapped our app component inside of provider and passed in our store,

* mapDispatchToProps()
>When you connect a component, that component will automatically be passed Redux's dispatch() method. What that means is that if you want to dispatch an action, you can do so in the component like this:

    import React, { Component } from 'react';
    import { connect } from 'react-redux';
    import { updateName } from './actions';

    class User extends Component {
      state = { name: '' }
      handleUpdateUser = () => {
        this.props.boundUpdateName(this.state.name)
      }
      render () {
        // ...
      }
    }

    export default connect()(User);

mapDispatchToProps() can clean up the code above just a bit. The whole point of mapDispatchToProps() is to make it so you can bind dispatch() to your action creators before they ever hit your component. In code, that looks like this:

    import React, { Component } from 'react';
    import { connect } from 'react-redux';
    import { updateName } from './actions';

    class User extends Component {
      state = { name: '' }
      handleUpdateUser = () => {
        this.props.boundUpdateName(this.state.name)
      }
      render () {
        // ...
      }
    }

    const mapDispatchToProps = dispatch => ({
      boundUpdateName: (name) => dispatch(updateName(name))
    });

    export default connect(null, mapDispatchToProps)(User);

mapDispatchToProps() is completely optional and I'm not convinced it makes things that much cleaner, but it is nice to know about.

### Connect Recap
connect() connects a React component to the Redux store. mapStateToProps() allows us to specify which state from the store you want passed to your React component. mapDispatchToProps() allows us to bind dispatch to your action creators before they ever hit your component.

[connect() from the react-redux docs](https://github.com/reactjs/react-redux/blob/master/docs/api.md#connectmapstatetoprops-mapdispatchtoprops-mergeprops-options)

[connect() vs. subscribe() on StackOverflow](https://stackoverflow.com/questions/41963225/redux-subscribe-vs-mapstatetoprops/41963751#41963751)


***

# Architect Redux Store
## combineReducers
### Reducer Composition
Up until this point, we’ve only ever had one reducer. This works, but as our app scales, it’ll probably become difficult to manage. Say we had a "users" reducer:

    function users (state = {}, action) {
      switch (action.type) {
        case 'ADD_USER' :
          return {};
        case 'REMOVE_USER':
          return {};
        default :
          return state;
      }
    }

What if we wanted to add books to our Redux store? Users and books are two very distinct pieces of data. It doesn’t make sense to have the users reducer manage books' state. This leads us to create another reducer:

    function users (state = {}, action) {
      // ...
    }

    function books (state = {}, action) {
      // ...
    }
We've separated our reducers to handle distinct, independent slices of state. This process is called reducer composition. However, we now have a problem: Redux’s createStore() method only accepts one reducer! In order to create a valid store, we still need to figure out a way to combine both of these reducers together into one reducer.

### combineReducers()
>combineReducers() is a helper function provided by Redux that turns an object whose values are different reducing functions into a single reducing function. We then pass this single "root reducer" into createStore() to create the application's store. Let's take a look at how this might look:

        // reducers/root_reducer.js

        import { combineReducers } from 'redux';

        function users (state = {}, action) {
          // ...
        }

        function books (state = {}, action) {
          // ...
        }

        export default combineReducers({
          users,
          books,
        });


      // store/store.js

      import rootReducer from '../reducers/root_reducer';

      const store = createStore(rootReducer)
      console.log(store.getState()) // { users: {}, books: {} }

### combineReducers() Recap
>As an application grows, so will the need for multiple reducers to manage different aspects of the Redux store. The problem is that Redux’s createStore() method takes in a single reducer, not multiple. To combine all of your reducers into one, you can use Redux’s combineReducers() method. This allows you to use reducer composition to manage the state in your store.

## Normalization(归一化)
When architecting a Redux store, there are two things you should keep in mind:

1. Do not duplicate data. If data lives in multiple places, you have no single source of truth, and you waste resources trying to keep the data in sync with each other.
2. Keep your store as shallow as possible. Nested data makes reducer logic more complicated (trying to update deeply nested data can get slow and complex quickly).

### Normalization Recap
Normalization is the process of removing duplicate pieces of data and making sure that the data is as shallow as possible. Not only does this allow applications to maintain the “single source of truth” in the store’s state -- reducer logic that updates that state is also kept clean and reasonable. Ultimately, normalizing your Redux store will lead to more efficient and consistent queries.

# Redux Middleware
## What is Middleware?
> As the Redux docs describe, middleware is a third-party extension point between dispatching an action and the moment it reaches the reducer.

### Middleware and Redux
Between the dispatching of actions and the reducer, we can introduce software called middleware to intercept the action before it ever reaches the reducer. As the Redux docs describe it, you can think of middleware as:

>…a third-party extension point between dispatching an action, and the moment it reaches the reducer.

Once middleware receives the action, it can then carry out a number of operations, including:

* Producing a side effect (e.g., logging state)
* Processing the action on its own (e.g., making an asynchronous HTTP request)
* Redirecting the action (e.g., to another piece of middleware)
* Running some code during the dispatch
* Dispatching supplementary actions

### Middleware Recap
Middleware can be implemented within the same unidirectional pattern of state management that Redux follows. In particular, middleware can intercept dispatched actions before they ever reach the reducer, then follow up by redirecting the action or producing a side effect.

We’ll jump into one particular side effect in the next section when we use logger middleware to print valuable information to the console.

## Implementing Middleware
### Where does Middleware Go in a Redux App?
Recall that the createStore() method is used to create the Redux store. Aside from passing in a reducer (oftentimes the combined "root reducer"), createStore() can also take in an optional enhancer argument, as well! Here is the method signature for createStore():

    store.createStore(reducer, [preloadedState], [enhancer])

Redux provides us with the applyMiddleware() function that we can use as our enhancer argument. applyMiddleware() can accept multiple arguments, so if needed, we can apply more than one middleware to an app. Let’s see this all in action, starting with the logger middleware!

### Example: logger Middleware
Remember that Redux is a “predictable state container” for web applications. When an action is dispatched, we expect to see a new state processed and saved (e.g. state cannot update by itself, nor should any external sources write directly to state). Wouldn’t it be great to log every action that occurs in the app, as well as the state before and after it?

We can apply logger middleware to do just that! The logger produces a side effect: printing the store’s state before and after the reducer processes the action.

Let’s jump in!

### Summary
We apply middleware in one centralized location in Redux apps: when creating a store. The createStore() method takes in a required reducer, but we can also pass in an optional enhancer argument. This argument is Redux’s applyMiddleware() function, which can take in multiple instances of middleware itself.

[redux-logger](https://github.com/evgenyrodionov/redux-logger)


## Thunks
### Background
Out of the box, the Redux store can only support the synchronous flow of data. Using middleware like thunk helps support asynchronicity in a Redux application. You can think of thunk as a wrapper for the store’s dispatch() method; rather than returning action objects, we can use thunk action creators to dispatch functions or Promises.

Note that without thunks, synchronous dispatches are the default. That is, we could still make API calls from React components (e.g., using the componentDidMount() lifecycle method to make these requests), but we strive for two things in Redux apps:

* Reusability (think composition)
* Predictability, in which only action creators can be the source of each state update

### Installation
In order to use thunk middleware in an app, be sure to install the redux-thunk package:

    npm install --save redux-thunk

### Thunk Action Creator Example
Let’s say that we’re building a web app that stores a user’s to-do items. After the user logs in, the app needs to fetch all of the user’s to-dos from a database. Since Redux only supports the synchronous flow of data, we can use thunk middleware to asynchronously produce the HTTP request for this fetch action.

Before we can write our thunk action creators, let’s make sure our store is ready to receive middleware:

    import { createStore, applyMiddleware } from 'redux';
    import thunk from 'redux-thunk';
    import rootReducer from '../reducers/root_reducer';

    const store = () => createStore(rootReducer, applyMiddleware(thunk));

    export default store;

Here, everything is set up for thunk middleware to be applied to the store: thunk middleware is imported from redux-thunk, and an instance of thunk is passed to the Redux’s applyMiddleware() enhancer function.

Additionally, let's say that the HTTP request looks like the following:

    export const fetchTodos = () => fetch('/api/todos');

Since thunk middleware allows us to write asynchronous action creators that return functions rather than objects, our new action creator can now look like:

      // actions/todo_actions.js

      import * as TodoAPIUtil from '../util/todo_api_util';

      export const RECEIVE_TODOS = "RECEIVE_TODOS";

      export const receiveTodos = todos => ({
        type: RECEIVE_TODOS,
        todos
      });

      export const fetchTodos = () => dispatch => (
        TodoAPIUtil
            .fetchTodos()
            .then(todos => dispatch(receiveTodos(todos)))
      );

receiveTodos() is an action creator that returns an object, with a type key of RECEIVE_TODOS along with the todos payload.

fetchTodos(), on the other hand, allows us to return a function. Here, we first make the HTTP request from TodoAPIUtil. By setting up a Promise, the action to receive all to-do items is dispatched only when the original request is resolved.

### Thunk's Underlying Implementation
If the above action creator (fetchTodos()) were written without the use of thunk middleware, we wouldn't see an ideal response from the reducer. After all, the reducer should only receive actions as plain JavaScript objects, not as functions!

    Consider this snippet of thunk middleware's source code below:

    function createThunkMiddleware(extraArgument) {
      return ({ dispatch, getState }) => next => action => {
        if (typeof action === 'function') {
          return action(dispatch, getState, extraArgument);
        }

        return next(action);
      };
    }

    const thunk = createThunkMiddleware();
    thunk.withExtraArgument = createThunkMiddleware;

    export default thunk;

Under the hood, thunk middleware intercepts actions of the type function before the dispatch is generated. In addition to dispatch, getState is also passed in as a second argument; this allows thunk action action creators to read the current state of the store.

### Summary & Further Research
If a web application requires interaction with a server, applying middleware such as thunk helps solve the issue of asynchronous data flow. Thunk allows us to write action creators that return functions (rather than objects). The thunk can then be used to delay an action dispatch, or to dispatch only if a certain condition is met (e.g., a request is resolved).

## App Structure & Organization
### Organizing the Directory Structure of a Redux Application
Aside from using middleware, we can also enhance our app in perhaps a more ancillary manner by choosing how we structure our file paths. After all, there are many moving parts and dependencies when it comes to Redux apps -- actions, reducers, the store, components, API utilities -- the list goes on.

By consciously thinking about how we organize our app’s assets, not only can we make it easier to find files we’re looking for, we can also make it easier to move things around (i.e., modularity). Here are two great ways that you can organize the directory structure when building Redux apps:

### Organization by Capability ("Type")
    Frontend
      - Components
          - component1.js
          - component2.js
          - component3.js
      - Actions
          - action1.js
          - action2.js
      - Reducers
          - reducer1.js
      - Util
      - Store
By organizing by capability, we know exactly where to look for certain assets: any action will be found in the Actions folder, any reducer will be found in Reducers, and so on. In fact, the “real world” example from Redux on GitHub structures the app this very way. Under this directory structure, if we wanted to import all actions into a component, we can get them all in a single import!

### Organization by Feature
If we need to make any changes, however, things might get tricky. What if a particular component’s requirements change? We’d have to manually look for that component’s related assets (actions, reducers, etc.) all in separate locations to make the necessary changes. An alternative way to structure the same application, then, is by feature:

      - nav
        - actions.js
        - index.js
        - reducer.js

      - dashboard
        - actions.js
        - index.js
        - reducer.js
This form of organization groups assets by their common “feature,” or “concept.” That is, all assets related to a navigation component are all together in a single, modular folder. It’s a great way to visually express what the application is all about, though if the app contains several hundred components, it can become more difficult to navigate through.

Ultimately, the choice is yours. Whatever way you choose to organize your directory structure, just be sure that it’s something that makes sense for your app, and it’s something you’re comfortable with!

### App Structure and Organization Recap
The two most popular ways to organize a Redux application are by:

Capability, in which all actions in an "Actions" folder, all reducers in a "Reducers" folder, etc.
Feature, in which, say, a "Sidebar" folder includes a file for all of the Sidebar's actions, a file for all of the Sidebar's reducers, etc.
All in all, there is no "right way" to split things up, though there are conventions we can practice to help manage the complexity of Redux. Considering the features, scale, and dependencies in your app, feel free to choose whichever structure makes the most sense. 

*** 

# React Native

## Up and Running with React Native

### Introduction

#### Course Map
Welcome! This course covers the React Native framework. Here's a quick breakdown of what the course looks like:
* Lesson 1 illustrates the benefits of using React Native to build native applications, as well as how to set up an effective dev environment.
* Lesson 2 compares the main ideological and API differences between React and React Native.
* Lesson 3 details styling and layout patterns for React Native applications.
* Lesson 4 examines routing patterns and strategies.
* Lesson 5 introduces native functionality (e.g., geolocation, notifications, etc.) and preparation of applications for the app store.

#### In-Class Project
During this course, you'll follow along and create a daily fitness-tracking application, UdaciFitness. You'll tie in what you've learned from React Fundamentals as well as React & Redux, then leverage React Native to create a fully functional mobile application!

### What is React Native/Why does it exist?
#### React Native under the Hood
When React was first introduced, a big selling point was the Virtual DOM. The idea is pretty standard in most UI libraries now, but when it first came out, it was groundbreaking! We can look at what exactly the Virtual DOM is by breaking down the process of what happens when you call setState().

The first thing React does when setState() is called is merge the object passed to setState() into the current state of the component. This will kick off a process called reconciliation. The end goal of reconciliation is to update the UI based on this new state in the most efficient way possible. To do this, React will construct a new tree of React elements (which you can think of as an object representation of your UI). Once it has this new tree, React will "diff" it against the previous element tree in order to figure out how the UI should change in response to the new state. By doing this, React will then know the exact changes which occurred, and by knowing exactly what changes occurred, it will able to minimize its footprint on the UI by only making updates where absolutely necessary.

This process of creating an object representation of the DOM is the whole idea behind the "Virtual DOM". Now, what if instead of targeting and rendering to the DOM, we need to target and render to another platform -- say iOS or Android. Theoretically, the DOM is just an implementation detail. Besides the name itself (which, in my opinion, was more of a marketing ploy than anything), there's nothing that couples the idea of the Virtual DOM to the actual DOM. This is the exact idea behind React Native. Instead of rendering to the web's DOM, React Native renders to native iOS or Android views. This allows us to build native iOS and Android applications just by using React Native.

#### Summary
React Native's "learn once, write anywhere" approach allows us to use the same principles that we know to develop for both web and native platforms. After all, under the hood, many of the same principles of the Virtual DOM, reconciliation, and diffing algorithm apply whether it's a web application built with React or a mobile application built with React Native.

### Dev Environment Setup
#### Create React Native App
When we build our app throughout this course, we'll be building it for both Android and iOS. One of the puzzles at hand is that we'll need to support two separate development environments: iOS uses Xcode, and Android uses Android Studio. This introduces a lot of complexity into this course; after all, both Xcode and Android Studio could probably each be their own set of courses!

Luckily for us, there's a new tool we can use that will allow us to develop for both Android and iOS without ever opening up Android Studio or Xcode. It's called, not surprisingly, Create React Native App. It's similar to Create React App in that all you have to do is install the CLI via NPM. Then, via the CLI, you can easily scaffold a brand new React Native project.

Just like Create React App, there are pros and cons to using Create React Native App (CRNA). First, the pros.

#### Create React Native App Pros
The obvious one is that Create React Native app minimizes the amount of time it takes to create a "hello world" application. The fact that you can run a command in your terminal and 15 seconds later have a project that run on both Android and iOS using JavaScript is pretty incredible. Next, and we'll look deeper into this one later on, Create React Native App allows you to easily develop on your own device. This way, any changes you make in your text editor will instantly show on the app running on your local phone. Next, and this is something I mentioned earlier, with Create React Native App you just need one build tool. You don't have to worry about Xcode or Android Studio. Lastly, there's no lock in. Just like Create React App, you can "eject" at anytime.

#### Create React Native Cons
Now, there are some cons, and granted they're pretty minor, but they're good to be aware of. First, if you're building an app that's going to be added to an existing native iOS or Android application, Create React Native App won't work. Second, if you need to build your own bridge between React Native and some native API that Create React Native App doesn't expose (which is pretty rare), Create React Native App won't work.

Let's jump right in!
#### Install Create React Native App
In order to use Create React Native App, go ahead and install it once globally:

    npm install -g create-react-native-app

Alternatively, feel free to use yarn as well (visit here for setup instructions):

    yarn global add create-react-native-app

#### Expo
Expo is a service that makes just about everything involving React Native a whole lot easier. The idea behind Expo is that there's no need to use Android Studio or Xcode. What's more: it even allows us to develop for iOS with Windows (or even Linux)!

With Expo, you can load and run projects built by Create React Native App with the same JavaScript you already know. There's no need to compile any native code. And much like Create React App, using Expo with Create React Native App lets us get an application up and running with almost no configuration.

We'll be relying on Expo heavily in this course. First things first: you need to install Expo. Head to the app store and install the Expo mobile app for your device:
* [Expo on Google Play (Android)](https://play.google.com/store/apps/details?id=host.exp.exponent)
* [Expo on the App Store (iOS)](https://itunes.apple.com/us/app/expo-client/id982107779)

#### Simulators
Expo together with Create React Native App is the fastest way to get up and running, but there are also other ways to start building your projects, as well. If you're looking to integrate React Native into an existing app, or if you've ejected your app from Create React Native App, feel free to follow the [Building Projects with Native Code](https://facebook.github.io/react-native/docs/getting-started.html) tab from the React Native docs. The guide also sets up iOS and Android simulators, allowing you to view your mobile apps right on your machine! We'll be utilizing both iOS and Android simulators in the interest of demoing projects in this course, but they are completely optional in getting started.

>💡 Bundling Error (Unexpected Token)💡

>If you're seeing bundling errors while attempting to run a simulator, try changing your Babel preset for React Native to version 2.1.0. Then, remove your node-modules directory, reinstall with npm install, and run the simulator again. For more information, check out this post on Stack Overflow.

#### Summary
Create React Native App is similar to Create React App in that it scaffolds and builds a starter application with minimal configuration. This allows us to have an app up and running without the need for Xcode or Android Studio! Some of the benefits include:

* Minimal "time to 'Hello World'"
* Development on your own device via Expo
* A single build tool
* No lock-in (i.e., ejection at any time)
You can also set up simulators to aid in development as well. But regardless of which platform we choose to develop for (iOS, Android), and which environment we're in (Mac, Windows, Linux) -- we're just building with the same old JavaScript that we're used to!

### Using the Debugger
#### Summary
What's great about React Native development is that it takes much of what you're used to from web development and takes it to native development. Accessing the in-app developer menu allows you to reload your JavaScript code, debug remotely via Developer Tools, and even display an in-app inspector.

#### To Debug
All you have to do is shake your phone, or press:

* ⌘D in the iOS simulator
* ⌘M in the Android simulator
#### To Refresh
To refresh the app, just:

* Double-tap “R” on your keyboard (if using the simulator)
* Shake the phone, then select “Refresh”


## React vs React Native
### Web vs Native

Native applications look and "feel" different because they are fundamentally different. Even though we're using the same React principles that you've learned throughout this program, keep in mind that this is no longer the web! While some of these distinctions are more apparent (e.g., the development process, access to native features, how users get updates, etc.), there are some key differences that we'll be taking a deep dive into during this course.

For one, native apps often leverage animations to help create a great user experience. Animations such as button effects, screen transitions, and other visual feedback may be subtle, but they support continuity and guidance in the apps you build. They all function to dynamically tell a story about how your application works. Without animations, an application can feel like just a collection of static screens. For now, stay tuned; we'll be checking out animations in-depth during Lesson 5.

Another key difference between native and web applications is in navigation. Recall that React Router's Route component allows us to map a URL to a specific UI component. In React Native, routers function as a stack; that is, individual screens are "pushed" and "popped" as needed. We'll look at routing more closely later in Lesson 4.

#### Android vs. iOS
Not only are there fundamental differences between native apps and web apps, you'll also find differences between how native platforms (iOS and Android) look and feel as well. Perhaps the most apparent are the distinct design philosophies on each platform: Android apps utilize Google's [Material Design](https://material.io/guidelines/material-design/introduction.html), while iOS apps take advantage of Apple's [Human Interface Design](https://developer.apple.com/ios/human-interface-guidelines/overview/themes/). When designing mobile applications, it's important to your users that an iOS app feels like an iOS app, and an Android app feels like an Android app.

Navigation between screens feels distinct between Android and iOS as well. Android devices have access to a navigation bar at the bottom of the screen, which allows users to go back to the previous screen (among other features). On iOS, the approach is different: there is no such universal navigation bar! When building the UI for an iOS application, it is important to include a back button (perhaps on a custom [navigation bar](https://developer.apple.com/ios/human-interface-guidelines/overview/themes/)) to help guide users through your app.

One more key difference between Android and iOS involves tab navigation. iOS apps include [tab bars](https://developer.apple.com/ios/human-interface-guidelines/ui-bars/tab-bars/) at the bottom of the app's screen, allowing for convenient access to different portions of the app. Likewise, Android apps include them as well; however tabs are distinctly located [at the top of the screen](https://material.io/guidelines/components/tabs.html). Both allow access to high-level content, and we'll explore React Native's TabNavigator in closer detail in Lesson 4.

#### Summary
When developing your React Native projects, keep in mind that you're designing for a different experience than that of web applications. Mobile applications look and feel different due to fundamental differences, such as subtle animations that build a sense of continuity for your users. Differences exist between Android and iOS as well, especially in their design philosophies and navigation. We'll look at some fundamental components that make up React Natives apps in the next section!

### Common React Native Components
#### Common React Native Components

When writing HTML, we're used to using <div> and <span> tags to define sections or to contain other elements on the page. In React Native, a similar principle applies, but this time we're using React Native's <View> component to build the application UI. Just like HTML's <div>, <View> components can accommodate several props (e.g. style), and can even be nested inside other <View> components!

<Text> works just how you'd expect, as well. Its main objective is to, by no surprise, render text in the application. Just like <View>, styling and nesting capabilities apply to <Text> components, as well.

#### Touchables
Users mainly interact with web apps with clicks. In the world of mobile apps, however, several different touch gestures are used to navigate through the app: tapping a button, swiping to scroll through a list, and so on.

React Native offers a number of components to handle "tapping gestures," or what is called Touchables. Let's take a look at them in detail in the following video:

* Button
* TouchableHighlight
* TouchableOpacity

>💡 Pause Udacifitness💡
>At this point, let's put the UdaciFitness project on hold for a bit and talk about some other common React Native components. For example, how would you handle lists >in a mobile app? What about forms, or images?

>Though these are not necessarily used in the in-class project, these components are still great to know as you develop React Native applications.

#### Lists
* ScrollView        renders all child components at once
* FlatList          renders only items visible on screen
* SectionList       renders on-screen items,but with headers
React Native comes with a few ways to render lists. You'll probably run into ScrollView and FlatList components most commonly, so let's take a look at both of these in detail!

>💡 Seeing Errors with ScrollView? 💡
>If you're running into errors mentioning that ScrollView has no propType..., we recommend reinstalling Create React Native App globally, as well as updating the Expo >mobile application. If you still find issues, feel free to check out this GitHub issue on the official React Native repo.

>💡 SectionList 💡
>What if you wanted to add section headers to a list? FlatList doesn’t quite support these, but React Native offers another list component that renders these headers >nicely. Feel free to check out SectionList in the React Native documentation for a closer look


#### Forms
Forms in React Native are just like the forms in React that you already know: the state of input form elements is controlled by the React component that renders that form. That is, form values are held in local component state, making state the "source of truth" for that form.

React Native provides a few basic components to use in your application's forms. We'll take a look at each of these more closely in the following video:

* TextInput
* KeyboardAvoidingView
* Slider
* Switch

>⚠️ Oops! (onChange vs. onChangeText) ⚠️
In the above video, App renders a TextInput component with an onChange prop. With the way that the event handler, handleTextChange(), is implemented, the prop should be onChangeText.

>While both methods are invoked on value change, onChangeText passes the actual value (text) as the argument. On the other hand, onChange passes the entire event object as an argument. Both are perfectly valid props, but the logic of your event handler will need to be tailored to the prop chosen. For more info, check out this post on Stack Overflow.

#### Other Components
We've just seen some of the most important components built into React Native. These components will get you started with the essential functionalities in the apps that you build -- but the list of available components goes on! Feel free to review the React Native documentation for a complete list. For starters, we recommend checking out:

* [ActivityIndicator](https://facebook.github.io/react-native/docs/activityindicator.html)
* [Picker](https://facebook.github.io/react-native/docs/picker.html)
* [WebView](https://facebook.github.io/react-native/docs/webview.html)
* [Modal](https://facebook.github.io/react-native/docs/modal.html)

#### Summary
React Native provides a variety of built-in components for developing mobile applications. While some support basic functionality in an application (e.g., text, images, lists), others offer more specialized functionality (e.g., pulling to refresh, displaying a loading indicator). Feel free to check out Components and APIs in the React Native documentation for an exhaustive list.

### AsyncStorage
#### Local Storage
In order to persist data in a web application, we'd normally store the data in some sort of database. This prevents app data from being lost between page refreshes. Using localStorage, we can achieve a similar effect for the user by storing this data directly in their browser. Best of all -- data stored in localStorage has no expiration date. This means that even if a session ends (e.g. the browser tab is closed), data will not be lost!

Feel free to check out [Window.localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) on MDN for an overview.

#### Example: Saving to localStorage
Let's say we're building a simple React and Redux application that lets users create and manage a list of tasks. Basic functionality allows users to add items to their task list, remove items, and mark items as completed.

Assuming much of this data is kept in the application's store, how would we go about persisting this data? One way would be to save to localStorage each time that state is updated. That is, the store's state will be saved with each dispatch:

        // store.js

        import { createStore } from 'redux';
        import Reducer from '../reducers/reducer';

        const configureStore = () => {
          const store = createStore(Reducer);

          store.subscribe(() => {
            localStorage.state = JSON.stringify(store.getState());
          });

          return store;
        };

        export default configureStore;

After the store is created, we call store.subscribe() and pass in a callback function. The callback effectively saves a JSON string of the store's state into localStorage. As a result, by subscribing to the store right after it is created, we can save data related to all of the user's tasks right into their browser!


The React Native documentation on [AsyncStorage](https://facebook.github.io/react-native/docs/asyncstorage.html) mentions:

>AsyncStorage is a simple, unencrypted, asynchronous, persistent, key-value storage system that is global to the app. It should be used instead of LocalStorage.

#### Summary
React Native's version of localStorage is AsyncStorage. Conveniently, since AsyncStorage is just an abstraction over iOS and Android equivalents, there's no need to consider the different environments.

We took a close look at AsyncStorage's three main methods:
* setItem
* removeItem
* clear
Feel free to visit the [documentation](https://facebook.github.io/react-native/docs/asyncstorage.html#methods) for a complete list.

### Redux and React Native

#### Redux and React Native

#### Adding Redux

Recall that Redux is a predictable state container for JavaScript applications. It is agnostic to any particular view library or framework, so not only can we use it with React, but we can integrate it into React Native applications, as well!

With its lean size and minimal dependencies, Redux is a great tool for React Native projects. And best of all: since React Native is still fundamentally just JavaScript, Redux can be added into projects the same way that we're used to. Let's check it out -- first, with building out actions!

>💡 Forgot Redux?💡
If you need a refresher on the principles of Redux, feel free to check out the previous course again, [React & Redux](https://classroom.udacity.com/nanodegrees/nd019/parts/7b1b9b53-cd0c-49c9-ae6d-7d03d020d672)! Since Redux is agnostic to any particular view library or framework, the same principles of Redux will apply to applications built with React Native as well.

#### Summary

Remember that React Native is fundamentally still just JavaScript. As such, adding Redux to help manage application state will involve the very same principles and processes as adding Redux to a web application.

## Styling&Layout

### CSS in JS

#### CSS in JS
Before we jump into how CSS in JavaScript works, let's check out an example of some "normal" HTML and CSS:

      <!-- index.css -->
      .avatar {
        border-radius: 5px;
        margin: 10px;
        width: 48px;
        height: 48px;
      }

      <!-- // index.html -->
      <div>
        <img class='avatar' src='https://tylermcginnis.com/tylermcginnis_glasses-300.png' />
      </div>

Nothing too surprising! But since we're not using HTML or CSS files to build mobile apps -- how would this look in React Native?

First, it important to know that all of the core components in React Native can accept a prop named style. One way we can leverage this prop is to provide styling to components with inline JavaScript objects:

    function Avatar ({ src }) {
      return (
        <View>
          <Image
            style={{borderRadius: 5, margin: 10, width: 48, height: 48}}
            source={{uri: 'https://tylermcginnis.com/tylermcginnis_glasses-300.png'}}
          />
        </View>
      );
    }

In the example above, the <Image> component receives two props: style and source. The value of style is just a plain old JavaScript object with borderRadius, margin, width, and height properties. Keep in mind that unlike CSS on the web, properties are written in camelCase (i.e., borderRadius in CSS in JS, but border-radius on the web).

This works, but things can get muddy quickly. Imagine if the inline object contained a dozen properties, or if we wanted the same style to apply to more than just one component! One way to keep your code DRY and reusable is to store the object in a variable:

    const styles = {
      image: {
        borderRadius: 5,
        margin: 10,
        width: 48,
        height: 48
      }
    };

    function Avatar ({ src }) {
      return (
        <View>
          <Image
            style={styles.image}
            source={{uri: 'https://tylermcginnis.com/tylermcginnis_glasses-300.png'}}
          />
        </View>
      );
    }

It's a great way to clean things up a bit, but React Native goes a step further with its StyleSheet API. Check out the following example:

    import React from 'react';
    import { StyleSheet, Text, View } from 'react-native';

    export default class TextExample extends React.Component {
      render() {
        return (
          <View>
            <Text style={styles.greenLarge}>This is large green text!</Text>
            <Text style={styles.red}>This is smaller red text!</Text>
          </View>
        );
      }
    }

    const styles = StyleSheet.create({
      greenLarge: {
        color: 'green',
        fontWeight: 'bold',
        fontSize: 40
      },
      red: {
        color: 'red',
        padding: 30
      },
    });

Here, an object containing styles is passed into StyleSheet's create method. It looks similar to styling with a JavaScript object variable! But as we mentioned above, using StyleSheet gives us a few benefits in terms of code quality and performance. We’ll take a closer look later in this Lesson as well, but this is how the React Native docs describe it:

>Code quality
>* By moving styles away from the render function, you're making the code easier to understand.
>* Naming the styles is a good way to add meaning to the low-level components in the render function.

>Performance
>* Making a stylesheet from a style object makes it possible to refer to it by ID instead of creating a new style object every time.
>* It also allows to send the style only once through the bridge. All subsequent uses are going to refer an id (not implemented yet).

Another benefit is that StyleSheet validates the content within the style object as well. This means that should there be any errors in any properties or values in your style objects, the console will throw an error during compilation instead of at runtime.

>💡 Additional Styling💡
If you wanted to implement more than one style to a component, the style prop can accept styles as an array:

    <Text style={[styles.red, styles.greenLarge]}>
      This will be red, then greenLarge
    </Text>

>The above <Text> component will render large green text, as the last style in the array will take precedence. This is a great way to inherit styles!

>💡 Libraries for CSS in JS💡

>Styling in React is going through a renaissance period right now just as Flux did a few years ago (which eventually gave us Redux). There are many different styling libraries popping up and each has different tradeoffs. Two of the most popular are [Glamorous](https://github.com/robinpowered/glamorous-native) and [Styled Components](https://github.com/styled-components/styled-components). The whole idea of both of these libraries is that styling is a primary concern of the component and because of that, should be coupled with the component itself. We'll take a look at using Styled Component with React Native a little bit later.

#### Summary
CSS in JS is a distinct approach to styling. The main idea is that styling is handled by JavaScript objects rather than traditional CSS. Styles can be written inline or accessed via object variables, but React Native offers a StyleSheet API that provides a performant and compositional way to style components.

Now that we've seen React Native handle styling, how do we manage the layout of a mobile application? We'll take a look at CSS's flexbox in the next section to do just that!

#### Further Learning
* [How can I use CSS-in-JS securely?](https://reactarmory.com/answers/how-can-i-use-css-in-js-securely)

### Flexbox Guide

#### Getting Started with Flexbox

Getting Started with Flexbox
If you aren't familiar with flexbox you're in good company, because I'm not either. That's a joke.

Whenever I learn a new technology, I like to answer the question, “Why does this specific technology exist?” With flexbox, the answer to this question may just be that creating an all-purpose layout with CSS can be quite cumbersome. The whole goal of flexbox is to create a more efficient way to "lay out, align, and distribute space among items in a container, even when their size is unknown and/or dynamic". In a nutshell, flexbox is all about creating dynamic layouts.

The main idea of flexbox is that you give the parent element the ability to control the layout of all of their (immediate!) child elements rather than having each child element control its own layout. When you do this, the parent becomes a flex container while the child elements become flex items. An example of this is instead of having to float to the left all children of an element and add margin to each one, instead, you can just have the parent element specify to have all of its children be laid out in a row with even space between them. So, layout responsibilities move from the children to the parent. This allows for more fine tuned control over the layout of your app.
There's a lot of content in this section broken down into the following sections:

* Flexbox Axes
* Flex Direction
* Justify Content
    * Flex-Start
    * Center
    * Flex-End
    * Space-Between
    * Space-Around
* Align Items
    * Flex-Start
    * Center
    * Flex-End
    * Stretch
* Centering Content
* The Flex Property
* Aligning Individual Items

#### Flexbox Axes

By far, the most important concept to understand when it comes to flexbox is that flexbox is all about different [axes](https://www.quora.com/What-is-the-plural-of-axis). You'll have a Main Axis and a Cross Axis.


In React Native, by default, the Main Axis is vertical while the Cross Axis is horizontal. Everything from here on out is built upon this concept of a Main Axis and Cross Axis.

When I say "…which will align all the child elements along the Main Axis" that means that, by default, all the children of the parent element will be laid out vertically from top to bottom. If I say "…which will align the child elements along the Cross Axis" that means that, by default, all the children elements will be laid out horizontally from left to right.

The rest of flexbox is just deciding how you want to align, position, stretch, spread, shrink, center, wrap child elements along the Main and Cross axis.

#### Flex Direction

You'll notice that I was very deliberate in mentioning the "default behavior" when it comes to the Main Axis and Cross Axis. That's because you can actually change which Axis is Main and which is Cross. That brings us to our first flexbox property, flex-direction (or flexDirection in React Native).

flex-direction has two values:

* row
* column

By default, every element in React Native has the flexDirection: column declaration. When an element has a flex-direction of column, its Main Axis is vertical and its Cross Axis is horizontal, just as we saw in the image above. However, if you give an element a flexDirection: row declaration, the axes switch. The Main axis becomes horizontal, while the Cross axis becomes vertical. Again, this is crucial because your entire layout is dependent on these two axes.

#### Justify Content

Now is when things start getting fun. Let's dive into the different properties and values we can use to align child elements along these axes. Let's focus entirely on the Main Axis, first.

In order to specify how children align themselves along the Main Axis, you'll use the justifyContent property. justifyContent has five different values you can use in order to change how the children align themselves along the Main Axis.

* flex-start
* center
* flex-end
* space-around
* space-between

Woah. I just dropped lots of unfamiliar terms. I'll walk through each and every one of them though, so we're good 💃🏽.

If you want to follow along (which I highly recommend you do), create a new React Native project called "FlexboxExamples" and swap out your App.js code with the following:

    import React, { Component } from 'react'
    import { StyleSheet, Text, View, AppRegistry } from 'react-native'

    class FlexboxExamples extends Component {
      render() {
        return (
          <View style={styles.container}>
            <View style={styles.box}/>
            <View style={styles.box}/>
            <View style={styles.box}/>
          </View>
        )
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
      },
      box: {
        height: 50,
        width: 50,
        backgroundColor: '#e76e63',
        margin: 10,
      }
    })

    export default FlexboxExamples;

Note that with the code above, the only thing we'll be changing is the styling in the container object in the styles StyleSheet object. Ignore flex: 1 for now.

#### Justify Content: Flex-Start

justifyContent: 'flex-start' will align every child element towards the start of the the Main Axis.

    container: {
      flex: 1,
      justifyContent: 'flex-start',
    }

If you were still struggling with the importance of Main Axis and Cross Axis hopefully it just clicked. Because flexDirection defaults to column, and we're using justifyContent which targets the Main Axis, our child elements are going to align themselves towards the start of the Main Axis which is the top left and work their way down.

#### Justify Content: Center

justifyContent: 'center' will align every child element towards the center of the the Main Axis. ​

    container: {
      flex: 1,
      justifyContent: 'center',
    }

#### Justify Content: Flex-End

justifyContent: 'flex-end' will align every child element towards the end of the the Main Axis. ​

    container: {
      flex: 1,
      justifyContent: 'flex-end',
    }

#### Justify Content: Space-Between

justifyContent: 'space-between' will align every child so that the space between each child is even along the Main Axis. ​

    container: {
      flex: 1,
      justifyContent: 'space-between',
    }

#### Justify Content: Space-Around
justifyContent: 'space-around' will align every child element so that there is even space around each element along the Main Axis. ​

    container: {
      flex: 1,
      justifyContent: 'space-around',
    }

Now I want you to think about what would happen if we changed the flexDirection of our container to row instead of the default value column? Instead of our Main Axis being vertical, it's going to be horizontal. That means any child elements are going to align themselves horizontally rather than vertically.

    container: {
      flex: 1,
      flexDirection: 'row',
      justifyContent: 'space-around',
    }

Notice that all we changed was the value for flexDirection, and it drastically altered our layout. Now you're starting to see the real power of flexbox.

#### Align Items (The Cross Axis)

Now let's turn our focus entirely to the Cross Axis. In order to specify how children align themselves along the Cross Axis, you'd use the align-items property.

You would think that alignItems has the exact same values as justifyContent. It's a reasonable guess, but you'd be wrong. This property has four different values you can use in order to change how the children align themselves among the Cross Axis.

* flex-start
* center
* flex-end
* stretch

#### Align Items - Flex-Start
alignItems: 'flex-start' will align every child element towards the start of the the Cross Axis. ​

    container: {
      flex: 1,
      alignItems: 'flex-start',
    }

#### Align Items: Center
alignItems: 'center' will align every child element towards the center of the Cross Axis. ​

    container: {
      flex: 1,
      alignItems: 'center',
    }

#### Align Items: Flex-End
alignItems: 'flex-end' will align every child element towards the end of the the Cross Axis. ​

    container: {
      flex: 1,
      alignItems: 'flex-end',
    }

#### Align Items: Stretch
alignItems: 'stretch' will stretch every child element along the Cross Axis as long as the child element does not have a specified height (flexDirection: row) or width (flexDirection: column). ​

    container: {
      flex: 1,
      alignItems: 'stretch',
    },
    box: {
      height: 50,
      backgroundColor: '#e76e63',
      margin: 10,
    }

Just when you thought you were getting the hang of it, flexbox throws a wrench in your brain. Whenever you set alignItems to stretch, each child element is going to stretch the full width or height of the parent container as long as that child element doesn't have a width or a height. Notice in the box styling, I removed the width: 50 because flexDirection is set to column by default meaning that flex items will be stretching horizontally (since we're using alignItems).

To cement this home, what will our UI look like if I change our styling to this?

      const styles = StyleSheet.create({
        container: {
          flex: 1,
          alignItems: 'stretch',
          flexDirection: 'row',
        },
        box: {
          width: 50,
          backgroundColor: '#e76e63',
          margin: 10,
        }
      })

Notice I've changed the flexDirection to row, and I've added back in width: 50 and removed the height: 50.


Let's break this down. First, the Main Axis is now running horizontally since we added flexDirection: row. This means that alignItems will be aligning the items along the vertical axis. Because we've removed the height of the child elements and added alignItems: stretch, those elements are going to stretch along the vertical axis for the entire length of their parent component, which in this case is the whole view.

Up until this point, we've only had one flex container or parent element. Don't get it twisted though; if you create more nested flex containers, the exact same logic above is going to be true for those child elements (flex items) but instead of being relative to the whole view (as in our example), they'll position themselves according to the their parent component. Your entire UI will be built upon nesting flex containers.

At this point, you're essentially a red belt in React Native styling TaeKwonDo. There are a few other flexbox features we need to look at, though.

You'll very quickly come to a realization that there are no percent-based styling in React Native. Though I agree it makes things a bit more difficult, everything you can do with percent-based styling you can do with flexbox. Remember the flex: 1 declaration we used in all the examples above? That's the property that's going to allow us to do it. Interestingly enough there's no exact comparison for this feature in flexbox on the web, but it is similar to flex-grow if you know what that does.

As we've seen over and over, flexbox is concerned with giving control to the parent element to handle the layout of its children elements. The flex property is a bit different as it allows child elements to specify their height or width in comparison to their sibling elements. The best way to explain flex is to look at some examples.

#### Centering Content
Let's start off with a view like this:

How would you implement that? Notice that our Main Axis is horizontal; this gives us a clue that we're using flexDirection: row. The boxes are in the center of both axes which means we're using justifyContent: 'center' and alignItems: 'center'.

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        flexDirection: 'row',
        justifyContent: 'center',
        alignItems: 'center',
      },
      box: {
        width: 50,
        height: 50,
        backgroundColor: '#e76e63',
        margin: 10,
      }
    })

#### The Flex Property
But now, what if we wanted to change our UI to look like this:
In the above image, it's exactly the same layout -- but now the middle section is twice as wide as its siblings! This is what the flex property allows us to do. Here’s the code:

    class FlexboxExamples extends Component {
      render() {
        return (
          <View style={styles.container}>
            <View style={[styles.box, {flex: 1}]}/>
            <View style={[styles.box, {flex: 2}]}/>
            <View style={[styles.box, {flex: 1}]}/>
          </View>
        )
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        flexDirection: 'row',
        justifyContent: 'center',
        alignItems: 'center',
      },
      box: {
        width: 50,
        height: 50,
        backgroundColor: '#e76e63',
        margin: 10,
      }
    })

    export default FlexboxExamples;

Notice I didn't add any styles; I just made the middle sibling have flex: 2 while the other siblings have flex: 1. This basically says "make sure that the middle sibling is twice as large along the Main Axis as the first and third children". This is the reason why flex can replace percentages because usually a percent-based layout is just one where specific elements are relative to other elements, exactly like we're doing above. It's also important to note that if you place flex: 1 on an element, that element is going to take up as much space as its parent takes up. That's why in most of our examples above because we want our "layout area" to be the size of the parent, which in our examples was the whole viewport.

Let's go even deeper!

#### Aligning Individual Flex Items
What if we wanted a layout like this?

It's as if the first and third element are centered both vertically and horizontally, but that second element has a mind of its own and is using flex-end along the Cross Axis. To implement this, we'll need a way to have the child element override a specific positioning it received from its parent. Good news: that's exactly what alignSelf allows us to do! Notice it begins with align, so just like alignItems, it's going to position itself along the Cross Axis. It also has the exact same options as alignItems (flex-start, flex-end, center, stretch).

The code to implement the image above is:

    class FlexboxExamples extends Component {
      render() {
        return (
          <View style={styles.container}>
            <View style={styles.box}/>
            <View style={[styles.box, {alignSelf: 'flex-end'}]}/>
            <View style={styles.box}/>
          </View>
        )
      }
    }

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        flexDirection: 'row',
        justifyContent: 'center',
        alignItems: 'center',
      },
      box: {
        width: 50,
        height: 50,
        backgroundColor: '#e76e63',
        margin: 10,
      }
    })

    export default FlexboxExamples;

Note that all we've done is add alignSelf: flex-end to the second child element and that overrode what it was instructed to do by the parent (alignItems: 'center').

If you've made it all the way through this, great work! I realize that was a lot to cover but I hope it's helped you get up and running with styling (and specifically flexbox) on React Native.

#### Summary
React Native leverages a version of flexbox to build component layout. This is primarily due to flexbox's ability to provide consistent layouts across different screen sizes.

Flexbox containers comprise of two axes: a main axis, as well as a cross axis. Some of the more critical properties to consider when building layouts with flexbox include flex-direction, justify-content, and align-items. React Native's implementation of flexbox is a bit different, however. We'll see just how in the very next section!

#### Further Research

[A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
[Flexbox Froggy](http://flexboxfroggy.com/)

### Layout In React Native
#### React Native's Flexbox Implementation
React Native implements flexbox for build layouts, but there are some key differences to keep in mind as you develop your applications. First, all containers in React Native are flex containers by default. Recall that in traditional CSS flexbox, you would normally define a flex container like so:

    /*example.css*/

    .container {
      display: flex;
    }

However, this is completely unnecessary in React Native! By default, everything is display: flex;. You can just use the defaults as they are, without adding different properties or writing extra code.

Another important distinction is how React Native handles flex-direction, a property that establishes the main axis (i.e., defining the direction in which flex items are placed). In web applications, items default to row. But since we're working on mobile devices, React Native sets the default to column, which lays out items vertically.

One more major difference you'll encounter is how the flex property is used. On the web, flex specifies how a flex item grows or shrinks to manage the space around it (along the main axis). In React Native, flex is generally used with flex items that are on the same level, but hold different flex values. For example:

    import React from 'react';
    import { View } from 'react-native';

    const FlexDemo = props => (
      <View style={{flex: 1}}>
        <View style={{flex: 1, backgroundColor: 'red'}} />
        <View style={{flex: 2, backgroundColor: 'green'}} />
        <View style={{flex: 3, backgroundColor: 'blue'}} />
      </View>
    );

    export default FlexDemo;

Here, FlexDemo is a stateless functional component which renders <View> components with different flex values. Its outermost container is set to flex: 1, which will expand the full available width along the main axis (i.e., the entire screen in this example). Its children <View> components will fill the space accordingly, rendering a blue background color that takes up three times as much space as red takes, and green that takes up exactly twice as much space as red takes.

#### Other Differences
In addition to the above, here is a list of defaults in other common CSS properties that React Native applies to components:

      box-sizing: border-box;
      position: relative;
      align-items: stretch;
      flex-shrink: 0;
      align-content: flex-start;
      border: 0 solid black;
      margin: 0;
      padding: 0;
      min-width: 0;

####  Platform API
Recall that React's approach to app development is "learn once, write anywhere." The goal is to use the same principles, technologies, and in the case of React Native -- the same code -- to develop applications. However, there may be cases that make sense to use distinct code for each mobile platform. For example, what if we wanted unique styling between iOS and Android visual components?

React Native gives us a convenient way to organize and separate code through the Platform API. Let's check out an example!


>💡 Dimensions API💡
React Native also comes with Dimensions, which allows you to select window's width and height in the user's device!

First, make sure you pull the API from React Native:

    import { Dimensions } from 'react-native';

Then, you can simply grab the window sizes with the Dimensions API's get method:

    const { width, height } = Dimensions.get('window');
Feel free to use these measurements to, for example, plan how your <View>s will look like.

#### Summary
React Native uses flexbox to manage layout in mobile applications. However, there are some minor distinctions between the official flexbox specification (i.e., CSS on the web) and React Native's own implementation. Most of these distinctions are just differences in default settings.

Since differences also exist in how Android and iOS applications should look and feel, React Native also offers a Platform API to do just that.

In the next section, we'll take a look at some common "gotchas" and best practices when styling components.

#### Further Research
* [Understanding React Native flexbox layout](https://medium.com/the-react-native-log/understanding-react-native-flexbox-layout-7a528200afd4)
* [Platform Specific Code](https://facebook.github.io/react-native/docs/platform-specific-code.html) from the React Native docs

### How Professionals Handle Styling
#### Styling: Stylesheet vs. Inline
Earlier you were introduced to React Native’s StyleSheet API for creating “stylesheets” out of JavaScript objects. At first this approach may seem a little strange, but there are some reasons behind it. Primarily those reasons are code quality and performance. Let’s take a look at some comparisons in regards to code quality.

    <View style={{
      borderRadius: 4,
      borderWidth: 0.5,
      borderColor: '#d6d7da',
    }}>
      <Text style={[
        {fontSize: 19, fontWeight: 'bold'}, 
        props.isActive && { color: 'red' }
      ]}>
        Welcome
      </Text>
    </View>

Above we have some JSX for a pretty simple UI. Notice, that even though this UI is rather simple, the styling of it makes it rather messy. This is perhaps the biggest benefit to the StyleSheet API: by moving styles away from the render function, the code becomes easier to read and understand. Not only that, but naming the styles is a good way to make components a little more declarative. With the StyleSheet API, we can change the code above to now look like this:

    var styles = StyleSheet.create({
      container: {
        borderRadius: 4,
        borderWidth: 0.5,
        borderColor: '#d6d7da',
      },
      title: {
        fontSize: 19,
        fontWeight: 'bold',
      },
      activeTitle: {
        color: 'red',
      },
    });

    <View style={styles.container}>
      <Text style={[styles.title, props.isActive && styles.activeTitle]} />
    </View>

On top of quality benefits, there are also performance benefits as well. Making a stylesheet from a style object makes it possible to refer to it by ID instead of creating a new style object every render.

#### Media Queries
One thing you may have noticed is that React Native (and specifically the StyleSheet API) doesn’t support [media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries). The reason for this is because, for the most part, you can design responsive grids with flexbox which will bypass the need to use media queries. In the rare case where flexbox just won’t work for your specific needs, you can use the [Dimensions](https://facebook.github.io/react-native/docs/dimensions.html) API which we covered earlier to get similar results.

#### CSS in JS Libraries
Styling in React is going through a renaissance period right now just as Flux did a few years ago (which eventually gave us Redux). There are many different styling libraries popping up and each has different tradeoffs.

Two of the most popular are [Glamorous](https://github.com/robinpowered/glamorous-native) and [Styled Components](https://github.com/styled-components/styled-components). The whole idea of both of these libraries is that styling is a primary concern of the component and because of that, should be coupled with the component itself.

Let’s take a look at not only the Styled Components library, but also how you’d use it with React Native.

#### Summary
In this section we took a deeper look into the benefits of the StyleSheet API as well as the Styled Components API and how it works on React Native.

#### Further Research
For further research on Styled Components, you can visit the official [documentation](https://www.styled-components.com/).

## Navigation
### TabNavigator
#### TabNavigator
By using React Navigation's TabNavigator, users can navigate through different screens within an application simply by pressing tabs that render different components. Say we have two basic functional components that just render some text, Hello and Goodbye:

      const Hello = () => (
        <View>
          <Text>Hello!</Text>
        </View>
      );

      const Goodbye = () => (
        <View>
          <Text>Goodbye!</Text>
        </View>
      );

If we want to add two tabs for users to select (one rendering Hello, the other rendering Goodbye), first we'll need to install react-navigation and then import TabNavigator:

    yarn add react-navigation
or

    npm install --save react-navigation
    import { TabNavigator } from 'react-navigation';
Once this is done, we can pass an object into TabNavigator like so:

    const Tabs = TabNavigator({
      Hello: {
        screen: Hello
      },
      Goodbye: {
        screen: Goodbye
      },
    });

Inside the object, each key-and-value pair represents a single tab. The keys represent the name of the tab; this is what users will see and press. Note that a screen property is included as well; this is the component that is rendered when the tab is active.

Here comes the interesting part: what TabNavigator returns is actually a component! Since we have stored this in a Tabs variable, we can just render this as we would with any component:

      // App.js

      // ...

      export default class App extends React.Component {
        render() {
          return (
            <Tabs />
          );
        }
      }

#### StatusBar
Recall that so far, our application has been using arbitrary padding to account for the status bar at the top of the device's screen. Let's go ahead and change that! React Native actually provides a simple StatusBar component to customize how the status bar appears in an application.

Before we take a look at how to implement StatusBar, be sure to import it from react-native:

    import { StatusBar } from 'react-native';

#### Summary
React Navigator offers a TabNavigator API that allows for navigation between different screens via individual tabs. Each tab is dedicated to rendering a specific component.

This section also detailed React Native's StatusBar component. StatusBar is relatively straightforward to use and is fully customizable -- we typically just set properties to change it!

In the next section, we'll take a look at React Navigator's StackNavigator API, which allows users to add and remove screens from a stack.

#### Further Research
* [StatusBar props](https://facebook.github.io/react-native/docs/statusbar.html#props) from the React Native docs
* [TabNavigator](https://reactnavigation.org/docs/navigators/tab) from the React Navigator docs

### StackNavigator
#### StackNavigator

When pressing an item in, say, an index view, we expect to go to a new screen with details on that item. React Navigation offers another navigator to do just that! With Stack Navigator, new screens are added and removed as a stack. This places screens on top of one another in a "last in, first out" manner, similar to Array's push() and pop() methods.

StackNavigator's usage is largely similar to that of TabNavigator. But rather than passing in an object of different tabs, we pass in an object of the different screens that should be available in that stack. First, go ahead an import StackNavigator from react-navigation.

    import { StackNavigator } from 'react-navigation';

Say we have two basic components, Home and Dashboard:

    const Home = ({ navigation }) => (
      <View>
        <Text>This is the Home view</Text>
        <TouchableOpacity onPress={() => navigation.navigate('Dashboard')}>
          <Text>Press here for the Dashboard</Text>
        </TouchableOpacity>
      </View>
    );

    const Dashboard = () => (
      <View>
        <Text>This is the Dashboard</Text>
      </View>
    );

Note that a navigation prop is passed to the stateless functional Home component, which allows navigation to another route. Once this is done, we can pass an object into StackNavigator similar to how we did for TabNavigator:

    const Stack = StackNavigator({
      Home: {
        screen: Home
      },
      Dashboard: {
        screen: Dashboard
      }
    })

The return value of passing an object into StackNavigator is a component as well, and we can render it as such!

    // App.js

    // ...

    export default class App extends React.Component {
      render() {
        return (
          <Stack />
        );
      }
    }

StackNavigator and TabNavigator often go hand-in-hand. Since they each return components, you'll often see one nested within the other. Let's see this in action as we implement this into UdaciFitness!

#### Summary
React Navigation's StackNavigator is another customizable navigation option based on adding and removing new screens to a stack. Its API is similar to that of TabNavigator; it takes in an object that defines all screens, then returns a component. Since both StackNavigator and TabNavigator both return components, a common practice is to nest these navigators within one another.

In the next section, we'll take a look at DrawerNavigator, in which screens are switched from a drawer that pops out from the side of the screen!

Further Research
* [Stack Navigation in React Native](https://medium.com/@swathylenjini/stack-navigation-in-react-native-2cd00374ff3a)

### DrawerNavigator
#### DrawerNavigator
DrawerNavigator
React Navigation offers one more basic navigator to create custom navigation through React Native apps: the DrawerNavigator. While TabNavigator uses tabs to help users navigate to specific screens, DrawerNavigator uses a drawer-like menu that slides in from the side of the screen. While we won't be implementing this into UdaciFitness -- it's still important to know and fairly common in React Native applications!

To use DrawerNavigator, be sure to import it from react-navigation:

  import { DrawerNavigator } from 'react-navigation';

Luckily, many of the same philosophies shared by StackNavigator and TabNavigator apply here as well! Let's check out two basic components again and see how DrawerNavigator renders them:

    const Home = ({ navigation }) => (
      <View>
        <Text>This is the Home view</Text>
        <TouchableOpacity onPress={() => navigation.navigate('DrawerOpen')}>
          <Text>Press here to open the drawer!</Text>
        </TouchableOpacity>
      </View>
    );

    const Dashboard = ({ navigation }) => (
      <View>
        <Text>This is the Dashboard view</Text>
        <TouchableOpacity onPress={() => navigation.navigate('DrawerOpen')}>
          <Text>Press here to open the drawer!</Text>
        </TouchableOpacity>
      </View>
    );

Note that rather than routing to another component, each TouchableOpacity wrapper opens the drawer. Likewise, 'DrawerClose' can be used to close the drawer. To simplify things, React Navigation also offers 'DrawerToggle' to automatically select which navigation is appropriate based on the current drawer state.

Similar to TabNavigator and StackNavigator, we can then pass an object into DrawerNavigator, render the component returned, and we're all set!

    const Drawer = DrawerNavigator({
      Home: {
        screen: Home
      },
      Dashboard: {
        screen: Dashboard
      }
    });
    // App.js

    // ...

    export default class App extends React.Component {
      render() {
        return (
          <Drawer />
        );
      }
    }

#### Summary
React Navigation's DrawerNavigator is used to easily set up a screen with drawer navigation. Many of the same practices we use to set up StackNavigator and TabNavigator apply to DrawerNavigator as well. Simply pass in an object containing the different screens, and the return value is a component ready to be rendered. As a result, this makes DrawerNavigator components easy for nesting with other navigators!

#### Further Research
* [DrawerNavigator](https://reactnavigation.org/docs/navigators/drawer) from the React Navigation docs

## Native Features

### Geolocation
#### Geolocation
A common feature of native applications is the ability to access and receive updates about the user's current location. Like most things, Expo makes this rather straightforward by giving us a JavaScript API that will work on both iOS and Android.

    import { Location } from 'expo';

Typically when dealing with location services, there are one of two features you'll need: getting the user's current location, or getting and watching the user's current location for updates. Expo's Location property gives us both of these options with getCurrentPositionAsync and watchPositionAsync.

getCurrentPositionAsync gets the current location of the device, without watching for future updates. watchPositionAsync will also get the current location of the device, but it will also subscribe to location updates. This way, you'll be notified if that device moves location.

For the full documentation on how to use Expo's Location property, visit [Location](https://docs.expo.io/versions/latest/sdk/location.html)

>💡 Geolocation Tips 💡
>Whenever you're dealing with a feature that requires the user's permission to work properly, it's important that you account for all the different UI options that could be shown. For example, when dealing with a user's location, there are three scenarios to manage:

>1 The user gives you permission to view their location (best-case scenario).
>2 The user decides to neither deny nor grant you permission to their location.
>3 The user denies giving you access to their location.

>In an ideal world, the user would always grant you permission to whatever you'd like, but, this isn't always the case and as a UI developer, you need to plan accordingly for those moments.

Be sure that you have included the following imports: in Live.js:

    import { Location, Permissions } from 'expo';
    import { calculateDirection } from '../utils/helpers';

Note: If you are running into errors with the code in this commit, update the initial value of the Live's state's coords property to a non-null value.

#### Summary
In this concept, we saw how to use Expo's Location property to watch the user's current location using watchPositionAsync. For further reading, feel free to check out the official [documentation](https://docs.expo.io/versions/latest/sdk/location.html).

### Animations
#### Animations
Animations are a fundamental aspect of any native application. Because of this, React Native comes built in with an animations library called Animated. The whole idea of Animated is that it "focuses on declarative relationships between inputs and outputs, with configurable transforms in between, and simple start/stop methods to control time-based animation execution." In other words, Animated allows you to establish different types of transformations on specific values. For example, you could easily animate an image's opacity property from 0 to 1, giving the effect that the image is slowly appearing.

There are three types of animation configurations that you have access to out of the box with Animated. They are decay, spring, and timing. Again, all three of these allow you to transform a specific value, but each differ in how that value is transformed: "decay" will start with an initial velocity and gradually slow to a stop, "spring" provides a normal spring type of animation, and "timing" animates a value of a specified time.

Let's take a look at some of these in action!

>⚠️ Cautions: Animations ⚠️
>Once you fully grasp the Animated API, a whole new world will open up to you. It sounds great, but this can be a double-edged sword. It's a great thing because you now have the ability to enhance the feel of your application with animations. However, with great power comes great responsibility.

>The goal of having animations is to add to the user's experience, not distract from it. By keeping this in mind whenever you're adding animations to your app, not only will your app perform better -- you'll also minimize the risk of ruining your user's experience with unnecessary animations.

#### Summary
In this section we learned how to improve your application's UX by using React Native's Animated library to add thoughtful animations. For more reading on Animated, you can view the official [documentation](https://facebook.github.io/react-native/docs/animated.html).

### Local Notifications
#### Local Notifications
When dealing with notifications, it's important to understand that there are two different types: push notifications, and local notifications.

Local notifications do not use or require any external infrastructure; they happen entirely on the device itself. That means that the only requirement for the device to display the notification is that the device is on. On the other hand, push notifications require you to have a server which handles pushing the notification to your user's devices when a certain event occurs.

But since we're not incorporating an external server, and all the logic about when we should show the notification can be done on the phone itself -- local notifications will be the most ideal for our application. Let's see how it's done!

>⚠️ Notifications on iOS ⚠️
>Before we jump in, note that with iOS, notifications (both push notifications and local notifications) do not appear at the top of the screen automatically if the application is in the foreground. Moreover, push notifications do not function in the iOS simulator (whether or not Expo is used).

>For more information, check out [this post](https://forums.expo.io/t/psa-reminder-notifications-in-ios-foregrounded-apps/641) in the Expo forums. This issue does not appear when working with notifications on Android.

#### Summary
In this section, you learned how to add local notifications to your app using Expo's Notifications property. For further reading, you can visit the [official documentation](https://docs.expo.io/versions/latest/sdk/notifications.html).

### Handling Photos
#### Handling Photos
At this point it shouldn't be a surprise that Expo provides a nice JavaScript abstraction over the native iOS and Android approaches to accessing photos from the device's photo gallery. The name of this property is ImagePicker and it does exactly what you would expect: "Provides access to the system's UI for selecting images from the phone's photo library or taking a photo with the camera."

We won't be adding any of this functionality to the UdaciFitness app we're building, but in the next video we will walk through how to use ImagePicker just in case you'll need it for a future project.

#### Summary
In this section, you learned about Expo's ImagePicker component to grab images from the phone's photo gallery. For more information, you can read the [official documentation](https://docs.expo.io/versions/latest/sdk/imagepicker.html).

### App Store Preparation
#### App Store Preparations
When you submit an app to either app store, there is more information you need to submit than just the app itself. For example, you need details such as the app description, icon, etc. Luckily for us, Expo make it easy to specify these sorts of things just by editing the app.json file at the root of our app folder. Here's an example of configurations we'll be adding in our UdaciFitness app:

    {
      "expo": {
        "sdkVersion": "19.0.0",
        "orientation": "portrait",
        "name": "Udacifitness",
        "description": "The best triathlon training app in the world.",
        "slug": "udacifitness",
        "version": "1.0",
        "icon": "https://maxcdn.icons8.com/Color/PNG/512/Sports/triathlon-512.png",
        "notification": {
          "icon": "http://www.student-scholarships.com/images/made/img/featured/nav_basketball_45_45.png"
        },
        "ios": {
        "bundleIdentifier": "org.udacifitness.exp",
        },
        "android": {
        "package": "org.udacifitness.exp",
        }
      },
    }

#### What are .apk and .ipa Files?
Before you submit your application to either app store, you need to "package" it appropriately. The iOS App Store will ask you for a .ipa ("iOS App Store Package") file and the Android Google Play store will ask you for a .apk ("Android Application Package") file. When you create either an ipa or a apk file, you're essentially creating a bundle of all of the necessary information that either App store needs in order to process and run your application.

The easiest way to generate both the .apk and the .ipa files is to use Expo's exp CLI. First, run npm install -g exp. Once that's installed (and after you've configured your app.json file), you can run exp build:ios to build your .ipa file, and exp build:android to build your .apk file.

Note that these will take anywhere from 10-20 minutes to build, so you'll need to be patient. To check the status of the build you can run exp build:status. Eventually that command will give you a URL where you can go to download either your .ipa or .apk files.

>⚠️ The Rest of the Way ⚠️
>The hardest part about uploading your application to either app store is generating a .ipa or .apk file. Because we covered that in the previous section, we're not going to cover the entire process of actually uploading your app. The following documents should help you: for iOS, [Uploading a Build for an App](https://developer.apple.com/library/content/documentation/LanguagesUtilities/Conceptual/iTunesConnect_Guide/Chapters/UploadingBinariesforanApp.html#//apple_ref/doc/uid/TP40011225-CH38-SW1) and for Android, [Upload an App](https://support.google.com/googleplay/android-developer/answer/113469?hl=en).

#### Summary
In this section we learned about preparing your application for the app store and generating .apk and .ipa files. For further reading, feel free t ocheck out [Building Standalone Apps with Expo](https://docs.expo.io/versions/latest/guides/building-standalone-apps.html).

## ES6
### Let and Const
There are now two new ways to declare variables in JavaScript: let and const.

Up until now, the only way to declare a variable in JavaScript was to use the keyword var. To understand why let and const were added, it’s probably best to look at an example of when using var can get us into trouble.

#### Hoisting
Hoisting is a result of how JavaScript is interpreted by your browser. Essentially, before any JavaScript code is executed, all variables are "hoisted", which means they're raised to the top of the function scope. So at run-time, the getClothing() function actually looks more like this…

#### let and const
Variables declared with let and const eliminate this specific issue of hoisting because they’re scoped to the block, not to the function. Previously, when you used var, variables were either scoped globally or locally to an entire function scope.

If a variable is declared using let or const inside a block of code (denoted by curly braces { }), then the variable is stuck in what is known as the temporal dead zone until the variable’s declaration is processed. This behavior prevents variables from being accessed only until after they’ve been declared.

#### Rules for using let and const
let and const also have some other interesting properties.

* Variables declared with let can be reassigned, but can’t be redeclared in the same scope.
* Variables declared with const must be assigned an initial value, but can’t be redeclared in the same scope, and can’t be reassigned.

#### Use cases
The big question is when should you use let and const? The general rule of thumb is as follows:

* use let when you plan to reassign new values to a variable, and
* use const when you don’t plan on reassigning new values to a variable.
Since const is the strictest way to declare a variable, we suggest that you always declare variables with const because it'll make your code easier to reason about since you know the identifiers won't change throughout the lifetime of your program. If you find that you need to update a variable or change it, then go back and switch it from const to let.

That’s pretty straightforward, right? But what about var?

#### What about var?
Is there any reason to use var anymore? Not really.

There are some arguments that can be made for using var in situations where you want to globally define variables, but this is often considered bad practice and should be avoided. From now on, we suggest ditching var in place of using let and const.

### Template Literals
Prior to ES6, the old way to concatenate strings together was by using the string concatenation operator ( + ).

    const student = {
      name: 'Richard Kalehoff',
      guardian: 'Mr. Kalehoff'
    };

    const teacher = {
      name: 'Mrs. Wilson',
      room: 'N231'
    }

    let message = student.name + ' please see ' + teacher.name + ' in ' + teacher.room + ' to pick up your report card.';

This works alright, but it gets more complicated when you need to build multi-line strings.

    let note = teacher.name + ',\n\n' +
      'Please excuse ' + student.name + '.\n' +
      'He is recovering from the flu.\n\n' +
      'Thank you,\n' +
      student.guardian;

However, that’s changed with the introduction of template literals (previously referred to as "template strings" in development releases of ES6).

    NOTE: As an alternative to using the string concatenation operator ( + ), you can use the String's concat() method, but both options are rather clunky for simulating true [string interpolation](https://en.wikipedia.org/wiki/String_interpolation).

#### Template Literals
Template literals are essentially string literals that include embedded expressions.

Denoted with backticks ( `` ) instead of single quotes ( '' ) or double quotes ( "" ), template literals can contain placeholders which are represented using ${expression}. This makes it much easier to build strings.

Here's the previous examples using template literals.

    let message = `${student.name} please see ${teacher.name} in ${teacher.room} to pick up your report card.`;

By using template literals, you can drop the quotes along with the string concatenation operator. Also, you can reference the object's properties inside expressions.

Here, you try. Change the greeting string below to use a template literal. Also, feel free to swap in your name for the placeholder.

Here’s where template literals really shine. In the animation above, the quotes and string concatenation operator have been dropped, as well as the newline characters ( \n ). That's because template literals also preserve newlines as part of the string!

>TIP: Embedded expressions inside template literals can do more than just reference variables. You can perform operations, call functions and use loops inside embedded expressions!

### Destructuring
In ES6, you can extract data from arrays and objects into distinct variables using destructuring.

This probably sounds like something you’ve done before, for example, look at the two code snippets below that extract data using pre-ES6 techniques:

    const point = [10, 25, -34];

    const x = point[0];
    const y = point[1];
    const z = point[2];

    console.log(x, y, z);
    Prints: 10 25 -34
The example above shows extracting values from an array.

    const gemstone = {
      type: 'quartz',
      color: 'rose',
      karat: 21.29
    };

    const type = gemstone.type;
    const color = gemstone.color;
    const karat = gemstone.karat;

    console.log(type, color, karat);
    Prints: quartz rose 21.29
And this example shows extracting values from an object.

Both are pretty straightforward, however, neither of these examples are actually using destructuring.

So what exactly is destructuring?

#### Destructuring
Destructuring borrows inspiration from languages like Perl and Python by allowing you to specify the elements you want to extract from an array or object on the left side of an assignment. It sounds a little weird, but you can actually achieve the same result as before, but with much less code; and it's still easy to understand.

Let’s take a look at both examples rewritten using destructuring.

#### Destructuring values from an array
    const point = [10, 25, -34];

    const [x, y, z] = point;

    console.log(x, y, z);
    Prints: 10 25 -34
In this example, the brackets [ ] represent the array being destructured and x, y, and z represent the variables where you want to store the values from the array. Notice how you don’t have to specify the indexes for where to extract the values from because the indexes are implied.

>TIP: You can also ignore values when destructuring arrays. For example, const [x, , z] = point; ignores the y coordinate and discards it.

#### Destructuring values from an object
    const gemstone = {
      type: 'quartz',
      color: 'rose',
      karat: 21.29
    };

    const {type, color, karat} = gemstone;

    console.log(type, color, karat);
    Prints: quartz rose 21.29

In this example, the curly braces { } represent the object being destructured and type, color, and karat represent the variables where you want to store the properties from the object. Notice how you don’t have to specify the property from where to extract the values. Because gemstone has a property named type, the value is automatically stored in the type variable. Similarly, gemstone has a color property, so the value of color automatically gets stored in the color variable. And it's the same with karat.

>TIP: You can also specify the values you want to select when destructuring an object. For example, let {color} = gemstone; will only select the color property from the gemstone object.

### Object Literal Shorthand
A recurring trend in ES6 is to remove unnecessary repetition in your code. By removing unnecessary repetition, your code becomes easier to read and more concise. This trend continues with the introduction of new shorthand ways for initializing objects and adding methods to objects.

#### Object literal shorthand
You’ve probably written code where an object is being initialized using the same property names as the variable names being assigned to them.

But just in case you haven’t, here’s an example.

    let type = 'quartz';
    let color = 'rose';
    let carat = 21.29;

    const gemstone = {
      type: type,
      color: color,
      carat: carat
    };

    console.log(gemstone);
    Prints: Object {type: "quartz", color: "rose", carat: 21.29}

Do you see the repetition? Doesn't type: type, color: color, and carat:carat seem redundant?

The good news is that you can remove those duplicate variables names from object properties if the properties have the same name as the variables being assigned to them.

Check it out!

Speaking of shorthand, there’s also a shorthand way to add methods to objects.

To see how that looks, let’s start by adding a calculateWorth() method to our gemstone object. The calculateWorth() method will tell us how much our gemstone costs based on its type, color, and carat.

    let type = 'quartz';
    let color = 'rose';
    let carat = 21.29;

    const gemstone = {
      type,
      color,
      carat,
      calculateWorth: function() {
        // will calculate worth of gemstone based on type, color, and carat
      }
    };

In this example, an anonymous function is being assigned to the property calculateWorth, but is the function keyword really needed? In ES6, it’s not!

#### Shorthand method names
Since you only need to reference the gemstone’s calculateWorth property in order to call the function, having the function keyword is redundant, so it can be dropped.

let gemstone = {
  type,
  color,
  carat,
  calculateWorth() { ... }
};

### Iteration
### Family of For Loops
The for...of loop is the most recent addition to the family of for loops in JavaScript.

It combines the strengths of its siblings, the for loop and the for...in loop, to loop over any type of data that is iterable (meaning it follows the iterable protocol which we'll look at in lesson 3). By default, this includes the data types String, Array, Map, and Set—notably absent from this list is the Object data type (i.e. {}). Objects are not iterable, by default.

Before we look at the for...of loop, let’s first take a quick look at the other for loops to see where they have weaknesses.

#### The for loop
The for loop is obviously the most common type of loop there is, so this should be a quick refresher.

    const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

    for (let i = 0; i < digits.length; i++) {
      console.log(digits[i]);
    }

Really the biggest downside of a for loop is having to keep track of the counter and exit condition.

In this example, we’re using the variable i as a counter to keep track of the loop and to access values in the array. We’re also using digits.length to determine the exit condition for the loop. If you just glance at this code, it can sometimes be confusing exactly what’s happening; especially for beginners.

While for loops certainly have an advantage when looping through arrays, some data is not structured like an array, so a for loop isn’t always an option.

### The for...in loop
The for...in loop improves upon the weaknesses of the for loop by eliminating the counting logic and exit condition.

    const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

    for (const index in digits) {
      console.log(digits[index]);
    }

But, you still have to deal with the issue of using an index to access the values of the array, and that stinks; it almost makes it more confusing than before.

Also, the for...in loop can get you into big trouble when you need to add an extra method to an array (or another object). Because for...in loops loop over all enumerable properties, this means if you add any additional properties to the array's prototype, then those properties will also appear in the loop.

    Array.prototype.decimalfy = function() {
      for (let i = 0; i < this.length; i++) {
        this[i] = this[i].toFixed(2);
      }
    };

    const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

    for (const index in digits) {
      console.log(digits[index]);
    }

Gross! This is why for...in loops are discouraged when looping over arrays.

>NOTE: The forEach loop is another type of for loop in JavaScript. However, forEach() is actually an array method, so it can only be used exclusively with arrays. There is also no way to stop or break a forEach loop. If you need that type of behavior in your loop, you’ll have to use a basic for loop.

### For...of Loop
#### For...of loop
The for...of loop is used to loop over any type of data that is iterable.

You write a for...of loop almost exactly like you would write a for...in loop, except you swap out in with of and you can drop the index.

    const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

    for (const digit of digits) {
      console.log(digit);
    }

This makes the for...of loop the most concise version of all the for loops.

>TIP: It’s good practice to use plural names for objects that are collections of values. That way, when you loop over the collection, you can use the singular version of the name when referencing individual values in the collection. For example, for (const button of buttons) {...}.

But wait, there’s more! The for...of loop also has some additional benefits that fix the weaknesses of the for and for...in loops.

You can stop or break a for...of loop at anytime.

    const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

    for (const digit of digits) {
      if (digit % 2 === 0) {
        continue;
      }
      console.log(digit);
    }

And you don’t have to worry about adding new properties to objects. The for...of loop will only loop over the values in the object.

    Array.prototype.decimalfy = function() {
      for (i = 0; i < this.length; i++) {
        this[i] = this[i].toFixed(2);
      }
    };

    const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

    for (const digit of digits) {
      console.log(digit);
    }

### Spread... Operator
#### Spread operator
The spread operator, written with three consecutive dots ( ... ), is new in ES6 and gives you the ability to expand, or spread, [iterable objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators#Iterators) into multiple elements.

Let’s take a look at a few examples to see how it works.

    const books = ["Don Quixote", "The Hobbit", "Alice in Wonderland", "Tale of Two Cities"];
    console.log(...books);

    Prints: Don Quixote The Hobbit Alice in Wonderland Tale of Two Cities

    const primes = new Set([2, 3, 5, 7, 11, 13, 17, 19, 23, 29]);
    console.log(...primes);

    Prints: 2 3 5 7 11 13 17 19 23 29

If you look at the output from the examples, notice that both the array and set have been expanded into their individual elements. So how is this useful?

    NOTE: Sets are a new built-in object in ES6 that we’ll cover in more detail in a future lesson.

#### Combining arrays with concat
One example of when the spread operator can be useful is when combining arrays.

If you’ve ever needed to combine multiple arrays, prior to the spread operator, you were forced to use the Array’s concat() method.

    const fruits = ["apples", "bananas", "pears"];
    const vegetables = ["corn", "potatoes", "carrots"];
    const produce = fruits.concat(vegetables);
    console.log(produce);
    Prints: ["apples", "bananas", "pears", "corn", "potatoes", "carrots"]

This isn’t terrible, but wouldn’t it be nice if there was a shorthand way to write this code?

For example, something like…

>⚠️ Upcoming const Warning ⚠️
>If you're following along by copy/pasting the code, then you've already declared the produce variable with the const keyword. The following code will try to redeclare and reassign the variable, so depending on how you're running the code, it might throw an error.

>Remember that variables declared with const cannot be redeclared or reassigned in the same scope.

    const produce = [fruits, vegetables];
    console.log(produce);
    Prints: [Array[3], Array[3]]

Unfortunately, that doesn’t work.

Instead of combining both arrays, this code actually adds the fruits array at the first index and the vegetables array at the second index of the produce array.

How about trying the spread operator?

### ...Rest Parameter
If you can use the spread operator to spread an array into multiple elements, then certainly there should be a way to bundle multiple elements back into an array, right?

In fact, there is! It’s called the rest parameter, and it’s another new addition in ES6.

#### Rest parameter
The rest parameter, also written with three consecutive dots ( ... ), allows you to represent an indefinite number of elements as an array. This can be helpful in a couple of different situations.

One situation is when assigning the values of an array to variables. For example,

    const order = [20.17, 18.67, 1.50, "cheese", "eggs", "milk", "bread"];
    const [total, subtotal, tax, ...items] = order;
    console.log(total, subtotal, tax, items);
    Prints: 20.17 18.67 1.5 ["cheese", "eggs", "milk", "bread"]

This code takes the values of the order array and assigns them to individual variables using destructuring. total, subtotal, and tax are assigned the first three values in the array, however, items is where you want to pay the most attention.

By using the rest parameter, items is assigned the rest of the values in the array (as an array).

#### Variadic functions
Another use case for the rest parameter is when you’re working with variadic functions. Variadic functions are functions that take an indefinite number of arguments.

For example, let’s say we have a function called sum() which calculates the sum of an indefinite amount of numbers. How might the sum() function be called during execution?

    sum(1, 2);
    sum(10, 36, 7, 84, 90, 110);
    sum(-23, 3000, 575000);

There’s literally an endless number of ways the sum() function could be called. Regardless of the amount of numbers passed to the function, it should always return the total sum of the numbers.

#### Using the arguments object
In previous versions of JavaScript, this type of function would be handled using the arguments object. The arguments object is an array-like object that is available as a local variable inside all functions. It contains a value for each argument being passed to the function starting at 0 for the first argument, 1 for the second argument, and so on.

If we look at the implementation of our sum() function, then you’ll see how the arguments object could be used to handle the variable amount of numbers being passed to it.

    function sum() {
      let total = 0;  
      for(const argument of arguments) {
        total += argument;
      }
      return total;
    }

Now this works fine, but it does have its issues:

If you look at the definition for the sum() function, it doesn’t have any parameters.
This is misleading because we know the sum() function can handle an indefinite amount of arguments.
It can be hard to understand.
If you’ve never used the arguments object before, then you would most likely look at this code and wonder where the arguments object is even coming from. Did it appear out of thin air? It certainly looks that way.

#### Using the rest parameter
Fortunately, with the addition of the rest parameter, you can rewrite the sum() function to read more clearly.

    function sum(...nums) {
      let total = 0;  
      for(const num of nums) {
        total += num;
      }
      return total;
    }
This version of the sum() function is both more concise and is easier to read. Also, notice the for...in loop has been replaced with the new for...of loop.

## Functions
### Arrow Functions

ES6 introduces a new kind of function called the arrow function. Arrow functions are very similar to regular functions in behavior, but are quite different syntactically. The following code takes a list of names and converts each one to uppercase using a regular function:

    const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(function(name) { 
      return name.toUpperCase();
    });
The code below does the same thing except instead of passing a regular function to the map() method, it passes an arrow function. Notice the arrow in the arrow function ( => ) in the code below:

    const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(
      name => name.toUpperCase()
    );
The only change to the code above is the code inside the map() method. It takes a regular function and changes it to use an arrow function.

>NOTE: Not sure how map() works? It's a method on the Array prototype. You pass a function to it, and it calls that function once on every element in the array. It then gathers the returned values from each function call and makes a new array with those results. For more info, check out [MDN's documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map).

#### Convert a function to an arrow function

    const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(function(name) { 
      return name.toUpperCase();
    });
With the function above, there are only a few steps for converting the existing "normal" function into an arrow function.

* remove the function keyword
* remove the parentheses
* remove the opening and closing curly braces
* remove the return keyword
* remove the semicolon
* add an arrow ( => ) between the parameter list and the function body

### Using Arrow Functions
Regular functions can be either function declarations or function expressions, however arrow functions are always expressions. In fact, their full name is "arrow function expressions", so they can only be used where an expression is valid. This includes being:

* stored in a variable,
* passed as an argument to a function,
* and stored in an object's property.
One confusing syntax is when an arrow function is stored in a variable.

    const greet = name => `Hello ${name}!`;

In the code above, the arrow function is stored in the greet variable and you'd call it like this:

    greet('Asser');
    Returns: Hello Asser!

#### Parentheses and arrow function parameteres

You might have noticed the arrow function from the greet() function looks like this:

    name => `Hello ${name}!`

If you recall, the parameter list appears before the arrow function's arrow (i.e. =>). If there's only one parameter in the list, then you can write it just like the example above. But, if there are two or more items in the parameter list, or if there are zero items in the list, then you need to wrap the list in parentheses:

    // empty parameter list requires parentheses
    const sayHi = () => console.log('Hello Udacity Student!');
    sayHi();

#### Concise and block body syntax

All of the arrow functions we've been looking at have only had a single expression as the function body:

    const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(
      name => name.toUpperCase()
    );

This format of the function body is called the "concise body syntax". The concise syntax:

* has no curly braces surrounding the function body
* and automatically returns the expression.

If you need more than just a single line of code in your arrow function's body, then you can use the "block body syntax".

    const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map( name => {
      name = name.toUpperCase();
      return `${name} has ${name.length} characters in their name`;
    });

Important things to keep in mind with the block syntax:

* it uses curly braces to wrap the function body
* and a return statement needs to be used to actually return something from the function.
So arrow functions are awesome!


* The syntax is a lot shorter,
* it's easier to write and read short, single-line functions,
* and they automatically return when using the concise body syntax!
>WARNING: Everything's not all ponies and rainbows though, and there are definitely times when you might not want to use an arrow function. So before you wipe from your memory how to write a traditional function, check out these implications:

* there's a gotcha with the this keyword in arrow functions
* go to the next lesson to find out the details!
* arrow functions are only expressions
* there's no such thing as an arrow function declaration

### "this" and Regular Functions

To get a handle on how this works differently with arrow functions, let's do a quick recap of how this works in a standard function. If you have a solid grasp of how this works already, feel free to jump over this section.

The value of the this keyword is based completely on how its function (or method) is called. this could be any of the following:

#### 1. A new object

If the function is called with new:

    const mySundae = new Sundae('Chocolate', ['Sprinkles', 'Hot Fudge']);

In the code above, the value of this inside the Sundae constructor function is a new object because it was called with new.

#### 2. A specified object

If the function is invoked with call/apply:

    const result = obj1.printName.call(obj2);

In the code above, the value of this inside printName() will refer to obj2 since the first parameter of call() is to explicitly set what this refers to.

#### 3. A context object

If the function is a method of an object:

    data.teleport();

In the code above, the value of this inside teleport() will refer to data.

#### 4. The global object or undefined

If the function is called with no context:

    teleport();

In the code above, the value of this inside teleport() is either the global object or, if in strict mode, it's undefined.

TIP: this in JavaScript is a complicated topic. We just did a quick overview, but for an in-depth look at how this is determined, check out [this All Makes Sense Now](https://github.com/getify/You-Dont-Know-JS/blob/master/this%20%26%20object%20prototypes/ch2.md)! from Kyle Simpson's book series You [Don't Know JS](https://github.com/getify/You-Dont-Know-JS/blob/master/README.md).

### "this" and Arrow Functions

With regular functions, the value of this is set based on how the function is called. With arrow functions, the value of this is based on the function's surrounding context. In other words, the value of this inside an arrow function is the same as the value of this outside the function.

Let's check out an example with this in regular functions and then look at how arrow functions will work.

    // constructor
    function IceCream() {
      this.scoops = 0;
    }

    // adds scoop to ice cream
    IceCream.prototype.addScoop = function() {
      setTimeout(function() {
        this.scoops++;
        console.log('scoop added!');
      }, 500);
    };

    const dessert = new IceCream();
    dessert.addScoop();


    Prints:
    scoop added!

After running the code above, you'd think that dessert.scoops would be 1 after half a millisecond. But, unfortunately, it's not:

    console.log(dessert.scoops);
    Prints:
    0

Can you tell why?

The function passed to setTimeout() is called without new, without call(), without apply(), and without a context object. That means the value of this inside the function is the global object and NOT the dessert object. So what actually happened was that a new scoops variable was created (with a default value of undefined) and was then incremented (undefined + 1 results in NaN):

    console.log(scoops);
    Prints:
    NaN

One way around this is to use closure:

    // constructor
    function IceCream() {
      this.scoops = 0;
    }

    // adds scoop to ice cream
    IceCream.prototype.addScoop = function() {
      const cone = this; // sets `this` to the `cone` variable
      setTimeout(function() {
        cone.scoops++; // references the `cone` variable
        console.log('scoop added!');
      }, 0.5);
    };

    const dessert = new IceCream();
    dessert.addScoop();

The code above will work because instead of using this inside the function, it sets the cone variable to this and then looks up the cone variable when the function is called. This works because it's using the value of the this outside the function. So if we check the number of scoops in our dessert right now, we'll see the correct value of 1:

    console.log(dessert.scoops);
    Prints:
    1

Well that's exactly what arrow functions do, so let's replace the function passed to setTimeout() with an arrow function:

    // constructor
    function IceCream() {
      this.scoops = 0;
    }

    // adds scoop to ice cream
    IceCream.prototype.addScoop = function() {
      setTimeout(() => { // an arrow function is passed to setTimeout
        this.scoops++;
        console.log('scoop added!');
      }, 0.5);
    };

    const dessert = new IceCream();
    dessert.addScoop();

Since arrow functions inherit their this value from the surrounding context, this code works!

    console.log(dessert.scoops);
    Prints:
    1

When addScoop() is called, the value of this inside addScoop() refers to dessert. Since an arrow function is passed to setTimeout(), it's using its surrounding context to determine what this refers to inside itself. So since this outside of the arrow function refers to dessert, the value of this inside the arrow function will also refer to dessert.

Now what do you think would happen if we changed the addScoop() method to an arrow function?

    // constructor
    function IceCream() {
        this.scoops = 0;
    }

    // adds scoop to ice cream
    IceCream.prototype.addScoop = () => { // addScoop is now an arrow function
      setTimeout(() => {
        this.scoops++;
        console.log('scoop added!');
      }, 0.5);
    };

    const dessert = new IceCream();
    dessert.addScoop();

Yeah, this doesn't work for the same reason - arrow functions inherit their this value from their surrounding context. Outside of the addScoop() method, the value of this is the global object. So if addScoop() is an arrow function, the value of this inside addScoop() is the global object. Which then makes the value of this in the function passed to setTimeout() also set to the global object!

### Default Function Parameters

Take a look at this code:

    function greet(name, greeting) {
      name = (typeof name !== 'undefined') ?  name : 'Student';
      greeting = (typeof greeting !== 'undefined') ?  greeting : 'Welcome';

      return `${greeting} ${name}!`;
    }

    greet(); // Welcome Student!
    greet('James'); // Welcome James!
    greet('Richard', 'Howdy'); // Howdy Richard!

What is all that horrible mess in the first two lines of the greet() function? All of that is there to provide default values for the function if the required arguments aren't provided. It's pretty ugly, though...

Fortunately, ES6 has introduced a new way to create defaults. It's called default function parameters.

#### Default function parameters

Default function parameters are quite easy to read since they're placed in the function's parameter list:

    function greet(name = 'Student', greeting = 'Welcome') {
      return `${greeting} ${name}!`;
    }

    greet(); // Welcome Student!
    greet('James'); // Welcome James!
    greet('Richard', 'Howdy'); // Howdy Richard!

Wow, that's a lot less code, so much cleaner, and significantly easier to read!

To create a default parameter, you add an equal sign ( = ) and then whatever you want the parameter to default to if an argument is not provided. In the code above, both parameters have default values of strings, but they can be any JavaScript type!

### 默认值和解构

#### 默认值和解构数组

你可以将默认函数参数和解构结合到一起， 创建非常强大的函数！

    function createGrid([width = 5, height = 5]) {
      return `Generates a ${width} x ${height} grid`;
    }

    createGrid([]); // Generates a 5 x 5 grid
    createGrid([2]); // Generates a 2 x 5 grid
    createGrid([2, 3]); // Generates a 2 x 3 grid
    createGrid([undefined, 3]); // Generates a 5 x 3 grid
    Returns:
    Generates a 5 x 5 grid
    Generates a 2 x 5 grid
    Generates a 2 x 3 grid
    Generates a 5 x 3 grid

createGrid() 函数预期传入的是数组。它通过解构将数组中的第一项设为 width，第二项设为 height。如果数组为空，或者只有一项，那么就会使用默认参数，并将缺失的参数设为默认值 5。

但是存在一个问题，下面的代码将不可行：

    createGrid(); // throws an error
    Uncaught TypeError: Cannot read property 'Symbol(Symbol.iterator)' of undefined

出现错误，因为 createGrid() 预期传入的是数组，然后对其进行解构。因为函数被调用时没有传入数组，所以出现问题。但是，我们可以使用默认的函数参数！

    function createGrid([width = 5, height = 5] = []) {
      return `Generating a grid of ${width} by ${height}`;
    }

看到函数参数中的新 = [] 了吗？如果 createGrid() 在被调用时没有任何参数，它将使用这个默认的空数组。因为数组是空的，因此没有任何内容可以解构为 width 和 height，因此将应用它们的默认值！通过添加 = [] 为整个参数设定一个默认值，下面的代码将可行：

    createGrid(); // Generates a 5 x 5 grid
    Returns: Generates a 5 x 5 grid

#### 默认值和解构对象

就像使用数组默认值解构数组一样，函数可以让对象成为一个默认参数，并使用对象解构：

    function createSundae({scoops = 1, toppings = ['Hot Fudge']}) {
      const scoopText = scoops === 1 ? 'scoop' : 'scoops';
      return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`;
    }

    createSundae({}); // Your sundae has 1 scoop with Hot Fudge toppings.
    createSundae({scoops: 2}); // Your sundae has 2 scoops with Hot Fudge toppings.
    createSundae({scoops: 2, toppings: ['Sprinkles']}); // Your sundae has 2 scoops with Sprinkles toppings.
    createSundae({toppings: ['Cookie Dough']}); // Your sundae has 1 scoop with Cookie Dough toppings.

    Returns:
    Your sundae has 1 scoop with Hot Fudge toppings.
    Your sundae has 2 scoops with Hot Fudge toppings.
    Your sundae has 2 scoops with Sprinkles toppings.
    Your sundae has 1 scoop with Cookie Dough toppings.

就像上面的数组示例，如果尝试调用函数时不传入参数，将不可行：

    createSundae(); // throws an error
    Uncaught TypeError: Cannot match against 'undefined' or 'null'.

我们可以通过向函数提供默认对象来防止出现此问题：

    function createSundae({scoops = 1, toppings = ['Hot Fudge']} = {}) {
      const scoopText = scoops === 1 ? 'scoop' : 'scoops';
      return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`;
    }

通过添加空对象作为默认参数，以防未提供参数，现在调用函数时没有任何参数将可行。

    createSundae(); // Your sundae has 1 scoop with Hot Fudge toppings.
    Returns: Your sundae has 1 scoop with Hot Fudge toppings.

#### 数组默认值与对象默认值

默认函数参数只是个简单的添加内容，但是却带来很多便利！与数组默认值相比，对象默认值具备的一个优势是能够处理跳过的选项。看看下面的代码：

    function createSundae({scoops = 1, toppings = ['Hot Fudge']} = {}) { … }

在 createSundae() 函数使用对象默认值进行解构时，如果你想使用 scoops 的默认值，但是更改 toppings，那么只需使用 toppings 传入一个对象：

    createSundae({toppings: ['Hot Fudge', 'Sprinkles', 'Caramel']});

将上述示例与使用数组默认值进行解构的同一函数相对比。

    function createSundae([scoops = 1, toppings = ['Hot Fudge']] = []) { … }

对于这个函数，如果想使用 scoops 的默认数量，但是更改 toppings，则必须以这种奇怪的方式调用你的函数：

    createSundae([undefined, toppings: ['Hot Fudge', 'Sprinkles', 'Caramel']]);

因为数组是基于位置的，我们需要传入 undefined 以跳过第一个参数（并使用默认值）来到达第二个参数。
除非你有很充足的理由来使用数组默认值进行数组解构，否则建议使用对象默认值进行对象解构！

### 类预览
下面快速查看下 JavaScript 类是怎么写的：

    class Dessert {
      constructor(calories = 250) {
        this.calories = calories;
      }
    }

    class IceCream extends Dessert {
      constructor(flavor, calories, toppings = []) {
        super(calories);
        this.flavor = flavor;
        this.toppings = toppings;
      }
      addTopping(topping) {
        this.toppings.push(topping);
      }
    }
注意到 Dessert 和 IceCream, 前面的新关键字 class ，以及 class IceCream extends Dessert 中的新关键字 extends 了吗？还有 IceCream 的 constructor() 方法中 super() 的调用。

在创建 JavaScript 类时，可以使用大量新的关键字和语法了。但是，在具体讲解如何编写 JavaScript 类之前，我们需要指出与基于类的语言相比，JavaScript 非常令人困惑的部分。

### JavaScript 类

ES5 “类”总结
因为 ES6 类只是一个“幻景”（语法糖），原型继承实际上在底层被隐藏起来了，我们快速了解下如何用 ES5 代码创建“类”：

    function Plane(numEngines) {
      this.numEngines = numEngines;
      this.enginesActive = false;
    }

    // methods "inherited" by all instances
    Plane.prototype.startEngines = function () {
      console.log('starting engines...');
      this.enginesActive = true;
    };

    const richardsPlane = new Plane(1);
    richardsPlane.startEngines();

    const jamesPlane = new Plane(4);
    jamesPlane.startEngines();

在上述代码中，Plane 函数是一个构造函数，它将用来创建新的 Plane 对象。具体的 Plane 对象的数据被传递给 Plane 函数，并设置到该对象上。每个 Plane 对象继承的方法被放置在 Plane.prototype 对象上。然后，richardsPlane 被创建后有一个引擎，而 jamesPlane 被创建后有四个引擎。但是，这两个对象都使用相同的 startEngines 方法来激活各自的引擎。

需要注意的事项：

构造函数使用 new 关键字被调用
按照惯例，构造函数名以大写字母开头
构造函数控制将被创建的对象的数据的设置
“继承”的方法被放在构造函数的原型对象上
当我们了解 ES6 类的原理时，请记住这几点，因为 ES6 类都在底层帮你设置了所有这些。

ES6 类
以下是同一 Plane 类使用新的 class 语法编写后的代码：

    class Plane {
      constructor(numEngines) {
        this.numEngines = numEngines;
        this.enginesActive = false;
      }

      startEngines() {
        console.log('starting engines…');
        this.enginesActive = true;
      }
    }

### 使用 JavaScript 类

为了证明类没有任何特别之处，我们来看看下面的代码：

    class Plane {
      constructor(numEngines) {
        this.numEngines = numEngines;
        this.enginesActive = false;
      }

      startEngines() {
        console.log('starting engines…');
        this.enginesActive = true;
      }
    }

    typeof Plane; // function
    Returns: function

没错，它只是个函数！甚至没有向 JavaScript 添加新类型。

>⚠️ 逗号都去哪了？ ⚠️
>你是否注意到，类中的方法定义之间没有任何逗号了？在类中，不用逗号来区分属性或方法。如果添加逗号，将出现 SyntaxError：unexpected token

### 静态方法

要添加静态方法，请在方法名称前面加上关键字 static。请看看下面的代码中的 badWeather() 方法。

    class Plane {
      constructor(numEngines) {
        this.numEngines = numEngines;
        this.enginesActive = false;
      }

      static badWeather(planes) {
        for (plane of planes) {
          plane.enginesActive = false;
        }
      }

      startEngines() {
        console.log('starting engines…');
        this.enginesActive = true;
      }
    }

注意 badWeather() 在前面有单词 static，而 startEngines() 没有？这样使得 badWeather() 成为 Plane 类中可以直接访问的方法，因此你可以这样调用它：

    Plane.badWeather([plane1, plane2, plane3]);

注意：对构造函数、类方法或原型继承的原理有点困惑？我们专门开设了一门课程。请参阅面向对象的 JavaScript。

#### 类的优势


设置内容更少
创建函数要编写的代码少多了
清晰地定义了构造函数
在类定义总，可以清晰地指定构造函数。
全部都包含起来了
类需要的所有代码都包含在类声明中。你可以同时设定一切内容，而不用在一个位置编写构造函数，然后向原型一个一个地添加方法，你可以同时做所有的事！

#### 使用类时需要注意的事项

class 不是魔术
关键字 class 带来了其它基于类的语言中的很多思想观念。它没有像变魔术一样向 JavaScript 类添加了此功能。
class 是原型继承的抽象形式
我们已经多次提到，JavaScript 类实际上使用的就是原型继承。
使用类需要用到 new
在创建 JavaScript 类的新实例时，必须使用关键字 new

    class Toy {
      ...
    }

    const myToy1 = Toy(); // throws an error
    Uncaught TypeError: Class constructor Toy cannot be invoked without 'new'

但是，添加关键字 new 后问题就解决了

    const myToy2 = new Toy(); // this works!

### super 和 extends

#### ES6 中的子类

我们已经了解了如何在 JavaScript 中创建类。现在使用新的 super 和 extends 关键字扩展类。

    class Tree {
      constructor(size = '10', leaves = {spring: 'green', summer: 'green', fall: 'orange', winter: null}) {
        this.size = size;
        this.leaves = leaves;
        this.leafColor = null;
      }

      changeSeason(season) {
        this.leafColor = this.leaves[season];
        if (season === 'spring') {
          this.size += 1;
        }
      }
    }

    class Maple extends Tree {
      constructor(syrupQty = 15, size, barkColor, leaves) {
        super(size, barkColor, leaves);
        this.syrupQty = syrupQty;
      }

      changeSeason(season) {
        super.changeSeason(season);
        if (season === 'spring') {
          this.syrupQty += 1;
        }
      }

      gatherSyrup() {
        this.syrupQty -= 3;
      }
    }

    const myMaple = new Maple(15, 5);
    myMaple.changeSeason('fall');
    myMaple.gatherSyrup();
    myMaple.changeSeason('spring');


Tree 和 Maple 都是 JavaScript 类。Maple 类是 Tree 的子类，并使用关键字 extends 将自己设为子类。要让子类可以访问到父类，需要使用关键字 super。注意到 super 有两种使用方式吗？在 Maple 的构造方法中，super 被用作函数。在 Maple 的changeSeason() 方法中，super 被用作对象！

与 ES5 子类对比
我们看看用 ES5 编写相同功能的代码：

    function Tree() {
      this.size = size || 10;
      this.leaves = leaves || {spring: 'green', summer: 'green', fall: 'orange', winter: null};
      this.leafColor;
    }

    Tree.prototype.changeSeason = function(season) {
      this.leafColor = this.leaves[season];
      if (season === 'spring') {
        this.size += 1;
      }
    }

    function Maple (syrupQty, size, barkColor, leaves) {
      Tree.call(this, size, barkColor, leaves);
      this.syrupQty = syrupQty || 15;
    }

    Maple.prototype = Object.create(Tree.prototype);
    Maple.prototype.constructor = Maple;

    Maple.prototype.changeSeason = function(season) {
      Tree.prototype.changeSeason.call(this, season);
      if (season === 'spring') {
        this.syrupQty += 1;
      }
    }

    Maple.prototype.gatherSyrup = function() {
      this.syrupQty -= 3;
    }

    const myMaple = new Maple(15, 5);
    myMaple.changeSeason('fall');
    myMaple.gatherSyrup();
    myMaple.changeSeason('spring');

这段代码和上面的类风格的代码都实现了相同的功能。

### 使用 JavaScript 子类

#### 使用子类

像大多数新增加的特性，使用 class、super 和 extends 创建子类时设置代码少了很多，语法更清晰。

只需记住，在底层，函数和原型之间的连接是一样的。

#### super 必须在 this 之前被调用

在子类构造函数中，在使用 this 之前，必须先调用超级类。

    class Apple {}
    class GrannySmith extends Apple {
      constructor(tartnessLevel, energy) {
        this.tartnessLevel = tartnessLevel; // `this` before `super` will throw an error!
        super(energy); 
      }
    }

## ES6内置功能

### Symbol

#### Symbols（标识符）

Symbol 是一种独特的且不可变的数据类型，经常用来标识对象属性。

要创建 Symbol，输入 Symbol()，并添加一个可选的字符串作为其描述。

    const sym1 = Symbol('apple');
    console.log(sym1);
    Symbol(apple)

它将创建唯一的标识符，并将其存储在 sym1 中。描述 "apple" 只是用来描述标识符的一种方式，但是不能用来访问标识符本身。

为了展示它的工作原理，如果你对具有相同描述的两个标识符进行比较……

    const sym2 = Symbol('banana');
    const sym3 = Symbol('banana');
    console.log(sym2 === sym3);
    false

结果是 false，因为描述只是用来描述符号，它并不是标识符本身的一部分。无论描述是什么，每次都创建新的标识符。
当然，依然很难弄明白，所以，我们来看一个之前视频中的示例，看看标识符的作用。下面是代表该示例中的 bowl（碗）的代码。

    const bowl = {
      'apple': { color: 'red', weight: 136.078 },
      'banana': { color: 'yellow', weight: 183.15 },
      'orange': { color: 'orange', weight: 170.097 }
    };

碗中包含水果，它们是 bowl 的属性对象。但是，当我们添加第二个香蕉时，遇到了问题。

    const bowl = {
      'apple': { color: 'red', weight: 136.078 },
      'banana': { color: 'yellow', weight: 183.151 },
      'orange': { color: 'orange', weight: 170.097 },
      'banana': { color: 'yellow', weight: 176.845 }
    };
    console.log(bowl);

    Object {apple: Object, banana: Object, orange: Object}

新添加的香蕉将上一个香蕉覆盖了。为了解决该问题，我们可以使用标识符。

    const bowl = {
      [Symbol('apple')]: { color: 'red', weight: 136.078 },
      [Symbol('banana')]: { color: 'yellow', weight: 183.15 },
      [Symbol('orange')]: { color: 'orange', weight: 170.097 },
      [Symbol('banana')]: { color: 'yellow', weight: 176.845 }
    };
    console.log(bowl);

    Object {Symbol(apple): Object, Symbol(banana): Object, Symbol(orange): Object, Symbol(banana): Object}

通过更改 bowl 的属性并使用标识符，每个属性都是唯一的标识符，第一个香蕉不会被第二个香蕉覆盖。

### 迭代器协议和可迭代协议

在继续之前，我们先花些时间看一下 ES6 中的两个新协议：

* 可迭代协议
* 迭代器协议

这两个协议不是内置的，但是它们可以帮助你理解 ES6 中的新迭代概念，就像给你展示标识符的使用案例一样。

#### 可迭代协议

可迭代协议用来定义和自定义对象的迭代行为。也就是说在 ES6 中，你可以灵活地指定循环访问对象中的值的方式。对于某些对象，它们已经内置了这一行为。例如，字符串和数组就是内置可迭代类型的例子。

可迭代协议用来定义和自定义对象的迭代行为。也就是说在 ES6 中，你可以灵活地指定循环访问对象中的值的方式。对于某些对象，它们已经内置了这一行为。例如，字符串和数组就是内置可迭代类型的例子。

    const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
    for (const digit of digits) {
      console.log(digit);
    }
    0 
    1 
    2 
    3 
    4 
    5 
    6 
    7 
    8 
    9 

在第一节课，我们提到，任何可迭代的对象都可以使用新的 for...of 循环。在这节课的稍后阶段，我们还将学习 Set（集合）和 Map（映射），它们也是内置可迭代类型。

#### 工作原理

为了使对象可迭代，它必须实现可迭代接口。如果你之前使用的是 Java 或 C 语言等语言，那么你可能熟悉接口，但是如果没用过这些语言，接口其实就是为了让对象可迭代，它必须包含默认的迭代器方法。该方法将定义对象如何被迭代。

迭代器方法（可通过常量 [Symbol.iterator] 获得）是一个无参数的函数，返回的是迭代器对象。迭代器对象是遵守迭代器协议的对象。

#### 迭代器协议

迭代器协议用来定义对象生成一系列值的标准方式。实际上就是现在有了定义对象如何迭代的流程。通过执行 .next() 方法来完成这一流程。

#### 工作原理

当对象执行 .next() 方法时，就变成了迭代器。.next() 方法是无参数函数，返回具有两个属性的对象：

1 value：表示对象内值序列的下个值的数据
2 done：表示迭代器是否已循环访问完值序列的布尔值
  1 如果 done 为 true，则迭代器已到达值序列的末尾处。
  1 如果 done 为 false，则迭代器能够生成值序列中的另一个值。

下面是之前的一个示例，但是我们改为使用数组的默认迭代器访问数组中的每个值。

    const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
    const arrayIterator = digits[Symbol.iterator]();

    console.log(arrayIterator.next());
    console.log(arrayIterator.next());
    console.log(arrayIterator.next());

    Object {value: 0, done: false}
    Object {value: 1, done: false}
    Object {value: 2, done: false}

### Set

#### 数学意义上的集合（Set）
回忆下之前的数学知识，Set 就是唯一项的集合。例如，{2, 4, 5, 6} 是 Set，因为每个数字都是唯一的，只出现一次。但是，{1, 1, 2, 4} 不是 Set，因为它包含重复的项目（1 出现了两次！）。

在 JavaScript 中，我们已经可以使用数组表示类似于数学意义上的集合。

    const nums = [2, 4, 5, 6];

但是，数组并不要求项目必须唯一。如果我们尝试向 nums 中添加一个 2，JavaScript 不会报错，会正常添加这个 2。

    nums.push(2);
    console.log(nums);
    [2, 4, 5, 6, 2]

现在，nums 不再是数学意义上的集合。

#### Set（集合）

在 ES6 中，有一个新的内置对象的行为和数学意义上的集合相同，使用起来类似于数组。这个新对象就叫做“Set”。Set 与数组之间的最大区别是：

* Set 不基于索引，不能根据集合中的条目在集合中的位置引用这些条目
* Set 中的条目不能单独被访问

基本上，Set 是让你可以存储唯一条目的对象。你可以向 Set 中添加条目，删除条目，并循环访问 Set。这些条目可以是原始值或对象。

#### 如何创建 Set

可以通过几种不同的方式创建 Set。第一种很简单：

    const games = new Set();
    console.log(games);
    Set {}

此代码会创建空的 Set games，其中没有条目。

如果你想根据值列表创建 Set，则使用数组：

    const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);
    console.log(games);

    Set {'Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart'}

注意上述示例在创建 Set 时，会自动移除重复的条目 "Super Mario Bros."，很整洁！

### 修改 Set

#### 修改 Set

创建 Set 后，你可能想要添加或删除条目。如何操作呢？可以使用名称对应的 .add() 和 .delete() 方法：

    const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);

    games.add('Banjo-Tooie');
    games.add('Age of Empires');
    games.delete('Super Mario Bros.');

    console.log(games);//Set {'Banjo-Kazooie', 'Mario Kart', 'Banjo-Tooie', 'Age of Empires'}

另一方面，如果你想要删除 Set 中的所有条目，可以使用 .clear() 方法。

    games.clear()
    console.log(games);
    Set {}

提示：如果你尝试向 Set 中 .add() 重复的条目，系统不会报错，但是该条目不会添加到 Set 中。此外，如果你尝试 .delete() Set 中不存在的条目，也不会报错，Set 保持不变。如果成功地添加或删除了条目，这两个方法都返回 true，反之返回 false。

### 使用 Set

#### 使用 Set

#### 查看长度

构建 Set 后，可以通过几个不同的属性和方法来处理 Set。

使用 .size 属性可以返回 Set 中的条目数：

    const months = new Set(['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']);
    console.log(months.size);

    12

注意，不能像数组那样通过索引访问 Set，因此要使用 .size 属性，而不是 .length 属性来获取 Set 的大小。

#### 检查是否存在某个条目
使用 .has() 方法可以检查 Set 中是否存在某个条目。如果 Set 中有该条目，则 .has() 将返回 true。如果 Set 中不存在该条目，则 .has() 将返回 false。

    console.log(months.has('September'));
    true

#### 检索所有值
最后，使用 .values() 方法可以返回 Set 中的值。.values() 方法的返回值是 SetIterator 对象。

    console.log(months.values());
    SetIterator {'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'}
    
稍后将讲解 SetIterator 对象！
提示：.keys() 方法将和 .values() 方法的行为完全一样：将 Set 的值返回到新的迭代器对象中。.keys() 方法是 .values() 方法的别名，和 Map（映射）中的类似。你稍后将在这节课的 Map 部分看到 .keys() 方法。

### Set 与迭代器

处理 Set 的最后一步是循环访问 Set。

如果还记得之前介绍的 ES6 中的新可迭代协议和迭代器协议，那么你会想起 Set 是内置可迭代类型。这意味着循环时的两件事：

1 你可以使用 Set 的默认迭代器循环访问 Set 中的每一项。
2 你可以使用新的 for...of 循环来循环访问 Set 中的每一项。

#### 使用 SetIterator
因为 .values() 方法返回新的迭代器对象（称为 SetIterator），你可以将该迭代器对象存储在变量中，并使用 .next() 访问 Set 中的每一项。

    const iterator = months.values();
    iterator.next();
    Object {value: 'January', done: false}

如果再次运行 .next() 呢？

    iterator.next();
    Object {value: 'February', done: false}

等等，一直运行到 done 等于 true 时，标志着 Set 的结束。

#### 使用 for...of 循环
一种更简单的方法去循环访问 Set 中的项目是 for...of 循环。

    const colors = new Set(['red', 'orange', 'yellow', 'green', 'blue', 'violet', 'brown', 'black']);
    for (const color of colors) {
      console.log(color);
    }

    red 
    orange 
    yellow 
    green 
    blue 
    violet 
    brown 
    black

### WeakSet

#### 什么是 WeakSet（弱集合）？

WeakSet 和普通 Set 很像，但是具有以下关键区别：

1 WeakSet 只能包含对象
2 WeakSet 无法迭代，意味着不能循环访问其中的对象
3 WeakSet 没有 .clear() 方法

你可以像创建普通 Set 那样创建 WeakSet，但是需要使用 WeakSet 构造函数。

    const student1 = { name: 'James', age: 26, gender: 'male' };
    const student2 = { name: 'Julia', age: 27, gender: 'female' };
    const student3 = { name: 'Richard', age: 31, gender: 'male' };

    const roster = new WeakSet([student1, student2, student3]);
    console.log(roster);

    WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'Richard', age: 31, gender: 'male'}, Object {name: 'James', age: 26, gender: 'male'}}

但是如果你尝试添加对象以外的内容，系统将报错！

    roster.add('Amanda');
    Uncaught TypeError: Invalid value used in weak set(…)

这是预期到的行为，因为 WeakSet 只能包含对象。但是为何只能包含对象？如果普通 Set 可以包含对象和其他类型的数据，为何还要使用 WeakSet？这个问题的答案与为何 WeakSet 没有 .clear() 方法有很大的关系……

#### 垃圾回收

在 JavaScript 中，创建新的值时会分配内存，并且当这些值不再需要时，将自动释放内存。这种内存不再需要后释放内存的过程称为垃圾回收。

WeakSet 通过专门使用对象作为键值来利用这一点。如果将对象设为 null，则本质上是删除该对象。当 JavaScript 的垃圾回收器运行时，该对象之前占用的内存将被释放，以便稍后在程序中使用。

    student3 = null;
    console.log(roster);
    WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'James', age: 26, gender: 'male'}}

这种机制的好处在于你不用去担心要删掉对 WeakSet 中已删除对象的引用，JavaScript 会帮你删除！如果对象被删除，当垃圾回收器运行时，该对象也会从 WeakSet 中删除。这样的话，如果你想要一种高效、轻便的解决方法去创建一组对象，就可以使用 WeakSet。

垃圾回收的发生时间点取决于很多因素。请参阅 [MDN 的文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management#垃圾回收)，详细了解用于处理 JavaScript 中的垃圾回收的算法。

### 创建和修改 Map

#### Map（映射）

如果说 Set 类似于数组，那么 Map 就类似于对象，因为 Map 存储键值对，和对象包含命名属性及值相类似。

本质上，Map 是一个可以存储键值对的对象，键和值都可以是对象、原始值或二者的结合。

#### 如何创建 Map

要创建 Map，只需输入：

    const employees = new Map();
    console.log(employees);
    Map {}

这样就会创建空的 Map employee，没有键值对。

#### 修改 Map

和 Set 不同，你无法使用值列表创建 Map；而是使用 Map 的 .set() 方法添加键值。

    const employees = new Map();

    employees.set('james.parkes@udacity.com', { 
        firstName: 'James',
        lastName: 'Parkes',
        role: 'Content Developer' 
    });
    employees.set('julia@udacity.com', {
        firstName: 'Julia',
        lastName: 'Van Cleve',
        role: 'Content Developer'
    });
    employees.set('richard@udacity.com', {
        firstName: 'Richard',
        lastName: 'Kalehoff',
        role: 'Content Developer'
    });

    console.log(employees);
    Map {'james.parkes@udacity.com' => Object {...}, 'julia@udacity.com' => Object {...}, 'richard@udacity.com' => Object {...}}

.set() 方法有两个参数。第一个参数是键，用来引用第二个参数，即值。

要移除键值对，只需使用 .delete() 方法。

    employees.delete('julia@udacity.com');
    employees.delete('richard@udacity.com');
    console.log(employees);
    Map {'james.parkes@udacity.com' => Object {firstName: 'James', lastName: 'Parkes', role: 'Course Developer'}}

同样，和 Set 类似，你可以使用 .clear() 方法从 Map 中删除所有键值对。

    employees.clear()
    console.log(employees);
    Map {}

>提示：如果你使用 .set() 向 Map 中添加键已存在的键值对，不会收到错误，但是该键值对将覆盖 Map 中的现有键值对。此外，如果尝试使用 .delete() 删除 Map 中不存在的键值，不会收到错误，而 Map 会保持不变。

如果成功地删除了键值对，.delete() 方法会返回 true，失败则返回 false。.set() 如果成功执行，则返回 Map 对象本身。

### 处理 Map

#### 处理 Map

构建 Map 后，可以使用 .has() 方法并向其传入一个键来检查 Map 中是否存在该键值对。

    const members = new Map();

    members.set('Evelyn', 75.68);
    members.set('Liam', 20.16);
    members.set('Sophia', 0);
    members.set('Marcus', 10.25);

    console.log(members.has('Xavier'));
    console.log(members.has('Marcus'));
    false
    true
    
还可以通过向 .get() 方法传入一个键，检索 Map 中的值。

    console.log(members.get('Evelyn'));
    75.68

### 循环访问 Map

#### 循环访问 Map

你已经创建了 Map，添加了一些键值对，现在你想循环访问该 Map。幸运的是，可以通过以下三种方式循环访问：

1 使用 Map 的默认迭代器循环访问每个键或值
2 使用新的 for...of 循环来循环访问每个键值对
3 使用 Map 的 .forEach() 方法循环访问每个键值对

#### 1. 使用 MapIterator

在 Map 上使用 .keys() 和 .values() 方法将返回新的迭代器对象，叫做 MapIterator。你可以将该迭代器对象存储在新的变量中，并使用 .next() 循环访问每个键或值。你所使用的方法将决定迭代器是否能够访问 Map 的键或值。

    let iteratorObjForKeys = members.keys();
    iteratorObjForKeys.next();
    Object {value: 'Evelyn', done: false}

使用 .next() 获得下个键值对。

    iteratorObjForKeys.next();
    Object {value: 'Liam', done: false}

等等。

    iteratorObjForKeys.next();
    Object {value: 'Sophia', done: false}

另一方面，使用 .values() 方法访问 Map 的值，然后重复同一流程。

    let iteratorObjForValues = members.values();
    iteratorObjForValues.next();
    Object {value: 75.68, done: false}

#### 2. 使用 for...of 循环

Map 的第二种循环访问方式是使用 for...of 循环。

    for (const member of members) {
      console.log(member);
    }
    ['Evelyn', 75.68]
    ['Liam', 20.16]
    ['Sophia', 0]
    ['Marcus', 10.25]

但是，在对 Map 使用 for...of 循环时，并不会得到一个键值或一个值。键值对会拆分为一个数组，第一个元素是键，第二个元素是值。有没有什么方法可以解决这一问题？

#### 3. 使用 forEach 循环

最后一种循环访问 Map 的方式是使用 .forEach() 方法。

    members.forEach((value, key) => console.log(value, key));
    'Evelyn' 75.68
    'Liam' 20.16
    'Sophia' 0
    'Marcus' 10.25

注意，在使用箭头函数后，forEach 循环是如何简单地读取数据的。对于 members 中的每个 value 和 key，都会被输出到控制台中。

### WeakMap

>提示：如果你已经看过 WeakSet 部分，那么这部分相当于复习了。WeakMap（弱映射）的行为和 WeakSet 的一样，只是 WeakMap 处理的是键值对，而不是单个条目。

#### 什么是 WeakMap？

WeakMap 和普通 Map 很像，但是具有以下关键区别：

1 WeakMap 只能包含对象作为键，
2 WeakMap 无法迭代，意味着无法循环访问，并且
3 WeakMap 没有 .clear() 方法。
你可以像创建普通 Map 那样创建 WeakMap，但是需要使用 WeakMap 构造函数。

    const book1 = { title: 'Pride and Prejudice', author: 'Jane Austen' };
    const book2 = { title: 'The Catcher in the Rye', author: 'J.D. Salinger' };
    const book3 = { title: 'Gulliver's Travels', author: 'Jonathan Swift' };

    const library = new WeakMap();
    library.set(book1, true);
    library.set(book2, false);
    library.set(book3, true);

    console.log(library);
    WeakMap {Object {title: 'Pride and Prejudice', author: 'Jane Austen'} => true, Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver's Travels', author: 'Jonathan Swift'} => true}

但是如果你尝试添加对象以外的内容作为键，系统将报错！

    library.set('The Grapes of Wrath', false);
    Uncaught TypeError: Invalid value used as weak map key(…)

这是可预期到的行为，因为 WeakMap 只能包含对象作为键。但是为何只能包含对象？同样，和 WeakSet 相似，WeakMap 利用垃圾回收机制让其可以更简单地使用和易维护。

#### 垃圾回收
在 JavaScript 中，创建新的值时会分配内存，并且当这些值不再需要时，将自动释放内存。这种内存不再需要后释放内存的过程称为垃圾回收。

WeakMap 通过专门处理对象作为键来利用这一点。如果将对象设为 null，则本质上是删除该对象。当 JavaScript 的垃圾回收器运行时，该对象之前占用的内存将被释放，以便稍后在程序中使用。

    book1 = null;
    console.log(library);
    WeakMap {Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver’s Travels', author: 'Jonathan Swift'} => true}

这种机制的好处在于你不用去担心要删掉对 WeakMap 中已删除对象的引用键，JavaScript 会帮你删除！如果对象被删除，当垃圾回收器运行时，该对象键也会从弱映射中删除。这样的话，如果你想要一种高效、轻便的解决方法去创建一组具有元数据的对象，就可以使用 WeakMap。

垃圾回收的发生时间点取决于很多因素。请参阅 MDN 的文档，详细了解用于处理 JavaScript 中的垃圾回收的算法。

### Promise

#### Promise

JavaScript Promise 是用新的 [Promise 构造函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) - new Promise() 创建而成的。promise 使你能够展开一些可以异步完成的工作，并回到常规工作。创建 promise 时，必须向其提供异步运行的代码。将该代码当做参数提供给构造函数：

    new Promise(function () {
        window.setTimeout(function createSundae(flavor = 'chocolate') {
            const sundae = {};
            // request ice cream
            // get cone
            // warm up ice cream scoop
            // scoop generous portion into cone!
        }, Math.random() * 2000);
    });

该代码在我发出请求时将会创建一个 promise，并且在几秒钟后启动。然后需要在 createSundae 函数中执行几个步骤。

#### 指示一个成功请求或者失败请求

但是完成这一切后，JavaScript 如何通知我们它已经完成操作，准备好让我们恢复工作？它通过向初始函数中传入两个函数来实现这一点，通常我们将这两个函数称为 resolve 和 reject。
该函数被传递给我们向 Promise 构造函数提供的函数 - 通常单词"resolve”用于表示当请求成功完成时，应该调用此函数。请注意第一行的 resolve：

    new Promise(function (resolve, reject) {
        window.setTimeout(function createSundae(flavor = 'chocolate') {
            const sundae = {};
            // request ice cream
            // get cone
            // warm up ice cream scoop
            // scoop generous portion into cone!
            resolve(sundae);
        }, Math.random() * 2000);
    });

当 sundae 被成功创建后，它会调用 resolve 方法并向其传递我们要返回的数据，在本例中，返回的数据是完成的 sundae。因此 resolve 方法用来表示请求已完成，并且成功完成了请求。
如果请求存在问题，无法完成请求，那么我们可以使用传递给该函数的第二个函数。通常，该函数存储在一个叫做"reject"的标识符中，表示如果请求因为某种原因失败了，应该使用该函数。请看看第一行的 reject：

    new Promise(function (resolve, reject) {
        window.setTimeout(function createSundae(flavor = 'chocolate') {
            const sundae = {};
            // request ice cream
            // get cone
            // warm up ice cream scoop
            // scoop generous portion into cone!
            if ( /* iceCreamConeIsEmpty(flavor) */ ) {
                reject(`Sorry, we're out of that flavor :-(`);
            }
            resolve(sundae);
        }, Math.random() * 2000);
    });

如果请求无法完成，则使用 reject 方法。注意，即使请求失败了，我们依然可以返回数据，在本例中，我们只是返回了一段文字，表示没有我们想要的冰激凌口味。
Promise构造函数需要一个可以运行的函数，运行一段时间后，将成功完成（使用 resolve 方法）或失败（使用 reject 方法）。当结果最终确定时（请求成功完成或失败），现在 promise 已经实现了，并且将通知我们，这样我们便能决定将如何对结果做处理。

#### Promise 立即返回对象

首先要注意的是，Promise 将立即返回一个对象。

    const myPromiseObj = new Promise(function (resolve, reject) {
        // sundae creation code
    });

该对象上具有一个 .then() 方法，我们可以让该方法通知我们 promise 中的请求成功与否。.then() 方法会接收两个函数：

1 请求成功完成时要运行的函数
2 请求失败时要运行的函数

    mySundae.then(function(sundae) {
        console.log(`Time to eat my delicious ${sundae}`);
    }, function(msg) {
        console.log(msg);
        self.goCry(); // not a real method
    });

可以看出，传递给 .then() 的第一个函数将被调用，并传入 Promise 的 resolve 函数需要使用的数据。这里，该函数将接收 sundae 对象。第二个函数传入的数据会在 Promise 的 reject 函数被调用时使用。这里，该函数收到错误消息"Sorry, we're out of that flavor :-("，在上述 Promise 代码中，reject 函数被调用。

### 更多 Promise

请参阅我们的 [Promise 课程](https://www.udacity.com/course/javascript-promises--ud898)，详细了解以下内容：

JavaScript Promise
如何处理返回的数据和错误
构建一个叫做 Exoplanet Explorer 的应用，并使用 JavaScript Promise 异步获取远程数据
有问题？ 你可以前往 优达学城论坛 与课程导师和其他学员一起讨论！

### Proxy

要创建 Proxy（代理）对象，我们使用 Proxy 构造函数 new Proxy();。Proxy 构造函数接收两个项目：

* 它将要代理的对象
* 包含将为被代理对象处理的方法列表的对象

第二个对象叫做处理器.

### Proxy 内的一个传递

创建 Proxy 的最简单方式是提供对象和空的 handler（处理器）对象。

    var richard = {status: 'looking for work'};
    var agent = new Proxy(richard, {});

    agent.status; // returns 'looking for work'

上述代码并没有对 Proxy 执行任何特殊操作，只是将请求直接传递给源对象！如果我们希望 Proxy 对象截获请求，这就是 handler 对象的作用了！
让 Proxy 变得有用的关键是当做第二个对象传递给 Proxy 构造函数的 handler 对象。handler 对象由将用于访问属性的方法构成。我们看看 get：

#### Get Trap（捕获器）

get 用来截获对属性的调用：

    const richard = {status: 'looking for work'};
    const handler = {
        get(target, propName) {
            console.log(target); // the `richard` object, not `handler` and not `agent`
            console.log(propName); // the name of the property the proxy (`agent` in this case) is checking
        }
    };
    const agent = new Proxy(richard, handler);
    agent.status; // logs out the richard object (not the agent object!) and the name of the property being accessed (`status`)

在上述代码中，handler 对象具有一个 get 方法（因为被用在 Proxy 中，所以将"function"（方法）称之为"trap"（捕获器））。当代码 agent.status; 在最后一行运行时，因为存在 get 捕获器，它将截获该调用以获得 status（状态）属性并运行 get 捕获器方法。这样将会输出 Proxy 的目标对象（richard 对象），然后输出被请求的属性（status 属性）的名称。它的作用就是这些！它不会实际地输出属性！这很重要 —— 如果使用了捕获器，你需要确保为该捕获器提供所有的功能。

#### 从 Proxy 内部访问目标对象

如果我们想真正地提供真实的结果，我们需要返回目标对象的属性：

    const richard = {status: 'looking for work'};
    const handler = {
        get(target, propName) {
            console.log(target);
            console.log(propName);
            return target[propName];
        }
    };
    const agent = new Proxy(richard, handler);
    agent.status; // (1)logs the richard object, (2)logs the property being accessed, (3)returns the text in richard.status

注意我们在 get trap 中添加了最后一行 return target[propName];，这样将会访问目标对象的属性并返回它。

#### 直接获取 Proxy 的返回信息

此外，我们可以使用 Proxy 提供直接的反馈：

    const richard = {status: 'looking for work'};
    const handler = {
        get(target, propName) {
            return `He's following many leads, so you should offer a contract as soon as possible!`;
        }
    };
    const agent = new Proxy(richard, handler);
    agent.status; // returns the text `He's following many leads, so you should offer a contract as soon as possible!`

对于上述代码，Proxy 甚至不会检查目标对象，直接对调用代码做出响应。

因此每当 Proxy 上的属性被访问，get trap 将接管任务。如果我们想截获调用以更改属性，则需要使用 set trap！

set trap 用来截获将更改属性的代码。set trap 将接收： 它代理的对象 被设置的属性 Proxy 的新值

    const richard = {status: 'looking for work'};
    const handler = {
        set(target, propName, value) {
            if (propName === 'payRate') { // if the pay is being set, take 15% as commission
                value = value * 0.85;
            }
            target[propName] = value;
        }
    };
    const agent = new Proxy(richard, handler);
    agent.payRate = 1000; // set the actor's pay to $1,000
    agent.payRate; // $850 the actor's actual pay

在上述代码中，注意 set trap 会检查是否设置了 payRate 属性。如果设置了，Proxy 就从中拿走 15% 的费用作为自己的佣金！当演员的薪酬是一千美元时，因为 payRate 属性已设置，代码从中扣除 15% 的费用，并将实际 payRate 属性设为 850；

#### 其他 Trap

我们查看了 get 和 set trap（可能是你最常用到的 Trap），但是实际上总共有 13 种不同的 Trap，它们都可以用在处理程序中！

1. [get trap](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/get) - 使 proxy 能处理对属性访问权的调用
2. [set trap](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler/set) - 使 proxy 能将属性设为新值
3. apply trap - 使 proxy 能被调用（被代理的对象是函数）
4. has trap - 使 proxy 能使用 in 运算符
5. deleteProperty trap - 使 proxy 能确定属性是否被删除
6. ownKeys trap - 使 proxy 能处理当所有键被请求时的情况
7. construct trap - 使 proxy 能处理 proxy 与 new 关键字一起使用当做构造函数的情形
8. defineProperty trap - 使 proxy 能处理当 defineProperty 被用于创建新的对象属性的情形
9. getOwnPropertyDescriptor trap - 使 proxy 能获得属性的描述符
10. preventExtenions trap - 使 proxy 能对 proxy 对象调用 Object.preventExtensions()
11. isExtensible trap - 使 proxy 能对 proxy 对象调用 Object.isExtensible
12. getPrototypeOf trap - 使 proxy 能对 proxy 对象调用 Object.getPrototypeOf
13. setPrototypeOf trap - 使 proxy 能对 proxy 对象调用 Object.setPrototypeOf

可以看出，有很多 trap 可以让 proxy 管理如何处理被代理的对象的调用。

### Proxy 与 ES5 Getter/Setter

一开始，可能不太清楚的是，ES5 中已经提供了 getter 和 setter 方法，为何还要 Proxy。对于 ES5 的 getter 和 setter 方法，你需要提前知道要获取/设置的属性：

    var obj = {
        _age: 5,
        _height: 4,
        get age() {
            console.log(`getting the "age" property`);
            console.log(this._age);
        },
        get height() {
            console.log(`getting the "height" property`);
            console.log(this._height);
        }
    };

对于上述代码，注意在初始化对象时，我们需要设置 get age() 和 get height()。因此，当我们调用下面的代码时，将获得以下结果：

    obj.age; // logs 'getting the "age" property' & 5
    obj.height; // logs 'getting the "height" property' & 4

但是当我们向该对象添加新的属性时，看看会发生什么：

    obj.weight = 120; // set a new property on the object
    obj.weight; // logs just 120

注意，并没有显示 age 和 height 属性那样生成的 getting the "weight" property 消息。

对于 ES6 中的 Proxy，我们不需要提前知道这些属性*：

    const proxyObj = new Proxy({age: 5, height: 4}, {
        get(targetObj, property) {
            console.log(`getting the ${property} property`);
            console.log(targetObj[property]);
        }
    });

    proxyObj.age; // logs 'getting the age property' & 5
    proxyObj.height; // logs 'getting the height property' & 4

就像 ES5 代码那样一切正常，但是当我们添加新的属性时，看看会发生什么：

    proxyObj.weight = 120; // set a new property on the object
    proxyObj.weight; // logs 'getting the weight property' & 120

看到了吗？向 proxy 对象中添加了 weight 属性，稍后检索它时，它显示了一条日志消息！

因此 proxy 对象的某些功能可能看起来类似于现有的 ES5 getter/setter 方法，但是对于 proxy，在初始化对象时，不需要针对每个属性使用 getter/setter 初始化对象。

### Proxy 小结

Proxy 对象介于真正的对象和调用代码之间。调用代码与 Proxy 交互，而不是真正的对象。要创建 Proxy：

使用 new Proxy() 构造函数
将被代理的对象传入为第一项
第二个对象是 handler（处理器）对象
handler 对象由 13 种不同的 trap 之一构成
trap 是一种函数，将截获对属相的调用，让你运行代码
如果未定义 trap，默认行为会被发送给目标对象
Proxy 是一种强大的创建和管理对象之间的交互的新方式。

### 生成器

每当函数被调用时，JavaScript 引擎就会在函数顶部启动，并运行每行代码，直到到达底部。无法中途停止运行代码，并稍后重新开始。一直都是这种“运行到结束”的工作方式：

    function getEmployee() {
        console.log('the function has started');

        const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

        for (const name of names) {
            console.log(name);
        }

        console.log('the function has ended');
    }

    getEmployee();

运行上述代码将在控制台中输出以下内容：

    the function has started
    Amanda
    Diego
    Farrin
    James
    Kagure
    Kavita
    Orit
    Richard
    the function has ended

如果你想先输出前三名员工的姓名，然后停止一段时间，稍后再从停下的地方继续输出更多员工的姓名呢？普通函数无法这么做，因为无法中途“暂停”运行函数。

#### 可暂停的函数

如果我们希望能够中途暂停运行函数，则需要使用 ES6 中新提供的一种函数，叫做 generator（生成器）函数！我们来看一个示例：

    function* getEmployee() {
        console.log('the function has started');

        const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

        for (const name of names) {
            console.log( name );
        }

        console.log('the function has ended');
    }

注意到 function 关键字后面的星号（即 *）了吗？星号表示该函数实际上是生成器！

现在看看当我们尝试运行该函数时，会发生什么：

    getEmployee();

    // this is the response I get in Chrome:
    getEmployee {[[GeneratorStatus]]: "suspended", [[GeneratorReceiver]]: Window}

### 生成器和迭代器

>警告：我们在上一部分学习了迭代知识，如果你有点忘记了，请再复习一遍，因为在生成器这部分又会提到迭代！

生成器被调用时，它不会运行函数中的任何代码，而是创建和返回迭代器。该迭代器可以用来运行实际生成器的内部代码。

    const generatorIterator = getEmployee();
    generatorIterator.next();

产生我们期望的代码：

    the function has started
    Amanda
    Diego
    Farrin
    James
    Kagure
    Kavita
    Orit
    Richard
    the function has ended

如果你自己尝试运行这段代码，迭代器的 .next() 方法第一次被调用时，它会运行生成器中的所有代码。注意到什么了吗？代码始终没有暂停！那么我们要怎么才能实现神奇的暂停功能呢？

#### 关键字 yield

关键字 yield 是 ES6 中新出现的关键字。只能用在生成器函数中。yield 会导致生成器暂停下来。我们向我们的生成器中添加 yield，试试看：

    function* getEmployee() {
        console.log('the function has started');

        const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

        for (const name of names) {
            console.log(name);
            yield;
        }

        console.log('the function has ended');
    }

注意，现在 for...of 循环中出现了 yield。如果我们调用该生成器（生成迭代器），然后调用 .next()，将获得以下输出：

    const generatorIterator = getEmployee();
    generatorIterator.next();

将输出以下内容到控制台：

    the function has started
    Amanda

暂停了！但是要真的确定下，我们看看下次迭代：

    generatorIterator.next();

将以下内容输出到控制台：

    Diego

它能完全记住上次停下的地方！它获取到数组中的下一项（Diego），记录它，然后再次触发了 yield，再次暂停。

现在能够很好的暂停了，但是如果将数据从生成器返回到外面的世界呢？我们可以使用 yield 实现这一点。

#### 向外面的世界生成数据

我们不再向控制台输出姓名并暂停，而是让代码返回姓名并暂停。

    function* getEmployee() {
        console.log('the function has started');

        const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

        for (const name of names) {
            yield name;
        }

        console.log('the function has ended');
    }

注意，现在从 console.log(name); 切换成了 yield name;。做出这一更改后，当生成器运行时，它会把姓名从函数里返回出去，然后暂停执行代码。我们看看具体效果：

    const generatorIterator = getEmployee();
    let result = generatorIterator.next();
    result.value // is "Amanda"

    generatorIterator.next().value // is "Diego"
    generatorIterator.next().value // is "Farrin"

### 向生成器中发送数据或从中向外发送数据

我们可以使用关键字 yield 从生成器中获取数据。我们还可以将数据发送回生成器中。方式是使用 .next() 方法：

    function* displayResponse() {
        const response = yield;
        console.log(`Your response is "${response}"!`);
    }

    const iterator = displayResponse();

    iterator.next(); // starts running the generator function
    iterator.next('Hello Udacity Student'); // send data into the generator
    // the line above logs to the console: Your response is "Hello Udacity Student"!

使用数据调用 .next()（即 .next('Richard')）会将该数据发送到生成器函数中上次离开的地方。它会将 yield 关键字替换为你提供的数据。

关键字 yield 用来暂停生成器并向生成器外发送数据，然后 .next() 方法用来向生成器中传入数据。下面是使用这两种过程来一次次地循环访问姓名列表的示例：

    function* getEmployee() {
        const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];
        const facts = [];

        for (const name of names) {
            // yield *out* each name AND store the returned data into the facts array
            facts.push(yield name); 
        }

        return facts;
    }

    const generatorIterator = getEmployee();

    // get the first name out of the generator
    let name = generatorIterator.next().value;

    // pass data in *and* get the next name
    name = generatorIterator.next(`${name} is cool!`).value; 

    // pass data in *and* get the next name
    name = generatorIterator.next(`${name} is awesome!`).value; 

    // pass data in *and* get the next name
    name = generatorIterator.next(`${name} is stupendous!`).value; 

    // you get the idea
    name = generatorIterator.next(`${name} is rad!`).value; 
    name = generatorIterator.next(`${name} is impressive!`).value;
    name = generatorIterator.next(`${name} is stunning!`).value;
    name = generatorIterator.next(`${name} is awe-inspiring!`).value;

    // pass the last data in, generator ends and returns the array
    const positions = generatorIterator.next(`${name} is magnificent!`).value; 

    // displays each name with description on its own line
    positions.join('\n');

生成器是强大的新型函数，能够暂停执行代码，同时保持自己的状态。生成器适用于一次一个地循环访问列表项，以便单独处理每项，然后再转到下一项。还可以使用迭代器来处理嵌套回调。例如，假设某个函数需要获得所有仓库的列表和被加星标的次数。在获得每个仓库的星标数量之前，需要获得用户的信息。获得用户的个人资料后，代码可以利用该信息查找所有的仓库。

生成器还将大量用于 JavaScript 语言未来的新增功能中。一个即将使用生成器的新功能是[异步函数](https://github.com/tc39/ecmascript-asyncawait)。

## ES6专业开发功能

### 使用 Polyfill

#### 什么是 polyfill？

>polyfill（或 polyfiller）是一段代码（或插件），可以为你（即开发工程师）提供本希望浏览器能原生提供的技术。

polyfill 一词由 [Remy Sharp](https://twitter.com/rem) 发明 - https://remysharp.com/2010/10/08/what-is-a-polyfill

作为开发工程师，我们应该能够使用 HTML5 API 进行开发，脚本能够创建应该存在的方法和对象。这种能考虑到未来发展趋势的开发形式意味着当用户升级软件时，你的代码不用更改，用户能够迁移到更好的原生体验。 来自关于 polyfill 的 HTML5 样板文件团队 - https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills

#### 深入研究：

https://en.wikipedia.org/wiki/Polyfill

#### polyfill 示例

以下代码是新的 ES6 String 方法 startsWith() 的 polyfill：

    if (!String.prototype.startsWith) {
      String.prototype.startsWith = function (searchString, position) {
        position = position || 0;
        return this.substr(position, searchString.length) === searchString;
      };
    }

可以看出，polyfill 只是普通的 JavaScript。

这段代码是简单的 polyfill（请在 MDN 上了解它），而[此处](https://github.com/mathiasbynens/String.prototype.startsWith/blob/master/startswith.js)是更加复杂的 polyfill。

### Polyfill 的其他用途

#### Polyfills 不仅仅用来修补 JavaScript 功能
JavaScript 是用来创建 polyfill 的语言，但是 polyfill 不仅仅用来填补缺失的 JavaScript 功能！有针对各种浏览器功能的 polyfill：

SVG
Canvas
网络存储（本地存储/会话存储）
视频
HTML5 元素
无障碍功能
Web Sockets
等等！
要获得更完整的 polyfill 列表，请访问此[链接](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills)

# Promise

## Course Map

[JavaScript Promises - Jake Archibald](https://developers.google.com/web/fundamentals/primers/promises)

* Fulfilled(Resolved): It worked
* Rrjected:It didn't work
* Pending:Still waiting
* Settled:Something happened

### Web Technologies
Issues with jQuery Promises:
10 June 2016 update! [With the 3.0 release, jQuery promises now satisfy Promises/A+ compliance!](https://blog.jquery.com/2016/06/09/jquery-3-0-final-released/)
[You're Missing the Point of Promises - Domenic Denicola (Pre-jQuery 3.0)](https://blog.domenic.me/youre-missing-the-point-of-promises/)
[jQuery Deferred Broken - Valerio Gheri (Pre-jQuery 3.0)](https://thewayofcode.wordpress.com/tag/jquery-deferred-broken/)
Q Style Promises
They're an implementation of the [Promises/A+ spec](https://promisesaplus.com/).
[$q service Documentation](https://goo.gl/J1K2iv).
Browser Implementation
[Can I Use... - Promises](https://caniuse.com/#search=promises)
[ES2015 Promises Polyfill](https://github.com/jakearchibald/es6-promise)
[Q Library](https://github.com/kriskowal/q)
[Bluebird Promises](https://github.com/petkaantonov/bluebird)
APIs that Use Promises
[Service Worker API](http://www.html5rocks.com/en/tutorials/service-worker/introduction/)
[Fetch API](https://davidwalsh.name/fetch)