---

copyright:
  years: 2020, 2025
lastupdated: "2025-06-19"

keywords: edge functions, CIS,

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using Edge function actions and triggers
{: #edge-functions-actions}

Edge functions consist of two main components: actions and triggers. Actions are JavaScript files that define logic to be executed at the ege. Triggers are URL-based routing rules that determine when and under what conditions those actions run. 
{: shortdesc}

Triggers link specific request patterns (like domains and paths) to actions. Without an associated trigger, an action won't impact traffic.

## Edge function actions
{: #edge-function-actions}

Actions are written in JavaScript and require an event listener to respond to a trigger event. Actions don't affect your traffic unless used by a trigger.

### Plan differences
{: #plan-differences}

Differences when working with actions depend on your plan:

**Standard plans** 

   * Allow only one action per account, automatically named after your domain (name can't be changed). 
   * To update an action, upload a new JavaScript file or edit the code directly in the editor. Uploading a new file replaces the existing action.
   * When you upload a JavaScript file, its name is always set to your domain name.

**Enterprise plans** 

   * Can upload an unlimited number of scripts, each with a unique names if wanted.
   * When creating an action, you can specify a custom name.
   * When uploading a JavaScript file, the action name is taken from the file name.

### Working with actions
{: #working-with-actions}

You can create, upload, edit, and manage actions to define the logic your Edge function runs in response to trigger events.

* **Create action** - Select **Create** to add an action by using the code editor. After you add your JavaScript code, select **Save** to create your action. 

* **Upload actions** - Select **Upload** to upload a JavaScript file. 

    Uploading or creating an action with the same name as an existing action causes the existing action to be overwritten. Rename the action file before you upload, or enter a unique name in the text input during creation to avoid this behavior.
    {: note}

* **Editing actions** - Selecting an action opens the action in the editor for modification. Whenever you save your changes, the action uploads to the Cloud edge. After updating, click **Save**. If the action is in use, the changes take effect immediately.

* **Deleting actions** - To delete an action, click the **Delete** icon in the **Actions** menu. An action can't be deleted while in use. To delete the action, remove it from the triggers first. The **Uses** column shows the number of triggers that are associated with this action. Delete can't be undone.

* **Associated triggers** - Add a trigger and associate it with an action.

## Edge function triggers
{: #edge-function-triggers}

Triggers (routes) determine how domain traffic is routed to actions. They associate URL patterns, based on a domain on the account, with a predefined action. The URL pattern must include the domain and may contain wildcards either as a prefix to the domain or at the end of the path. If no path is specified, a `/` is added implicitly. URL patterns can't contain infix wildcards or query parameters.

### Plan differences
{: #plan-differences-triggers}

There are no differences in how triggers work across plans. All plans support adding, editing, and deleting triggers.

### Working with triggers
{: #working-with-triggers}

You must add a domain before adding triggers. However, triggers can be added without having actions.

* **Adding triggers** - Go to the **Triggers** tab and click **Add trigger**. Enter a URL pattern and select an action from the list of existing actions.

    * You can also select **Avoid Edge Functions** for a trigger's path to remain active without running any Edge function action. For example, if you have an action named `my-function` assigned to `gamma.cistest-load.com/*`, but want the path `gamma.cistest-load.com/data` to avoid running `my-function`, create a separate trigger for `gamma.cistest-load.com/data` and enable **Avoid Edge Functions**. This allows the path `gamma.cistest-load.com/data` to remain active without using the action `my-function`.

* **Editing triggers** - Update a trigger by selecting the menu option in the table row for the trigger, then make changes and click **Save**.

* **Deleting triggers** Delete a trigger using the menu option in the table row for a selected trigger. This action can't be undone.
