# Getting started with Vue.js

## What is Vue.js

#### Vue.js is a front end Javascript library to build modern web applications. 
#### Vue took all of the succesfull things from the other JS libraries and created their own framework around that. 
#### Features include but not limited to:

* ##### A virtual DOM with reactive components that offer the View layer only, props and a Redux-like store similar to React.
* ##### Conditional rendering, and services, similar to Angular.
* ##### Cleaner, more semantic API offerings.
* ##### Slightly better performance than React.
* ##### No use of polyfills like Polymer.


## Installation

#### There are multiple ways to install Vue, but in this guide we will focus on the Vue CLI method.
CLI stands for command line interface and the Vue CLI website has all the necessary docs on the finer details of the tool which we will not cover here. 

#### Step 1
Open up a terminal,  on the command line, paste/type the following command. 

```bash
npm install -g @vue/cli
```
_(Please note that you have to have npm installed, which we also will not cover in this guide.)_

#### Step 2

Let's create our very own Vue app by running the following command in the terminal:

```bash
vue create insert-app-name-here
```
The Vue CLI will start the process of installing your app by creating a folder in the root folder from where you ran the command. You will be prompted with a default or manual installation option. Once again refer to the official Vue CLI docs to determine what you need. 

#### Step 3

Open the above folder in your favourite code editor. 

#### Step 4
Vue CLI uses PostCSS internally, but we need to add some grunt and install these postcss plugins. There are more plugins available, but for now these will suffice. From the terminal install these...
```bash
yarn add --dev postcss-preset-env
yarn add --dev postcss-nested
```
In the package.json file, add these two lines under postcss plugins 
```json
"postcss-nested": {},
"postcss-preset-env": {},
```
It should look like this when done.
```json
"postcss": {
    "plugins": {
      "autoprefixer": {},
      "postcss-preset-env": {},
      "postcss-nested": {}
    }
  },
```

## Getting Started

Firstly, my personal preference is to change the following line of code in the **package.json** file(normally on line 6)
from
```json
"serve": "vue-cli-service serve",
```
to
```json
"dev": "vue-cli-service serve",
```

Now from the command line start up the local develop environment by running the following command:
```bash
yarn dev
```
Open up the link in your browser, normally at port 8080, and voila!!

## Basics

In your `.vue` file, you can place everything you need for your component. We can semantically create files that follow this logic:
```vue
<template>
  <div>
     <!-- Write your HTML with Vue in here -->	
  </div>
</template>

<script>
  export default {
     // Write your Vue component logic here
  }
</script>

<style scoped>
  /* Write your styles for the component in here */
</style>
```
The most basic way of importing/exporting components into a file;
```vue
import New from './components/New.vue';

export default {
  components: {
    appNew: New
  }
}
```
Lets kick off with a very basic example:
```html
<div id="app">
 {{ text }} make some lemonade.
</div>
```
-------------
```js
new Vue({
 el: '#app',
 data: {
   text: 'When life gives you lemons, '
 }
});
```
Vue.js uses an HTML-based template syntax and the most basic form of data binding is text interpolation using the “Mustache” syntax.

### Conditional Rendering and Directives
#### Some examples
##### v-for
```html
<div id="app">
  <ul>
    <li v-for="item in items">
      {{ item }}
    </li>
  </ul>
</div>
```
```js
const app4 = new Vue({
  el: '#app',
  data: {
    items: [
      'Thingamabob',
      'another thingamabob',
      'some stuff',
      'booh yah!'
    ]
  }
});
```
#### v-model
```html
<div id="app">
  <h3>Type here:</h3>
  <textarea v-model="message" class="message" rows="5" maxlength="72"></textarea><br>
  <p class="text">{{ message }} </p>
</div>
```
```js
new Vue({
  el: '#app',
  data() {
    return {
      message: 'This is a good place to type things.'  
    }
  }
});
```
Vue enables us to very easily set up two-way binding between the **textarea** and the **paragraph** with v-model.

#### More Examples

Conditional Rendering
```js
v-if, v-else-if, v-else
```
```js
<g v-if="flourish === 'A'"></g>
<g v-else-if="flourish === 'B'"></g>
<g v-else></g>
```

Bind attributes dynamically, or pass props
```js
v-bind
```
```html
<div :style="{ background: color }"></div>
```
Attaches an event listener to the element
```js
v-on
```
```html
<button @click="fnName"></button>
```
Event Handlers
We will still be using binding and listeners above to listen to DOM events, but we are going to create methods. A Vue method is a function associated with the Vue instance. Methods are defined inside the **methods** property. Methods are especially useful when you need to perform an action and you attach a **v-on** directive on an element to handle events.
```js
new Vue({
  el: '#app',
  data() {
   return {
    counter: 0
   }
  },
  methods: {
   increment() {
     this.counter++;
   }
  }
});
```
```html
<div id="app">
  <p><button @click="increment">+</button> {{ counter }}</p>
</div>
```
 Dynamic style bindings
 ```js
 new Vue({
  el: '#app',
  data() {
    return {
      counter: 0,
      x: 0
    }
  },
  methods: {
    increment() {
      this.counter++;
   },
   decrement() {
     this.counter--;
   },
   xCoordinate(e) {
     this.x = e.clientX;
   }
  }
});
```
```html
<div id="app" :style="{ backgroundColor: `hsl(${x}, 80%, 50%)` }" @mousemove="xCoordinate">
  <p><button @click="increment">+</button> {{ counter }} <button @click="decrement">-</button></p>
  <p>Pixels across: {{ x }}</p>
</div>
```
We didn't even need to pass in the event to the @mousemove handler, Vue will automatically pass it for you to be available as a parameter for the method. 

