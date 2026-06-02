---

copyright:
  years: 2023, 2026
lastupdated: "2026-06-02"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Altering headers
{: #altering-headers}

This example illustrates how to add, change, or delete headers sent in a request or returned in a response.
{: shortdesc}

You can't modify the value of certain headers, such as `server`, `eh-cache-tag`, or `eh-cdn-cache-control`.
{: note}

```js
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  const response = await fetch(request)
  
  // Clone the response so that it's no longer immutable
  const newResponse = new Response(response.body, response)
  
  // Add a custom header with a value
  newResponse.headers.append("X-CIS-Functions-Hello", "Hello from CIS Workers")
  
  // Delete headers
  newResponse.headers.delete("x-header-to-delete")
  newResponse.headers.delete("x-header2-to-delete")
  
  // Adjust the value for an existing header
  newResponse.headers.set("x-header-to-change", "NewValue")
  
  return newResponse
}
```
{: codeblock}
