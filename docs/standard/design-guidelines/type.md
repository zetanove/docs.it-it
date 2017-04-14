---
title: "Indicazioni per la progettazione di tipo | Microsoft Docs"
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
  - "indicazioni per la progettazione di tipo"
  - "linee guida di progettazione di tipo, sulle linee guida di progettazione di tipo"
  - "Digitare linee guida di progettazione nella classe indicazioni per la progettazione di librerie [.NET Framework]"
  - "tipi di linee guida di progettazione [.NET Framework]"
ms.assetid: 6b49314e-8bba-43ea-97ca-4e0255812f95
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Indicazioni per la progettazione di tipo
Dalla prospettiva del CLR, sono disponibili solo due categorie di tipi: tipi di riferimento e tipi di valore, ma ai fini di una discussione sulla progettazione di framework, tipi verrà diviso in gruppi logici, ciascuno con proprie regole di progettazione specifica.  
  
 Le classi sono caso generale di tipi di riferimento. Costituiscono la maggior parte dei tipi nella maggior parte dei Framework. Classi dovute alla grande diffusione per l'ampio set di funzionalità orientate a oggetti che supportano e la loro applicabilità generale. Classi base e classi astratte sono gruppi logici speciali relativi all'estendibilità.  
  
 Le interfacce sono tipi che possono essere implementati da entrambi i tipi di riferimento e tipi di valore. Può pertanto fungono da radici di polimorfiche gerarchie di tipi di riferimento e tipi di valore. Inoltre, interfacce possono essere utilizzate per simulare l'ereditarietà multipla, in modo nativo non è supportato da CLR.  
  
 Le strutture sono caso generale di tipi di valore e devono essere riservate per tipi semplici e di piccoli, simili a primitive di linguaggio.  
  
 Le enumerazioni sono un tipo speciale di tipi di valore utilizzato per definire una breve serie di valori, ad esempio giorni della settimana, colori della console e così via.  
  
 Le classi statiche sono tipi deve essere contenitori per i membri statici. Vengono comunemente utilizzati per fornire collegamenti ad altre operazioni.  
  
 Delegati, le eccezioni, gli attributi, matrici e raccolte sono tutti i casi speciali di destinato a utilizzi specifici tipi di riferimento e linee guida per la progettazione e utilizzo vengono trattate altrove in questo manuale.  
  
 **✓ si** assicurarsi che ogni tipo è un set ben definito di membri correlati, non solo un insieme casuale di funzionalità correlate.  
  
## In questa sezione  
 [Scelta tra classi e Struct](../../../docs/standard/design-guidelines/choosing-between-class-and-struct.md)  
 [Progettazione di classi astratte](../../../docs/standard/design-guidelines/abstract-class.md)  
 [Progettazione di classi statiche](../../../docs/standard/design-guidelines/static-class.md)  
 [Progettazione dell'interfaccia](../../../docs/standard/design-guidelines/interface.md)  
 [Progettazione di struct](../../../docs/standard/design-guidelines/struct.md)  
 [Progettazione di enum](../../../docs/standard/design-guidelines/enum.md)  
 [Tipi annidati](../../../docs/standard/design-guidelines/nested-types.md)  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)