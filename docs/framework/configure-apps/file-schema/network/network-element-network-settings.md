---
title: "Elemento &lt;network&gt; (Impostazioni di rete) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#network"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp/network"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<network> (elemento)"
  - "network (elemento)"
ms.assetid: 2c2c6ad4-ed11-48ab-b28e-2bc0ba9b42c7
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# Elemento &lt;network&gt; (Impostazioni di rete)
Configura le opzioni di rete per un server SMTP \(Simple Mail Transport Protocol\) esterno.  
  
## Sintassi  
  
```  
  
      <network  
  clientDomain="string"   
  defaultCredentials="true|false"  
  enableSsl="true|false"  
  host="string"   
  password="string"  
  port="integer"   
  targetName="string"  
  userName="string"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`clientDomain`|Specifica il nome di dominio client da utilizzare nella richiesta iniziale di protocollo SMTP per connettersi al server di posta SMTP.  Il valore predefinito è il nome localhost del computer locale che invia la richiesta.|  
|`defaultCredentials`|Specifica se devono essere utilizzate le credenziali predefinite dell'utente per accedere al server di posta SMTP per transazioni SMTP.  Il valore predefinito è `false`.|  
|`enableSsl`|Specifica se viene utilizzato SSL per accedere a un server di posta elettronica SMTP.  Il valore predefinito è `false`.|  
|`host`|Specifica il nome host del server di posta SMTP da utilizzare per transazioni SMTP.  Questo attributo non ha un valore predefinito.|  
|`password`|Specifica la password da utilizzare per l'autenticazione al server di posta SMTP.  Questo attributo non ha un valore predefinito.|  
|`port`|Specifica il numero di porta da utilizzare per connettersi al server di posta SMTP.  Il valore predefinito è 25.|  
|`targetName`|Specifica il nome del provider di servizi \(SPN, Service Provider Name\) da utilizzare per l'autenticazione quando si utilizza la protezione estesa per le transazioni SMTP.  Questo attributo non ha un valore predefinito.|  
|`userName`|Specifica il nome utente da utilizzare per l'autenticazione al server di posta SMTP.  Questo attributo non ha un valore predefinito.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<smtp\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/smtp-element-network-settings.md)|Configura le opzioni di invio della posta elettronica per il protocollo SMTP \(Simple Mail Transport Protocol\).|  
  
## Note  
 In alcuni server SMTP è necessario autenticarsi prima di utilizzare il server.  Per effettuare questa operazione utilizzando le credenziali di rete predefinite sull'host, impostare l'attributo `defaultCredentials` su `true` La proprietà <xref:System.Net.Configuration.SmtpNetworkElement.DefaultCredentials%2A?displayProperty=fullName> può essere utilizzata per ottenere il valore corrente dell'attributo `defaultCredentials` dai file di configurazione applicabili.  
  
 È inoltre possibile utilizzare l'autenticazione di base, ovvero un nome utente e una password, per autenticarsi nel server SMTP.  Per utilizzare questa opzione, è necessario specificare un nome utente e una password validi per il server SMTP specificato.  
  
> [!NOTE]
>  L'autenticazione di base prevede l'invio dei valori `userName` e `password` al server non crittografato.  In tal modo le credenziali possono essere visualizzate da qualsiasi utente effettui il monitoraggio del traffico di rete e utilizzate per la connessione al server.  È pertanto consigliabile prendere in considerazione l'utilizzo di un meccanismo di autenticazione con un livello di protezione più elevato, come Kerberos o NT LAN Manager \(NTLM.\) Se `defaultCredentials` è impostato su `true`, verrà utilizzato Kerberos o NTLM se il server supporta questi protocolli.  
  
 L'autenticazione di base e le credenziali di rete predefinite si escludono a vicenda, ovvero se si imposta `defaultCredentials` su `true` e si specifica un nome utente e una password, verrà utilizzata la credenziale di rete predefinita e i dati di autenticazione di base verranno ignorati.  
  
 Per l'autenticazione di base, se si specifica un `userName`, è necessario specificare anche una `password` per autenticarsi sul server di posta.  
  
 La proprietà <xref:System.Net.Configuration.SmtpNetworkElement.UserName%2A?displayProperty=fullName> può essere utilizzata per ottenere il valore corrente dell'attributo `userName` dai file di configurazione applicabili.  La proprietà <xref:System.Net.Configuration.SmtpNetworkElement.Password%2A?displayProperty=fullName> può essere utilizzata per ottenere il valore corrente dell'attributo `password` dai file di configurazione applicabili.  Di norma, per motivi di sicurezza, l'attributo `password` non viene immesso nei file di configurazione.  
  
 L'attributo `clientDomain` modifica il nome di dominio client utilizzato nella richiesta iniziale di protocollo SMTP per un server di posta SMTP.  È possibile impostare l'attributo `clientDomain` sul nome di dominio completo del computer locale, anziché sul nome del localhost utilizzato per impostazione predefinita.  Fornisce maggiore conformità agli standard del protocollo SMTP.  Il valore predefinito è il nome localhost del computer locale che invia la richiesta.  La proprietà <xref:System.Net.Configuration.SmtpNetworkElement.ClientDomain%2A?displayProperty=fullName> può essere utilizzata per ottenere il valore corrente dell'attributo `clientDomain` dai file di configurazione applicabili.  
  
 Gli attributi `targetName` vengono utilizzati per l'autenticazione quando si utilizza la protezione estesa.  Il formato del valore predefinito è "SMTPSVC\/\<host\>" dove \<host\> è il nome host del server di posta elettronica SMTP.  La proprietà <xref:System.Net.Configuration.SmtpNetworkElement.TargetName%2A?displayProperty=fullName> può essere utilizzata per ottenere il valore corrente dell'attributo `targetName` dai file di configurazione applicabili.  
  
 L'attributo `enableSsl` specifica se viene utilizzato SSL per accedere a un server di posta SMTP.  La classe <xref:System.Net.Mail.SmtpClient?displayProperty=fullName> supporta solo l'Estensione del servizio SMTP per il protocollo SMTP protetto su Transport Layer Security come definito in RFC 3207.  In questa modalità, la sessione SMTP inizia in un canale non crittografato, quindi il client invia al server un comando STARTTLS per attivare la protezione delle comunicazioni tramite SSL.  Per ulteriori informazioni vedere RFC 3207 pubblicato da Internet Engineering Task Force \(IETF\).  
  
 Un metodo di connessione alternativo è quello in cui una sessione SSL viene stabilita in fase iniziale, prima che venga inviato qualsiasi comando di protocollo.  Questo metodo di connessione qualche volta è chiamato SMTPS e per impostazione predefinita utilizza la porta 465.  Questo metodo di connessione alternativo che utilizza SSL non è attualmente supportato.  
  
 La proprietà <xref:System.Net.Configuration.SmtpNetworkElement.EnableSsl%2A?displayProperty=fullName> può essere utilizzata per ottenere il valore corrente dell'attributo `enableSsl` dai file di configurazione applicabili.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito vengono specificati i parametri SMTP appropriati per l'invio della posta elettronica mediante le credenziali di rete predefinite.  
  
```  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="network">  
        <network  
          clientDomain="www.contoso.com"  
          defaultCredentials="true"  
          enableSsl="false"  
          host="mail.contoso.com"  
          port="25"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.Configuration.SmtpNetworkElement?displayProperty=fullName>   
 <xref:System.Net.Configuration.SmtpSection?displayProperty=fullName>   
 <xref:System.Net.Mail.SmtpClient?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)