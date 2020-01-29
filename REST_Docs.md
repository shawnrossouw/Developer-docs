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
http://www.mysite.com/contact.html?key=value
` 

"&" to add another value.

Example
```
Key = Value
name = shawn
make = honda
```

In Javascript you would write a function that would GET_the_url_parameters and return the value. 

In php you would GET the url parameter like this: 
```php
$_GET['project']
```
#### Forms

In html we can use the form as an example. The default method for form is GET. If a form does not have a action set it will append the form data as a url parameter and the reload the page. In the example below the form submit button would go to the about page and append the form data as url parameter. 
```html
<form method="GET" action="about.html">
  
</form>
```

Using POST instead of GET above the browser will still redirect to the about page but the data wont be appended as a url parameter but as an POST object/form payload. Its more secure as the data cant be intercepted. 

#### Form Inputs

Basic type inputs. Needs two required attributes i.e name="" and type="". Value is recorded by the user and can be used a default value. Placeholder is the ghost value that populates the field. The default state of a field is blurred. The focus state is when the user clicks in the field. Text area which has formatting is a WYSISWYG text area. Text area without formatting is a plain text area. Label tags is mainly used for screen readers. If label and inputs is used correctly, the input field will be focussed when the user clicks on the label. 

```html
<form>
  <input type="text/password/email/submit" name="First Name" value="default value"  />

  <textarea name="message"> 

  </textarea>

  <select name="Key">
    <option value="Value">
  </select>
  
  <label for="name of input"> First Name
    <input name="" />
  </label>
</form>

```


#### Github API Example.

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
