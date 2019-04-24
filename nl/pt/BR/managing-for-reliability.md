---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gerencie a implementação de seu IBM CIS para confiabilidade ideal

Para atingir a confiabilidade ideal para a sua implementação do IBM CIS, é possível definir uma configuração útil do DNS e configurar os Balanceadores de Carga Globais. Para confiabilidade adicional, é possível usar nossas Regras de Página para ter certeza de que seu conteúdo da web seja entregue aos seus clientes, mesmo que seu servidor de origem ou cache tenha um problema. Este documento fornece detalhes sobre algumas boas práticas para tornar sua implementação do IBM CIS idealmente confiável.

Geralmente, nossas melhores práticas recomendadas são essas:

 * Configure o DNS para aproveitar os servidores proxy do IBM CIS e outros recursos
 * Use um ou mais Balanceadores de Carga Globais para distribuir o tráfego de seu site uniformemente
 * Configure Regras de Página apropriadas para gerenciar seu armazenamento em cache e outras opções

Cada um desses itens fornece determinada funcionalidade que pode ser usada para criar uma implementação do CIS mais confiável.

Observe que a interface do CIS é organizada em seções para *segurança*, *confiabilidade* e *desempenho*. O menu de navegação principal é mostrado na figura a seguir, com os Balanceadores de Carga Globais e itens de menu de DNS revelados:

![DNS de navegação à esquerda](images/cis-left-navigation.png)


