---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: TLS Options, secure connection, Automatic HTTPS

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Opções de TLS
{:#cis-tls-options}

As opções de TLS permitem controlar se os visitantes podem procurar seu website durante uma conexão segura, e quando o fizerem, como CIS se conectará ao seu servidor de origem.

## Regravação automática de HTTPS
{:#automatic-https-rewrite}

As regravações automáticas de HTTPS ajudam a corrigir o conteúdo misto, mudando "http" para "https" para todos os recursos ou links em seu website que podem ser fornecidos com HTTPS. Essa configuração está localizada na página de configuração de segurança **Avançado**.

## Modos de criptografia TLS
{:#tls-encryption-modes}

Essas opções são listadas na ordem do menos seguro (Desativado) para o mais seguro (Assinado pela CA de ponta a ponta). 
 * Desativado (não recomendado)
 * Cliente para borda (borda para origem não criptografada, certificados autoassinados não são suportados) 
 * Completamente flexível (os certificados de borda para origem podem ser autoassinados) 
 * Assinatura completa da CA (padrão e recomendado)
 * Pull de origem somente HTTPS (Apenas corporativo)

### Desativado 
{:#tls-encryption-modes-off}
Nenhuma conexão segura entre seu visitante e o CIS e nenhuma conexão segura entre o CIS e seu servidor da web. Os visitantes podem apenas visualizar seu website sobre HTTP e qualquer visitante que tentar se conectar usando HTTPS receberá um `HTTP 301 Redirect` para a versão HTTP simples de seu website.

### Cliente para a borda
{:#tls-encryption-modes-client-to-edge}

Uma conexão segura entre seu visitante e o CIS, mas nenhuma conexão segura entre o CIS e seu servidor da web. Não é necessário ter um certificado TLS em seu servidor da web, mas seus visitantes ainda verão o site como sendo ativado por HTTPS. Essa opção não é recomendada se você possui alguma informação confidencial em seu website. Essa configuração só funcionará para a porta 443->80. Ela deve ser usada somente como um último recurso se você não é capaz de configurar o TLS em seu próprio servidor da web. Ela é _menos segura_ do que qualquer outra opção (mesmo “Desativado”) e poderia causar problemas quando você decidisse abandoná-la.

### Flexível de ponta a ponta
{:#tls-encryption-modes-end-to-end-flexible}

Uma conexão segura entre seu visitante e o CIS e conexão segura (mas não autenticada) entre o CIS e seu servidor da web. Deve-se ter o servidor configurado para responder a conexões HTTPS, com pelo menos um certificado autoassinado. A autenticidade do certificado não é verificada: do ponto de vista do CIS
(quando nos conectamos ao seu servidor de origem), é o equivalente a ignorar essa mensagem de erro. Contanto que o endereço de seu servidor de origem esteja correto em suas configurações de DNS, você sabe que nós estamos nos conectando ao seu servidor, não outra pessoa.

### Assinado pela CA de ponta a ponta
{:#tls-encryption-modes-end-to-end-ca-signed}

Padrão e recomendado. Uma conexão segura entre o visitante e o CIS e conexão segura e autenticada entre o CIS e seu servidor da web. Deve-se ter o servidor configurado para responder a conexões HTTPS, com um certificado TLS válido. Esse certificado deve ser assinado por uma autoridade de certificação, ter uma data de expiração no futuro e responder pelo nome de domínio de solicitação (nome do host). Recomendamos que você continue usando esse modo TLS para as melhores práticas de segurança, a menos que você entenda as possíveis ameaças de segurança relacionadas à mudança para um dos modos menos rígidos.

### Pull de origem somente HTTPS
{:#tls-encryption-modes-origin-only-pull}

*Apenas Enterprise.* Esse modo tem os mesmos requisitos de certificado que a Assinatura completa da CA e também faz upgrade de todas as conexões entre o CIS e seu servidor da web de origem de HTTP para HTTPS, mesmo se o conteúdo original solicitado está sobre HTTP.

## Versão mínima do TLS
{:#minimum-tls-version}

Configura a versão mínima do TLS para o tráfego que tenta se conectar ao seu site. Por padrão, é configurado para 1.0. As versões mais altas do TLS fornecem segurança adicional, mas podem não ser suportadas por todos os navegadores. Isso pode fazer com que alguns clientes não consigam se conectar ao seu site.
