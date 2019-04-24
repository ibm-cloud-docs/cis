---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer configuration, glb configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}

# 开始配置全局负载均衡器
{:#begin-global-load-balancer-configuration}

开始配置您的全局负载均衡器。

1. 在**可靠性**部分下，选择**全局负载均衡器**。 
    
    <img src="images/reliability6.png" alt="图样" style="width: 300px;"/>

2. 滚动到“运行状况检查”部分。 

   此配置是可选的。如果您没有定义任何定制的运行状况检查，系统将使用“/”作为缺省运行状况检查路径。
   {:note}

3. 单击**创建运行状况检查**按钮来定义定制的运行状况检查。   

   提供您希望在其中执行运行状况检查的路径。您可以使用 HTTP 或 HTTPS 协议进行运行状况检查。 
   
4. 在**高级选项**下，您可以定制其他参数，例如运行状况检查时间间隔、重试次数、请求方法和响应主体。 
   
   <img src="images/reliability7.png" alt="图样" style="width: 300px;"/>
   
5. 单击**供应资源**以完成运行状况检查配置。 
