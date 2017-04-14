---
title: "Progettazione dell&#39;interfaccia | Microsoft Docs"
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
  - "interfacce [.NET Framework], linee guida di progettazione"
  - "indicazioni per la progettazione di tipo, le interfacce"
  - "classe libreria linee guida di progettazione [.NET Framework], interfacce"
ms.assetid: a016bd18-6710-4358-9438-9f190a295392
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Progettazione dell&#39;interfaccia
Sebbene la maggior parte delle API meglio vengono modellate utilizzando le classi e struct, vi sono casi in cui le interfacce sono più appropriati o l'unica opzione.  
  
 CLR supporta l'ereditarietà multipla \(ad esempio, le classi CLR non possono ereditare da più di una classe di base\), ma consente i tipi per implementare una o più interfacce oltre che eredita da una classe di base. Di conseguenza, vengono spesso utilizzate per ottenere l'effetto di ereditarietà multipla. Ad esempio, <xref:System.IDisposable> è un'interfaccia che consente ai tipi di supporto disposability indipendente da qualsiasi altra gerarchia di ereditarietà in cui si desidera partecipare.  
  
 L'altro caso in cui la definizione di un'interfaccia è appropriata è durante la creazione di un'interfaccia comune che può essere supportata da diversi tipi, inclusi alcuni tipi di valore. Tipi di valore non possono ereditare da tipi diversi da <xref:System.ValueType>, ma possono implementare interfacce, pertanto, tramite un'interfaccia è l'unica opzione per fornire un tipo base comune.  
  
 **✓ si** definire un'interfaccia se è necessario alcune API comuni devono essere supportati da un set di tipi che include i tipi di valore.  
  
 **✓ PROVARE** definisce un'interfaccia se è necessario supportare la funzionalità per i tipi che ereditano già da un altro tipo.  
  
 **X evitare** utilizzare interfacce marker \(interfacce senza membri\).  
  
 Se è necessario contrassegnare una classe con una caratteristica specifica \(indicatore\), in generale, utilizzare un attributo personalizzato anziché un'interfaccia.  
  
 **✓ si** fornire almeno un tipo che è un'implementazione di un'interfaccia.  
  
 Eseguendo questo consente di convalidare la struttura dell'interfaccia. Ad esempio, <xref:System.Collections.Generic.List%601> è un'implementazione del <xref:System.Collections.Generic.IList%601> interfaccia.  
  
 **✓ si** forniscono almeno una API che utilizza ciascuna interfaccia definita \(un metodo che l'interfaccia come parametro o una proprietà tipizzata come l'interfaccia\).  
  
 Eseguendo questo consente di convalidare la progettazione dell'interfaccia. Ad esempio, <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=fullName> utilizza il <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName> interfaccia.  
  
 **X non** aggiungere membri a un'interfaccia fornita in precedenza.  
  
 In questo modo potrebbe compromettere le implementazioni dell'interfaccia. Per evitare problemi di controllo delle versioni, è necessario creare una nuova interfaccia.  
  
 Fatta eccezione per le situazioni descritte in queste linee guida, è consigliabile, in generale, scegliere classi anziché le interfacce nella progettazione di librerie riutilizzabili di codice gestito.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di tipo](../../../docs/standard/design-guidelines/type.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)