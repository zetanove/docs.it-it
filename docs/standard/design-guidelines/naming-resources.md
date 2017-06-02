---
title: "Nomi delle risorse | Microsoft Docs"
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
  - "risorse localizzati nomi [.NET Framework]"
  - "localizzazione, convenzioni di denominazione"
  - "nomi delle risorse"
  - "applicazioni globali, convenzioni di denominazione"
  - "applicazioni internazionali, convenzioni di denominazione"
ms.assetid: 8b0e97f3-7877-44fd-bc76-e05d36d5d79c
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Nomi delle risorse
Poiché possono fare riferimento a risorse localizzabili mediante alcuni oggetti come se fossero proprietà, convenzioni di denominazione per le risorse sono simili alle linee guida per la proprietà.  
  
 **✓ si** utilizzare il sistema Pascal le chiavi di risorsa.  
  
 **✓ si** fornire descrittivo anziché identificatori brevi.  
  
 **X non** utilizzare parole chiave specifiche del linguaggio dei principali linguaggi CLR.  
  
 **✓ si** utilizzare solo caratteri alfanumerici e caratteri di sottolineatura nei nomi delle risorse.  
  
 **✓ si** utilizzare la seguente convenzione di denominazione per le risorse di messaggio eccezione.  
  
 L'identificatore di risorsa deve essere il nome del tipo di eccezione e un identificatore breve dell'eccezione:  
  
 `ArgumentExceptionIllegalCharacters`   
 `ArgumentExceptionInvalidName`   
 `ArgumentExceptionFileNameIsMalformed`  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Convenzioni di denominazione](../../../docs/standard/design-guidelines/naming-guidelines.md)