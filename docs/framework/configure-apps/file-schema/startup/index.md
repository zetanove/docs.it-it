---
title: "Schema delle impostazioni di avvio | Microsoft Docs"
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
  - "schema di configurazione [.NET Framework], impostazioni di avvio"
  - "impostazioni di avvio (schema)"
  - "schema delle impostazioni di avvio"
ms.assetid: 03de6972-442a-4648-9f3e-efa654e3b949
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Schema delle impostazioni di avvio
Le impostazioni di avvio specificano la versione di Common Language Runtime mediante la quale eseguire l'applicazione.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<requiredRuntime\>](../../../../../docs/framework/configure-apps/file-schema/startup/requiredruntime-element.md)|Specifica che l'applicazione supporta solo la versione 1.0 di Common Language Runtime \(CLR\).  Nelle applicazioni compilate con la versione 1.1 sarà necessario utilizzare l'elemento **\<supportedRuntime\>**.|  
|[\<supportedRuntime\>](../../../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md)|Specifica le versioni di Common Language Runtime supportate dall'applicazione.|  
|[\<avvio\>](../../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)|Contiene gli elementi **\<requiredRuntime\>** e **\<supportedRuntime\>**.|  
  
## Vedere anche  
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [\<PaveOver\> Specifying Which Runtime Version to Use](http://msdn.microsoft.com/it-it/c376208d-980d-42b4-865b-fbe0d9cc97c2)