---
title: "Operatori di uguaglianza | Microsoft Docs"
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
  - "classe libreria linee guida di progettazione [.NET Framework] è uguale a (metodo)"
  - "classe libreria linee guida di progettazione [.NET Framework], operatore di uguaglianza"
  - "operatore di uguaglianza (= =) [.NET Framework]"
  - "Equals (metodo)"
  - "= = (operatore di uguaglianza) [.NET Framework]"
ms.assetid: bc496a91-fefb-4ce0-ab4c-61f09964119a
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Operatori di uguaglianza
In questa sezione vengono illustrati gli operatori di uguaglianza overload e fa riferimento a `operator==` e `operator!=` come operatori di uguaglianza.  
  
 **X non** overload degli operatori di uguaglianza e non l'altro.  
  
 **✓ si** assicurarsi che <xref:System.Object.Equals%2A?displayProperty=fullName> e gli operatori di uguaglianza hanno esattamente la stessa semantica e caratteristiche di prestazioni simili.  
  
 Ciò significa che spesso `Object.Equals` deve essere sottoposto a override quando sono sottoposti a overload gli operatori di uguaglianza.  
  
 **X evitare** generazione di eccezioni da operatori di uguaglianza.  
  
 Ad esempio, restituisce false se uno degli argomenti è null anziché generare `NullReferenceException`.  
  
## Operatori di uguaglianza sui tipi di valore  
 **✓ si** overload gli operatori di uguaglianza sui tipi di valore, se l'uguaglianza è significativa.  
  
 Nella maggior parte dei linguaggi di programmazione, vi è Nessuna implementazione predefinita di `operator==` per i tipi di valore.  
  
## Operatori di uguaglianza sui tipi di riferimento  
 **X evitare** overload degli operatori di uguaglianza sui tipi di riferimento modificabile.  
  
 Molti linguaggi sono operatori di uguaglianza predefinito per tipi di riferimento. Gli operatori incorporati in genere implementano l'uguaglianza di riferimento e molti sviluppatori sono sorpresi quando viene modificato il comportamento predefinito per l'uguaglianza di valore.  
  
 Questo problema viene ridotta per i tipi di riferimento non modificabile perché l'immutabilità rende molto più difficile da notare la differenza tra uguaglianza di riferimento e uguaglianza di valore.  
  
 **X evitare** overload degli operatori di uguaglianza sui tipi di riferimento, se l'implementazione è notevolmente più lento rispetto a quello di uguaglianza di riferimento.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Linee guida di utilizzo](../../../docs/standard/design-guidelines/usage-guidelines.md)