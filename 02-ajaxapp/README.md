# Entry point

Entry point is the first part to be called in the application.
You need to prepare entry point when making an application.

In terms of Web-application, entry point is always HTML document.
After loading HTML document by web browser, Javascripts that is called in it will be executed.

## Create project directory

ajaxapp
├── - index.html
└── - index.js

```{shell}
$ npx @js-primer/local-server
```

## Web browser and DOM(Document Object Model)

When loading HTML documents, DOM:Document Object Model is created.
JavaScript can manuplate objects of DOM.

Sample

```{javascript}
const heading = document.querySelector("h2");
const headingText = heading.textContent;

const button = document.createElement("button");
button.textContent = "Push Me";

document.body.appendChild(button);
```

---
# HTTP communication

Next, looking the implementation for calling Github API. We need to use HTTP communication to call Github API via Fetch API.

## Fetch API

Fetch API is API:Application Program Interface to get resources via HTTP comm. 

To send a request, we use `fetch` method. Github provides API for getting user info. URI is 

`https://api.github.com/user/[user id]`

```{javascript}
const userId = "[user id]";
fetch(`https://api.github.com/user/${encodeURIComponent(userId)}`);
```

## Receiving responses

`fetch` method returns `Promise` object. this Promise instance will be resolved by `Response` object as reponse of the request.
After returning the response for request, `then` callback will be called.

```{javascript}
const userId = "js-primer-example";
const fetchUserInfo = function(userId) {
  fetch(`https://api.github.com/user/${encodeURIComponent(this.userId)}`)
  .then(response => P{
    console.log(response.status); // => 200
    return response.json().then(userInfo => {
      console.log(userInfo); // => {...}
    });
  });
}

btn.addEventListner("click", {userId: userId, handleEvent: fetchUserInfo});
```

## Error handling

considering error such as network error or response error.

```{javascript}
then.((res) => {
    if (!res.ok) {
        // response error
    } else {
        // success
    }
}).catch( e => {
    // error something
})
```

---
# Displaying data

In this section, code for displaying the user information that fetched using `fetchUserInfo` is showed.

This is the template.

```
const view = `
<h4>${userInfo.name} {@${userInfo.login}}</h4>
<img src="${userInfo.avator_url}" alt="${userInfo.login}" height="100">
<dl>
  <dt>Location</dt>
  <dd>${userInfo.location}</dd>
  <dt>Repositories</dt>
  <dd>${userInfo.public_repos}</dd>
</dl>
`
```

---
# Utilizing promise  

Do refactoring utilizing `Promise` to handle error properly.

## Split functions  

- create `main` function.
  - `main` function call `fetchUserInfo`

## Error handling with `Promise`

- user Async Function
- functionize
  - `createView`: create HTML element with user info.
  - `displayView`: display HTML element created by `createView`
