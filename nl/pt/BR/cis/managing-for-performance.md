---
  
copyright:
   years: 2018
lastupdated: "2018-03-16"
 
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Gerencie sua implementação do CIS para melhor desempenho

O IBM Cloud Internet Services (CIS) pode fornecer a melhor experiência para seus clientes porque ele otimiza suas imagens e armazena o conteúdo da web o mais próximo possível de seus usuários finais. Seu conteúdo é carregado por meio de servidores de borda de proxy (o que reduz a latência).

Com o IBM CIS, é possível aprimorar ainda mais o desempenho de seu site usando as melhores práticas para acelerar o carregamento de seu conteúdo da web. A seguir estão algumas melhores práticas específicas para aprimorar o desempenho de seu conteúdo da web dentro do CIS.

**Melhores práticas recomendadas:**

 * Armazene em cache o máximo possível de seu conteúdo da web estático e semiestático
 * Para conteúdo orientado a eventos, limpe seu cache usando a API
 
## Melhor prática 1: armazene em cache o máximo possível de conteúdo estático e semiestático

  * Ative **Armazenar tudo em cache** para páginas da web HTML estáticas
  * Use **Tempo de vida (TTL)** conservador para seu conteúdo que muda ocasionalmente

### Utilize TTLs (Time-to-Lives) conservadores para conteúdo que muda ocasionalmente
Se o conteúdo raramente muda, é possível configurar um TTL conservador para utilizar nosso cache o máximo possível. Se você tiver uma alta porcentagem de solicitações de revalidação, será possível aumentar os TTLs de seu conteúdo sem afetar negativamente seus clientes. Usando o cache de maneira mais eficaz, você aumentará o desempenho porque revalidará com menos frequência.

### Como sei se os itens estão sendo armazenados em cache?
O IBM CIS inclui o cabeçalho de resposta `CF-Cache-Status` quando ele tenta armazenar um objeto em cache. Se o armazenamento em cache for bem-sucedido, o valor desse cabeçalho indicará seu status com uma destas palavras-chave:

* **MISS:** o ativo ainda não estava no cache ou o TTL expirou (isto é, ele atingiu a idade máxima de controle de cache igual a 0).
* **HIT:** o ativo foi entregue por meio do cache.
* **EXPIRED:** esse ativo foi entregue por meio do cache, mas a próxima solicitação exigirá revalidação.
* **REVALIDATED:** o ativo foi entregue por meio do cache. O TTL foi expirado, mas uma solicitação `If-Modified-Since` para a origem indicou que o recurso não mudou. Portanto, a versão em cache é considerada válida novamente.

## Melhor prática 2: para conteúdo orientado a eventos, use a API para limpar o cache
Por exemplo, toda vez que um novo post fosse incluído em seu blog, você poderia facilmente limpar o cache do CIS usando um comando de API. É comum ver o conteúdo orientado a eventos e nós o facilitamos para garantir que nenhum conteúdo antigo atinja seus usuários. Os comandos para limpar o cache imediatamente em toda a nossa rede global são listados a seguir. É possível usar o aplicativo de armazenamento em cache ou você pode usar a API.

  * Limpar o cache usando uma Cache-Tag
  * Limpar o cache globalmente
  * Limpar o cache por Regra de página
  * Usar recursos de armazenamento em cache avançados

### Limpar o cache por Cache-Tag
Cache-Tags permitem que você defina depósitos de conteúdo que deseja limpar. É uma excelente maneira de combinar objetos que normalmente são mudados juntos. Por exemplo, uma postagem do blog HTML e todo o seu conteúdo de imagem poderiam ser identificados juntos. O conteúdo exclusivo do dispositivo móvel também pode ser empacotado usando cache-tags, de modo que você possa limpar tudo ao enviar por push uma nova atualização para seu domínio móvel.

### Limpar o cache globalmente
Você também tem a opção de forçar todo o nosso cache para revalidação. É possível reconfigurar todos os objetos armazenados em cache para que cada solicitação seja roteada para o servidor de origem.

### Limpar o cache por Regra de página
Regras de Página permitem que você limpe o cache inteiro com base em uma expressão regular. É possível utilizar uma Regra de Página predefinida e revalidar todas as ocorrências com relação a essa Regra de Página. É possível criar até 50 Regras de Página por página.

### Usar recursos de armazenamento em cache avançados

**Efetuar bypass do cache no cookie:** configurado em uma Regra de Página, esse recurso permite servir um objeto armazenado em cache, a menos que exista um cookie com um nome específico. Por exemplo, é possível servir uma versão em cache da página inicial, a menos que você localize um cookie`SessionID` indicando que o cliente está com login efetuado e, portanto, deve ser apresentado com conteúdo personalizado.
