Close.io
========

A Close.io API wrapper for Node.js. See the API documentation at http://developer.close.io/

**Installation**

```npm install --save close.io```

**Usage**

```
npm install
mocha test
```

Get an API key from your settings page: https://app.close.io/settings/

```javascript
var Closeio = require('close.io');

var closeio = new Closeio("YOUR_API_KEY_HERE");

closeio.lead.create({name: "Spider Man"})
.then(function(lead){
  return closeio.lead.read(lead.id);
}).then(function(lead){
  return closeio.lead.update(lead.id, {name: "Peter Parker"});
}).then(function(lead){
  return closeio.lead.delete(lead.id);
}).then(function(){
  return closeio.lead.search({name:"Bruce Wayne"});
}).then(function(search_results){}, function(err){
  console.log("There has been an error.");
  console.log(err);
});
```

**Searching for Leads**

The `lead.search` method accepts either a string or a dictionary of search keywords as valid parameters.

To use a string to specify your search query, pass a `query` parameter to the `lead.search` method:

```javascript
closeio.lead.search({query: 'name:"Bruce Wayne" email_address:bruce@wayneenterprises.com'})
.then(function(search_results){
  console.log(search_results.total_results);
});
```

To use a dictionary of search keywords to specify your search query, structure your parameters as follows:
```javascript
closeio.lead.search({name: "Bruce Wayne", email_address: 'bruce@wayneenterprises.com'})
.then(function(search_results){
  console.log(search_results.total_results);
});
```

**Note**: The `query` parameter will override any other search keywords present in your dictionary.
