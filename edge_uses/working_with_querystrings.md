# Working with Querystrings
Edge Functions allows for working with querystrings. Here’s an example that redirects an unauthenticated user and adds the original url to the url as a querystring.

```javascript
addEventListener('fetch', event => {
  event.respondWith(handle(event.request))
})

function parseCookies(headers) {
  const parsedCookie = {}
  if (headers.has("Cookie")) {
    for (let cookie of headers.get("Cookie").split(";")) {
      if (cookie) {
        const [ key, value ] = cookie.split("=")
        parsedCookie[key.trim()] = value.trim()
      }
    }
  }
  return parsedCookie
}

async function handle(request) {
  // Check for session-id in cookie. If present, then proceed with request

  const parsedCookies = parseCookies(request.headers);
  if (parsedCookies && parsedCookies['session-id']) {
    return fetch(request)
  }

  // URI encode the original request to be sent as redirect_url in query params

  const encodedRedirectUrl = encodeURIComponent(request.url);

  // This will cause an infinite loop in the previewer, but will work in production

  return Response.redirect(`https://www.example.com/signin?redirect_url=${encodedRedirectUrl}`, 302)
}
```
