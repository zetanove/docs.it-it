---
title: "Elemento &lt;mailSettings&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#mailSettings"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<mailSettings> (elemento)"
  - "mailSettings (elemento)"
ms.assetid: 54f0f153-17e5-4f49-afdc-deadb940c9c1
caps.latest.revision: 20
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 20
---
# Elemento &lt;mailSettings&gt; (Impostazioni di rete)
Configura le opzioni di invio della posta elettronica.  
  
## Sintassi  
  
```  
  
      <mailSettings  
  <smtp> … </smtp>  
/mailsettings>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|[Elemento \<smtp\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/smtp-element-network-settings.md)|Configura le opzioni del protocollo SMTP \(Simple Mail Transport Protocol\).|  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[Elemento \<system.Net\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)|Contiene le impostazioni che indicano il modo in cui .NET Framework si connette alla rete.|  
  
## Esempio  
 Nell'esempio di codice riportato di seguito vengono specificati i parametri SMTP appropriati per l'invio della posta elettronica mediante le credenziali di rete predefinite.  
  
```  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="network">  
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
 <xref:System.Net.Mail.SmtpClient>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)