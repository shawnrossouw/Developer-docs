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

