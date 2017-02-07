# Backend Starter Kit (Beta)

:truck: A boilerplate for :star2: Node.js :star2:, Express, Mongoose, Heroku, mLab, Nodemon, PM2, and Babel.

[![Build Status](https://travis-ci.org/Shyam-Chen/Backend-Starter-Kit.svg?branch=master)](https://travis-ci.org/Shyam-Chen/Backend-Starter-Kit)
 //
[![Dependency Status](https://david-dm.org/Shyam-Chen/Backend-Starter-Kit.svg)](https://david-dm.org/Shyam-Chen/Backend-Starter-Kit)
[![devDependency Status](https://david-dm.org/Shyam-Chen/Backend-Starter-Kit/dev-status.svg)](https://david-dm.org/Shyam-Chen/Backend-Starter-Kit?type=dev)

[Live Demo](https://expressmongoose-live-demo.herokuapp.com/)

This seed repository provides the following features:
* ---------- **Primary Key** ----------
* [x] Server-side platform with [**Node**](https://nodejs.org/en/).
* [x] Application framework with [**Express**](http://expressjs.com/).
* [x] Dadabase object modeling with [**Mongoose**](http://mongoosejs.com/).
* [x] Application cloud hosting with [**Heroku**](https://www.heroku.com/).
* [x] Dadabase cloud hosting with [**mLab**](https://mlab.com/).
* ---------- **Secondary Key** ----------
* [x] Utility functions with [**Lodash**](https://lodash.com/).
* [x] Reactive extensions with [**ReactiveX**](http://reactivex.io/).
* [x] State container with [**Redux**](http://redux.js.org/).
* [x] Immutable collections with [**Immutable**](http://facebook.github.io/immutable-js/).
* ---------- **Dev Tools** ----------
* [x] Automatically restart with [**Nodemon**](https://github.com/remy/nodemon).
* [x] Next generation JavaScript with [**Babel**](https://github.com/babel/babel).
* ---------- **Test Tools** ----------
* [x] Static code analyzer with [**ESLint**](https://github.com/eslint/eslint).
* [x] Test framework with [**Mocha**](https://github.com/mochajs/mocha).
* [x] Assertion library with [**Chai**](https://github.com/chaijs/chai).
* [x] Test spies with [**Sinon**](https://github.com/sinonjs/sinon).
* ---------- **Environment** ----------
* [x] Operating system with [**Linux**](https://github.com/torvalds/linux).
* [x] Text editor with [**Atom**](https://github.com/atom/atom).
* [x] Keeping application alive with [**PM2**](https://github.com/Unitech/pm2).
* [ ] Serving static resources with [**Nginx**](https://github.com/nginx/nginx).
* [ ] HTTP caching with [**Varnish**](https://github.com/varnishcache/varnish-cache).
* [x] Version control with [**Git**](https://github.com/git/git).
* [x] Fast and deterministic builds with [**Yarn**](https://github.com/yarnpkg/yarn).
* [ ] Software container with [**Docker**](https://github.com/docker/docker).
* [ ] Continuous integration with [**Travis**](https://github.com/travis-ci/travis-ci).

## Getting Started

1) Clone this Boilerplate
```bash
$ git clone --depth 1 https://github.com/Shyam-Chen/Backend-Starter-Kit.git <PROJECT_NAME>
$ cd <PROJECT_NAME>
```

2) Install Dependencies
```bash
$ yarn install
```

3) Run the Application
```bash
$ yarn start
```

## Using Docker

1) Build the Image
```bash
$ docker build -t Backend-Starter-Kit .
```

2) Run the Container
```bash
$ docker run -it -p 8000:8000 --name app Backend-Starter-Kit
```

3) Just Compose
```bash
$ docker-compose up
```

## Using Libraries

1) Example of Lodash
```js
import { Observable } from 'rxjs/Observable';
import { of } from 'rxjs/observable/of';
import { lowerFirst } from 'lodash';

Observable::of(lowerFirst('Hello'), lowerFirst('World'))
  .subscribe(result => console.log(result));
  // hello
  // world
```

2) Example of ReactiveX
```js
import { Observable } from 'rxjs/Observable';
import { timer } from 'rxjs/observable/timer';
import { of } from 'rxjs/observable/of';
import { mapTo } from 'rxjs/operator/mapTo';
import { combineAll } from 'rxjs/operator/combineAll';

Observable::timer(2000)
  ::mapTo(Observable::of('Hello', 'World'))
  ::combineAll()
  .subscribe(result => console.log(result));
  // ["Hello"]
  // ["World"]
```

3) Example of Redux
```js
import { filter } from 'rxjs/operator/filter';
import { map } from 'rxjs/operator/map';
import { combineReducers, createStore, applyMiddleware } from 'redux';
import { combineEpics, createEpicMiddleware } from 'redux-observable';

// Types
const INCREMENT = 'INCREMENT';
const DECREMENT = 'DECREMENT';
const RESET = 'RESET';
const INCREMENT_IF_ODD = 'INCREMENT_IF_ODD';
const DECREMENT_IF_EVEN = 'DECREMENT_IF_EVEN';

// Reducers
const counterReducer = (state = 0, action) => {
  switch (action.type) {
    case INCREMENT:
      return state + 1;
    case DECREMENT:
      return state - 1;
    case RESET:
      return 0;
    default:
      return state;
  }
};

// Actions
const increment = () => ({ type: INCREMENT });
const decrement = () => ({ type: DECREMENT });
const reset = () => ({ type: RESET });
const incrementIfOdd = () => ({ type: INCREMENT_IF_ODD });
const decrementIfEven = () => ({ type: DECREMENT_IF_EVEN });

// Epics
const incrementIfOddEpic = (action$, store) =>
  action$.ofType(INCREMENT_IF_ODD)
    ::filter(() => store.getState().counterReducer % 2 === 1)
    ::map(increment);

const decrementIfEvenEpic = (action$, store) =>
  action$.ofType(DECREMENT_IF_EVEN)
    ::filter(() => store.getState().counterReducer % 2 === 0)
    ::map(decrement);

const rootEpic = combineEpics(incrementIfOddEpic, decrementIfEvenEpic);
const epicMiddleware = createEpicMiddleware(rootEpic);

// Store
const rootReducer = combineReducers({ counterReducer });
const store = createStore(rootReducer, applyMiddleware(epicMiddleware));

store.subscribe(() => {
  const { counterReducer } = store.getState();
  console.log(counterReducer);
});

store.dispatch(increment());
// 1

store.dispatch(incrementIfOdd());
// 1
// 2

store.dispatch(decrementIfEven());
// 2
// 1

store.dispatch(reset());
// 0

store.dispatch(decrement());
// -1
```

4) Example of Immutable
```js
import { Observable } from 'rxjs/Observable';
import { from } from 'rxjs/observable/from';
import { Map } from 'immutable';

const map1 = Map({ a: 1, b: 2, c: 3 });
const map2 = map1.set('b', 4);

Observable::from(map2)
  .subscribe(val => console.log(val));
  // ["a", 1]
  // ["b", 4]
  // ["c", 3]
```

## Other Commands

```bash
$ yarn run dev
$ yarn run test
$ yarn run prod

$ yarn run clean
$ yarn run reset
$ yarn run reinstall
```

## Directory Structure

```
.
├── scripts
│   └── build|deploy|install|test.sh
├── src
│   ├── ctrls
│   │   └── ...
│   ├── models
│   │   └── ...
│   ├── routes
│   │   └── ...
│   ├── utils
│   │   └── ...
│   └── index.js
├── test
│   └── ...
└── package.json
```
