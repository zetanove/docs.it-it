---
title: "Matrici | Microsoft Docs"
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
  - "classe libreria linee guida di progettazione [.NET Framework], matrici"
  - "matrici [.NET Framework], linee guida di utilizzo"
  - "matrici vuote"
ms.assetid: 66a1b3d8-6f3f-4715-b235-e1ff95e32d8e
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Matrici
**✓ si** preferire l'utilizzo di raccolte nelle matrici delle API pubbliche. Il [Collection](../../../docs/standard/design-guidelines/guidelines-for-collections.md) sezione vengono fornite informazioni dettagliate su come scegliere tra le raccolte e matrici.  
  
 **X non** utilizzare campi di matrice di sola lettura. Il campo è di sola lettura e non può essere modificato, ma gli elementi nella matrice possono essere modificati.  
  
 **✓ PROVARE** utilizzando le matrici di matrici anziché le matrici multidimensionali.  
  
 Una matrice di matrici è una matrice con elementi che sono anche le matrici. Le matrici che costituiscono gli elementi possono presentare dimensioni diverse, la spazio inutilizzato sarà inferiore per alcuni insiemi di dati \(ad esempio, matrice di tipo sparse\) rispetto a matrici multidimensionali. Inoltre, CLR consente di ottimizzare operazioni sugli indici su matrici di matrici, in modo che potrebbe presentare migliorate prestazioni di runtime in alcuni scenari.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 <xref:System.Array>   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Linee guida di utilizzo](../../../docs/standard/design-guidelines/usage-guidelines.md)