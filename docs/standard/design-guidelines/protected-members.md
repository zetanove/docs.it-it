---
title: "Membri protetti | Microsoft Docs"
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
  - "protetto membri [.NET Framework]"
  - "membri protetti"
  - "non è sealed classi [.NET Framework]"
  - "membri protetti di classi [.NET Framework]"
  - "classi non sealed"
  - "personalizzazione del comportamento (classe)"
ms.assetid: aa0b58ee-3956-494d-ab48-471ae5db8740
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Membri protetti
Membri protetti da soli non forniscono alcun estendibilità, ma può rendere più potente di estendibilità tramite la creazione di sottoclassi. Possono essere utilizzati per esporre le opzioni di personalizzazione avanzate senza complicare inutilmente l'interfaccia pubblica principale.  
  
 Finestre di progettazione di Framework devono prestare attenzione ai membri protetti perché il nome "protetto" può offrire un falso senso di sicurezza. Chiunque è in grado di sottoclasse di una classe non sealed e membri di accesso protetto e pertanto le stesse procedure di codifica difensive utilizzati per i membri pubblici applicano ai membri protetti.  
  
 **✓ PROVARE** utilizzando i membri per la personalizzazione avanzata protetti.  
  
 **✓ si** trattare i membri protetti in classi non sealed come pubblici allo scopo di analisi di sicurezza, documentazione e compatibilità.  
  
 Chiunque può ereditare da una classe e accedere ai membri protetti.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Progettazione finalizzata all'estensibilità](../../../docs/standard/design-guidelines/designing-for-extensibility.md)