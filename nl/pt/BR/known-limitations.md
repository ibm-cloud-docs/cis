---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, Free Trial plan, dedicated certificate, known issues

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 
{:note: .note} 
{:important: .important} 
{:deprecated: .deprecated} 
{:generic: data-hd-programlang="generic"}

# Limitações conhecidas
{:#known-limitations}

 * Recomendamos usar o Chrome.
 
 * O plano de Avaliação grátis é limitado a uma instância por conta. Depois de criar uma instância de recurso e incluir um domínio nela, você não terá permissão para incluir novas instâncias de recursos para o CIS. Essa restrição será impingida mesmo se você excluir um domínio de teste e, em seguida, tentar incluir um domínio novamente na mesma instância de recurso. Você vai encontrar um erro se tentar fazer isso.

 * Para esse serviço, nós suportamos a delegação de subdomínio usando apenas registros NS de outro provedor. A delegação CNAME não é suportada.
  
 * Não é possível incluir proxy em registros curinga (*) A, AAAA e CNAME.

 * Quando você exclui um certificado dedicado, ele pode reaparecer na lista por um curto período antes que a exclusão seja concluída.
 
 * Para modificar os nomes de host do certificado dedicado customizado após a solicitação, deve-se solicitar um novo certificado e, em seguida, excluir o antigo. 
 
 * As Regras de IP criadas com códigos de país de duas letras podem ser feitas apenas com a ação `Desafiar`. Se desejar bloquear os visitantes de um país, faça upgrade para o plano Enterprise ou insira as regras em seu servidor para bloquear completamente.

## Balanceador de carga global
{:#known-limitations-glb}

 * O Cloud Internet Services permite que você use o caractere `_` em nomes de host do balanceador de carga, no entanto, os clusters do Kubernetes não podem usar `_`. 

 * O plano Standard permite um máximo de 5 balanceadores de carga, conjuntos e verificações de funcionamento. Cada conjunto pode ter um total de 6 origens, mas somente 6 origens exclusivas são permitidas em cada instância do CIS.

* Não é possível filtrar os eventos de verificação de funcionamento para conjuntos e origens excluídos, mas eles ainda aparecem na tabela.

* Se você filtrar os Eventos de verificação de funcionamento por `Funcionamento do conjunto`, conjuntos `Comprometidos` serão incluídos porque são tecnicamente saudáveis, mas podem conter uma ou mais origens críticas.

* Ao incluir o nome do cabeçalho da solicitação para uma verificação de funcionamento, use `Host`. O uso de `host` em letras minúsculas para uma verificação de funcionamento causa uma falha.

## DNS
{:#known-limitations-dns}

 * A exportação de registros de DNS inclui registros CNAME da Cloudflare que devem ser ocultados. Esses registros começam com `_` e, geralmente, têm um segundo registro com o mesmo nome, mas o `_` é removido.
   ```
   Ex.
   _cf.generate.yourdomain.com 0	IN	CNAME address.alias.com
   cf.generate.yourdomain.com 0	IN	CNAME address2.alias.com
   ```
 
   Esses registros devem ser removidos do arquivo de zona para serem importados corretamente.
 
 * Exportar registros de DNS do CAA não funciona corretamente. O `<tag>` e `<value>` são codificados em HEX. 
 
    CAA `<flags>` `<tag>` `<value>`
  {:note}
   ```
   Ex.
   Registro CAA Original
   caa.yourdomain.com.	1	IN	CAA	0 emita "letsencrypt.org"

   Registro CAA exportado
   caa.yourdomain.com.	1	IN	CAA	0 6973737565 "6c657473656e63727970742e6f7267"
   ```
   Esses registros devem ser convertidos de HEX para sequência ou removidos e incluídos manualmente antes da importação.

## Regras de página
{:#known-limitations-pagerules}

   * A atualização das configurações de regras de página usando o plug-in do CIS para a CLI do IBM Cloud poderá resultar em um erro se o ID da regra de página não estiver incluído na sequência JSON ou no arquivo JSON para a atualização. Como solução alternativa, envie a atualização usando um arquivo completo de configuração JSON para a regra de página, incluindo o ID.
   * A remoção das configurações de regra de página com o uso da IU do CIS pode não remover a configuração, mesmo que a IU relate uma atualização bem-sucedida. Como solução alternativa, use o plug-in do CIS para a CLI do IBM Cloud para remover a configuração e inclua o ID da regra de página no documento de atualização JSON:
      ```
      $> ibmcloud cis page-rule-update <domain-id> <rule-id> -j <file>
      ```
      O arquivo JSON deve incluir a configuração de regra de página completa, incluindo o ID, com as atualizações necessárias.
