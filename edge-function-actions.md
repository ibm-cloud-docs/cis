---

copyright:
  years: 2020, 2025
lastupdated: "2025-07-03"

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

You can create, upload, edit, and manage actions to define the logic your Edge function runs in response to trigger events.

* **Creating an action** - Click **Create** to add an action by using the code editor. After you add your JavaScript code, click **Save** to create your action. 

* **Uploading an action** - Click **Upload** to upload a JavaScript file. 

    Uploading or creating an action with the same name as an existing action causes the existing action to be overwritten. Rename the action file before you upload, or enter a unique name in the text input during creation to avoid this behavior.
    {: note}

* **Editing an action** - Selecting an action opens the action in the editor for modification. Make your changes and click **Save**. When you save your changes, the action uploads to the Cloud edge. If the action is in use, the changes take effect immediately.

* **Deleting an action** - Click the Delete icon in the table row for the selected action. An action can't be deleted while in use. To delete the action, remove it from the triggers first. The **Uses** column shows the number of triggers that are associated with this action. Delete can't be undone.

* **Associating a trigger** - Add a trigger and associate it with an action.

## Edge function triggers
{: #edge-function-triggers}

Triggers (routes) determine how domain traffic is routed to actions. They associate URL patterns, based on a domain on the account, with a predefined action. The URL pattern must include the domain and may contain wildcards either as a prefix to the domain or at the end of the path. If no path is specified, a `/` is added implicitly. URL patterns can't contain infix wildcards or query parameters.

### Plan differences
{: #plan-differences-triggers}

There are no differences in how triggers work across plans. All plans support adding, editing, and deleting triggers.

### Working with triggers
{: #working-with-triggers}

You must add a domain before adding triggers. However, triggers can be added without having actions.

* **Adding a trigger** - Go to the **Triggers** tab and click **Add trigger**. Enter a URL pattern and select an action from the list of existing actions.

   To keep a trigger path active without running an Edge function, enable **Avoid edge functions**. For example, if `my-function` is assigned to `gamma.cistest-load.com/*`, but you want `gamma.cistest-load.com/data` to bypass it, create a separate trigger for `/data` and enable **Avoid edge functions**. This ensures the `/data` path stays active without invoking `my-function`.

* **Editing a trigger** - Click the **Edit icon** ![Edit icon](../icons/edit-tagging.svg "Edit") in the table row for the selected trigger, then make changes and click **Save**.

* **Deleting a trigger** - Click the **Delete icon** ![Delete icon](../icons/delete.svg "Delete") in the table row for the selected trigger. This action can't be undone.

## Related links
{: #related-links-edge-functions}

* [How Edge functions work](/docs/cis?topic=cis-working-with-edge-functions)
* [Edge function examples](/docs/cis?group=edge-function-examples)
