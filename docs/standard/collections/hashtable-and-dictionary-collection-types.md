---
title: "Tipi di raccolte Hashtable e Dictionary | Microsoft Docs"
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
  - "raccolte [.NET Framework], Hashtable (tipo di raccolta)"
  - "raggruppamento di dati in raccolte, Hashtable (tipo di raccolta)"
  - "hash (funzione)"
  - "tabelle hash"
  - "Hashtable (classe), raggruppamento di dati in raccolte"
  - "Hashtable (tipo di raccolta)"
ms.assetid: bfc20837-3d02-4fc7-8a8f-c5215b6b7913
caps.latest.revision: 16
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 16
---
# Tipi di raccolte Hashtable e Dictionary
La classe <xref:System.Collections.Hashtable?displayProperty=fullName> e le classi generiche <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> e <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName> implementano l'interfaccia <xref:System.Collections.IDictionary?displayProperty=fullName>.  La classe generica <xref:System.Collections.Generic.Dictionary%602> implementa inoltre l'interfaccia generica <xref:System.Collections.Generic.IDictionary%602>.  Ogni elemento di queste raccolte è pertanto una coppia chiave\-valore.  
  
 Un oggetto <xref:System.Collections.Hashtable> è costituito da bucket che contengono gli elementi della raccolta.  Un bucket è un sottogruppo virtuale di elementi all'interno di <xref:System.Collections.Hashtable>, che rende più semplici e veloci le operazioni di ricerca e recupero rispetto alla maggior parte delle raccolte.  Ogni bucket è associato a un codice hash, generato usando una funzione hash ed basato sulla chiave dell'elemento.  
  
 La classe generica <xref:System.Collections.Generic.HashSet%601> è una raccolta non ordinata destinata a contenere elementi univoci.  
  
 Una funzione hash è un algoritmo che restituisce un codice hash numerico basato su una chiave.  La chiave è il valore di una proprietà dell'oggetto che viene archiviato.  Una funzione hash deve sempre restituire lo stesso codice hash per la stessa chiave.  È possibile per una funzione hash generare lo stesso codice hash per due chiavi diverse, ma una funzione hash che genera un codice hash univoco per ogni chiave univoca offre prestazioni migliori durante il recupero di elementi dalla tabella hash.  
  
 Ogni oggetto usato come elemento in un oggetto <xref:System.Collections.Hashtable> deve essere in grado di generare un codice hash per se stesso tramite un'implementazione del metodo <xref:System.Object.GetHashCode%2A>.  È tuttavia anche possibile specificare una funzione hash per tutti gli elementi in un oggetto <xref:System.Collections.Hashtable> usando un costruttore <xref:System.Collections.Hashtable> che accetta un'implementazione di <xref:System.Collections.IHashCodeProvider> come uno dei parametri.  
  
 Quando un oggetto viene aggiunto a <xref:System.Collections.Hashtable>, viene archiviato nel bucket associato al codice hash corrispondente al codice hash dell'oggetto.  Quando viene cercato un valore in <xref:System.Collections.Hashtable>, viene generato il codice hash per tale valore e viene eseguita la ricerca nel bucket associato a tale codice hash.  
  
 Ad esempio, una funzione hash per una stringa potrebbe prendere i codici ASCII di ogni carattere della stringa e combinarli per generare un codice hash.  La stringa "picnic" avrebbe un codice hash diverso da quello della stringa "basket", pertanto le due stringhe si troverebbero in bucket diversi.  "Stressed" e "desserts" avrebbero invece lo stesso codice hash e si troverebbero nello stesso bucket.  
  
 Le classi <xref:System.Collections.Generic.Dictionary%602> e <xref:System.Collections.Concurrent.ConcurrentDictionary%602> ``  hanno la stessa funzionalità della classe <xref:System.Collections.Hashtable>.  Un oggetto <xref:System.Collections.Generic.Dictionary%602> di un tipo specifico \(diverso da <xref:System.Object>\) offre prestazioni migliori rispetto a un oggetto <xref:System.Collections.Hashtable> per i tipi di valore,  in quanto gli elementi di <xref:System.Collections.Hashtable> sono di tipo <xref:System.Object>. Le conversioni boxing e unboxing vengono in genere eseguite quando si archivia o si recupera un tipo di valore.  La classe <xref:System.Collections.Concurrent.ConcurrentDictionary%602> ``  deve essere usata quando più thread potrebbero accedere contemporaneamente alla raccolta.  
  
## Vedere anche  
 <xref:System.Collections.Hashtable>   
 <xref:System.Collections.IDictionary>   
 <xref:System.Collections.IHashCodeProvider>   
 <xref:System.Collections.Generic.Dictionary%602>   
 <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>   
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName>   
 [Tipi di raccolte comunemente utilizzate](../../../docs/standard/collections/commonly-used-collection-types.md)