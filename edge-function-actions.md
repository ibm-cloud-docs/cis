---

copyright:
  years: 2020, 2024
lastupdated: "2024-07-17"

keywords: edge functions, CIS,

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Working with Edge functions actions
{: #edge-functions-actions}

Actions are written in JavaScript and require an event listener to respond to a trigger event. Actions do not effect your traffic unless used by a trigger. 
{: shortdesc}

* **Standard plans** Have a maximum of one action. The action is assigned a name that is the same as your domain. You can replace your action by uploading another file, or update your action by using the code editor. Uploading another file removes the existing action.
* **Enterprise plans** Can upload an unlimited number of scripts. These scripts can be given unique names.

* **Create action** Select **Create** to add an action by using the code editor. After you add your JavaScript code, select **Save** to create your action.
    * **Standard plans** The name is not editable and is set to the name of your domain.
    * **Enterprise plans** Enter a name for your action.

* **Upload actions** Use the **Upload** button to upload a JavaScript file.
    * **Standard plans** The action name is set to the name of your domain.
    * **Enterprise plans** The name of the action is the name of the file.

    Uploading or creating an action with the same name as an existing action causes the existing action to be overwritten. Rename the action file before you upload, or enter a unique name in the text input during creation to avoid this behavior.
    {: note}

* **Editing actions** Selecting an action opens the action in the editor for modification. Whenever you save your changes, the action uploads to the Cloud edge. After updating, select **Save**. If the action is in use, the changes take effect immediately.

* **Deleting actions** To delete an action, click the **Delete** icon in the **Actions** table. An action cannot be deleted while in use. To delete the action, remove it from the triggers first. The **Uses** column shows the number of triggers that are associated with this action. Delete cannot be undone.

* **Associated triggers** Add a trigger and associate it with an action.

## Working with triggers
{: #triggers}

Triggers (routes) determine domain traffic routing to the actions. Triggers associate certain URL patterns, based on a domain on the account, with a predefined action. The URL must contain the domain, but it can contain wildcards either as a prefix to the domain, or at the end of the path. If no path is given on the pattern, a `/` is added implicitly. The URL pattern cannot contain infix wildcards or query parameters. 

You must add a domain to add triggers. You can add triggers without having actions.

* **Adding triggers** Go to the **Triggers** tab and click **Add trigger**. Enter a URL pattern and select an action from the list of existing actions.
    * For an action, you can also select **Avoid Edge Functions**. This allows the trigger's path to remain active, but avoid using any Edge function actions. For example, the action called `my-function` and a trigger with the path `gamma.cistest-load.com/*`. If the path `gamma.cistest-load.com/data` should not use the action `my-function`, create another trigger with the path `gamma.cistest-load.com/data` and the option **Avoid Edge Functions**. This allows the path `gamma.cistest-load.com/data` to remain active without using the action `my-function`.

* **Editing triggers** Update a trigger using the menu option in the table row for a selected trigger. After updating select **Save**.
* **Deleting triggers** Delete a trigger using the menu option in the table row for a selected trigger. This action cannot be undone.
