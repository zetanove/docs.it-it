---
title: "Denominazione dei parametri | Microsoft Docs"
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
  - "parametri, i nomi"
  - "nomi di parametri [.NET Framework]"
ms.assetid: ca3c956e-725a-441b-b4e3-eab5d472f41c
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Denominazione dei parametri
Oltre alla motivazione ovvia di leggibilità, è importante seguire le linee guida per i nomi di parametro perché i parametri vengono visualizzati nella documentazione e nella finestra di progettazione quando gli strumenti di progettazione visiva forniscono Intellisense e funzionalità di esplorazione di classe.  
  
 **✓ si** utilizzare Camel nei nomi di parametro.  
  
 **✓ si** utilizzare nomi di parametro descrittivi.  
  
 **✓ PROVARE** utilizzare nomi basati sul significato del parametro anziché il tipo del parametro.  
  
### Denominazione dei parametri di Overload di operatore  
 **✓ si** utilizzare `left` e `right` per nomi di parametro di overload di operatore binario se è presente alcun significato per i parametri.  
  
 **✓ si** utilizzare `value` per unario dell'overload dell'operatore i nomi dei parametri se è presente alcun significato per i parametri.  
  
 **✓ PROVARE** nomi significativi per l'operatore di overload parametri se questo modo si aggiunge un valore significativo.  
  
 **X non** utilizzare abbreviazioni o indici numerici per l'operatore di overload i nomi dei parametri.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Convenzioni di denominazione](../../../docs/standard/design-guidelines/naming-guidelines.md)