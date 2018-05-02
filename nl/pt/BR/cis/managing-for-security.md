---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gerencie seu IBM CIS para segurança ideal

As configurações de segurança do IBM Cloud Internet Services (CIS) incluem padrões protegidos projetados para evitar falsos positivos e influência negativa em seu tráfego. No entanto, essas configurações padrão protegidas não fornecem a melhor postura de segurança para cada cliente. Execute as etapas a seguir para certificar-se de que sua conta do CIS esteja configurada de uma maneira segura:

**Recomendações e melhores práticas:**

* Proteja endereços IP de origem efetuando proxy e aumentando a ofuscação
* Configure seu Nível de Segurança seletivamente
* Ative seu Web Application Firewall (WAF) com segurança

## Melhor prática 1: proteja seus endereços IP de origem

Quando é efetuado proxy de um subdomínio usando o IBM CIS, todo o tráfego é protegido porque nós respondemos ativamente com endereços IP específicos para o IBM CIS (por exemplo, todos os seus clientes se conectam a proxies do CIS primeiro e seus endereços IP de origem são obscurecidos).

### Use proxies do IBM CIS para todos os registros de DNS para tráfego HTTP(S) de sua origem

Para melhorar a segurança de seu endereço IP de origem, deve ser efetuado proxy de todo tráfego HTTP(S).

**Veja a diferença você mesmo - Consulte um registro sem proxy e com proxy:**

```
$ dig greycloud.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig orangecloud.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```

### Obscureça registros de origem não proxy com nomes não padrão
Quaisquer registros que não podem estar em proxy por meio do IBM CIS e que ainda usam seu IP de origem, tal como FTP, podem ser protegidos criando ofuscação adicional. Em particular, se você requer um registro para sua origem que não pode ter o proxy efetuado pelo IBM CIS, use um nome não padrão. Por exemplo, em vez de `ftp.example.com` use `[random word or-random characters].example.com.` Essa ofuscação torna menos provável que as varreduras de dicionário de seus registros de DNS exponham seus endereços IP de origem.

### Use intervalos de IP separados para tráfego HTTP e não HTTP, se possível
Alguns clientes usam intervalos de IP separados para tráfego HTTP e não HTTP, permitindo, assim, que eles efetuem proxy de todos os registros que apontam para seu intervalo de IP HTTP e obscureçam todo tráfego não HTTP com uma sub-rede de IP diferente.

## Melhor prática 2: configure seu Nível de Segurança seletivamente
Seu **Nível de segurança** estabelece o sigilo de nosso **Banco de dados de reputação de IP**. O IBM CIS vê mais de 1 bilhão de endereços IP exclusivos a cada mês, de mais de 7 milhões de websites, o que permite que nosso sistema identifique agentes maliciosos e impeça que eles atinjam seus ativos da web. Para evitar interações negativas ou falsos positivos, configure o **Nível de segurança** por domínio para aumentar a segurança onde necessário e diminuí-la onde apropriado.

### Aumente o nível de segurança para áreas sensíveis para 'alto'
É possível aumentar essa configuração incluindo uma **Regra de página** para páginas de administração ou páginas de login, para reduzir tentativas de força bruta:

1. Crie uma **Regra de página** com o padrão de URL de sua API (por exemplo, `www.example.com/wp-login`). 
2. Identifique a configuração de **Nível de segurança**.
3. Marque a configuração como **Alto**.
4. Selecione **Recurso de provisão**.

### Diminua o nível de segurança para caminhos ou APIs não sensíveis para reduzir falsos positivos
Essa configuração pode ser diminuída para páginas gerais e tráfego da API: 

1. Crie uma **Regra de página** com o padrão de URL de sua API (por exemplo, `www.example.com/api / *`).
2. Identifique a configuração de **Nível de segurança**.
3. Mude o Nível de segurança para **Baixo** ou **Essencialmente desativado**.
4. Selecione **Recurso de provisão**.

