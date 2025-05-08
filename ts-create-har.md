---

copyright:
  years: 2022, 2025
lastupdated: "2025-05-08"

keywords: HAR files, HAR, HTTP Archive

subcollection: cis

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# How do I generate a HAR file?
{: #generate-har-files}
{: troubleshoot}

When troubleshooting {{site.data.keyword.cis_full_notm}}, it can be helpful to generate an HTTP Archive (HAR) file. The HAR file is a record of all web browser requests including the request and response headers, the body content, and the page load time.
{: shortdesc}

You have an issue using {{site.data.keyword.cis_short_notm}} and need to generate a HAR file for Support.
{: tsCauses}

A HAR file can include sensitive details such as passwords, payment information, and private keys. Manually remove sensitive information from HAR files using a text editor before you provide the file to Support.
{: important}

Use the following sections to generate HAR files in Firefox, Chrome, or Safari browsers.
{: tsResolve}

## How to generate a HAR file in Firefox
{: #har-firefox}

1. In Firefox, go to the page within {{site.data.keyword.cis_short_notm}} where you are experiencing trouble.
1. Select the Firefox menu (three horizontal parallel lines) at the upper-right of your browser window, then select **Developer > Network**.
1. The Developer Network Tools open as a docked panel at the side or bottom of the browser window. Click the **Network** tab.
1. The recording starts automatically after you start performing actions in the browser.
1. Refresh the {{site.data.keyword.cis_short_notm}} page that you are on, or go through the steps to reproduce the problem you've been experiencing while Firefox is recording activity.
1. After you have reproduced the issue, right-click anywhere under the **File** column in the docked panel and click **Save All As HAR**.
1. Save the HAR file in a location you choose, and send the file to Support.

## How to generate a HAR file in Chrome
{: #har-chrome}

1. In Chrome, go to the page within {{site.data.keyword.cis_short_notm}} where you are experiencing trouble.
1. Select the Chrome menu (three vertical dots) at the top-right of your browser window, then select **Tools > Developer Tools**.
1. The Developer Tools open as a docked panel at the side or bottom of the browser window. Click the **Network** tab.
1. Select the option **Preserve log**.
1. The recording starts automatically, and a red "Record network log" icon appears at the top left of the Network tab. If not, click the black "Stop recording network log" icon, to start recording activity in your browser.
1. Refresh the {{site.data.keyword.cis_short_notm}} page you are on or go through the steps to reproduce the problem you've been experiencing while Chrome is recording activity.
1. After you have successfully reproduced the issue while recording, right-click any of the items within the Network tab and select **Save all as HAR with Content** to save a copy of the activity that you recorded.
1. Save the HAR file in a location you choose, and send the file to Support.

## How to generate a HAR file in Safari
{: #har-safari}

1. In Safari, first check to see if you have a "Develop" menu at the top of the page. If not, go to **Safari > Preferences > Advanced** and check "Show Develop Menu in menu bar".
1. In Safari, go to the page within {{site.data.keyword.cis_short_notm}} where you are experiencing trouble.
1. Navigate to **Develop > Show Web Inspector**.
    This menu option is not available until you browse somewhere beyond Safari's starting page. The Web Inspector opens as a docked panel at the bottom of Safari.
    {: note}

1. Click the **Network** tab.
1. Refresh the {{site.data.keyword.cis_short_notm}} page that you are on or go through the steps to reproduce the problem you've been experiencing while Safari is recording activity.
1. After you have reproduced the issue, Control + click the resource that you want to capture the HAR file for, and click **"Export HAR"**.
1. Save the HAR file in a location you choose, and send the file to Support.

## How to generate a HAR file in Microsoft Edge
{: #har-edge}

1. In Microsoft Edge, go to the page within {{site.data.keyword.cis_short_notm}} where you are experiencing trouble.
1. Click the Edge menu (three vertical dots) at the top-right of your browser window, then select **More Tools > Developer Tools**.
1. Select the Network tab, then click **Record** in the upper left corner of the tab and verify that it is recording. If it is not yet recording, click **Record** to start recording.
1. Check the box next to **Preserve Log**.
1. Select **Clear** to remove any existing logs from the **Network** tab.
    Do not close the Developer Tools panel. This ends the recording and the HAR file will be lost.
    {: note}

1. Refresh the {{site.data.keyword.cis_short_notm}} page you are on or go through the steps to reproduce the problem you've been experiencing while Edge is recording activity.
1. After you have reproduced the issue, right-click anywhere on the grid of network requests and choose **"Save as HAR with Content"**.
1. Save the HAR file in a location you choose, and send the file to Support.
