---
title: Tipi di raccolta ordinati | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SortedDictionary collection type
- SortedList class, grouping data in collections
- grouping data in collections, SortedList collection type
- SortedList collection type
- collections [.NET Framework], SortedList collection type
ms.assetid: 3db965b2-36a6-4b12-b76e-7f074ff7275a
caps.latest.revision: 16
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 2ac1552dba8756d033ee02651142476c4a15a485
ms.lasthandoff: 04/18/2017

---
# <a name="sorted-collection-types"></a>Tipi di raccolta ordinati
La classe <xref:System.Collections.SortedList?displayProperty=fullName>, la classe generica <xref:System.Collections.Generic.SortedList%602?displayProperty=fullName> e la classe generica <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=fullName> sono simili alla classe <xref:System.Collections.Hashtable> e alla classe generica <xref:System.Collections.Generic.Dictionary%602> perché implementano l'interfaccia <xref:System.Collections.IDictionary>, ma conservano l'ordinamento degli elementi per chiave e non hanno il recupero e l'inserimento O(1) caratteristici delle tabelle hash. Le tre classi hanno diverse funzionalità in comune:  
  
-   Le tre classi implementano l'interfaccia <xref:System.Collections.IDictionary?displayProperty=fullName>. Le due classi generiche inoltre implementano l'interfaccia generica <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>.  
  
-   Ogni elemento è una coppia chiave/valore per scopi di enumerazione.  
  
    > [!NOTE]
    >  La classe non generica <xref:System.Collections.SortedList> restituisce oggetti <xref:System.Collections.DictionaryEntry> quando enumerata, nonostante i due tipi generici restituiscano oggetti <xref:System.Collections.Generic.KeyValuePair%602>.  
  
-   Gli elementi vengono ordinati in base a un'implementazione <xref:System.Collections.IComparer?displayProperty=fullName> (per la classe non generica <xref:System.Collections.SortedList>) o un'implementazione <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName> (per le due classi generiche).  
  
-   Ogni classe specifica le proprietà che restituiscono raccolte contenenti solo chiavi o solo valori.  
  
 Nella tabella seguente sono elencate alcune delle differenze tra le due classi SortedList e la classe <xref:System.Collections.Generic.SortedDictionary%602>.  
  
|Classe non generica <xref:System.Collections.SortedList> e classe generica <xref:System.Collections.Generic.SortedList%602>|Classe generica <xref:System.Collections.Generic.SortedDictionary%602>|  
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|Le proprietà che restituiscono chiavi e valori vengono indicizzate, consentendo un efficiente recupero indicizzato.|Senza recupero indicizzato.|  
|Il recupero è O(log `n`).|Il recupero è O(log `n`).|  
|L'inserimento e la rimozione sono in genere O(`n`); l'inserimento è tuttavia O(1) per i dati già presenti nell'ordinamento in modo che ogni elemento venga aggiunto alla fine dell'elenco. (Ciò presuppone che non sia necessario un ridimensionamento).|L'inserimento e la rimozione sono O(log `n`).|  
|Usa meno memoria rispetto a <xref:System.Collections.Generic.SortedDictionary%602>.|Usa più memoria rispetto alla classe non generica <xref:System.Collections.SortedList> e alla classe generica <xref:System.Collections.Generic.SortedList%602>.|  
  
 Per gli elenchi ordinati o i dizionari che devono essere accessibili contemporaneamente da più thread, è possibile aggiungere logica di ordinamento per una classe che deriva da <xref:System.Collections.Concurrent.ConcurrentDictionary%602>.  
  
> [!NOTE]
>  Per i valori che contengono le proprie chiavi (ad esempio, record dei dipendenti che contengono un numero di ID dipendente) è possibile creare una raccolta con chiave che include alcune caratteristiche di un elenco e alcune caratteristiche di un dizionario mediante la derivazione dalla classe generica <xref:System.Collections.ObjectModel.KeyedCollection%602>.  
  
 A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], la classe <xref:System.Collections.Generic.SortedSet%601> fornisce un albero auto-bilanciato che mantiene i dati ordinati dopo inserimenti, eliminazioni e ricerche. Questa classe e la classe <xref:System.Collections.Generic.HashSet%601> implementano l'interfaccia <xref:System.Collections.Generic.ISet%601>.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Collections.IDictionary?displayProperty=fullName>   
 <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>   
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602>   
 [Tipi di raccolte comunemente utilizzate](../../../docs/standard/collections/commonly-used-collection-types.md)