### O que significam as configurações de Nível de Segurança?
Nossas configurações de Nível de Segurança estão alinhadas com as pontuações de ameaça que determinados endereços IP adquirem do comportamento malicioso em nossa rede. Uma pontuação de ameaça acima de 10 é considerada alta.

* **ALTO**: pontuações de ameaça maiores que 0 são desafiadas.
* **MÉDIO**: pontuações de ameaça maiores que 14 são desafiadas.
* **BAIXO**: pontuações de ameaça maiores que 24 são desafiadas.
* **ESSENCIALMENTE DESATIVADO**: pontuações de ameaça maiores que 49 são desafiadas.

Recomendamos que você revise as configurações de nível de segurança periodicamente e é possível localizar instruções em nosso [documento Melhores práticas para a configuração do CIS](best-practices.html)

## Melhor prática 3: ative o Web Application Firewall (WAF) com segurança
Seu WAF está disponível na seção **Segurança**. Vamos percorrer essas configurações em ordem reversa para assegurar que seu WAF seja configurado o mais seguro possível antes de ativá-lo para seu domínio inteiro. Essas configurações iniciais podem reduzir falsos positivos preenchendo o Aplicativo de Tráfego com eventos do WAF para ajuste adicional. Seu WAF é atualizado automaticamente para manipular novas vulnerabilidades à medida que elas são identificadas.

O WAF protege você contra os seguintes tipos de ataques:
* Ataque de injeção de SQL
* Cross-site scripting
* Falsificação de site cruzado

O WAF contém um conjunto de regras padrão que inclui regras para parar os ataques mais comuns. Neste momento, nós permitimos que você ative ou desative o WAF. Consulte o documento [Conjunto de regras padrão do WAF](waf-rule-set.html) para obter mais detalhes sobre o conjunto de regras padrão e o comportamento de cada regra.

Para obter mais informações sobre o WAF, consulte o [documento Conceitos do WAF](waf-concept.html)

## Melhor prática 4: defina suas configurações de TLS
O IBM CIS fornece algumas opções para criptografar seu tráfego. Como um proxy reverso, fechamos conexões TLS em nossos data centers e abrimos uma nova conexão TLS para seu servidor de origem.

O TLS oferece quatro modos de operação:
* **Desativado**: o TLS fica desativado nesse modo, ele não é recomendado.
* **Cliente para borda**: o TLS criptografa o tráfego do CIS para seus clientes, mas não do CIS para seus servidores de origem.
* **Flexível de ponta a ponta**: o TLS criptografa todo o tráfego; no entanto, é possível usar um certificado autoassinado para proteger o tráfego entre o CIS e seus servidores de origem.
* **Assinado pela CA de ponta a ponta**: o TLS criptografa todo o tráfego; deve-se usar um certificado assinado por uma CA.

Para obter mais detalhes sobre suas opções de TLS, consulte [este documento](ssl-options.html).

O IBM CIS permite usar certificados customizados ou você pode utilizar um certificado curinga provisionado para você pelo CIS.

### Faça upload de um certificado customizado
É possível fazer upload de seu certificado customizado clicando no botão **Incluir certificado** e inserindo seu certificado, a chave privada e o método de pacote configurável. Se você fizer upload de seu próprio certificado, obterá compatibilidade imediata com o tráfego criptografado e manterá o controle sobre seu certificado (por exemplo, um certificado de Validação estendida (EV)). Se fizer upload de um certificado customizado, você será responsável por gerenciá-lo. Por exemplo, o IBM CIS não rastreia datas de expiração de certificado. 

![certificado customizado](images/upload-custom-certificate.png)

### Utilize um certificado provisionado
A IBM tem parceria com várias Autoridades de Certificação (CAs) para fornecer certificados curinga de domínio para nossos clientes. A verificação manual pode ser necessária para configurar esses certificados. Sua equipe de suporte pode ajudá-lo a executar essas etapas adicionais.
