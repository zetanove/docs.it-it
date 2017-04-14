---
title: "Come rendere sealed | Microsoft Docs"
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
  - "limitazione dell'estensibilità"
  - "classi [.NET Framework], chiusura"
  - "blocco della personalizzazione"
  - "classi sealed"
ms.assetid: cc42267f-bb7a-427a-845e-df97408528d4
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Come rendere sealed
Una delle funzionalità del framework orientato a oggetti è che gli sviluppatori possono estendere e personalizzarli in modi imprevisti per i progettisti del framework. Questa è la potenza e pericolo di progettazione estensibile. Quando si progetta la struttura, è pertanto molto importante per progettare con attenzione per l'estendibilità quando si desidera e per limitare l'estendibilità quando è pericoloso.  
  
 L'utilizzo di un meccanismo potente che impedisce di estendibilità è sealed. È possibile bloccare la classe o i singoli membri. Una classe impedisce agli utenti di ereditare dalla classe. Bloccaggio di un membro impedisce agli utenti di ignorare un determinato membro.  
  
 **X non** proteggere le classi senza che sia un buon motivo per eseguire questa operazione.  
  
 Chiusura di una classe perché è non riescono a immaginare uno scenario di estendibilità non è una buona ragione. Agli utenti di Framework come ereditare da classi per diversi motivi non prevedibile, quali l'aggiunta di membri maggiore praticità. Vedere [Classi non sealed](../../../docs/standard/design-guidelines/unsealed-classes.md) per alcuni dei motivi non prevedibile gli utenti desiderano ereditare da un tipo.  
  
 Buone ragioni per una classe, tra cui:  
  
-   La classe è una classe statica. Vedere [Progettazione di classi statiche](../../../docs/standard/design-guidelines/static-class.md).  
  
-   La classe archivia i segreti di protezione nei membri protetti ereditati.  
  
-   La classe eredita molti membri virtuali e i costi di bloccaggio li singolarmente si superano i vantaggi di lasciare la classe non sealed.  
  
-   La classe è un attributo che richiede ricerca runtime molto veloce. Gli attributi sealed hanno livelli di prestazioni leggermente superiori rispetto a quelli non sealed. Vedere [Attributi](../../../docs/standard/design-guidelines/attributi.md).  
  
 **X non** dichiarare membri virtuali o protetti su tipi sealed.  
  
 Per definizione, tipi sealed non possono essere ereditati da. Ciò significa che i membri protetti su tipi sealed non possono essere chiamati e metodi virtuali su tipi sealed non possono essere sottoposto a override.  
  
 **✓ PROVARE** sealing membri che si esegue l'override.  
  
 I problemi derivanti dall'introduzione di membri virtuali \(illustrati in [Membri virtuali](../../../docs/standard/design-guidelines/virtual-members.md)\) applicare sostituzioni, anche se a un livello leggermente inferiore. Bloccaggio di un override ci consente di nascondere questi problemi a partire da quel punto nella gerarchia di ereditarietà.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Progettazione finalizzata all'estensibilità](../../../docs/standard/design-guidelines/designing-for-extensibility.md)   
 [Classi non sealed](../../../docs/standard/design-guidelines/unsealed-classes.md)