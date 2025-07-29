---

copyright:
  years: 2020, 2025
lastupdated: "2025-07-29"

keywords: edge functions

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using Edge function actions and triggers
{: #edge-functions-actions}

Edge functions consist of two main components: actions and triggers. Actions are JavaScript files that define logic to be run at the edge. Triggers are routing rules based on URLs that define when and under what circumstances those actions should run. Triggers connect specific request patterns (like domains and paths) to the appropriate actions. Without an associated trigger, an action won't impact traffic.
{: shortdesc}

## Edge function actions
{: #edge-function-actions}

Actions are written in JavaScript and require an event listener to respond to a trigger event. Actions don't affect your traffic unless used by a trigger.

### Plan differences
{: #plan-differences}

Differences when working with actions depend on your plan:

#### Standard plans
{: #standard-plans}

   * Allow only one action per account, automatically named after your domain (name can't be changed).
   * To update an action, upload a new JavaScript file or edit the code directly in the editor. Uploading a new file replaces the existing action.
   * When you upload a JavaScript file, its name is always set to your domain name.

#### Enterprise plans
{: #enterprise-plans}

   * Can upload an unlimited number of scripts, each with a unique names if wanted.
   * When creating an action, you can specify a custom name.
   * When uploading a JavaScript file, the action name is taken from the file name.

### Working with actions
{: #working-with-actions}

You can create, upload, edit, and manage actions to define the logic your Edge function runs in response to trigger events. The console provides tools for each of the core operations:

* **Creating an action** - Click **Create** to add an action by using the built-in code editor. After you add your JavaScript code, click **Save** to create your action.
* **Reading an action** - Click on an existing action from the actions table to open it in the editor. This allows you to view its code without making changes.
* **Updating an action** - To modify an action, open it in the editor by clicking on it in the list. Make your changes, then click Save. When you save your changes, the updated action is uploaded to the Cloud edge. If the action is in use, the updates take effect immediately.
* **Uploading an action** - Click **Upload** to upload a JavaScript file. Uploading or creating an action with the same name as an existing action causes the existing action to be overwritten. Rename the action file before uploading, or enter a unique name during creation to avoid this behavior.

   Uploading can also be used as part of creating or updating an action, depending on whether the name already exists.

* **Deleting an action** - To delete an action, click the Delete icon (trash can) in the table row for the selected action. An action can't be deleted while it’s associated with a trigger. To delete the action, you must first remove all triggers that use it. The **Uses** column shows how many triggers are linked to each action.
* **Associating a trigger** - Triggers are required for an action to run. Add a trigger from the **Triggers** tab and select the action from the list of existing actions. The **Uses** column in the actions table displays the number of triggers currently linked to each action.

## Edge function triggers
{: #edge-function-triggers}

Triggers (routes) determine how domain traffic is routed to actions. They associate URL patterns, based on a domain on the account, with a predefined action. The URL pattern must include the domain and may contain wildcards either as a prefix to the domain or at the end of the path. If no path is specified, a `/` is added implicitly. URL patterns can't contain infix wildcards or query parameters.

### Plan differences
{: #plan-differences-triggers}

There are no differences in how triggers work across plans. All plans support adding, editing, and deleting triggers.

### Working with triggers
{: #working-with-triggers}

You must add a domain before adding triggers. Triggers define how traffic is routed to your Edge function actions. A trigger connects a URL pattern with an existing action.

Triggers can be created even if no actions exist yet, but they will not invoke any logic until an action is selected.
{: note}

* **Adding a trigger** - Go to the **Triggers** tab and click **Add trigger**. Enter a URL pattern, then select an action from the list of existing actions to associate with this pattern. This establishes the link between a route and an action.

   To keep a trigger path active without running an Edge function, enable **Avoid edge functions**. For example, if `my-function` is assigned to `gamma.cistest-load.com/*`, but you want `gamma.cistest-load.com/data` to bypass it, create a separate trigger for `/data` and enable **Avoid edge functions**. This ensures the `/data` path remains active without invoking `my-function`.

* **Editing a trigger** - Click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit") in the table row of the trigger that you want to modify, then make changes and click **Save**.
* **Deleting a trigger** - Click the **Delete** icon ![Delete icon](../icons/delete.svg "Delete") in the table row of the trigger that you want to modify. This action can't be undone. Deleting a trigger removes the association between the route and the action.

## Related links
{: #related-links-edge-functions}

* [How Edge functions work](/docs/cis?topic=cis-working-with-edge-functions)
* [Edge function examples](/docs/cis?group=examples)
