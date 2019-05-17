---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Attack Concepts, Application layer attacks, common types of internet attacks

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 分布式拒绝服务 (DDoS) 攻击概念
{:#distributed-denial-of-service-ddos-attack-concepts}

DDoS 攻击是 Web 站点或主机可能会遇到的最常见的因特网攻击类型。

## 什么是 DDoS 攻击？
{:#what-is-a-ddos-attack}

分布式拒绝服务 (DDoS) 攻击是指通过在目标或其周围基础设施产生大量因特网流量，恶意尝试中断服务器、服务或网络的正常通信。DDoS 攻击利用很多被破坏的计算机系统作为攻击流量的源来实施有效攻击。被利用的机器可以包括计算机和其他联网资源，如 IoT 设备。总体看来，DDoS 攻击就像是高速公路的交通堵塞，让正常车流无法到达预期目的地。

## DDoS 攻击是如何进行的？
{:#how-does-a-ddos-attack-work}

攻击者控制联机机器的网络执行 DDoS 攻击。计算机和其他机器（如 IoT 设备）被恶意软件感染，将每台机器都变成机器人（或 zombie）。攻击者控制被称为_僵尸网络_的机器人组。 

建立僵尸网络后，攻击者通过使用远程控制向每个机器人发送更新的指令来指示机器执行操作。目标 IP 地址可能会接收来自大量机器人的请求，从而导致目标服务器或网络溢出容量。这样就会对正常流量创建拒绝服务。因为每个机器人都是合法的因特网设备，所以很难将攻击流量与正常流量分离开。 

## 有哪些常见的 DDoS 攻击类型？
{:#what-are-common-types-of-ddos-attacks}

DDoS 攻击向量以不同的网络连接组件为目标。尽管几乎所有 DDoS 攻击都是让目标设备或网络的流量溢出，但攻击可分为三个类别。攻击者可以使用一个或多个攻击向量，甚至可以根据目标采取的对策来循环使用这些攻击向量。

常见类型包括：

 * 应用程序层攻击（第 7 层）
 * 协议攻击（第 3 层和第 4 层）
 * 容量耗尽攻击（放大攻击）

### 应用程序层攻击
{:#application-layer-attacks}

应用程序层攻击有时称为_第 7 层 DDoS 攻击_（指 OSI 模型的第 7 层）。这些攻击的目标是耗尽被攻击者的资源，其攻击目标是在服务器上生成 Web 页面并将 Web 页面传递给访问者以响应 HTTP 请求的层（即应用程序层）。第 7 层攻击很难防范，因为很难将流量识别为恶意的。

### 协议攻击
{:#protocol-attacks}

协议攻击利用 ISO 协议堆栈的第 3 层和第 4 层中的缺陷使目标无法访问。这些攻击（也称为状态耗尽攻击）会导致服务中断，因为其使用了 Web 应用程序服务器或中间资源（例如防火墙和负载均衡器）的所有可用_状态表_容量。 
  
### 容量耗尽攻击
{:#volumetric-attacks}

此类攻击尝试通过使用目标和更广泛的因特网之间的所有可用带宽来造成拥塞。大量数据通过放大形式或通过其他可产生大量流量的方法（例如，来自僵尸网络的请求）发送到目标。 


## 如果受到 DDoS 攻击应该怎么办？
{:#under-ddos-attack}

**步骤 1：**从**概述**屏幕打开“防御模式”。 

![防御模式](images/defense-mode.png)

**步骤 2：**设置 DNS 记录以实现最高安全性。

**步骤 3：**不要对来自 IBM CIS 的请求进行速率限制或调速，我们需要带宽来帮助您解决该情况。

**步骤 4：**必要时阻止特定国家或地区和访问者。