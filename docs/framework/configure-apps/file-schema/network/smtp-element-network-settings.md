---
title: "Elemento &lt;smtp&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#smtp"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<smtp> (elemento)"
  - "smtp (elemento)"
ms.assetid: 220b0329-e384-4e0c-86b4-0945ad17efd9
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# Elemento &lt;smtp&gt; (Impostazioni di rete)
Configura il formato di invio, il metodo di invio e l'indirizzo del mittente dei messaggi di posta elettronica.  
  
## Sintassi  
  
```  
  
      <smtp  
  deliveryFormat="format"   
  deliveryMethod="method"   
  from="from address"   
  <specifiedPickupDirectory> … </ specifiedPickupDirectory >  
  <network> … </network>  
/smtp>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`deliveryFormat`|Specifica il formato di invio dei messaggi di posta elettronica in uscita.  I valori accettabili sono SevenBit e International.|  
|`deliveryMethod`|Specifica il metodo di invio dei messaggi di posta elettronica.  I valori accettabili sono network, pickupDirectoryFromIis e specifiedPickupDirectory.|  
|`from`|Specifica l'indirizzo del mittente dei messaggi di posta elettronica in uscita.|  
  
### Elementi figlio  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`specifiedPickupDirectory`|Configura la directory locale per un server SMTP \(Simple Mail Transport Protocol\).|  
|`network`|Configura le opzioni di rete per un server SMTP esterno.|  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[Elemento \<mailSettings\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/mailsettings-element-network-settings.md)|Configura le opzioni di invio della posta elettronica.|  
  
## Esempio  
 Nell'esempio di codice riportato di seguito vengono specificati i parametri SMTP appropriati per l'invio della posta elettronica mediante le credenziali di rete predefinite.  
  
```  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="network" deliveryFormat="SevenBit"  from="ben@contoso.com">  
        <network  
          host="localhost"  
          port="25"  
          defaultCredentials="true"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.Configuration.SmtpSection?displayProperty=fullName>   
 <xref:System.Net.Mail.SmtpClient?displayProperty=fullName>   
 <xref:System.Net.Mail.SmtpDeliveryFormat>   
 <xref:System.Net.Mail.SmtpDeliveryMethod>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)