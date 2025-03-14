---

copyright:
  years: 2023, 2025
lastupdated: "2025-02-24"

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
export default {
	async fetch(request) {
		const response = await fetch("https://example.com");

		// Clone the response so that it's no longer immutable
		const newResponse = new Response(response.body, response);

		// Add a custom header with a value
		newResponse.headers.append(
			"x-workers-hello",
			"Hello from Cloudflare Workers",
		);

		// Delete headers
		newResponse.headers.delete("x-header-to-delete");
		newResponse.headers.delete("x-header2-to-delete");

		// Adjust the value for an existing header
		newResponse.headers.set("x-header-to-change", "NewValue");

		return newResponse;
	},
};
```
{: codeblock}
