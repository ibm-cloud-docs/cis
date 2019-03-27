---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: edge functions beta, edge functions

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Edge Functions (Beta)
{: #edge-functions}

CIS Edge Functions allow you to create new applications or modify existing applications, without having to configure or maintain infrastructure, by utilizing a serverless execution environment. Edge Functions can be defined and uploaded to the Cloud edge to process requests before they reach the origin. CIS Edge functions can be used to modify HTTP requests and responses, make parallel requests, or generate responses from the Cloud edge.

## How Edge Functions work
{: #how-edge-functions-work}

Edge Functions associates **actions** with URIs based on a defined domain. This association is called a **trigger**. Incoming requests to your site will be intercepted at the cloud's edge and matched against the triggers in your account or domain. If the request URL matches the trigger's URI the action associated with the trigger is executed. 

Edge functions are modeled on the [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) available in modern web browsers, and use the same API whenever possible.

The Service Worker API allows you to intercept any request which is made to your site. Once your JavaScript is handling the request, you may elect to make any number of subrequests to your site or others, and finally return any response you would like to your visitor.

Unlike standard Service Workers, Edge Functions run on CIS edge servers, not in the user’s browser. That means you can trust that your code will run in a trusted environment where it cannot be bypassed by malicious clients. It also means that the user does not need to be using a modern browser that supports Service Workers – you can even intercept requests from API clients that aren't browsers at all.

Internally, Edge Functions use the same V8 JavaScript engine which is used in the Google Chrome browser to run workers on our infrastructure. V8 dynamically compiles your JavaScript code into ultra-fast machine code, making it very performant. This makes it possible for your code to execute in microseconds, and for our edge to execute many thousands of scripts per second.

While Edge Functions does use V8, it does not use Node.js. The JavaScript APIs available to you inside workers are implemented by us directly. Working with V8 directly allows the code to run more efficiently and with the security controls needed to keep the customers and the infrastructure safe.


## Actions
{: #edge-functions-actions}

Actions are written in JavaScript and require an event listener to respond to a trigger event. Actions will not affect your traffic unless used by a trigger. 

### Enterprise vs Standard Plans
{:#edge-functions-enterprise-v-standard-plans}

Standard plans have a maximum of one action. The action is assigned a name that is the same as your domain. You may replace your action by uploading another file or update your action using the code editor. Uploading another file will remove the existing action.

Enterprise plans can upload an unlimited number of scripts. These can be given unique names.

### Create actions
{: #edge-functions-create-actions}

Select **Create** to add an action using the code editor. On Enterprise plans enter a name for your action. On Standard plans the name is not editable and is set to the name of your domain. After adding your Javascript code, select **Save** to create your action. 

### Upload actions
{: #edge-functions-upload-actions}

Use the **Upload** button to upload a Javascript file. On Enterprise plans the name of the action is the name of the file. On Standard plans the action name is set to the name of your domain.

Uploading or creating an action with the same name as an existing action will cause the existing action to be overwritten. Rename the action file before uploading or enter a unique name in the text input while creating to avoid this behavior.
{:note}

### Edit actions
{: #edge-functions-edit-actions}

Selecting an action opens the action in the editor for modification. Whenever you save your changes the action will upload to the cloud's edge. After updating select **Save**. If the action is in use, the changes will take effect immediately. 

### Delete actions
{: #edge-functions-delete-actions}

Delete an action by clicking the **delete** icon in the **Actions** table. An action cannot be deleted while in use. To delete the action, remove it from the triggers, first. The **Uses** column shows the number of triggers that are associated with this action. Delete cannot be undone.


### Associated Triggers
{: #edge-functions-associated-triggers}

Add a trigger and associate it with an action.

### Edge Functions Known Limitations
{: #edge-functions-known-limitations}

Uploading an action with the same name as an existing action. The existing action will be overwritten. Rename the action file before uploading to avoid this behavior.


## Triggers
{: #triggers}

### About Triggers
{: #about-triggers}

Triggers (routes) determine domain traffic routing to the Actions. Triggers associate certain URL patterns, based on a domain on the account, with a predefined action. The URL must contain the domain, but it can contain wildcards either as a prefix to the domain or at the end of the path. If no path is given on the pattern a `/` is added implicitly. The URL pattern cannot contain infix wildcards or query parameters. 

You must add a domain to add triggers. You may add triggers without having actions.

### Add triggers
{: #add-triggers}

Go to the **Triggers** tab and click **Add trigger**. Enter a URL pattern and select an action from the list of existing actions. 

For an action you can also select **Avoid Edge Functions**. This allows the trigger's path to remain active but avoid using any Edge Function actions. For example, there is an action called `my-function` and a trigger with the path `beta.cistest-load.com/*`. If the path `beta.cistest-load.com/data` should not use the action `my-function` create another trigger with the path `beta.cistest-load.com/data` and the option **Avoid Edge Functions**. This allows the path `beta.cistest-load.com/data` to remain active without using the action `my-function`.

### Edit triggers
{: #edit-triggers}

Update a trigger using the menu option in the table row for a selected trigger. After updating select **Save**.

### Delete triggers
{: #delete-triggers}

Delete a trigger using the menu option in the table row for a selected trigger. This action cannot be undone.


## Use Cases
{: #edge-functions-use-cases-examples}

These examples are for demonstration purposes only, and not intended for use in production. 
{:important}
* [A/B Testing](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#ab-testing)
* [Adding a Response Header](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#add-response-header)
* [Aggregating Multiple Requests](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#aggregate-multiple-requests)
* [Conditional Routing](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#conditional-routing)
* [Hot-link Protection](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#hot-link-protection)
* [Originless Responses](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#originless-responses)
* [Post Requests](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#post-requests)
* [Setting a Cookie](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#setting-cookies)
* [Signed Requests](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#signed-requests)
* [Streaming Responses](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#streaming-responses)
