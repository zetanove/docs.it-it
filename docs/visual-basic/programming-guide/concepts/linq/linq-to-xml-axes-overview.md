---
title: LINQ to XML Axes Panoramica (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 9161f151-cfa8-4408-94ba-08a9ba3a486d
caps.latest.revision: 4
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b127aa6b443e865c76831d886f110550ec785e9b
ms.lasthandoff: 03/13/2017


---
# <a name="linq-to-xml-axes-overview-visual-basic"></a>LINQ to panoramica degli assi XML (Visual Basic)
Dopo aver creato un albero XML o aver caricato un documento XML in un albero XML, è possibile eseguire query su di essa per cercare elementi e attributi e recuperarne i valori. Recuperare le raccolte tramite il *metodi dell'asse*, denominati anche *assi*. Alcuni degli assi sono metodi di <xref:System.Xml.Linq.XElement>e <xref:System.Xml.Linq.XDocument>le classi che restituiscono <xref:System.Collections.Generic.IEnumerable%601>raccolte.</xref:System.Collections.Generic.IEnumerable%601> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> Alcuni degli assi sono metodi di estensione nella <xref:System.Xml.Linq.Extensions>classe.</xref:System.Xml.Linq.Extensions> Gli assi implementati come metodi di estensione operano sulle raccolte e restituiscono raccolte.  
  
 Come descritto in [Cenni preliminari sulla classe XElement](http://msdn.microsoft.com/library/d35180fe-7016-4895-9bfc-ba1e3f7875ec), un <xref:System.Xml.Linq.XElement>oggetto rappresenta un nodo singolo elemento.</xref:System.Xml.Linq.XElement> Il contenuto di un elemento può essere semplice o complesso (talvolta definito contenuto strutturato). Un elemento semplice può essere vuoto o può contenere un valore. Se il nodo include contenuto strutturato, è possibile usare i diversi metodi dell'asse per recuperare enumerazioni di elementi discendente. I metodi dell'asse usati più di frequente sono <xref:System.Xml.Linq.XContainer.Elements%2A>e <xref:System.Xml.Linq.XContainer.Descendants%2A>.</xref:System.Xml.Linq.XContainer.Descendants%2A> </xref:System.Xml.Linq.XContainer.Elements%2A>  
  
 Oltre ai metodi dell'asse, che restituiscono raccolte, esistono altri due metodi che in genere si utilizzano in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] query. Il <xref:System.Xml.Linq.XContainer.Element%2A>metodo restituisce un singolo <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XContainer.Element%2A> Il <xref:System.Xml.Linq.XElement.Attribute%2A>metodo restituisce un singolo <xref:System.Xml.Linq.XAttribute>.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement.Attribute%2A>  
  
 Per molti scopi, le query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] costituiscono il modo più potente per esaminare un albero, estrarre dati da esso e trasformarlo. [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]le query vengono eseguite su oggetti che implementano <xref:System.Collections.Generic.IEnumerable%601>e [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] assi restituito <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>raccolte, e <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XAttribute>raccolte.</xref:System.Xml.Linq.XAttribute> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.Generic.IEnumerable%601> Tali raccolte sono necessarie per l'esecuzione delle query.  
  
 Oltre ai metodi dell'asse che recuperano raccolte di elementi e attributi, sono disponibili altri metodi dell'asse che consentono di scorrere l'albero con maggior dettaglio. Ad esempio, anziché gestire elementi e attributi, è possibile operare sui nodi dell'albero. I nodi costituiscono un livello di granularità più preciso rispetto a elementi e attributi. Quando usano i nodi, è possibile esaminare commenti XML, nodi di tipo text, istruzioni di elaborazione e altro ancora. Questa funzionalità è ad esempio utile per chi intende scrivere il codice per un elaboratore di testo e desidera salvare i documenti in formato XML. Tuttavia, la maggior parte dei programmatori XML è interessata principalmente a elementi, attributi e ai relativi valori.  
  
## <a name="methods-for-retrieving-a-collection-of-elements"></a>Metodi per il recupero di una raccolta di elementi  
 Di seguito è riportato un riepilogo dei metodi per la <xref:System.Xml.Linq.XElement>classe (o le relative classi base) che vengono chiamati su un <xref:System.Xml.Linq.XElement>per restituire una raccolta di elementi.</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XElement>  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=fullName>|Restituisce un <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>i predecessori di questo elemento.</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> Un overload restituisce un <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>predecessori che hanno specificato <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601>|  
|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName>|Restituisce un <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>i discendenti di questo elemento.</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> Un overload restituisce un <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>discendenti che hanno specificato <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601>|  
|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName>|Restituisce un <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>degli elementi figlio di questo elemento.</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> Un overload restituisce un <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>elementi figlio che hanno specificato <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601>|  
|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=fullName>|Restituisce un <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>degli elementi che seguono l'elemento.</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> Un overload restituisce un <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement>degli elementi che seguono l'elemento che hanno specificato <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601>|  
|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName>|Restituisce un <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>degli elementi che precedono l'elemento.</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> Un overload restituisce un <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement>degli elementi che precedono l'elemento che hanno specificato <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601>|  
|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=fullName>|Restituisce un <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>di questo elemento e i relativi predecessori.</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> Un overload restituisce un <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement>degli elementi che hanno specificato <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601>|  
|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=fullName>|Restituisce un <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>dell'elemento e dei relativi discendenti.</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> Un overload restituisce un <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement>degli elementi che hanno specificato <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601>|  
  
## <a name="method-for-retrieving-a-single-element"></a>Metodo per il recupero di un singolo elemento  
 Il metodo seguente consente di recuperare un singolo elemento figlio da un <xref:System.Xml.Linq.XElement>oggetto.</xref:System.Xml.Linq.XElement>  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Element%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.Element%2A?displayProperty=fullName>|Restituisce il primo figlio <xref:System.Xml.Linq.XElement>oggetto che ha specificato <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XElement>|  
  
## <a name="method-for-retrieving-a-collection-of-attributes"></a>Metodo per il recupero di una raccolta di attributi  
 Il metodo seguente recupera gli attributi da un <xref:System.Xml.Linq.XElement>oggetto.</xref:System.Xml.Linq.XElement>  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=fullName>|Restituisce un <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XAttribute>di tutti gli attributi.</xref:System.Xml.Linq.XAttribute> </xref:System.Collections.Generic.IEnumerable%601>|  
  
## <a name="method-for-retrieving-a-single-attribute"></a>Metodo per il recupero di un singolo attributo  
 Il metodo seguente consente di recuperare un singolo attributo da un <xref:System.Xml.Linq.XElement>oggetto.</xref:System.Xml.Linq.XElement>  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName>|Restituisce il <xref:System.Xml.Linq.XAttribute>che ha specificato <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XAttribute>|  
  
## <a name="see-also"></a>Vedere anche  
 [Assi LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
