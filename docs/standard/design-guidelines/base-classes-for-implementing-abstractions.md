---
title: "Classi di base per l&#39;implementazione di astrazioni | Microsoft Docs"
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
  - "astrazioni [.NET Framework]"
  - "classi base, astrazioni"
ms.assetid: 37a2d9a4-9721-482a-a40f-eee2c1d97875
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Classi di base per l&#39;implementazione di astrazioni
In teoria, una classe diventa una classe di base quando un'altra classe è derivata da esso. Ai fini di questa sezione, tuttavia, una classe di base è una classe progettata principalmente per fornire un'astrazione comune o per altre classi di riutilizzare parte implementazione tuttavia l'ereditarietà predefinita. Classi di base si trovano in genere al centro delle gerarchie di ereditarietà, tra un'astrazione alla radice di una gerarchia e diverse implementazioni personalizzate nella parte inferiore.  
  
 Fungono da supporti di implementazione per l'implementazione di astrazioni. Ad esempio, una delle astrazioni del Framework per le raccolte ordinate di elementi è il <xref:System.Collections.Generic.IList%601> interfaccia. Implementazione di <xref:System.Collections.Generic.IList%601> non è semplice, e pertanto il Framework fornisce diverse classi di base, ad esempio <xref:System.Collections.ObjectModel.Collection%601> e <xref:System.Collections.ObjectModel.KeyedCollection%602>, che fungono da helper per l'implementazione di raccolte personalizzate.  
  
 Classi di base in genere non sono adatte a fungere da astrazioni autonomamente, perché tendono a contenere una quantità eccessiva di implementazione. Ad esempio, la `Collection<T>` classe di base contiene un numero elevato di implementazione legato al fatto che implementa il metodo non generico `IList` interfaccia \(per la migliore integrazione con le raccolte non generiche\) e al fatto che è una raccolta di elementi archiviati nella memoria in uno dei relativi campi.  
  
 Come illustrato in precedenza, classi base possono fornire una Guida in linea preziosissima per gli utenti che desiderano implementare astrazioni, ma allo stesso tempo possono essere un ostacolo significativo. Aggiungono della superficie di attacco e aumentare la profondità delle gerarchie di ereditarietà e così concettualmente complicare il framework. Di conseguenza, le classi di base da utilizzare solo se forniscono valore aggiunto significativo agli utenti di framework. Essi devono essere evitate se forniscono valore solo per gli implementatori di framework, in cui è necessario considerare fortemente case delega a un'implementazione interna anziché ereditarietà da una classe base.  
  
 **✓ PROVARE** le classi di base che astratta anche se non contengono alcun membro astratto. Ovviamente questo comunica agli utenti che la classe è progettata esclusivamente per essere ereditata.  
  
 **✓ PROVARE** collocare le classi base in uno spazio dei nomi separato dai tipi di scenario principale. Per definizione, le classi di base sono destinate a scenari di estensibilità avanzata e pertanto non sono interessanti per la maggior parte degli utenti.  
  
 **X evitare** denominazione delle classi di base con un suffisso "Base" se la classe è destinata all'utilizzo delle API pubbliche.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Progettazione finalizzata all'estensibilità](../../../docs/standard/design-guidelines/designing-for-extensibility.md)