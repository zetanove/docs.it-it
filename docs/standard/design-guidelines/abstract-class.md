---
title: "Progettazione di classi astratte | Microsoft Docs"
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
  - "tipo di linee guida di progettazione, classi astratte"
  - "classi astratte, linee guida di progettazione"
  - "classe libreria linee guida di progettazione [.NET Framework], classi"
  - "astratta classi [.NET Framework]"
  - "classi [.NET Framework], linee guida di progettazione"
  - "tipo di linee guida di progettazione, classi"
ms.assetid: d3646e6d-5c1f-4922-8fb0-ec5effb30d60
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Progettazione di classi astratte
**X non** definire costruttori interni pubblici o protetti in tipi astratti.  
  
 I costruttori devono essere pubblici solo se gli utenti dovranno creare istanze del tipo. Poiché è possibile creare istanze di un tipo astratto, un tipo astratto con costruttore pubblico è correttamente progettato e fuorviante per gli utenti.  
  
 **✓ si** definisce un protetto o un costruttore interno per le classi astratte.  
  
 Un costruttore protetto è più comune e consente semplicemente la classe di base eseguire il proprio inizializzazione quando vengono creati sottotipi.  
  
 Un costruttore interno può essere utilizzato per limitare le implementazioni concrete della classe astratta per l'assembly che definisce la classe.  
  
 **✓ si** fornire almeno un tipo concreto che eredita da ogni classe astratta da consegnare.  
  
 Eseguendo questo consente di convalidare la struttura della classe astratta. Ad esempio,  <xref:System.IO.FileStream?displayProperty=fullName> è un'implementazione della <xref:System.IO.Stream?displayProperty=fullName> classe astratta.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di tipo](../../../docs/standard/design-guidelines/type.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)