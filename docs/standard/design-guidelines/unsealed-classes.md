---
title: "Classi non sealed | Microsoft Docs"
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
  - "non è sealed classi [.NET Framework]"
  - "classi non sealed"
  - "ereditarietà, classi"
ms.assetid: 9a3bd505-90f5-4053-9f0d-3cf5fa3d3ebf
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Classi non sealed
Classi sealed non possono essere ereditate da e consentirne l'estendibilità. Al contrario, le classi che possono essere ereditate da vengono denominate classi non sealed.  
  
 **✓ PROVARE** utilizzando le classi non sealed senza aggiunti membri virtuali o protetti come un ottimo modo per fornire ancora molto apprezzati di un framework di estensibilità.  
  
 Gli sviluppatori spesso vogliono ereditare da classi non sealed in modo da poter aggiungere i membri di praticità, ad esempio costruttori personalizzati, nuovi metodi o gli overload del metodo. Ad esempio,  `System.Messaging.MessageQueue` è bloccato e pertanto consente agli utenti di creare code personalizzate che per impostazione predefinita in un percorso di coda specifica o per aggiungere metodi personalizzati che semplificano l'API per scenari specifici.  
  
 Classi non vengono bloccate per impostazione predefinita nei linguaggi di programmazione più, e questo è il valore predefinito consigliato per la maggior parte delle classi di Framework. L'estendibilità previsti da tipi non sealed è molto apprezzato dagli utenti di framework e molto conveniente fornire a causa dei costi relativamente basso di test associati a tipi non sealed.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Progettazione finalizzata all'estensibilità](../../../docs/standard/design-guidelines/designing-for-extensibility.md)   
 [Come rendere sealed](../../../docs/standard/design-guidelines/sealing.md)