# Updating Error Statuses
This example catches request errors between 400 and 599 and returns static content in its place with a 200 status.

```javascript
addEventListener('fetch', event => {
  event.respondWith(handle(event.request))
})

async function handle(request) {
  let response = await fetch(request)

  if (response.status >= 400 && response.status <= 599) {
    response = new Response('Body generation example', {
      status: 200,
      statusText: 'OK'
    })
  }

  return response
}
```
