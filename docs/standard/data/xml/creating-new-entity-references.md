---
title: "Creazione di nuovi riferimenti alle entit&#224; | Microsoft Docs"
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
ms.assetid: a42f81b3-0403-4e34-b346-7d2129804e54
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Creazione di nuovi riferimenti alle entit&#224;
Il metodo **CreateEntityReference** consente di creare un nuovo nodo **XmlEntityReference**.  Il modello DOM XML cerca di vedere se il nome dell'entità a cui si fa riferimento è già stato dichiarato.  In caso affermativo, i nodi figlio del nodo **XmlEntityReference** vengono copiati dal nodo della dichiarazione di entità.  Se non vi è alcuna dichiarazione di entità corrispondente, viene associato un nodo di testo vuoto come unico figlio del nodo del riferimento all'entità.  Poiché i nodi figlio del nodo **XmlEntityReference** sono copie di altri nodi, questi nodi figlio sono in sola lettura e non è possibile modificarli.  
  
 Dopo aver copiato i nodi, è probabile che vi sia uno spazio dei nomi nell'area di validità nel punto del riferimento all'entità.  Tale spazio dei nomi incide sulla configurazione di qualsiasi nodo di elemento o di attributo generato.  
  
> [!NOTE]
>  Il DOM aggiunge nodi figlio a **EntityReference** solo quando si inserisce tale nodo nel documento.  I nodi **EntityReference** appena creati non hanno nodi figlio.  
  
 Anche se **XmlDataDocument** è una classe derivata di **XmlDocument**, **XmlDataDocument** non supporta la creazione di riferimenti alle entità,  dal momento che gli elementi figlio di **EntityReference** sono in sola lettura.  I nodi figlio di un nodo **EntityReference** possono interessare più di una regione.  In tal caso, la parte di riga associata alla regione contenente una parte di **EntityReference** sarà di sola lettura.  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)