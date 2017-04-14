---
title: "Modifiche della sicurezza in .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
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
  - "AllowPartiallyTrustedCallers (attributo)"
  - ".NET Framework 4, modifiche di sicurezza"
  - ".NET Framework (sicurezza)"
  - "codice SecurityTransparent"
  - "SecurityCritical (codice)"
  - "sicurezza di accesso al codice, modifiche"
ms.assetid: 5e87881c-9c13-4b52-8ad1-e34bb46e8aaa
caps.latest.revision: 52
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 52
---
# Modifiche della sicurezza in .NET Framework
La modifica più importante apportata alla sicurezza in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] è costituita dall'assegnazione di nomi sicuri. Per una descrizione delle modifiche, vedere [Denominazione sicura avanzata](../../../docs/framework/app-domains/enhanced-strong-naming.md).  
  
 .NET Framework offre un modello di sicurezza a due livelli per le applicazioni gestite. Le applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] vengono eseguite in un contenitore di sicurezza di Windows tramite cui viene limitato l'accesso alle risorse. All'interno del contenitore, le applicazioni gestite sono completamente attendibili. Da una prospettiva di sicurezza per l'accesso di codice \(CAS\), non c'è niente che uno sviluppatore possa fare per elevare il livello di privilegi. Per informazioni sui privilegi concessi da Windows, vedere [Dichiarazioni di funzionalità delle app \(app di Windows Store\)](http://go.microsoft.com/fwlink/?LinkId=230436) in Windows Dev Center. Per informazioni sulla creazione di un'app [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], vedere [Creare la prima app di Windows Store in C\# o Visual Basic](http://go.microsoft.com/fwlink/?LinkId=230461).