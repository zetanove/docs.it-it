---
title: "Linee guida | Microsoft Docs"
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
  - "librerie, libreria di classi .NET Framework"
  - "classe indicazioni per la progettazione di librerie [.NET Framework] su"
  - "linee guida di progettazione della libreria di classi [.NET Framework]"
ms.assetid: 5fbcaf4f-ea2a-4d20-b0d6-e61dee202b4b
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Linee guida
In questa sezione vengono fornite linee guida per la progettazione di librerie che estendono e interagiscono con .NET Framework. L'obiettivo è garantire agli sviluppatori di librerie API coerenza e facilità d'uso, fornendo un modello di programmazione unificato che sia indipendente dal linguaggio di programmazione utilizzato per lo sviluppo. È consigliabile seguire queste linee guida di progettazione durante lo sviluppo di classi e componenti in grado di estendere .NET Framework. Progettazione di librerie incoerente negativamente sulla produttività degli sviluppatori e scoraggia l'adozione.  
  
 Le linee guida sono organizzate come raccomandazioni semplice con le condizioni di prefisso `Do`, `Consider`, `Avoid`, e `Do not`. Queste linee guida servono per consentire agli sviluppatori di librerie di classi di comprendere i compromessi tra diverse soluzioni. Possono esserci situazioni in cui corretta progettazione delle librerie richiede che violi le linee guida di progettazione. Dovrebbero essere rari casi, è importante che esista un motivo chiaro e inevitabile per prendere la decisione.  
  
 Queste linee guida sono state estratte dal libro *Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition*, Krzysztof Cwalina e Brad Abrams.  
  
## In questa sezione  
 [Convenzioni di denominazione](../../../docs/standard/design-guidelines/naming-guidelines.md)  
 Vengono fornite linee guida per la denominazione di assembly, spazi dei nomi, tipi e membri nelle librerie di classi.  
  
 [Indicazioni per la progettazione di tipo](../../../docs/standard/design-guidelines/type.md)  
 Vengono fornite linee guida per l'utilizzo di classi statiche e astratte, interfacce, enumerazioni, strutture e altri tipi.  
  
 [Indicazioni per la progettazione di membri](../../../docs/standard/design-guidelines/member.md)  
 Vengono fornite linee guida per la progettazione e utilizzando le proprietà, metodi, costruttori, campi, eventi, operatori e i parametri.  
  
 [Progettazione finalizzata all'estensibilità](../../../docs/standard/design-guidelines/designing-for-extensibility.md)  
 Vengono illustrati i meccanismi di estendibilità, ad esempio una sottoclasse, utilizzando gli eventi, i membri virtuali e i callback e viene illustrato come scegliere i meccanismi che meglio soddisfano i requisiti del framework.  
  
 [Linee guida di progettazione per le eccezioni](../../../docs/standard/design-guidelines/exceptions.md)  
 Descrive linee guida per la progettazione, generando un'eccezione e l'intercettazione delle eccezioni.  
  
 [Linee guida di utilizzo](../../../docs/standard/design-guidelines/usage-guidelines.md)  
 Vengono fornite istruzioni per l'utilizzo di tipi comuni, ad esempio matrici, gli attributi e raccolte, che supportano la serializzazione e l'overload degli operatori di uguaglianza.  
  
 [Modelli di progettazione comuni](../../../docs/standard/design-guidelines/common-design-patterns.md)  
 Vengono fornite linee guida per la scelta e implementare il modello dispose e le proprietà di dipendenza.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Panoramica](../../../docs/framework/get-started/overview.md)   
 [Guida di orientamento a .NET Framework](http://msdn.microsoft.com/it-it/0b46b7c6-9163-4f99-8e58-0d1ee7da8c67)   
 [Guida di sviluppo](../../../docs/framework/development-guide.md)