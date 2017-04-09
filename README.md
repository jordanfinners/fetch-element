# \<fetch-element\>

Element for interacting with the fetch api and queuing requests up if working offline 

[![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg)](https://www.webcomponents.org/element/jordanfinners/fetch-element)

## Installation

`bower install fetch-offline-element --save`

## Usage

Include the element in your element/html page.
```
<link rel="import" href="../bower_components/fetch-element/fetch-element.html">
```
Add to your html
```
<fetch-element id="request"></fetch-element>
```

In you're javascript you can interact with it like so
```
let req = new Request('url', {method: 'POST', body: body})
    this.$.request.fetch(req)
        .then(function (response) {
            if (response.status === 202){
                ///handle offline by returning body
                return body
            }
            ///otherwise returns a data stream, converting it to json
            return response.json()
          })
          .then(function(stuff){
            console.log(stuff)
          })
```

Pass the fetch element a request object, created using the [Request constructor](https://developer.mozilla.org/en-US/docs/Web/API/Request)

If you are offline, the element will add the request to the queue stored in the local cache and return you a 202 where you can then handle being offline

If you are online, the element will flush the cache in order which the were sent and then make a fetch request and return a promise, with a [response object](https://developer.mozilla.org/en-US/docs/Web/API/Response)

Cavet the [fetch api](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) doesn't reject the promise if a 404 or 500 is returned from the server.

## Contributing

1. Fork it
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :)
