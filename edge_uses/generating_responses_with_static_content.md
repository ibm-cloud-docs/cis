# Generating Responses with Static Content
Edge Functions allow you to generate responses with static content and gzip your response without any external libraries.

```javascript
addEventListener('fetch', event => {
  event.respondWith(handle(event.request))
})

let content = `
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Simple Edge Functions Static Content Response</title>
  </head>
  <body>
    <p>Hello from Edge Functions!</p>
  </body>
</html>
`;

async function handle(request) {

  return new Response(content, {
    status: 200,
    statusText: "OK",
    headers: {
      'cache-control': "max-age=100",
      'content-type': "text/html; charset=utf-8",
      'content-encoding': "gzip"
    }
  })
}
```
