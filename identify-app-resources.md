---



copyright:
  years: 2017
lastupdated: "2018-06-20"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Identify your application resources

Identify the your application's resources, such as origin pools and health check mechanisms.
 
1. Navigate to the **Origin Pools** section, and click **Create pool** to define a new origin pool. 

   Origin pools are server resources delivering applications to your clients. 
   
2. Assign a name to your Origin Pool, and select the health check mechanism defined earlier. Add your application server as your Origin. You may add one or more Origins by clicking **Add Origin**. 

   **NOTE:** If your application servers are sitting behind a local load balancer such as an IBM Cloud Load Balancer, then add your load balancer’s FQDN or virtual IP as your Origin instead of adding your individual servers. 
   
3. Click **Provision Resource** to complete the creation of your Origin Pool.  

   <img src="images/reliability8.png" alt="drawing" style="width: 300px;"/>
   
   The Origin Pool will initially show up as **Unhealthy**. Its state will change to **Healthy** after a successful health check by the system. You may need to refresh your browser to see the state change. 
   
   <img src="images/reliability9.png" alt="drawing" style="width: 300px;"/>
   
   **NOTE:** If you have multiple origins within your Origin Pool, then use the healthy origin threshold to specify the minimum number of origins that must be healthy before declaring the pool healthy. 
   
4. Define as many origin pools as the number of application farms you have. These farms may be within the same or different
geographic regions. In our example, we’ll create two origin pools representing an application farm in the United States west and east coasts. 

   <img src="images/reliability10.png" alt="drawing" style="width: 300px;"/>
