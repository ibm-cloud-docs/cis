# Changing Origins
You can change traffic gradually from an old storage bucket to a new one with Edge Functions.

```javascript
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

function getRandomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min
}

async function handleRequest(request) {
  const BLUE_TRAFFIC_PERCENTAGE = 80
  const randomNumber = getRandomInt(1, 100)

  if (randomNumber <= BLUE_TRAFFIC_PERCENTAGE) {
    let url = new URL(request.url)
    url.host = 'blue-bucket.sfo2.digitaloceanspaces.com'
    return fetch(url, request)
  }

  return fetch(request)
}
```

You can also change origins for different regions based on request headers.

```javascript
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  const countryCode = request.headers.get("cf-ipcountry")

  if (countryCode === 'US' || countryCode === 'DE' || countryCode === 'IE' ) {
    let url = new URL(request.url)
    url.host = 'eu.example.com'
    return fetch(url, request)
  }

  return fetch(request)
}
```
