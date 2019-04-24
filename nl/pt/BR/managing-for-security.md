---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-26"

keywords: IBM CIS, optimal security, Security Level

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Gerencie seu IBM CIS para segurança ideal
{:#manage-your-ibm-cis-for-optimal-security}
As configurações de segurança do IBM Cloud Internet Services (CIS) incluem padrões protegidos projetados para evitar falsos positivos e influência negativa em seu tráfego. No entanto, essas configurações padrão protegidas não fornecem a melhor postura de segurança para cada cliente. Realize as etapas a seguir para garantir que sua conta do CIS esteja configurada de forma segura.

**Recomendações e melhores práticas:**

* Proteja endereços IP de origem efetuando proxy e aumentando a ofuscação
* Configure seu Nível de Segurança seletivamente
* Ative seu Web Application Firewall (WAF) com segurança

## Melhor prática 1: proteja seus endereços IP de origem
{:#best-practice-secure-origin-ip-address}

Quando é efetuado proxy de um subdomínio usando o IBM CIS, todo o tráfego é protegido porque nós respondemos ativamente com endereços IP específicos para o IBM CIS (por exemplo, todos os seus clientes se conectam a proxies do CIS primeiro e seus endereços IP de origem são obscurecidos).

### Use proxies do IBM CIS para todos os registros de DNS para tráfego HTTP(S) de sua origem
{:#use-cis-proxies-for-dns-records}

Para melhorar a segurança de seu endereço IP de origem, deve ser efetuado proxy de todo tráfego HTTP(S).

**Veja a diferença você mesmo - Consulte um registro sem proxy e com proxy:**

```
$ dig nonproxied.theburritobot.com +short
1.2.3.4 (O endereço IP da origem)

$ dig proxied.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (Endereços IP do CIS)
```

### Obscureça registros de origem não proxy com nomes não padrão
{:#obsure-non-proxied-origin-records-with-non-standard-names}
Quaisquer registros que não podem estar em proxy por meio do IBM CIS e que ainda usam seu IP de origem, tal como FTP, podem ser protegidos criando ofuscação adicional. Em particular, se você requer um registro para sua origem que não pode ter o proxy efetuado pelo IBM CIS, use um nome não padrão. Por exemplo, em vez de `ftp.example.com` use `[random word or-random characters].example.com.` Essa ofuscação torna as varreduras de dicionário de seus registros de DNS menos propensas a expor os endereços IP de sua origem.

### Use intervalos de IP separados para tráfego HTTP e não HTTP, se possível
{:#use-separate-ipranges-for-traffic}
Alguns clientes usam intervalos de IP separados para tráfego HTTP e não HTTP, permitindo, assim, que eles efetuem proxy de todos os registros que apontam para seu intervalo de IP HTTP e obscureçam todo tráfego não HTTP com uma sub-rede de IP diferente.

## Melhor prática 2: configure seu Nível de Segurança seletivamente
{:#best-practice-configure-security-level-selectively}
Seu **Nível de segurança** estabelece o sigilo de nosso **Banco de dados de reputação de IP**. Para evitar interações negativas ou falsos positivos, configure o **Nível de segurança** por domínio para aumentar a segurança onde necessário e diminuí-la onde apropriado.

### Aumente o nível de segurança para áreas sensíveis para 'alto'
{:#increase-security-level-for-sensitive-areas}
É possível aumentar essa configuração na página Segurança avançada para seu domínio ou incluindo uma **Regra de página** para páginas de administração ou de login, com o objetivo de reduzir as tentativas de força bruta:

1. Crie uma **Regra de página** com o padrão de URL de sua API (por exemplo, `www.example.com/wp-login`). 
2. Identifique a configuração de **Nível de segurança**.
3. Marque a configuração como **Alto**.
4. Selecione **Recurso de provisão**.

### Diminua o nível de segurança para caminhos ou APIs não sensíveis para reduzir falsos positivos
{:#decrease-security-level-non-sensitive-paths-reduce-false-positives}
Essa configuração pode ser diminuída para páginas gerais e tráfego da API: 

1. Crie uma **Regra de página** com o padrão de URL de sua API (por exemplo, `www.example.com/api / *`).
2. Identifique a configuração de **Nível de segurança**.
3. Mude o Nível de segurança para **Baixo** ou **Essencialmente desativado**.
4. Selecione **Recurso de provisão**.

### O que significam as configurações de Nível de Segurança?
{:#what-do-security-level-settings-mean}
Nossas configurações de Nível de Segurança estão alinhadas com as pontuações de ameaça que determinados endereços IP adquirem do comportamento malicioso em nossa rede. Uma pontuação de ameaça acima de 10 é considerada alta.

* **ALTO**: pontuações de ameaça maiores que 0 são desafiadas.
* **MÉDIO**: pontuações de ameaça maiores que 14 são desafiadas.
* **BAIXO**: pontuações de ameaça maiores que 24 são desafiadas.
* **ESSENCIALMENTE DESATIVADO**: pontuações de ameaça maiores que 49 são desafiadas.
* **OFF**: *Apenas Empresa* 
* **SOB ATAQUE**: deverá ser usado apenas quando seu website estiver sob um ataque DDoS. Os visitantes recebem uma página intersticial por cerca de cinco segundos enquanto o CIS analisa o tráfego e o comportamento para garantir que sejam visitantes legítimos tentando acessar seu website. **SOB ATAQUE** pode afetar algumas ações em seu domínio, como o uso de uma API. É possível configurar um nível de segurança customizado para sua API ou qualquer outra parte de seu domínio criando uma regra de página para essa seção.

Recomendamos que você revise as configurações de nível de segurança periodicamente e é possível localizar instruções em nosso [documento Melhores práticas para a configuração do CIS](/docs/infrastructure/cis?topic=cis-best-practices-for-cis-setup)

## Melhor prática 3: ative o Web Application Firewall (WAF) com segurança
{:#best-practice-activate-waf-safely}
Seu WAF está disponível na seção **Segurança**. Vamos percorrer essas configurações em ordem reversa para assegurar que seu WAF seja configurado o mais seguro possível antes de ativá-lo para seu domínio inteiro. Essas configurações iniciais podem reduzir falsos positivos preenchendo **Eventos de segurança** para ajustes adicionais. Seu WAF é atualizado automaticamente para manipular novas vulnerabilidades à medida que elas são identificadas.

O WAF protege você contra os seguintes tipos de ataques:
* Ataque de injeção de SQL
* Cross-site scripting
* Falsificação de site cruzado

O WAF contém um conjunto de regras padrão que inclui regras para parar os ataques mais comuns. No momento, permitimos que você ative ou desative as regras específicas do WAF e de ajuste nos conjuntos de regras do WAF. Consulte o documento [Conjunto de regras padrão do WAF](/docs/infrastructure/cis?topic=cis-waf-default-rule-set) para obter mais detalhes sobre o conjunto de regras padrão e o comportamento de cada regra.

Para obter mais informações sobre o WAF, consulte o [documento Conceitos do WAF](/docs/infrastructure/cis?topic=cis-web-application-firewall-concepts-q-a)

## Melhor prática 4: defina suas configurações de TLS
{:#best-practice-configure-tls-settings}
O IBM CIS fornece algumas opções para criptografar seu tráfego. Como um proxy reverso, fechamos as conexões TLS em nossos data centers e abrimos uma nova conexão TLS com seu servidor de origem.

O TLS oferece quatro modos de operação:
* **Desativado**: o TLS fica desativado nesse modo, ele não é recomendado.
* **Cliente para borda**: o TLS criptografa o tráfego do CIS para seus clientes, mas não do CIS para seus servidores de origem.
* **Flexível de ponta a ponta**: o TLS criptografa todo o tráfego; no entanto, é possível usar um certificado autoassinado para proteger o tráfego entre o CIS e seus servidores de origem.
* **Assinado pela CA de ponta a ponta**: o TLS criptografa todo o tráfego; deve-se usar um certificado assinado por uma CA.

Para obter mais detalhes sobre suas opções de TLS, consulte [este documento](/docs/infrastructure/cis?topic=cis-tls-options).

O IBM CIS permite usar certificados customizados ou você pode utilizar um certificado curinga provisionado para você pelo CIS.

### Upload de certificados customizados
{:#upload-custom-certs}
É possível fazer upload de seu certificado customizado clicando no botão **Incluir certificado** e inserindo seu certificado, a chave privada e o método de pacote configurável. Se você fizer upload de seu próprio certificado, obterá compatibilidade imediata com o tráfego criptografado e manterá o controle sobre seu certificado (por exemplo, um certificado de Validação estendida (EV)). Se fizer upload de um certificado customizado, você será responsável por gerenciá-lo. Por exemplo, o IBM CIS não rastreará a data de expiração do certificado. 

![certificado customizado](images/upload-custom-certificate.png)

### Pedido de certificados dedicados
{:#order-dedicated-certs}
O CIS torna o gerenciamento de seus certificados fácil, oferecendo certificados dedicados. Não é mais necessário gerar chaves privadas, criar solicitações de assinatura de certificado (CSR) ou lembrar-se de renovar os certificados. É possível solicitar um certificado dedicado clicando no botão **Incluir Certificado** e solicitando um certificado curinga ou inserindo nomes de host para solicitar um certificado customizado dedicado. Os tipos de certificado são:

 * Certificado SHA-2/ECDSA assinado usando a chave P-256, 
 * Certificado SHA-2/RSA assinado usando a chave RSA de 2048 bits e 
 * Certificado SHA-1/RSA assinado usando a chave RSA de 2048 bits. 
 
O CIS pode realizar emissões para todos os TLDs, exceto para `.cu`, `.iq`, `.ir`, `.kp`, `.sd`, `.ss` e `.ye`. O CIS gerencia a data de expiração. Para editar os nomes de host em seu certificado dedicado customizado, reordene-os e, em seguida, exclua-os. Por exemplo, você solicita um certificado dedicado customizado com o nome de host `alpha.yourdomain.com`. Para incluir o nome de host `beta.yourdomain.com` em seu certificado dedicado customizado, solicite outro certificado dedicado customizado com os nomes de host `alpha.yourdomain.com` e `beta.yourdomain.com`. Em seguida, _deve-se_ excluir o certificado dedicado customizado original.

Em seu primeiro pedido, ocorre um processo de Validação de Controle de Domínio (DCV) de certificado dedicado, que gera um registro TXT correspondente. Se você excluir o registro TXT, o processo DCV ocorrerá novamente quando você solicitar outro certificado dedicado. Se você excluir um certificado dedicado, o registro TXT correspondente ao processo DCV não será excluído.
{:note}

A seguir estão os erros comuns vistos ao solicitar certificados dedicados:
* `Erro ao conectar-se ao serviço de certificado.`
* `Erro ao solicitar a partir do serviço de certificado.`
{:note}

Se um erro ocorrer em sua solicitação de certificado, atualize a página e tente novamente.

![dedicated-certificate](images/order-dedicated-certificate.png)

### Utilize um certificado provisionado
{:#utilize-provisioned-certificate}
A IBM tem parceria com várias Autoridades de Certificação (CAs) para fornecer certificados curinga de domínio para nossos clientes. A verificação manual pode ser necessária para configurar esses certificados. Sua equipe de suporte pode ajudá-lo a executar essas etapas adicionais.

### Prioridade de certificado em nossa borda
{:#certificate-prioirity-at-our-edge}
A prioridade pela qual os certificados são exibidos em nossa borda é:
1. Customizado e transferido por upload
2. Customizado dedicado
3. Curinga dedicado
4. Universal

### Versão mínima do TLS
{:#security-minimum-tls-version}
Consulte [Versão mínima do TLS](/docs/infrastructure/cis?topic=cis-tls-options#minimum-tls-version). Os níveis mais altos do TLS fornecem mais segurança, mas podem evitar que os clientes se conectem ao seu site.
