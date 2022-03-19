---
sidebar_label: 'vercel.json'
sidebar_position: 6
---
# vercel.json

### Array Properties
#### 1. rewrites

```
"rewrites:[
    {"source": "/route", "destination": "url"}
]"
```

A rewrite is a server side routing where the page is directed to a new route but the original URL does not change.


#### 2. redirects
```
"redirects:[
    {"source": "/route", "destination": "url", "permanent": false}
]"
```

A redirect is the opposite of rewrite where it is client sided routing and changes the original URL to its destination.


##### "source"
The source is simply a route that the website will be directed to.

##### "destination"
The destination refers to the url that the specific route should be directed to.

##### "permanent"
The permanent value is optional but a permanent value means that the new redirect target will be shown in the search results.

### How to make a new rewrite/redirect route
Check the [FAQ](https://tamudatathon.com/docs/galaxy/FAQ) page.
