---
copyright:
  years: 2018
lastupdated: "2018-03-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Limitações conhecidas

 * Nossa recomendação é usar o Chrome.

 * No Firefox e Safari, as datas *transferido por upload*, *modificado* e *expira* para um certificado não podem ser exibidas.

 * A edição da correspondência de URL para uma regra de página faz com que a regra seja colocada na prioridade mais baixa.
 
 * Sem um domínio configurado, é possível navegar para **Confiabilidade > Balanceadores de cargas globais** para criar seus conjuntos de balanceadores de cargas e verificações de funcionamento. No entanto, se você selecionar **Criar balanceador de carga**, configurar o balanceador de carga e clicar em **Provisionar 1 recurso**, a solicitação será rejeitada porque um domínio é necessário. Essa limitação funcional ajuda o usuário a entender o propósito dos conjuntos e monitores no fluxo de criação do balanceador de carga.
 
 * O programa Early Access está limitado a uma instância por conta. Depois de criar uma instância de recurso e incluir um domínio nela, você não terá permissão para incluir novas instâncias de recursos para o CIS. Essa restrição será impingida mesmo se você excluir um domínio de teste e, em seguida, tentar incluir um domínio novamente na mesma instância de recurso. Você vai encontrar um erro se tentar fazer isso.

 * Ao incluir um novo domínio, nosso sistema atualmente não reúne ou importa seus registros de domínio existentes.

 * Para esse programa Access Early, nós suportamos a delegação de subdomínio apenas usando registros NS de outro provedor. A delegação CNAME não é suportada.
