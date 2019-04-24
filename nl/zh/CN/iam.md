---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Access Group Writer role, CIS instance, IAM

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# IAM 和 CIS
{:#iam-and-cis}

IBM Cloud Internet Services (CIS) 利用 IAM 以执行授权和认证。

如果不希望向 CIS 实例添加任何人，那么可忽略此页面。
{:note}

根据导航树，通过三个 CIS Functional Scope 限制访问： 
* 可靠性 - 例如，DNS 和 GLB
* 安全性 - 例如，证书、IP 防火墙规则和速率限制
* 性能 - 例如，页面规则、高速缓存和路由

此部分将遍历如何提供实例的细颗粒度访问控制。

## 角色
{:#iam-and-cis-roles}

使用以下三个角色来利用 IAM
* 读者 - 可获取有关实例和域的信息
* 写入者 - 可对现有配置进行更改
* 管理者 - 可创建或删除实例、域和配置

## 访问组和用户
{:#iam-and-cis-access-groups-users}

可将策略直接分配给用户或分配给访问组。
建议将策略分配给访问组以最大限度减少创建的策略数量并减少管理这些策略的工作量。

## 高速缓存
{:#iam-and-cis-cache}

我们高速缓存授权结果，并在相同请求再次到达时使用高速缓存进行决策。高速缓存达到生存时间（10 分钟）后，将到期。

## 最佳实践
{:#iam-and-cis-best-practices}

1. 不要修改策略，而是删除现有策略，然后创建新策略。

## 场景
{:#iam-and-cis-scenarios}

此部分遍历通过 CIS 创建的访问策略的不同示例。 

### 带有`配置`类型的域级别
{:#iam-and-cis-scenarios-domain-level}

#### 访问在访问组上具有`安全配置`的单个域
##### 写入者角色

Bob 具有一个 CIS 实例 `cis-test-instance`，以及两个域 `bob.com` 和 `bob-ibm.com`。
Bob 想要为公司中的所有安全工程师 (sec-group) 提供仅 **`bob.com`** 上**安全配置**的“写入者”角色的访问权。

这些步骤显示如何创建 IAM 策略以实现此场景。

在 Bob 登录到 cis-test-instance 后，他：
1. 单击导航栏中的**帐户 > 访问权**选项卡
1. 选择想要提供访问权的**访问组** - **sec-group**
1. 选择 **`bob.com`**
1. 选择**写入者**角色
1. 选择**安全配置**选项
1. 单击**创建策略**

在“管理”选项卡上：
针对 **sec-group** 创建以下策略：

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e

Service Instance 
    name: cis-test-instance  
    id: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9 
Domain 
    name: bob.com
    id: 4b23ec772965f672f96f05670e36827e 
Config Type
    cfgType: security
```

现在，sec-group 有权仅查看 `bob.com`，并且可修改与安全性相关的值。 

##### 针对访问组从“写入者”更新为“管理者”角色

如果 Bob 想要将 sec-group 的角色从“写入者”更新为“管理者”，那么他需要删除现有策略。 
1. 转至**管理 IAM 选项卡 > 访问组 > sec-group > 访问策略**
1. 删除以下策略 
  ```
  Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
  ```

然后，Bob 必须创建新策略。 
1. 单击导航栏中的**帐户 > 访问权**选项卡
1. 选择想要提供访问权的**访问组** - **sec-group**
1. 选择 **`bob.com`**
1. 选择**管理者**角色
1. 选择**安全配置**选项
1. 单击**创建策略**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

如果未删除现有策略（写入者），那么为管理者创建策略的尝试将失败。

##### 更新配置以包含性能以及安全性

如果 Bob 想要为“管理者”授予 sec-group 访问权以访问 `bob.com` 上的性能配置以及安全性，那么：
1. 单击导航栏中的**帐户 > 访问权**选项卡
1. 选择想要提供访问权的**访问组** - **sec-group**
1. 选择 **`bob.com`**
1. 选择**管理者**角色
1. 选择**性能配置**选项
1. 单击**创建策略**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: performance, domainId: 4b23ec772965f672f96f05670e36827e

```

#### 访问具有`安全配置`的所有域

如果想要针对先前示例中的 `bob.com` 和 `bob-ibm.com` 提供安全操作，那么必须通过针对每个域重复相应步骤来创建新策略。唯一区别是为每个策略选择各自的域。

1. 单击导航栏中的**帐户 > 访问权**选项卡
1. 选择想要提供访问权的**访问组** - **sec-group**
1. 选择 **`bob.com`**
1. 选择**管理者**角色
1. 选择**安全配置**选项
1. 单击**创建策略**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

1. 单击导航栏中的**帐户 > 访问权**选项卡
1. 选择想要提供访问权的**访问组** - **sec-group**
1. 选择 **`bob-ibm.com`**
1. 选择**管理者**角色
1. 选择**安全配置**选项
1. 单击**创建策略**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 7ad7341865246f5df482ad9f76aafb5a
```



#### 访问具有`安全配置`和`可靠性配置`的单个域

Bob 具有 1 个 CIS 实例 cis-test-instance 以及 2 个域 `bob.com` 和 `bob-ibm.com`。
Bob 想要为 Tony 提供仅 **`bob-ibm.com`** 上**安全和可靠性操作**的“写入者”角色的访问权。

在 Bob 登录到 cis-test-instance 后，他：
1. 单击导航栏中的**帐户 > 访问权**选项卡
1. 选择想要为其提供访问权的 **Tony**
1. 选择 **`bob-ibm.com`**
1. 选择**写入者**角色
1. 选择**安全和可靠性**选项的复选框 
1. 单击**创建策略**

这将在每个配置类型的后端创建两个策略。

### 带有所有配置类型的域级别
{:#iam-and-cis-scenarios-domain-level-all-config-types}

Bob 想要在域级别授权 Tony 读取/写入/管理。

#### 写入
在 Bob 登录到 cis-test-instance 后，他：
1. 单击导航栏中的**帐户 > 访问权**选项卡
1. 选择想要为其提供访问权的 **Tony**
1. 选择 **`bob.com`**
1. 选择**写入者**角色
1. 选中 CIS Functional Scope 的所有框
1. 单击**创建策略**

```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### 管理者
在 Bob 登录到 cis-test-instance 后，他：
1. 单击导航栏中的**帐户 > 访问权**选项卡
1. 选择想要为其提供访问权的 **Tony**
1. 选择 **`bob.com`**
1. 选择**管理者**角色
1. 选中 CIS Functional Scope 的所有框
1. 单击**创建策略**

```
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### 读者
在 Bob 登录到 cis-test-instance 后，他：
1. 单击导航栏中的**帐户 > 访问权**选项卡
1. 选择想要为其提供访问权的 **Tony**
1. 选择 **`bob.com`**
1. 选择**读者**角色
  1. 预先选中了所有复选框以显示用户需要整个域的*最小*读访问权，并且无法授予对域的部分访问权
1. 单击**创建策略**


```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

### 实例级别 - 所有域
{:#iam-and-cis-scenarios-instance-level}

必须通过 IAM 管理页面创建和管理此策略。

实例级别访问意味着 Bob 可向 Tony 授予实例 1（共提供了 10 个实例）的许可权。
Tony 能够查看此实例中的所有域。 

如果 Bob 想要授予“写入者”或“管理者”以访问以下项，那么他需要提供实例级别访问权：
* 负载均衡器 - 池和运行状况检查
* 防火墙访问规则
* 工作程序 

在“管理 IAM”页面中，在服务实例 cis-test-instance 上创建写入者/管理者策略。

```
Manager	Resource	Only service instance cis-test-instance of CIS 	
or
Writer	Resource	Only service instance cis-test-instance of CIS 	
```

## 管理 IAM 策略 
{:#manage-iam-policies}

CIS 允许用户创建 IAM 策略，但是必须通过 [IAM 页面](
https://{DomainName}/iam#/overview) 完成管理。

## 注
{:#iam-note}
对于在 CIS 实例中的“访问”页面上创建的每个策略，将依次创建 2-3 个策略。

1. 服务实例平台查看者角色允许添加的用户在仪表板上查看实例。

**示例**
```
Viewer	Resource	Only service instance cis-instance-instance of CIS 	
```

2. 域级别读访问权是细颗粒度访问权生效的最低需求。

**示例**
```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
```
3. 使用提供的配置类型创建的策略。

**示例**
```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

**常见问题及解答**
1. 如何获取服务实例标识？

   复制概述页面上的 CRN
   ```
   crn:v1:test:public:internet-svcs:global:a/2c38d9a9913332006a27665dab3d26e8:836f33a5-d3e1-4bc6-876a-982a8668b1bb::
   ```
CRN 的最后一部分是服务实例：`836f33a5-d3e1-4bc6-876a-982a8668b1bb`。
   
   或者
   
   单击在资源列表主页上包含 CIS 实例的行，并复制服务实例标识的 GUID。

2. 我已删除策略，但是我将此策略授予的用户仍可执行该操作！

   CIS 会高速缓存授权结果，并且高速缓存的 TTL 为 10 分钟。  
   
   在 IAM 授权时，它使用来自访问组的访问策略以及用户自己的策略，然后做出决策。

3. 供应因特网服务需要哪些许可权？

   如果无法创建资源并将其添加到资源组，那么很可能是在处理访问权问题。您必须至少具有对资源组本身的“查看者”角色，还必须至少具有对帐户中服务的“编辑者”角色。您可以联系帐户管理员来确认帐户中分配给您的访问权。有关更多信息，请参阅[管理对资源的访问权](/docs/iam?topic=iam-iammanidaccser)。
   
 
