---
title: "Elemento &lt;specifiedPickupDirectory&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#specifiedPickupDirectory"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp/specifiedPickupDirectory"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<specifiedPickupDirectory> (elemento)"
  - "specifiedPickupDirectory (elemento)"
ms.assetid: 0121f49d-bff2-4bc6-af06-f1628dcd61f1
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# Elemento &lt;specifiedPickupDirectory&gt; (Impostazioni di rete)
Configura la directory locale per un server SMTP \(Simple Mail Transport Protocol\).  
  
## Sintassi  
  
```  
  
      <specifiedPickupDirectory  
  pickupDirectoryLocation="directory"   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`pickupDirectoryLocation`|Directory in cui le applicazioni salvano la posta elettronica per consentirne l'elaborazione successiva mediante il server SMTP.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<smtp\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/smtp-element-network-settings.md)|Configura le opzioni di invio della posta elettronica per il protocollo SMTP \(Simple Mail Transport Protocol\).|  
  
## Note  
 L'attributo `specifiedPickupDirectory` imposta la directory in cui le applicazioni salvano i messaggi di posta elettronica da elaborare mediante il server SMTP.  
  
## Esempio  
 Nell'esempio di codice seguente la directory c:\\maildrop viene specificata come directory di prelievo della posta elettronica.  
  
```  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="specifiedPickupDirectory">  
        <specifiedPickupDirectory  
          pickupDirectoryLocation="c:\maildrop"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.Mail.SmtpClient?displayProperty=fullName>   
 <xref:System.Net.Configuration.SmtpSection?displayProperty=fullName>   
 <xref:System.Net.Configuration.SmtpSpecifiedPickupDirectoryElement?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)