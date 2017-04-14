---
title: "Tipi di raccolta ordinati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "raccolte [.NET Framework], SortedList (tipo di raccolta)"
  - "raggruppamento di dati in raccolte, SortedList (tipo di raccolta)"
  - "SortedDictionary (tipo di raccolta)"
  - "SortedList (classe), raggruppamento di dati in raccolte"
  - "SortedList (tipo di raccolta)"
ms.assetid: 3db965b2-36a6-4b12-b76e-7f074ff7275a
caps.latest.revision: 16
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 16
---
# Tipi di raccolta ordinati
La classe <xref:System.Collections.SortedList?displayProperty=fullName> e le classi generiche <xref:System.Collections.Generic.SortedList%602?displayProperty=fullName> e <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=fullName> sono simili alla classe <xref:System.Collections.Hashtable> e alla classe generica <xref:System.Collections.Generic.Dictionary%602> in quanto implementano l'interfaccia <xref:System.Collections.IDictionary>, ma si distinguono da queste perché mantengono i rispettivi elementi ordinati per chiave e non presentano la caratteristica di inserimento e recupero basata su O\(1\) delle tabelle hash.  Le tre classi hanno diverse funzionalità comuni:  
  
-   Tutte e tre le classi implementano l'interfaccia <xref:System.Collections.IDictionary?displayProperty=fullName>.  Le due classi generiche implementano anche l'interfaccia generica <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>.  
  
-   Ciascun elemento è costituito da una coppia chiave\-valore a scopo di enumerazione.  
  
    > [!NOTE]
    >  In caso di enumerazione, la classe non generica <xref:System.Collections.SortedList> restituisce oggetti <xref:System.Collections.DictionaryEntry>, sebbene i due tipi generici restituiscano oggetti <xref:System.Collections.Generic.KeyValuePair%602>.  
  
-   Gli elementi vengono ordinati in base a un'implementazione di <xref:System.Collections.IComparer?displayProperty=fullName> \(per la classe non generica <xref:System.Collections.SortedList>\) oppure in base a un'implementazione di <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName> \(per le due classi generiche\).  
  
-   Per ciascuna classe sono disponibili proprietà per la restituzione di raccolte contenenti solo le chiavi o solo i valori.  
  
 Nella seguente tabella sono riportate le differenze tra le due classi SortedList e la classe <xref:System.Collections.Generic.SortedDictionary%602>.  
  
|Classe non generica <xref:System.Collections.SortedList> e classe generica <xref:System.Collections.Generic.SortedList%602>|Classe generica <xref:System.Collections.Generic.SortedDictionary%602>|  
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|Le proprietà che restituiscono chiavi e valori sono indicizzate, in modo da rendere efficiente il recupero indicizzato.|Il recupero indicizzato non è supportato.|  
|Il recupero è basato su O\(log `n`\).|Il recupero è basato su O\(log `n`\).|  
|L'inserimento e la rimozione sono in genere basati su O\(`n`\). Tuttavia, per i dati già ordinati l'inserimento è basato su O\(1\), in modo che ciascun elemento venga aggiunto alla fine dell'elenco. Questo presuppone che non sia necessario un ridimensionamento.|L'inserimento e la rimozione sono basati su O\(log `n`\).|  
|Viene utilizzata una minore quantità di memoria rispetto alla classe <xref:System.Collections.Generic.SortedDictionary%602>.|Viene utilizzata una maggiore quantità di memoria rispetto alla classe non generica <xref:System.Collections.SortedList> e alla classe generica <xref:System.Collections.Generic.SortedList%602>.|  
  
 Per dizionari o elenchi ordinati che devono essere accessibili contemporaneamente da più thread, è possibile aggiungere logica di ordinamento a una classe derivata da <xref:System.Collections.Concurrent.ConcurrentDictionary%602>.  
  
> [!NOTE]
>  Per i valori che contengono le rispettive chiavi, ad esempio i record dei dipendenti contenenti un ID dipendente, è possibile creare una raccolta con chiavi che presenti alcune caratteristiche di un elenco e altre di un dizionario mediante la derivazione dalla classe generica <xref:System.Collections.ObjectModel.KeyedCollection%602>.  
  
 A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], la classe <xref:System.Collections.Generic.SortedSet%601> fornisce una struttura ad albero auto\-bilanciata che mantiene i dati ordinati dopo operazioni di inserimento, eliminazione e ricerca.  Questa classe e la classe <xref:System.Collections.Generic.HashSet%601> implementano l'interfaccia <xref:System.Collections.Generic.ISet%601>.  
  
## Vedere anche  
 <xref:System.Collections.IDictionary?displayProperty=fullName>   
 <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>   
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602>   
 [Tipi di raccolte comunemente utilizzate](../../../docs/standard/collections/commonly-used-collection-types.md)