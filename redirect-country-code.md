---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-31"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Redirecting country code response
{: #redirect-country-code}

This example illustrates how to redirect a response based on the country code in the header of a visitor.
{: shortdesc}

```js
export default {
	async fetch(request) {
		/**
		 * A map of the URLs to redirect to
		 * @param {Object} countryMap
		 */
		const countryMap = {
			US: "https://example.com/us",
			EU: "https://example.com/eu",
		};

		// Use the cf object to obtain the country of the request
		// more on the cf object: https://developers.cloudflare.com/workers/runtime-apis/request#incomingrequestcfproperties
		const country = request.cf.country;

		if (country != null && country in countryMap) {
			const url = countryMap[country];
			// Remove this logging statement from your final output.
			console.log(
				`Based on ${country}-based request, your user would go to ${url}.`,
			);
			return Response.redirect(url);
		} else {
			return fetch("https://example.com", request);
		}
	},
};
```
