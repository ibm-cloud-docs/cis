---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Page Rules, web content, IBM CIS deployment

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Gerencie a implementação de seu IBM CIS para confiabilidade ideal
{:manage-your-ibm-cis-deployment-for-optimal-reliability}

Para atingir a confiabilidade ideal para a sua implementação do IBM CIS, é possível definir uma configuração útil do DNS e configurar os Balanceadores de Carga Globais. Para confiabilidade adicional, é possível usar nossas Regras de Página para ter certeza de que seu conteúdo da web seja entregue aos seus clientes, mesmo que seu servidor de origem ou cache tenha um problema. Este documento fornece detalhes sobre algumas boas práticas para tornar sua implementação do IBM CIS idealmente confiável.

Geralmente, nossas melhores práticas recomendadas são essas:

 * Configure o DNS para aproveitar os servidores proxy do IBM CIS e outros recursos
 * Use um ou mais Balanceadores de Carga Globais para distribuir o tráfego de seu site uniformemente
 * Configure Regras de Página apropriadas para gerenciar seu armazenamento em cache e outras opções

Cada um desses itens fornece determinada funcionalidade que pode ser usada para criar uma implementação do CIS mais confiável.

Observe que a interface do CIS é organizada em seções para *segurança*, *confiabilidade* e *desempenho*. O menu de navegação principal é mostrado na figura a seguir, com os Balanceadores de Carga Globais e itens de menu de DNS revelados:

![DNS de navegação à esquerda](images/cis-left-navigation.png)


