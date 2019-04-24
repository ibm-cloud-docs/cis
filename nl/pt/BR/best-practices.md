---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Best practices, CIS setup

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Melhores práticas para a configuração do CIS
{:#best-practices-for-cis-setup}

Como o IBM CIS está posicionado na borda de sua rede, será necessário efetuar algumas etapas para garantir uma fácil integração com seus serviços do CIS. A seguir estão algumas melhores práticas recomendadas para integrar o CIS com seus servidores de origem. 

É possível executar essas etapas antes ou depois que mudar seu DNS e ativar nosso serviço de proxy. Essas recomendações permitem que o IBM CIS se conecte aos seus servidores de origem corretamente. Eles o ajudarão a evitar quaisquer problemas com o tráfego da API ou HTTPS e ajudarão seus logs a capturar os endereços IP corretos de seus clientes, em vez dos endereços IP do CIS de proteção.

A seguir está relacionado o que precisará ser configurado:

 * Melhor prática 1: restaure os IPs de origem de seus clientes
 * Melhor prática 2: incorpore endereços IP do CIS
 * Melhor prática 3: certifique-se de que suas configurações de segurança não interfiram no tráfego da API
 * Melhor prática 4: defina suas configurações de segurança o mais estritamente possível
 
## Melhor prática 1: saiba como restaurar os IPs de origem de seus clientes
{:#best-practice-know-how-to-restore-origininating-ip}

Como um proxy reverso, fornecemos o IP de origem nestes cabeçalhos:

  * `CF-Connecting-IP`
  * `X-Forwarded-For`
  * `True-Client-IP` (opcional)

É possível restaurar os endereços IP do usuário usando uma variedade de ferramentas, para infraestruturas como Apache, Windows IIS e NGINX.

## Melhor prática 2: incorpore endereços IP do CIS para tornar a integração mais fácil
{:#best-practice-incorporate-cis-ip-addresses}

A seguir estão as duas etapas a serem realizadas:

  * Remova qualquer limitação de taxa de endereços IP do CIS
  * Configure suas ACLs para permitir apenas endereços IP do CIS e outras partes confiáveis

É possível localizar a lista atualizada de intervalos de IP para o IBM CIS [neste local](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses).

## Melhor prática 3: revise suas configurações de segurança para garantir que elas não interfiram no tráfego da API
{:#best-practice-review-security-settings-interference}

O IBM CIS geralmente acelera o tráfego da API removendo a sobrecarga de conexão. No entanto, a postura de segurança padrão pode interferir em muitas chamadas API. Recomendamos que você execute algumas ações para evitar a interferência em seu tráfego de API quando o proxy estiver ativo.

 * Desative recursos de segurança seletivamente, usando os recursos de **Regras de página**.
   * Crie uma Regra de Página com o padrão de URL de sua API, tal como `api.example.com`
   * Inclua os comportamentos de regra a seguir:
     * Selecione **Nível de segurança** para **Essencialmente desativado**
     * Selecione **TLS** para **Desativado**
     * Selecione **Verificação de integridade do navegador** para **Desativado**
   * Selecione **Provisionar recurso**

 * Como alternativa, é possível desativar **Web Application Firewall** globalmente na página Segurança.

| *O que a Verificação de Integridade do Navegador faz?* | 
|------------------------------------------------|
| *A verificação de integridade do navegador procura cabeçalhos de HTTP que são comumente abusados por remetentes de spam. Ela impede que o tráfego com esses cabeçalhos acesse sua página. Ela também bloqueia os visitantes que não têm um agente do usuário ou quem inclui um agente do usuário não padrão (essa tática é comumente utilizada por robôs, crawlers ou APIs de abuso).* |

## Melhor prática 4: defina suas configurações de segurança o mais estritamente possível
{:#best-practice-configure-stict-security-settings}

O CIS fornece algumas opções para criptografar seu tráfego. Como um proxy reverso, fechamos as conexões TLS em nossos data centers e abrimos uma nova conexão TLS para seus servidores de origem. Para sua finalização com o CIS, é possível fazer upload de um certificado customizado por meio de sua conta, é possível usar um certificado curinga provisionado para você pelo CIS ou ambos.

### Faça upload de um certificado customizado
{:#strict-upload-custom-cert}
 
É possível fazer upload de sua chave pública e privada ao criar um domínio corporativo. Se você fizer upload de seu próprio certificado, obterá compatibilidade imediata com o tráfego criptografado e manterá o controle sobre seu certificado (por exemplo, um certificado de Validação estendida (EV)). Se fizer upload de um certificado customizado, você será responsável por gerenciá-lo. Por exemplo, o IBM CIS não rastreia datas de expiração de certificado. 
 
### Como alternativa, utilize um certificado fornecido pelo CIS
{:#strict-utilize-cert-cis-provisioned}
 
O IBM CIS tem parceria com várias Autoridades de Certificação (CAs) para fornecer certificados curinga de domínio para nossos clientes, por padrão. Pode ser necessária uma verificação manual para configurar esses certificados e sua equipe de suporte pode ajudá-lo a executar essas etapas adicionais.
 
### Mude sua configuração de TLS para **Assinado pela CA de ponta a ponta**
{:#strict-change-tls-setting}
 
A maioria dos nossos clientes corporativos utiliza a configuração de segurança Assinado pela CA de Ponta a Ponta. Uma configuração **Assinado pela CA de ponta a ponta** requer um certificado assinado pela CA válido instalado em seu servidor da web. A data de expiração do certificado deve estar no futuro e ele deve ter um *nome do host* ou *Nome Alternativo de Assunto (SAN)* correspondente.

