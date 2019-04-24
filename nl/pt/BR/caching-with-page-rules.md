---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Use Page Rules, standard cache levels, Custom Caching Sets

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Use as regras de página com o armazenamento em cache
{:#use-page-rules-with-caching}

As Regras de Página oferecem a capacidade de executar várias ações com base na URL da página, tal como criar redirecionamentos, ajustar o comportamento do armazenamento em cache ou ativar e desativar serviços.

Uma Regra de Página entrará em vigor em um padrão de URL especificado que corresponda ao formato a seguir:

`<scheme>://<hostname><:port>/<path>`

Por exemplo:

`https://www.example.com:80/image.png`

Os componentes `scheme` e `port` são opcionais. Se o componente `scheme` for omitido, o formato aceitará os protocolos `http://` e `https://`. Se `port` não for especificado, a regra corresponderá a todas as portas. É possível executar correspondências curinga básicas usando um símbolo `*` em seu padrão de regra, permitindo que ele corresponda a uma série de padrões similares.

**Coisas importante para lembrar com relação às Regras de Página:**

 * Somente uma Regra de Página entrará em vigor em qualquer solicitação determinada.
 * As Regras de Página têm prioridade em uma ordem de cima para baixo. Quando uma URL corresponde a uma regra, apenas essa regra é aplicada; ou seja, se uma Regra de Página já foi acionada em uma solicitação, quaisquer regras subsequentes que também correspondam ao padrão de URL não entrarão em vigor. 
 * Como uma regra geral, recomendamos ordenar suas regras da mais específica para a menos específica.
 * As Regras de Página podem ser desativadas, nesse caso elas não executarão nenhuma ação, mas ainda poderão ser vistas na lista e editadas. Configurar o comutador *Ativado* para "Desativado" cria uma Regra de Página que está desativada inicialmente.


## Encaminhamento (Redirecionamento de URL)
{:#forwarding-url-redirection}

Redireciona uma URL para outra usando um redirecionamento de HTTP 301 ou 302. Os conteúdos de qualquer seção de uma URL à qual um curinga corresponda podem ser referenciados usando a sintaxe `$X`. O `X` indica o índice de um glob no padrão: `$1` é substituído pela primeira correspondência curinga, `$2` pela segunda correspondência curinga, e assim por diante.

Por exemplo, suponha que você configure a seguinte regra:

![imagem](images/url-redirection-example.png)

Aqui, uma solicitação para `www.example.com/stuff/things` será redirecionada para `http://example.com/stuff/things`.

Tenha cuidado para não criar um redirecionamento no qual o domínio aponte para si mesmo como um destino. Esse erro pode causar um erro de redirecionamento infinito e as URLs afetadas não serão capazes de resolver.
{:note}


## Redirecionamento para HTTPS
{:#redirecting-to-https}

Se desejar redirecionar seus visitantes para usar HTTPS, use a configuração **Sempre usar HTTPS** em vez de:

![imagem2](images/url-matching-patterns.png)


## Armazenamento em cache customizado
{:#custom-caching}

Configura o comportamento de armazenamento em cache para qualquer URL correspondente ao padrão de Regra de Página, usando qualquer um dos níveis de cache padrão. Configurar **Nível de cache** como **Armazenar tudo em cache** armazena em cache qualquer conteúdo, mesmo que ele não seja um de nossos tipos de arquivo estático padrão. Configurar **Nível de cache** com a configuração **Efetuar bypass** evita o armazenamento em cache nessa URL.

Ao especificar o nível de cache usando Regras de página, é possível configurar um **TTL de edge cache**, que controla por quanto tempo o CIS manterá os arquivos em nosso cache.

**TTL de cache do navegador** controla por quanto tempo os recursos armazenados em cache pelos navegadores do cliente permanecerão válidos. Se um navegador solicitar um recurso novamente e o TTL não tiver expirado, o navegador receberá uma resposta `HTTP 304 (Not Modified)`. É possível configurar o intervalo de TTLs de 30 minutos a 1 ano.

Nem todos os comportamentos de armazenamento em cache padrão são estritamente compatíveis com RFC. A configuração de **Controle de cache de origem** por meio de Regras de Página usa um conjunto mais recente de regras de armazenamento em cache que visa aderir mais estreitamente aos RFCs, principalmente com relação à revalidação. Por exemplo, nosso comportamento padrão com `max-age=0` é não armazenar em cache de maneira nenhuma, enquanto que a configuração de **Controle de cache de origem** armazena em cache, mas ele sempre é revalidado.

O exemplo a seguir configura uma Regra de Página para armazenar em cache tudo o que está localizado na pasta `/images`. Os recursos armazenados em cache expiram em 30 minutos no navegador do usuário e eles expiram após um dia nos data centers do IBM CIS:

![imagem3](images/url-example.png)

**Fornecer conteúdo antigo** fornece páginas de nosso cache, mesmo quando seu servidor fica inativo. Os visitantes veem uma versão limitada de seu site, com uma mensagem que indica que eles estão no modo de navegação off-line. 

Esse recurso retorna um status HTTP 503. Quando os servidores estiverem on-line novamente, o CIS levará os visitantes à navegação regular.

Se a página solicitada não estiver no cache, o visitante verá uma página de erro que informará que ela está off-line.
Se uma regra de página **Armazenar tudo em cache** estiver ativada com prazos de expiração inferiores à frequência do armazenamento em cache, **Fornecer conteúdo antigo** será limpo no intervalo correspondente.
{:note}
