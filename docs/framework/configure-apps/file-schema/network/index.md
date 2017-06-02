---
title: "Schema delle impostazioni di rete | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "impostazioni di configurazione [.NET Framework], reti"
  - "connessioni [.NET Framework], elementi di configurazione di rete"
  - "elementi [.NET Framework], elementi di configurazione di rete"
  - "Internet, elementi di configurazione di rete"
  - "elementi di configurazione di rete"
  - "risorse di rete, elementi di configurazione di rete"
  - "impostazioni di rete"
  - "ricezione di dati, elementi di configurazione di rete"
  - "invio di dati, elementi di configurazione di rete"
ms.assetid: f1de5a0f-76c5-4833-819f-5222b8146340
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Schema delle impostazioni di rete
Le impostazioni di rete indicano il modo in cui .NET Framework si connette a Internet.  Nella tabella riportata di seguito viene descritta la funzione di ciascun elemento di configurazione figlio in [Elemento \<system.Net\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md).  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<authenticationModules\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/authenticationmodules-element-network-settings.md)|Consente di specificare i moduli utilizzati per autenticare le richieste Internet.|  
|[Elemento \<connectionManagement\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/connectionmanagement-element-network-settings.md)|Consente di specificare il numero massimo di connessioni agli host Internet.|  
|[Elemento \<defaultProxy\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md)|Consente di specificare il server proxy utilizzato per le richieste HTTP inviate a Internet.|  
|[Elemento \<mailSettings\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/mailsettings-element-network-settings.md)|Contiene le impostazioni per le opzioni di invio della posta elettronica.|  
|[Elemento \<requestCaching\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)|Consente di specificare i moduli utilizzati per richiedere informazioni dagli host Internet.|  
|[Elemento \<requestCaching\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)|Configura opzioni di rete di base per lo spazio dei nomi <xref:System.Net?displayProperty=fullName>.|  
|[Elemento \<webRequestModules\> \(Impostazioni di rete\)](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|Consente di specificare i moduli utilizzati per richiedere informazioni dagli host Internet.|  
  
 Le impostazioni Uri specificano come vengono gestiti in .NET Framework gli indirizzi Web espressi tramite Uniform Resource Identifier \(URI\).  Nella tabella riportata di seguito viene descritta la funzione di ciascun elemento di configurazione figlio in [Elemento \<Uri\> \(impostazioni URI\)](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md).  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<idn\> \(Impostazioni URI\)](../../../../../docs/framework/configure-apps/file-schema/network/idn-element-uri-settings.md)|Specifica se l'analisi IDN \(Internationalized Domain Name\) viene applicata ai nomi di dominio.|  
|[Elemento \<iriParsing\> \(Impostazioni URI\)](../../../../../docs/framework/configure-apps/file-schema/network/iriparsing-element-uri-settings.md)|Specifica se l'analisi IRI \(International Resource Identifier\) viene applicata a un oggetto <xref:System.Uri> e se devono essere applicate le regole di analisi IRI.|  
|[Elemento \<schemeSettings\> \(impostazioni URI\)](../../../../../docs/framework/configure-apps/file-schema/network/schemesettings-element-uri-settings.md)|Specifica come un oggetto <xref:System.Uri> verrà analizzato per schemi specifici.|  
  
## Vedere anche  
 [configurazione di applicazioni Internet](../../../../../docs/framework/network-programming/configuring-internet-applications.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)