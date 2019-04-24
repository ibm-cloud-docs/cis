---
copyright:
  years: 2018
lastupdated: "2018-02-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Opções de TLS
As opções de TLS permitem controlar se os visitantes podem procurar seu website durante uma conexão segura, e quando o fizerem, como CIS se conectará ao seu servidor de origem.

Essas opções são listadas na ordem do menos seguro (Desativado) para o mais seguro (Assinado pela CA de ponta a ponta). 

Modos de criptografia TLS:

 * Desativado (não recomendado)
 * Cliente para borda (borda para origem não criptografada, certificados autoassinados não são suportados) 
 * Flexível de ponta a ponta (borda para origem, certificados podem ser autoassinados) 
 * Assinado pela CA de ponta a ponta (recomendado)

## Desativado 
Nenhuma conexão segura entre seu visitante e o CIS e nenhuma conexão segura entre o CIS e seu servidor da web. Os visitantes podem apenas visualizar seu website sobre HTTP e qualquer visitante que tentar se conectar usando HTTPS receberá um `HTTP 301 Redirect` para a versão HTTP simples de seu website.

## Cliente para a borda
Uma conexão segura entre seu visitante e o CIS, mas nenhuma conexão segura entre o CIS e seu servidor da web. Não é necessário ter um certificado TLS em seu servidor da web, mas seus visitantes ainda verão o site como sendo ativado por HTTPS. Essa opção não é recomendada se você possui alguma informação confidencial em seu website. Essa configuração só funcionará para a porta 443->80. Ela deve ser usada somente como um último recurso se você não é capaz de configurar o TLS em seu próprio servidor da web. Ela é _menos segura_ do que qualquer outra opção (mesmo “Desativado”) e poderia causar problemas quando você decidisse abandoná-la.

## Flexível de ponta a ponta
Uma conexão segura entre seu visitante e o CIS e conexão segura (mas não autenticada) entre o CIS e seu servidor da web. Será necessário ter seu servidor configurado para responder conexões HTTPS, com um certificado autoassinado pelo menos. A autenticidade do certificado não é verificada: do ponto de vista do CIS
(quando nos conectamos ao seu servidor de origem), é o equivalente a ignorar essa mensagem de erro. Contanto que o endereço de seu servidor de origem esteja correto em suas configurações de DNS, você sabe que nós estamos nos conectando ao seu servidor, não outra pessoa.

## Assinado pela CA de ponta a ponta
Recomendado. Uma conexão segura entre o visitante e o CIS e conexão segura e autenticada entre o CIS e seu servidor da web. Será necessário ter seu servidor configurado para responder conexões HTTPS, com um certificado TLS válido. Esse certificado deve ser assinado por uma autoridade de certificação, ter uma data de expiração no futuro e responder pelo nome de domínio de solicitação (nome do host).
