---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Use as regras de página

Uma Regra de Página especifica algumas configurações e valores que podem ser aplicados a um padrão de URL específico que faz referência ao seu domínio. As Regras de Página ajudam a gerenciar a segurança, o desempenho e a confiabilidade com base em cada URL individual em seu site. A tabela a seguir descreve as Regras de Página que estão disponíveis para todos os clientes, os comportamentos que elas produzem e quaisquer considerações especiais que você deve ter em mente antes de usá-las.

## Segurança

| **Configuração** | **Comportamento** | **Considerações** |
|-----------|----------|----------------|
|**Verificação de integridade do navegador**|Procura por cabeçalhos de HTTP comuns abusados por remetentes de spam e nega acesso à sua página. Também bloqueia os visitantes que não têm um agente do usuário ou incluem um agente do usuário não padrão (também comumente usado por robôs, crawlers ou APIs de abuso). | |
|**Desativar segurança**|Desativa os seguintes recursos: <ul><li>Ofuscação de e-mail</li> <li>Exclusões do lado do servidor</li> <li>WAF</li></ul>|Se uma regra for configurada para desativar a segurança e outra regra for configurada para ativar o WAF, a regra do WAF terá precedência, independentemente da ordem em que aparecem.|
|**Ofuscação de e-mail**|Ativa ou desativa a ofuscação de e-mail. | |
|**Cabeçalho de localização geográfica de IP**|Inclui o código do país do local do visitante com todas as solicitações para seu website. As informações podem ser localizadas no cabeçalho de HTTP `CF-IPCountry`. | |  
|**Nível de segurança**|Controla o quão alta uma pontuação de ameaça do cliente deve ser para que um cliente encontre uma página de desafio. Essa configuração pode ser usada para que seu site sempre apresente aos visitantes o desafio **Modo de Defesa** quando eles visitarem seu site. | |
|**Exclusões do lado do servidor**|Ativa ou desativa as exclusões do lado do servidor.  | |
|**TLS**|Controla qual dos modos TLS é usado. | |
|**WAF**|Ativa ou desativa o WAF. | |  
|**Regravações de HTTPS automáticas**|Ativa ou desativa regravações de HTTPS automáticas.  | |
|**Criptografia oportunista**|Ativa ou desativa a criptografia oportunista.  | |
|**Cache Deception Armor**|Ativa ou desativa o Cache Deception Armor. | |
|**Sempre usar HTTPS**|Converte qualquer URL `http://` em uma URL `https://` criando um redirecionamento`301`.|O uso dessa configuração desativa a definição de todas as outras configurações para a regra, porque o IBM CIS força um redirecionamento para `HTTPS` para a solicitação, que se torna uma nova solicitação que é, então, avaliada com relação às Regras de Página. |

## Desempenho
| **Configuração** | **Comportamento** | **Considerações** |
|-----------|----------|----------------|
|**TTL de cache do navegador**|Controla por quanto tempo os recursos armazenados em cache pelos navegadores do cliente permanecem válidos. | |
|**Efetuar bypass de cache no cookie**|Entregar um objeto armazenado em cache a menos que vejamos um cookie de um nome específico, por exemplo, servir uma versão em cache da página inicial, a menos que vejamos um cookie `SessionID` indicando que o cliente está com login efetuado e, portanto, deve ser apresentado conteúdo personalizado. | |
|**Nível de cache**|**Efetuar bypass** - Recursos que correspondem a essa Regra de Página não são armazenados em cache.<br>**Nenhuma sequência de consultas** - Entrega recursos do cache apenas quando não há sequência de consultas.<br>**Ignorar sequência de consultas** - Entrega o mesmo recurso para todos independente da sequência de consultas.<br>**Padrão** - Entrega um recurso diferente cada vez que a sequência de consultas muda.<br> **Armazenar tudo em cache** - Recursos que correspondem à Regra de Página são armazenados em cache.|Por padrão, o conteúdo HTML não é armazenado em cache. Uma Regra de Página para armazenar em cache conteúdo HTML estático deve ser gravada. |
|**TTL do edge cache**|Controla por quanto tempo o IBM CIS reterá arquivos em nosso cache. |Essa configuração é opcional ao especificar o nível de cache. |

## Confiabilidade
| **Configuração** | **Comportamento** | **Considerações** |
|-----------|----------|----------------|
|**Sempre on-line**|Mantém uma versão limitada do site on-line se o servidor fica inativo. |Para obter mais informações, visualize [Gerenciando a implementação do CIS para confiabilidade ideal](managing-for-reliability.html) |
|**Controle de cache de origem**|Determine qual conteúdo é armazenado em cache por meio da origem e com que frequência o conteúdo é atualizado |Para obter mais informações, visualize [Gerenciando a implementação do CIS para confiabilidade ideal](managing-for-reliability.html) |
|**URL de encaminhamento** |URL a ser utilizada caso o site fique indisponível. | O uso dessa opção desativa a definição de todas as outras configurações, porque você está encaminhando a solicitação para outro lugar. Para obter mais informações, visualize [Gerenciando a implementação do CIS para confiabilidade ideal](managing-for-reliability.html)|

## Padrões de URL da regra de página

Uma Regra de Página terá efeito sobre um padrão de URL especificado, correspondendo ao seguinte formato:

`<scheme>://<hostname><:port>/<path>`

Um exemplo utilizando cada componente seria:

`https://www.example.com:80/image.png`

Os componentes *scheme* e *port* são opcionais. Se o esquema for omitido, ele cobrirá ambos os protocolos `http://` e `https://`. Se a porta não for especificada, a regra corresponderá a todas as portas. É possível executar correspondências curinga básicas usando um símbolo '*' em seu padrão de regra, permitindo que ele corresponda a uma série de padrões similares em vez de apenas um.

Aqui estão três coisas importantes para lembrar com relação às Regras de Página:

 * Somente uma Regra de Página entrará em vigor em qualquer solicitação determinada.
 * As Regras de Página têm prioridade na ordem de cima para baixo.
 * Quando uma URL corresponder a uma regra, apenas essa regra será aplicada; ou seja, se uma Regra de Página já foi acionada em uma solicitação, quaisquer regras subsequentes que também correspondam ao padrão de URL não entrarão em vigor. Como uma regra geral, recomendamos ordenar as regras da _mais específica_ para a _menos específica_.

As Regras de Página podem ser desativadas, nesse caso elas não executarão nenhuma ação. Elas ainda poderão ser vistas na lista e poderão ser editadas. Configurar o comutador **Ativado** para **Desativado** criará uma Regra de Página que inicialmente está desativada.

Para obter mais informações, consulte o [documento de instruções Armazenamento em cache e regras de página](caching-with-page-rules.html).
