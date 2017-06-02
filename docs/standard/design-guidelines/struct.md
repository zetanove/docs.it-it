---
title: "Progettazione di struct | Microsoft Docs"
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
  - "classe libreria linee guida di progettazione [.NET Framework], strutture"
  - "deallocazione di strutture"
  - "allocazione di strutture"
  - "tipi di valore, strutture"
  - "progettazione di struttura"
  - "indicazioni per la progettazione di tipo, strutture"
  - "strutture di progettazione [.NET Framework]"
ms.assetid: 1f48b2d8-608c-4be6-9ba4-d8f203ed9f9f
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Progettazione di struct
Il tipo di valore generico è più noto anche come una struttura, la parola chiave c\#. In questa sezione vengono fornite linee guida per la progettazione di struct generale.  
  
 **X non** fornisce un costruttore predefinito per una struttura.  
  
 Attenendosi a questa linea guida consente matrici di strutture possono essere creati senza dover eseguire il costruttore su ogni elemento della matrice. Si noti che in c\# non consente strutture possono disporre di costruttori predefiniti.  
  
 **X non** definire tipi di valore modificabile.  
  
 Tipi di valore modificabile avere diversi problemi. Ad esempio, quando una metodo Get della proprietà viene restituito un tipo di valore, il chiamante riceve una copia. Poiché la copia viene creata in modo implicito, gli sviluppatori potrebbero non essere consapevoli che è Impossibile cambiare la copia e non il valore originale. Inoltre, alcuni linguaggi \(linguaggi dinamici, in particolare\) verificarsi dei problemi con tipi di valore modificabile perché anche le variabili locali, quando viene dereferenziato, causare una copia da eseguire.  
  
 **✓ si** garantire che uno stato in cui tutti i dati di istanza è impostato su zero, false o null \(come appropriato\) è valido.  
  
 Ciò impedisce la creazione accidentale di istanze non valide quando viene creata una matrice di strutture.  
  
 **✓ si** implementare <xref:System.IEquatable%601> sui tipi di valore.  
  
 Il <xref:System.Object.Equals%2A?displayProperty=fullName> metodo sui tipi di valore determina la conversione boxing e l'implementazione predefinita non è molto efficiente, poiché utilizza la reflection.<xref:System.IEquatable%601.Equals%2A> offre prestazioni migliori e può essere implementato in modo che questo evento non comporta la conversione boxing.  
  
 **X non** estendere in modo esplicito <xref:System.ValueType>. Infatti, la maggior parte dei linguaggi evitare questo problema.  
  
 In generale, le strutture possono essere molto utili ma devono essere utilizzate solo per i valori di piccole dimensioni, single, non modificabili che non essere boxed frequentemente.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di tipo](../../../docs/standard/design-guidelines/type.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Scelta tra classi e Struct](../../../docs/standard/design-guidelines/choosing-between-class-and-struct.md)