## Configurando o DNS
{:#setting-up-dns}
 
 Para começar a definir sua configuração do DNS, selecione **DNS** no menu de navegação, conforme mostrado anteriormente.
 
 Para obter informações detalhadas sobre a configuração e o gerenciamento de seu DNS para a confiabilidade, [consulte esse documento](/docs/infrastructure/cis?topic=cis-set-up-your-domain-name-system-dns-for-ibm-cis).


## Configurando balanceadores de carga globais
{:#setting-up-glb}


Para começar a configurar seus Balanceadores de Carga Globais, selecione **Balanceadores de carga globais** no menu de navegação.

Para obter informações detalhadas sobre como configurar e gerenciar seus balanceadores de carga globais, [consulte esse documento](/docs/infrastructure/cis?topic=cis-global-load-balancer-glb-concepts).

## Usando Regras de Página para aumentar a confiabilidade
{:#using-page-rules-to-increase-reliability}

A seguir estão algumas configurações de Regra de Página recomendadas para fornecer máxima confiabilidade ao seu site:

 * Fornecer conteúdo antigo
 * Controle de cache de origem
 * URL de encaminhamento

## Fornecer conteúdo antigo
{:#serve-stale-content}

É possível usar a configuração de Regra de página **Fornecer conteúdo antigo** para manter uma versão limitada do site on-line, caso o servidor fique inativo.

Com **Fornecer conteúdo antigo**, quando seu servidor fica inativo, o IBM CIS fornece páginas de nosso cache, portanto, seus visitantes ainda veem algumas das páginas que estão tentando visitar. Seus visitantes veem uma mensagem na parte superior da página informando que estão no modo de navegação off-line. Fornecer conteúdo antigo retorna um status HTTP 503, no entanto, 503 também é usado por muitos outros aplicativos da web. Quando o servidor ficar on-line novamente, o IBM CIS colocará os usuários de volta na navegação regular.

Se o IBM CIS não tiver a página solicitada em seu cache, seu visitante verá uma página de erro que permite que ele saiba que a página do website que está sendo solicitada está off-line.

### Como configurar Fornecer conteúdo antigo
{:#setting-up-serve-stale-content}
Para ativar **Fornecer conteúdo antigo**, siga essas etapas:

 * Use o menu de navegação para selecionar Regras de página em Desempenho.
 * Crie uma Regra de Página com o padrão de URL de seu domínio.
 * Inclua a configuração **Fornecer conteúdo antigo** com a alternância ativada.
 * Selecione Recurso de provisão.

### Limitações de Fornecer conteúdo antigo
{limitations-serve-stale-content}

 * **Entizar Conteúdo Stale** armazena em cache os primeiros 10 links de seu HTML raiz, em seguida, apenas os primeiros links de cada uma dessas páginas, e, finalmente, os primeiros links de cada uma dessas páginas subsequentes. Isso significa que apenas algumas páginas em seu site podem ser visualizadas quando seu servidor de origem fica inativo.

 * Os sites incluídos recentemente não têm um grande cache disponível, o que significa que **Fornecer conteúdo antigo** poderá não funcionar se você tiver incluído o site somente alguns dias atrás.

 * O CIS não mostrará conteúdo privado nem manipulará o envio de formulários (POSTs) se o seu servidor estiver inativo. Os visitantes são mostrados como uma página `error on checkout` ou `items requerem um login para visualizar`.

 * Para acionar **Fornecer conteúdo antigo**, é preciso que seu servidor da web esteja retornando um código de erro HTTP padrão de tempo limite 502 ou 504. Fornecer conteúdo antigo também funciona quando encontramos problemas ao entrar em contato com sua origem (Erros 521 e 523), tempos limites (522 e 524), erros de SSL (525 e 526) ou um erro desconhecido (520). **Fornecer conteúdo antigo** não é acionado para outros códigos de resposta HTTP, como 404s, 500, 503, erros de conexão com o banco de dados, erro do servidor interno ou respostas vazias do servidor.

 * **Fornecer conteúdo antigo** não funcionará se uma regra de página "Armazenar tudo em cache" estiver ativada com o "TTL de expiração de edge cache" inferior à frequência do armazenamento em cache, pois "TTL de expiração de edge cache" faz com que o cache **Fornecer conteúdo antigo** seja limpo no intervalo correspondente.

## Controle de cache de origem
{:#origin-cache-control}
É possível usar a configuração da Regra de Página **Controle de cache de origem** para determinar qual conteúdo de sua origem é armazenado em cache e a frequência com que o conteúdo é atualizado, o que tem um efeito sobre a confiabilidade e o desempenho. Por padrão, se nenhuma configuração muda e nenhum cabeçalho que impede o armazenamento em cache é enviado de seu servidor de origem, o IBM CIS armazena todo o conteúdo estático em cache com determinadas extensões. Esses tipos de conteúdo incluem imagens, CSS e JavaScript. Usa-se esse armazenamento em cache principalmente por motivos de desempenho.

Para configurar o **Controle do cache de origem**, use as Regras de página para ativar cabeçalhos específicos que fornecem o comportamento desejado com relação a cada recurso de seu conteúdo. Para entender como usar o **Controle do cache de origem**, é necessária uma explicação mais geral das Regras de página e do comportamento geral do armazenamento em cache do CIS para fins de contexto, o que é coberto nas próximas diversas seções. Existem três métodos que podem ser usados para controlar o armazenamento em cache em geral e **Controle de cache de origem** é o segundo.

A configuração de **Controle de cache de origem** chama regras de armazenamento em cache que buscam aderir estritamente às melhores práticas e RFCs da Internet, principalmente com relação à revalidação. Por exemplo, o comportamento padrão do CIS com `max-age=0` não é armazenar em cache de maneira nenhuma, enquanto que a configuração de **Controle de cache de origem** armazena em cache, mas ele é sempre revalidado.

### Como configurar o Controle de cache de origem
{:#setting-up-origin-cache-control}

 * Use o menu de navegação para selecionar Regras de página em Desempenho.
 * Crie uma Regra de página com o padrão de URL que faz referência a seu domínio.
 * Inclua a configuração **Controle de cache de origem** com o comutador ativado.
 * Selecione Recurso de provisão.

### Precedência da regra de página
{:#page-rule-precedence}

Duas Regras de Página específicas têm precedência para armazenamento em cache geral:

 * Se uma Regra de Página tiver o **Nível de cache** configurado como `Bypass`, os recursos que correspondem a essa Regra de Página não serão armazenados em cache. O IBM CIS ainda age como um proxy e nossos outros recursos de desempenho permanecem ativos. No entanto, seu conteúdo é buscado a partir de seu servidor de origem diretamente, em vez de ser servido a partir de nosso cache.

 * Se uma Regra de Página tiver o **Nível de cache** configurado como `Armazenar tudo em cache`, os recursos que correspondem à Regra de Página serão armazenados em cache. **Usar essa configuração de Regra de Página é a única maneira de nos dizer para armazenar em cache recursos além do que consideramos estático, incluindo HTML.**

Se nenhuma Regra de página estiver configurada, usaremos o modo de armazenamento em cache `Standard`, que é baseado na extensão do recurso. Armazenamos em cache somente recursos estáticos.

### Cabeçalhos de controle de cache de origem
{:#origin-cache-control-headers}

A segunda maneira de alterar o que o IBM CIS armazena em cache é por meio de cabeçalhos de armazenamento em cache enviados pela origem. O CIS respeita essas configurações, mas é possível substituí-las especificando uma configuração de Regra de página **TTL de edge cache**. A seguir estão os cabeçalhos que consideramos ao decidir quais recursos de sua origem armazenar em cache:

 * Se o cabeçalho **Cache-Control** for configurado como `private`, `no-store`, `no-cache` ou `max-age=0` ou se houver um cookie na resposta, o IBM CIS não armazenará o recurso em cache. Observe que o material sigiloso não deve ser armazenado em cache, portanto, é possível considerar o uso de um desses cabeçalhos nesse caso.

 * Se o cabeçalho **Cache-Control** for configurado como `public` e o `max-age` for maior que 0 ou se os cabeçalhos `Expires` forem configurados a qualquer momento no futuro, armazenaremos o recurso em cache.

**Nota:** conforme as regras de RFC, `Cache-Control: max-age` supera cabeçalhos `Expires`. Se virmos ambos e eles forem conflitantes, `max-age` vencerá.

### Usando o cabeçalho 's-maxage'
{:#using-the-s-maxage-header}

A terceira forma de controlar o comportamento do armazenamento em cache e o comportamento do armazenamento em cache do navegador juntos é usando o cabeçalho Cache-Control `s-maxage`.

Normalmente, nós respeitamos a diretiva `max-age`:

`Cache-Control: max-age=1000`

No entanto, se desejar especificar um tempo limite de cache diferente do navegador, será possível usar `s-maxage`. A seguir há um exemplo que informa ao IBM CIS para armazenar o objeto em cache por 200 segundos e ao navegador para armazenar o objeto em cache por 60 segundos.

`Cache-Control: s-maxage=200, max-age=60`

Basicamente, `s-maxage` destina-se a ser seguido APENAS por proxies reversos (de modo que o navegador deve ignorá-lo), por outro lado, no entanto, nós (IBM CIS) damos prioridade a `s-maxage` se ele está presente. Respeitamos o valor que for maior: a configuração de cache do navegador ou o cabeçalho `max-age`.

### Resumo sobre cabeçalhos de controle de cache e Regras de Página para confiabilidade
{:#summary-cache-control-headers-page-rules}

Para resumir, a seguir estão algumas áreas principais a serem consideradas para confiabilidade com relação ao armazenamento em cache:

 * Verifique os cabeçalhos de armazenamento em cache de sua origem para garantir que não haja cabeçalhos de substituição para recursos armazenáveis em cache (`Cache-Control` e `Expires`).

 * O CIS sempre armazena conteúdo estático em cache por padrão, com o TTL a seguir, dependendo do código de retorno:

```
200 301    120m;
302 303    20m;
403        5m; for reliability
404        5m;
any        0s;
```

 * Para armazenar mais itens em cache, crie uma Regra de página com **Nível de cache** configurado para `Armazenar tudo em cache` na URL desejada (se seu servidor da web retornar um 404 ao solicitar essa URL, armazenaremos esse resultado em cache por apenas cinco minutos).

 * Para evitar o armazenamento em cache em uma URL, crie uma Regra de página com **Nível de cache** configurado para `Efetuar bypass`.


## URL de encaminhamento
{:#forwarding-url}

Caso seu site esteja indisponível, crie uma Regra de página com a configuração **URL de encaminhamento** usada para garantir que seu conteúdo esteja sempre disponível.

Ao ativar uma **URL de encaminhamento**, todas as outras configurações são desativadas porque você está enviando todo o tráfego para outra URL.
{:note}

### Como configurar uma URL de encaminhamento
{:#setting-up-forwarding-url}

 * Use o menu de navegação para selecionar Regras de página em Desempenho.
 * Crie uma Regra de página com o padrão de URL que faz referência a seu domínio.
 * Inclua a configuração **URL de encaminhamento**.
 * Selecione o tipo de encaminhamento e insira a URL de destino.
 * Selecione Recurso de provisão.

### Exemplos de encaminhamento
{:#forwarding-examples}

Imagine que você deseja tornar mais fácil para qualquer pessoa acessar uma URL como:

    *www.example.com/+

    *example.com/+

Esse padrão corresponde a:

    http://example.com/+
    http://www.example.com/+
    https://www.example.com/+
    https://blog.example.com/+
    https://www.blog.example.com/+
    Etc...

Ele não corresponde a:

    http://www.example.com/blog/+  [extra directory before the +]
    http://www.example.com+  [no trailing slash]


Depois de ter criado o padrão que corresponde ao que você deseja, inclua a configuração **URL de encaminhamento**, selecione o tipo de encaminhamento e insira a URL de destino. Por exemplo:

    https://plus.google.com/yourid

Selecione Recurso de provisão. Dentro de alguns segundos, quaisquer solicitações que correspondam ao padrão serão encaminhadas à nova URL com o redirecionamento especificado.

### Opções avançadas de encaminhamento
{:#advanced-forwarding-options}

Se você usar um redirecionamento básico, como encaminhar o domínio raiz para `www.yourdomain.com`, você perderá qualquer outra coisa na URL. Por exemplo, você poderia configurar o padrão:

    example.com

E fazê-lo encaminhar para:

    `http://www.example.com`

Mas se alguém inserisse:

    `example.com/some-particular-page.html`

Em seguida, são redirecionados para:

    `www.example.com`

em vez de

    `www.example.com/some-particular-page.html`

A solução é usar variáveis. Cada curinga corresponde a uma variável que pode ser referenciada no endereço de encaminhamento. As variáveis são representadas por um `$` seguido por um número. Para referir-se ao primeiro curinga, você usaria `$1`, para referir-se ao segundo curinga, você usaria `$2`, e assim por diante. Para corrigir o encaminhamento da raiz para `www` no exemplo anterior, use o mesmo padrão:

    `example.com/*`

Em seguida, configure a URL a seguir para que o tráfego realize o encaminhamento:

    `http://www.example.com/$1`

Nesse caso, se alguém fosse para:

    `example.com/some-particular-page.html`

Eles são redirecionados para:

    `http://www.example.com/some-particular-page.html`
