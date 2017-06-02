---
title: "Membri virtuali | Microsoft Docs"
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
  - "membri sottoponibili a override"
  - "membri virtual"
  - "membri [.NET Framework] virtuali"
ms.assetid: 8ff4eb97-0364-43ec-8a02-934b5cd94d19
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Membri virtuali
Membri virtuali possono essere sottoposto a override, in modo da modificarne il comportamento della sottoclasse. Sono molto simili alle richiamate in termini di estensibilità che forniscono, ma sono migliori in termini di prestazioni di esecuzione e il consumo di memoria. Inoltre, i membri virtuali sembrano più naturali in scenari che richiedono la creazione di uno speciale tipo di un tipo esistente \(specializzazione\).  
  
 Membri virtuali offrono prestazioni migliori rispetto a callback ed eventi, ma non offra prestazioni migliori rispetto ai metodi non virtuali.  
  
 Lo svantaggio principale di membri virtuali è che il comportamento di un membro virtuale può essere modificato solo in fase di compilazione. Il comportamento di un callback può essere modificato in fase di esecuzione.  
  
 Membri virtuali, come i callback \(e forse maggiore callback\), sono i costi di progettare, testare e mantenere, in quanto tutte le chiamate a un membro virtuale possono essere sottoposto a override in maniera imprevista e possono eseguire codice arbitrario. Inoltre, molto più complessa in genere è necessario definire chiaramente il contratto di membri virtuali, pertanto il costo di progettazione e la documentazione di essi è superiore.  
  
 **X non** rendere i membri virtuali a meno che non si dispone di un buon motivo per eseguire questa operazione e si è a conoscenza di tutti i costi relativi alla progettazione, test e gestione di tali membri.  
  
 Membri virtuali sono meno impensabili in termini di modifiche apportate a tali senza compromettere la compatibilità. Inoltre, sono più lenti rispetto ai membri non virtuale, principalmente perché le chiamate a membri virtuali non vengono impostati come inline.  
  
 **✓ PROVARE** limitazione dell'estensibilità solo a quelle strettamente necessario.  
  
 **✓ si** preferire l'accessibilità protetta rispetto all'accessibilità pubblica per i membri virtuali. I membri pubblici devono forniscono l'estensibilità \(se richiesto\) effettuando la chiamata a un membro virtuale protetta.  
  
 I membri pubblici di una classe devono fornire il set corretto di funzionalità per i consumer diretti di tale classe. Membri virtuali sono progettati per essere sottoposto a override nelle sottoclassi e accessibilità protetta è un ottimo modo per definire l'ambito di tutti i punti di estendibilità virtuale a cui possono essere utilizzati.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Progettazione finalizzata all'estensibilità](../../../docs/standard/design-guidelines/designing-for-extensibility.md)