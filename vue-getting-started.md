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
Vue CLI uses PostCSS internally, but we need to add some bells and whistles.
```bash
yarn add --dev postcss-preset-env
yarn add --dev postcss-nested
```
In the package .json file, add these under postcss plugins
```json
"postcss-nested": {},

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

Lets kick off with a very basic example:
```html
<div id="app">
 {{ text }} Nice to meet Vue.
</div>
```
-------------
```js
new Vue({
 el: '#app',
 data: {
   text: 'Hello World!'
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
      'thingie',
      'another thingie',
      'lots of stuff',
      'yadda yadda'
    ]
  }
});
```
#### v-model
```html
<div id="app">
  <h3>Type here:</h3>
  <textarea v-model="message" class="message" rows="5" maxlength="72"></textarea><br>
  <p class="booktext">{{ message }} </p>
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
We will still be using binding and listeners above to listen to DOM events, but we are going to create methods. In vue they are called methods. 
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
