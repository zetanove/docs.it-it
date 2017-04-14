---
title: "Astrazioni (interfacce e tipi astratti) | Microsoft Docs"
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
  - "astratta interfacce [.NET Framework]"
  - "interfacce astratte [.NET Framework]"
  - "tipi astratti [.NET Framework]"
  - "astratta tipi [.NET Framework]"
ms.assetid: 0a632bc7-9b03-44ee-8842-c82f88672a45
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Astrazioni (interfacce e tipi astratti)
Un'astrazione è un tipo che descrive un contratto, ma non fornisce un'implementazione completa del contratto. Astrazioni vengono in genere implementate come classi astratte o interfacce, e hanno un set ben definito della documentazione di riferimento che descrive la semantica dei tipi di implementazione del contratto richiesta. Alcune delle astrazioni più importanti in .NET Framework includono <xref:System.IO.Stream>, <xref:System.Collections.Generic.IEnumerable%601>, e <xref:System.Object>.  
  
 È possibile estendere Framework implementando un tipo concreto che supporta il contratto di un'astrazione e utilizzo di questo tipo concreto con framework API consumer \(opera in\) l'astrazione.  
  
 È molto difficile progettare un'astrazione significativa e utile che è in grado di sopportare il test di tempo. La difficoltà principale riceve il set di membri, non è più e meno non corretto. Se un'astrazione ha troppi membri, diventa difficile o addirittura impossibili da implementare. In caso affermativo troppo pochi membri per la funzionalità promesso diventa inutile in molti scenari interessanti.  
  
 Troppi astrazioni in un framework anche influire negativamente sull'usabilità del framework. È spesso molto difficile da comprendere un'astrazione senza informazioni sulle modalità di integrazione nell'immagine più grande di implementazioni concrete e le API utilizzano l'astrazione. Inoltre, i nomi delle astrazioni e i relativi membri sono necessariamente astratti che spesso li rende difficile e inaccessibile senza prima conoscere il contesto più ampio del loro utilizzo.  
  
 Tuttavia, le astrazioni forniscono l'estensibilità estremamente potente che spesso non possono corrispondere ad altri meccanismi di estensibilità. Sono alla base di molti modelli di architettura, ad esempio plug\-in, inversione del controllo \(IoC\), le pipeline e così via. Inoltre, sono estremamente importanti per la testabilità di Framework. Astrazioni buona rendono possibile sottoporre a stub pesante dipendenze allo scopo di unit test. In sintesi, astrazioni sono responsabili per la ricchezza ricercata dei moderni Framework orientato a oggetti.  
  
 **X non** fornisce astrazioni a meno che non vengono verificati per lo sviluppo di diverse implementazioni concrete e le API utilizzano le astrazioni.  
  
 **✓ si** scegliere con attenzione tra una classe astratta e un'interfaccia quando si progetta un'astrazione.  
  
 **✓ PROVARE** fornire test di riferimento per le implementazioni concrete delle astrazioni. Tali test dovrebbero consentire agli utenti di verificare la corretta implementazione del contratto.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Progettazione finalizzata all'estensibilità](../../../docs/standard/design-guidelines/designing-for-extensibility.md)