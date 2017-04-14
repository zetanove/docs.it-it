---
title: "Nomi di assembly e DLL | Microsoft Docs"
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
  - "nomi di DLL [.NET Framework]"
  - "nomi di assembly [.NET Framework]"
  - "assembly [.NET Framework], nomi"
  - "I nomi di DLL"
ms.assetid: e800b610-31b4-4949-9c14-cb60e9f254be
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Nomi di assembly e DLL
Un assembly è l'unità di distribuzione e l'identità per i programmi di codice gestito. Anche se gli assembly possono estendersi su uno o più file, in genere un assembly viene eseguito il mapping uno a uno con una DLL. Pertanto, in questa sezione viene descritto solo DLL convenzioni di denominazione, che quindi possono essere mappate a convenzioni di denominazione di assembly.  
  
 **✓ si** scegliere nomi per l'assembly DLL che suggeriscono grandi blocchi di funzionalità, ad esempio System. Data.  
  
 Nomi di assembly e DLL non sono necessario che corrispondano ai nomi dello spazio dei nomi, ma è opportuno seguire il nome dello spazio dei nomi per la denominazione di assembly. Una buona regola empirica consiste nel denominare la DLL in base al prefisso comune degli assembly contenuti nell'assembly. Ad esempio, un assembly con due spazi dei nomi `MyCompany.MyTechnology.FirstFeature` e `MyCompany.MyTechnology.SecondFeature`, potrebbe essere denominata `MyCompany.MyTechnology.dll`.  
  
 **✓ PROVARE** denominare le DLL in base al modello seguente:  
  
 `<Company>.<Component>.dll`  
  
 dove `<Component>` contiene uno o più clausole separate da punti. Ad esempio:  
  
 `Litware.Controls.dll`.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Convenzioni di denominazione](../../../docs/standard/design-guidelines/naming-guidelines.md)