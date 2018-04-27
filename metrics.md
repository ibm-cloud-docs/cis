---
copyright:
  years: 2018
lastupdated: "2018-04-26"
---

# How to use the CIS Metrics Tools

You can use the CIS Metrics tools (from the side navigation bar) to display information about Domain and DNS metrics in easy-to-digest charts and tables.

The CIS Metrics tools suite contains these tools:
 * **Domain Metrics**, which consists of Web Traffic, Performance, and Security tools
 * **DNS Metrics**, which consists of three traffic tools
    
**Notes:** 

 * The smallest viewable increment for CIS Metrics is 6 hours.
 * Each chart displays only the top ten items. You can click on any item in the key to toggle the display of that item.

## Domain Metrics
The **Domain Metrics** tools are a series of charts, tables, and graphs that show web traffic, performance, and security information.

**Note**: **Domain Metrics** can retrieve up to 90 days at one time, but retrieving 3 different 30-day ranges is quicker.

### Web Traffic
The **Web Traffic** tool is a set of five tabs that show you helpful information about the traffic to your website. 
* **Requests** shows cached and uncached requests made on the domain.
* **Bandwidth** shows cached and uncached bandwidth in bytes. 
* **Unique Visitors** shows the number of unique visitors to the site.
* **Threats** shows the total number of threats that are blocked.
* **Status Codes** shows the different HTTP status codes returned to the end users.


### Performance
The **Performance** tool can help you optimize your site's performance.


![Domain Performance Metrics image](images/domain-metrics-performance.png)

* **Fewer Servers Needed** is shown as a percentage, which is a rough estimate of how much less capacity you need for handling your site’s traffic. It's based on the number of requests and bandwidth you've saved by using CIS. It is intended to help you see how much less web traffic is going to your Origin server.

* **Bandwidth Saved** is a percentage that shows how much bandwidth you've saved by using CIS. It is used in calculating the **Fewer Servers Needed** metric.

### Security
The **Security** tool is a chart that shows the number of threats stopped.

![Domain Security Metrics image](images/domain-metrics-security.png)

## DNS Metrics
The **DNS Metrics** tool provides a series of charts that cover DNS traffic and the top-queried DNS records.

### Traffic
The Traffic section consists of two tabs that display **Queries by Response Code** and **Queries by Record Type**. Use the dropdown menu to select the date range displayed.

![DNS Traffic image](images/dns-metrics-traffic.png)

### Top queried DNS records
This table contains a paginated list of the most-queried DNS records, in descending order. It shows the name and type of the record, and the number of queries received.

### Top DNS records returning NXDOMAIN
This table contains a paginated list of the requests made to non-existent internet domains, in descending order. It shows the name and type of the record, and the number of queries received. If there are no NXDOMAIN responses, this chart will be empty.
