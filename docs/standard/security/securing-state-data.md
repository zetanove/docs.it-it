---
title: "Securing State Data | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "security [.NET Framework], state data"
  - "code security, state data"
  - "secure coding, state data"
  - "state data security"
ms.assetid: 12671309-2877-43fe-a3df-6863507e712d
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# Securing State Data
Nelle applicazioni che consentono la gestione di dati sensibili o decisioni di qualsiasi tipo in materia di sicurezza è necessario mantenere il controllo dei dati e non consentire l'accesso diretto da parte di altro codice potenzialmente dannoso.  Il modo migliore per proteggere i dati in memoria è dichiararli come variabili private o interne, ovvero con ambito limitato allo stesso assembly.  Anche questi dati sono tuttavia soggetti a un tipo di accesso che è necessario determinare.  
  
-   Tramite meccanismi di reflection, è possibile ottenere e impostare membri privati in codice altamente attendibile che può fare riferimento all'oggetto.  
  
-   Tramite serializzazione, è possibile ottenere e impostare membri privati in codice altamente attendibile se è possibile accedere ai dati corrispondenti nella forma serializzata dell'oggetto.  
  
-   Nella fase di debug, questi dati possono essere letti.  
  
 Accertarsi che nessun metodo o proprietà esponga tali valori in modo non intenzionale.  
  
 In alcuni casi, i dati possono essere dichiarati come "protected" con accesso limitato alla classe e alle classi derivate.  L'esposizione aggiuntiva suggerisce comunque l'adozione delle seguenti precauzioni:  
  
-   Controllare il codice autorizzato a derivare dalla classe vincolandolo allo stesso assembly o utilizzando la sicurezza dichiarativa descritta in [Sicurezza dell'accesso ai metodi](../../../docs/framework/misc/securing-method-access.md) per richiedere identità o autorizzazioni valide per la derivazione del codice dalla classe.  
  
-   Accertarsi che per tutte le classi derivate sia implementata una protezione di questo tipo o che siano sealed.  
  
## Vedere anche  
 [Secure Coding Guidelines](../../../docs/standard/security/secure-coding-guidelines.md)