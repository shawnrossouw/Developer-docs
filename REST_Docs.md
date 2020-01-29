### REST API docs

### Introduction

Browser communicates with the server via http/https/ftp/ssh etc requests. Browser creates a GET request via http to the server. 

Other requests include:
- POST
- DELETE
- PUT

#### GET
To fetch/retrieve data from the server. 
On a website to retrieve the actual page. Like clicking a link to another page.

#### POST
To send data to the server to store, for example in a database. 
To send data through use of a form, login or ajax.

#### DELETE
Tp delete a record on a server or to delete a file. 

#### PUT
Is similar to POST but convention is to save an attachment. 

#### URL Parameters

Append information/data on the url via a "Key value pair". Example:
`
http://www.mysite.com/contact?key=value
` 

"&" to add another value.

Example
```
Key = Value
name = shawn
make = honda
```



Example HTML
```html
<a href="https://github.com/shawnrossouw" class="card">
  <img src="" class="image"></img>
  <div class="name"></div>
  <div class="company"></div>
  <div class="blog"></div>
  <div class="bio"></div>
</a>
```
JS promises is a way to use data from a request before it arrives.

A promise receives 2 arguments which are functions, i.e resolve and reject.

```js
let name = 'user';

function render(user){
  document.querySelector('.image').src = user.avatar_url;
  document.querySelector('.name').innerHTML = user.name;
  document.querySelector('.company').innerHTML = user.company;
  document.querySelector('.bio').innerHTML = user.bio;
  document.querySelector('.blog').innerHTML = user.blog;
}

fetch('https://api.github.com/users/shawnrossouw')
  .then(req => req.json())
  .then(data => {
  console.log(data);
  render(data);
})
```