### Let's Continue
#### Basic Routing without VueRouter

The Vue documentation suggest to use the officially-supported <a href="https://github.com/vuejs/vue-router">Vue Router Libary</a> for most SPA's, but since this is a getting started guide, we will explore the most basic form of routing in Vue.js. 

#### What is routing?

Routing is a critical feature in a SPA which allows navigation between "pages" within the application, by dynamically rendering page-level components. 

#### Setup
Firstly, we create a **routes.js** file in the root of the app. 
Then we can go ahead and create our "pages" also in the root of the app folder nl:
* HomePage.vue
* AboutPage.vue

Inside the **routes.js** file we will import these two "pages" and,
```js
import HomePage from "./HomePage";
import AboutPage from "./AboutPage";
```
declare the route to each "page" inside a variable
```js
const routes = {
  "/": HomePage,
  "/about": AboutPage
};
```
And then locally registering the component using: 
```js
export default {}
```
Calling the data function and returning the path and filename of the current page in javascript as an object. 
```js
export default {
  data() {
    return { current: window.location.pathname };
  }
};
```
We then use a computed property for complex logic and create a function which returns the current path;
```js
export default {
  data() {
    return { current: window.location.pathname };
  },
  computed: {
    routedComponent() {
      return routes[this.current];
    }
  },
};
```
Lasty, we call the render function, which will return a virtual DOM node;
```js
export default {
  data() {
    return { current: window.location.pathname };
  },
  computed: {
    routedComponent() {
      return routes[this.current];
    }
  },
  render(createElement) {
    return createElement(this.routedComponent);
  }
};
```
In our root app, normally App.vue we will import the newly created routes;
```js
<script>
import routes from "./routes";

export default {
  components: {
    routes
  }
};
</script>
```
```html
<template>
  <div id="app">
    <routes />
  </div>
</template>
```
Lasty we are going to create some navigation buttons to link between our "pages". For this we will need to create a method which will handle our click event right below our components;
```js
export default {
  components: {
    routes
  },
  methods: {
    goTo(routes) {
      window.location = routes;
    }
  }
};
```
```html
<template>
  <div id="app">
    <button @click="goTo('/')">Home</button>
    <button @click="goTo('/about')">About</button>
    <routes />
  </div>
</template>
```
## Vue State Management

Vuex is vue’s own state management pattern and library. State is the data your components depend on. As your app grows each component might have its own version of state. If one component changes state and a distant relative uses the same state, that change needs to be communicated. Default way is to communicate events up and passing down props to share data. That can become overly complicated. VueX consolidates all state into one place. One location that contains the state of the whole application.

Its implementation includes a store, custom mutators and it will reactively update any components that are reading data from the store.

### Basic example of App state and props

Lets create a new vue component called child.vue and pass it props in the form of a counter which we will update from the parent component.
```html
<template>
  <div class="child-item">
    <div class="num">{{ count }}</div>
  </div>
</template>
```
```js
<script>
export default {
  props: {
    count: {
      type: Number,
      required: true
    }
  }
};
</script>
```
In our parent component we import our child component,
```js
<script>
import child from "./components/child";

export default {
  components: {
    child
  }
};
</script>
```
We can then pass the count prop we created in the child as data in the parent. 
```js
<script>
import child from "./components/child";

export default {
  components: {
    child
  },
  data() {
    return {
      count: 0
    };
  },
};
</script>
```
Now lets build our increment and decrement functions as methods to show how the count integer can be updated with state, as well as the actual buttons with html.
```js
<script>
import child from "./components/child";

export default {
  components: {
    child
  },
  data() {
    return {
      count: 0
    };
  },
  methods: {
    increment() {
      this.count++;
    },
    decrement() {
      this.count--;
    }
  }
};
</script>
```
```html
<template>
  <div class="parent-component">
    <h1>This is the Parent Component</h1>
    <h3>
      <button @click="decrement">-</button>
      Adjust the state
      <button @click="increment">+</button>
    </h3>
    <h2>
      This is the app state
      <span class="num">{{ count }}</span>
    </h2>
    <hr />
    <h4>
      <child count="1"></child>
    </h4>
    <p>This child uses a static integer as props</p>
    <hr />
    <h4>
      <child :count="count"></child>
    </h4>
    <p>This is the same child that uses state as props</p>
  </div>
</template>
```
And thats it for now. Vue is a incredible lightweigth and powerfull js framework. Keep an eye out for future updates on more advanced topics. 
