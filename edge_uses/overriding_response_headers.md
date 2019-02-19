# Overriding Response Headers
This example shows how you can override response headers in Edge Functions.

```javascript
addEventListener('fetch', event => {
  event.respondWith(handle(event.request))
})

async function handle(request) {
  let response = await fetch(request)
  response = new Response(response.body, response)

  const headerNameSrc = 'Orig-Header'
  const headerNameDst = 'Last-Modified'

  if (response.headers.has(headerNameSrc)) {
    response.headers.set(headerNameDst, response.headers.get(headerNameSrc))
    console.log(`Response header "${headerNameDst}" was set to "${response.headers.get(headerNameDst)}"`)
  }

  return response
}
```
