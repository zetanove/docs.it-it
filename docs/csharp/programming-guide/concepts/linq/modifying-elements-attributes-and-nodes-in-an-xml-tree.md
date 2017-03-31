---
title: Modifica di elementi, attributi e nodi in un albero XML | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 0ed22e4e-4c6b-4eb1-b0eb-06685efd8c33
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6fa51b22af73d716b01444540edb7c8d814cd293
ms.lasthandoff: 03/13/2017


---
# <a name="modifying-elements-attributes-and-nodes-in-an-xml-tree"></a>Modifica di elementi, attributi e nodi in un albero XML
Nella tabella seguente sono riepilogati i metodi e le proprietà che è possibile usare per modificare un elemento, i relativi elementi figlio o gli attributi.  
  
 I metodi seguenti modificano <xref:System.Xml.Linq.XElement>.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName>|Sostituisce un elemento con XML analizzato.|  
|<xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=fullName>|Rimuove tutto il contenuto di un elemento (nodi figlio e attributi).|  
|<xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=fullName>|Rimuove gli attributi di un elemento.|  
|<xref:System.Xml.Linq.XElement.ReplaceAll%2A?displayProperty=fullName>|Sostituisce tutto il contenuto di un elemento (nodi figlio e attributi).|  
|<xref:System.Xml.Linq.XElement.ReplaceAttributes%2A?displayProperty=fullName>|Sostituisce gli attributi di un elemento.|  
|<xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=fullName>|Imposta il valore di un attributo. Crea l'attributo se non esiste. Se il valore è impostato su `null`, rimuove l'attributo.|  
|<xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=fullName>|Imposta il valore di un elemento figlio. Crea l'elemento se non esiste. Se il valore è impostato su `null`, rimuove l'elemento.|  
|<xref:System.Xml.Linq.XElement.Value%2A?displayProperty=fullName>|Sostituisce il contenuto (nodi figlio) di un elemento con il testo specificato.|  
|<xref:System.Xml.Linq.XElement.SetValue%2A?displayProperty=fullName>|Imposta il valore di un elemento.|  
  
 I metodi seguenti modificano <xref:System.Xml.Linq.XAttribute>.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=fullName>|Imposta il valore di un attributo.|  
|<xref:System.Xml.Linq.XAttribute.SetValue%2A?displayProperty=fullName>|Imposta il valore di un attributo.|  
  
 I metodi seguenti modificano <xref:System.Xml.Linq.XNode> (incluso <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XDocument>).  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.ReplaceWith%2A?displayProperty=fullName>|Sostituisce un nodo con nuovo contenuto.|  
  
 I metodi seguenti modificano <xref:System.Xml.Linq.XContainer> (<xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XDocument>).  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.ReplaceNodes%2A?displayProperty=fullName>|Sostituisce i nodi figlio con nuovo contenuto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Modifica degli alberi XML (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
