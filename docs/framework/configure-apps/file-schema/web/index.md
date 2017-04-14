---
title: "Schema delle impostazioni Web | Microsoft Docs"
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
  - "sistema di configurazione ASP.NET, Schema delle impostazioni Web"
  - "file di configurazione [ASP.NET]"
  - "schema di configurazione [.NET Framework], impostazioni Web"
  - "Impostazioni Web (schema)"
  - "impostazioni Web, schema [ASP.NET]"
  - "file di configurazione Web.config [ASP.NET]"
ms.assetid: ae1ac356-267d-4753-8d7a-7a04eb45a9be
caps.latest.revision: 6
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# Schema delle impostazioni Web
Le impostazioni Web specificano le impostazioni ASP.NET a livello di esecuzione e relative alla CPU che si applicano al comportamento relativo all'intero processo gestito dal livello di hosting ASP.NET.  Queste impostazioni sono diverse dalle impostazioni relative al tipo di dominio di applicazione specificate nel file Web.config di un'applicazione ASP.NET.  
  
 Le impostazioni Web sono contenute in file Aspnet.config contenuti nelle cartelle di installazione specifiche per ogni versione di .NET Framework.  Ad esempio, il file Aspnet.config per [!INCLUDE[dnprdnext](../../../../../includes/dnprdnext-md.md)] si trova nella cartella seguente:  
  
 `C:\Windows\Microsoft.NET\Framework\v2.0.50727\`  
  
 Le impostazioni Web non sono utilizzate in altri file di configurazione quali il file machine.config, il file Web.config della radice o il file Web.config a livello di applicazione.  
  
 [Elemento \<Configuration\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [Elemento \<system.web\> \(impostazioni Web\)](../../../../../docs/framework/configure-apps/file-schema/web/system-web-element-web-settings.md)  
  
 [Elemento \<applicationPool\> \(impostazioni Web\)](../../../../../docs/framework/configure-apps/file-schema/web/applicationpool-element-web-settings.md)  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<system.web\>](../../../../../docs/framework/configure-apps/file-schema/web/system-web-element-web-settings.md)|Contiene informazioni utilizzate dal livello di hosting ASP.NET.|  
|[\<applicationPool\>](../../../../../docs/framework/configure-apps/file-schema/web/applicationpool-element-web-settings.md)|Specifica le impostazioni ASP.NET a livello di esecuzione e relative alla CPU che si applicano al comportamento relativo all'intero processo gestito dal livello di hosting ASP.NET.|  
  
## Vedere anche  
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)