## Configurando o DNS
 
 Para começar a definir sua configuração do DNS, selecione **DNS** no menu de navegação, conforme mostrado anteriormente.
 
 Para obter informações detalhadas sobre como configurar e gerenciar o DNS para confiabilidade, [consulte este documento](dns.html#setting-up-your-domain-name-system-dns-for-ibm-cis).


## Configurando balanceadores de carga globais


Para começar a configurar seus Balanceadores de Carga Globais, selecione **Balanceadores de carga globais** no menu de navegação.

Para obter informações detalhadas sobre como configurar e gerenciar seus Balanceadores de Carga Globais, [consulte este documento](glb.html#global-load-balancer-glb-concepts).

## Usando Regras de Página para aumentar a confiabilidade

A seguir estão algumas configurações de Regra de Página recomendadas para fornecer máxima confiabilidade ao seu site:

 * Sempre on-line
 * Controle de cache de origem
 * URL de encaminhamento

 ## Sempre on-line

É possível usar a configuração da Regra de Página **Sempre on-line** para manter uma versão limitada de seu site on-line se seu servidor
ficar inativo.

Com **Sempre on-line**, seu servidor ficará inativo e o IBM CIS entregará páginas de nosso cache para que seus visitantes ainda vejam algumas das páginas que estão tentando visitar. Seus visitantes verão uma mensagem na parte superior da página informando que eles estão no modo de navegação off-line. Sempre on-line retorna um status HTTP 503, no entanto, 503 também é usado por muitos outros aplicativos da web. Quando o servidor ficar on-line novamente, o IBM CIS colocará os usuários de volta na navegação regular.

Se o IBM CIS não tiver a página solicitada em seu cache, seu visitante verá uma página de erro que permite que ele saiba que a página do website que está sendo solicitada está off-line.

### Como configurar Sempre on-line

Para ativar **Sempre on-line**, siga estas etapas:

 * Use o menu de navegação para selecionar Regras de página em Desempenho.
 * Crie uma Regra de Página com o padrão de URL de seu domínio.
 * Inclua a configuração **Sempre on-line** com o comutador ativado.
 * Selecione Recurso de provisão.

 ### Limitações de Sempre on-line

 * **Sempre on-line** armazena em cache os primeiros 10 links de seu HTML raiz, em seguida, apenas os primeiros links de cada uma dessas páginas e, por fim, os primeiros links de cada uma dessas páginas subsequentes. Isso significa que apenas algumas páginas em seu site estarão visíveis quando seu servidor de origem ficar inativo.

 * Sites incluídos recentemente não terão um cache grande de seus sites disponível, o que significa que **Sempre on-line** poderá não funcionar se você incluiu o site há apenas alguns dias.

 * O CIS não será capaz de mostrar conteúdo privado ou de manipular o envio de formulário (POSTs) se seu servidor estiver inativo. Será mostrado um erro aos visitantes nas páginas de check-out ou nos itens que requerem um login para visualização.

 * Para acionar **Sempre on-line**, o seu servidor da web deve estar retornando um tempo limite de Código de erro de HTTP padrão 502 ou 504. Sempre on-line também funciona quando encontramos problemas ao contatar sua origem (Erros 521 e 523), tempos limites (522 e 524), erros de SSL (525 e 526) ou um erro desconhecido (520). **Sempre on-line** não será acionado para outros códigos de resposta HTTP, como 404s, 500, 503, erros de conexão com o banco de dados, erro interno do servidor ou respostas vazias do servidor.

 * **Sempre on-line** não funcionará se uma regra de página "Armazenar tudo em cache" estiver ativada com o "TTL de expiração do edge cache" menor que a frequência de armazenamento em cache (clientes Free: 7 dias, clientes Pro: 3 dias e clientes Business e Enterprise: 1 dia), porque "TTL de expiração do edge cache" faz com que o cache **Sempre on-line** seja limpo no intervalo correspondente.

## Controle de cache de origem

É possível usar a configuração da Regra de Página **Controle de cache de origem** para determinar qual conteúdo de sua origem é armazenado em cache e a frequência com que o conteúdo é atualizado, o que tem um efeito sobre a confiabilidade e o desempenho. Por padrão, se nenhuma configuração muda e nenhum cabeçalho que impede o armazenamento em cache é enviado de seu servidor de origem, o IBM CIS armazena todo o conteúdo estático em cache com determinadas extensões. Esses tipos de conteúdo incluem imagens, CSS e JavaScript. Usa-se esse armazenamento em cache principalmente por motivos de desempenho.

Para configurar o **Controle de cache de origem**, você utilizaria Regras de Página para ativar cabeçalhos específicos que fornecem o comportamento desejado com relação a cada recurso de seu conteúdo. Para entender como usar o **Controle de cache de origem**, é necessária uma explicação mais geral das Regras de Página e do comportamento geral do armazenamento em cache para o CIS para fornecer contexto, o que você verá nas várias seções a seguir. Existem três métodos que podem ser usados para controlar o armazenamento em cache em geral e **Controle de cache de origem** é o segundo.

A configuração de **Controle de cache de origem** chama regras de armazenamento em cache que buscam aderir estritamente às melhores práticas e RFCs da Internet, principalmente com relação à revalidação. Por exemplo, o comportamento padrão do CIS com `max-age=0` não é armazenar em cache de maneira nenhuma, enquanto que a configuração de **Controle de cache de origem** armazena em cache, mas ele é sempre revalidado.

### Como configurar o Controle de cache de origem

 * Use o menu de navegação para selecionar Regras de página em Desempenho.
 * Crie uma Regra de página com o padrão de URL que faz referência a seu domínio.
 * Inclua a configuração **Controle de cache de origem** com o comutador ativado.
 * Selecione Recurso de provisão.

### Precedência da regra de página

Duas Regras de Página específicas têm precedência para armazenamento em cache geral:

 * Se uma Regra de Página tiver o **Nível de cache** configurado como `Bypass`, os recursos que correspondem a essa Regra de Página não serão armazenados em cache. O IBM CIS ainda age como um proxy e nossos outros recursos de desempenho permanecem ativos. No entanto, seu conteúdo não será entregue por meio de nosso cache, ele será buscado diretamente em seu servidor de origem.

 * Se uma Regra de Página tiver o **Nível de cache** configurado como `Armazenar tudo em cache`, os recursos que correspondem à Regra de Página serão armazenados em cache. **Usar essa configuração de Regra de Página é a única maneira de nos dizer para armazenar em cache recursos além do que consideramos estático, incluindo HTML.**

Se nenhuma Regra de Página for configurada, usaremos o modo de armazenamento em cache `Padrão`, que é baseado na extensão do recurso. Nós armazenaremos em cache apenas recursos estáticos (conforme mencionado anteriormente).

### Cabeçalhos de controle de cache de origem

A segunda maneira de alterar o que o IBM CIS armazenará em cache é por meio de cabeçalhos de armazenamento em cache enviados da origem. O CIS respeitará essas configurações, mas será possível substituí-las especificando uma configuração de Regra de Página **TTL de edge cache**. A seguir estão os cabeçalhos que consideramos ao decidir quais recursos de sua origem armazenar em cache:

 * Se o cabeçalho **Cache-Control** for configurado como `private`, `no-store`, `no-cache` ou `max-age=0` ou se houver um cookie na resposta, o IBM CIS não armazenará o recurso em cache. Observe que o material sigiloso não deve ser armazenado em cache, portanto, é possível considerar o uso de um desses cabeçalhos nesse caso.

 * Se o cabeçalho **Cache-Control** for configurado como `public` e o `max-age` for maior que 0 ou se os cabeçalhos `Expires` forem configurados a qualquer momento no futuro, armazenaremos o recurso em cache.

**Nota:** conforme as regras de RFC, `Cache-Control: max-age` supera cabeçalhos `Expires`. Se virmos ambos e eles forem conflitantes, `max-age` vencerá.

### Usando o cabeçalho 's-maxage'

A terceira forma de controlar o comportamento do armazenamento em cache e o comportamento do armazenamento em cache do navegador juntos é usando o cabeçalho Cache-Control `s-maxage`.

Normalmente, nós respeitamos a diretiva `max-age`:

`Cache-Control: max-age=1000`

Mas, se você desejar especificar um tempo limite de cache que seja diferente do navegador, poderemos usar `s-maxage`. A seguir há um exemplo que informa ao IBM CIS para armazenar o objeto em cache por 200 segundos e ao navegador para armazenar o objeto em cache por 60 segundos.

`Cache-Control: s-maxage=200, max-age=60`

Basicamente, `s-maxage` destina-se a ser seguido APENAS por proxies reversos (de modo que o navegador deve ignorá-lo), por outro lado, no entanto, nós (IBM CIS) damos prioridade a `s-maxage` se ele está presente. Nós respeitaremos o valor que for superior: a configuração de cache do navegador ou o cabeçalho `max-age`.

### Resumo sobre cabeçalhos de controle de cache e Regras de Página para confiabilidade

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

 * Para armazenar mais em cache, crie uma Regra de Página com **Nível de cache** configurado como "Armazenar tudo em cache" na URL desejada (se seu servidor da web retornar um 404 ao solicitar essa URL, armazenaremos esse resultado em cache por apenas 5m).

 * Para evitar o armazenamento em cache em uma URL, crie uma Regra de Página com **Nível de cache** configurado como "Efetuar bypass".


 ## URL de encaminhamento

Para assegurar que seu conteúdo esteja sempre disponível (HA), é possível criar uma Regra de Página com a configuração **URL de encaminhamento** para ser usada caso seu site esteja indisponível.

 **Nota:** quando você ativa uma **URL de encaminhamento**, todas as outras configurações são desativadas porque você está enviando todo o tráfego para outra URL.

### Como configurar uma URL de encaminhamento

 * Use o menu de navegação para selecionar Regras de página em Desempenho.
 * Crie uma Regra de página com o padrão de URL que faz referência a seu domínio.
 * Inclua a configuração **URL de encaminhamento**.
 * Selecione o tipo de encaminhamento e insira a URL de destino.
 * Selecione Recurso de provisão.

### Exemplos de encaminhamento:

Imagine que você deseja tornar mais fácil para qualquer pessoa acessar uma URL como:

    *www.example.com/+

    *example.com/+

Esse padrão corresponderá:

    http://example.com/+
    http://www.example.com/+
    https://www.example.com/+
    https://blog.example.com/+
    https://www.blog.example.com/+
    Etc...

Isto não corresponderá:

    http://www.example.com/blog/+  [extra directory before the +]
    http://www.example.com+  [no trailing slash]


Depois de ter criado o padrão que corresponde ao que você deseja, inclua a configuração **URL de encaminhamento**, selecione o tipo de encaminhamento e insira a URL de destino. Por exemplo:

    https://plus.google.com/yourid

Selecione Recurso de provisão. Dentro de alguns segundos quaisquer solicitações que correspondam ao padrão serão encaminhadas à nova URL com o encaminhamento especificado.

### Opções de encaminhamento avançadas:

Se você usar um redirecionamento básico, tal como o encaminhamento do domínio-raiz para www.yourdomain.com, perderá qualquer outra coisa na URL. Por exemplo, você poderia configurar o padrão:

    example.com

E fazê-lo encaminhar para:

    http://www.example.com

Mas se alguém inserisse:

    example.com/some-particular-page.html

Ele seria redirecionado para:

    www.example.com

em vez de

    www.example.com/some-particular-page.html

A solução é usar variáveis. Cada curinga corresponde a uma variável que pode ser referenciada no endereço de encaminhamento. As variáveis são representadas por um `$` seguido por um número. Para referir-se ao primeiro curinga, você usaria `$1`, para referir-se ao segundo curinga, você usaria `$2`, e assim por diante. Para corrigir o encaminhamento da raiz para `www` no exemplo anterior, você poderia usar o mesmo padrão:

    example.com/*

Então, você configuraria a URL a seguir para a qual o tráfego seria encaminhado:

    http://www.example.com/$1

Nesse caso, se alguém fosse para:

    example.com/some-particular-page.html

Ele seria redirecionado para:

    http://www.example.com/some-particular-page.html
