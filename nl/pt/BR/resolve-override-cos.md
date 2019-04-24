---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: resolve override, Cloud Object Storage, bucket resource

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Resolver substituição com o COS
{: #resolve-override-cos}

## Casos de uso
{: #cos-use-cases}

Faça com que a solicitação que corresponde à regra de página seja resolvida para um recurso de depósito do Cloud Object Storage (COS).


## Pré-requisitos
{: #cos-prerequisites}

As etapas a seguir consideram que você tenha uma instância existente do COS e um depósito com acesso público. Para obter informações sobre o acesso público, consulte [Permitindo o acesso público](/docs/services/cloud-object-storage/iam?topic=cloud-object-storage-allowing-public-access).


## Etapas da criação de regra de página
{: #cos-create-page-rule}

* Navegue para **Desempenho->Regras de Página**.
* Clique no botão **Criar regra**.
* Insira o valor desejado para a correspondência de URL. Por exemplo, `*.foo.com/*`.
  * Observe que a correspondência de URL deve corresponder ao nome do seu objeto do COS.
  * Por exemplo, se tiver um objeto chamado reports.txt no depósito `my-bucket1`, ambas as correspondências de URL serão válidas:
    * `*.foo.com/*`
    * `*.foo.com/reports.txt`
* Use o menu suspensa para selecionar **Resolver substituição com o COS** na seção **Desempenho**.
* Use a lista suspensa **Instância de armazenamento de objeto de nuvem** para selecionar a instância desejada.
* Use o menu suspenso **Depósito** para selecionar o depósito desejado.
* Para criar a Regra de página, clique no botão **Fornecer um recurso**.


## Explicação detalhada de conceitos
{: #cos-detail-concepts}

Ao criar uma regra de página **Resolver substituição com o COS**, o CIS criará automaticamente os outros recursos necessários para a integração do COS. Eles incluem:

**CNAME**
* Um registro de DNS do CNAME para o `<bucket-name>.<cos-endpoint>` como `<bucket-name>`.
* Por exemplo, se seu domínio do CIS for `foo.com`, você terá um depósito COS chamado `images` e seu terminal público COS será `s3.us-west.objectstorage.uat.test.net`, em seguida, o CIS criará um CNAME como `images.foo.com` que aponta para `images.s3.us-west.objectstorage.uat.uat.test.net`.
Se a regra de página Resolver substituição com o COS não for mais necessária, o CNAME deverá ser excluído manualmente com a regra de página.
{:note}

**Substituição do cabeçalho do host**
* A configuração Substituição do cabeçalho do host substituirá o cabeçalho do host para o URI que corresponde à regra de página por `<bucket-name>.<cos-endpoint>`.
* Usando o exemplo anterior, o valor de Substituição do cabeçalho do host será configurado como `images.s3.us-west.objectstorage.uat.test.net`.


## Excluindo a Regra de Página
{: #cos-delete-page-rule}

Se a regra de página Resolver substituição com o COS não for mais necessária, o CNAME deverá ser excluído _manualmente_ com a regra de página.


## Editando a regra de página
{: #cos-edit-page-rule}

Após editar a regra de página, **Resolver substituição com o COS** não será mais exibido na página. No entanto, **Resolver substituição** `<bucket>.<domain>` e **Substituição do cabeçalho do host** `<bucket>.<cos-endpoint>` substituirão **Resolver substituição com o COS**.

Fazer mudanças em **Resolver substituição** _não_ criará automaticamente um novo registro de CNAME (por exemplo, `<updated-bucket>.<domain>`). Isso é feito somente na criação inicial de uma regra de página, com o uso de **Resolver substituição com o COS**. Para criar automaticamente o registro de CNAME para o depósito, siga as etapas em [Criar regra de página](#cos-create-page-rule).
