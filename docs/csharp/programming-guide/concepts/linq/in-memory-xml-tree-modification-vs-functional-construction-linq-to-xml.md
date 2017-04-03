---
title: Differenze tra la modifica dell&quot;albero XML in memoria e la costruzione funzionale (LINQ to XML) (C#) | Microsoft Docs
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
ms.assetid: b5afc31d-a325-4ec6-bf17-0ff90a20ffca
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ed42b0d8acf1baeba84feb1d0a3ed72f2d3b76ea
ms.lasthandoff: 03/13/2017


---
# <a name="in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml-c"></a>Differenze tra la modifica dell'albero XML in memoria e la costruzione funzionale (LINQ to XML) (C#)
La modifica di un albero XML sul posto è un approccio tradizionale per cambiare la forma di un documento XML. In una tipica applicazione un documento viene caricato in un archivio dati quale DOM o [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], viene usata un'interfaccia di programmazione per inserire o eliminare nodi oppure per modificarne il contenuto, quindi il file XML viene salvato in un file o trasmesso tramite una rete.  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] consente di adottare un altro approccio che risulta utile in molti scenari: la *costruzione funzionale*. Nella costruzione funzionale la modifica di dati viene considerata come un problema di trasformazione, anziché come una modifica dettagliata di un archivio dati. Se è possibile trasformare in modo efficiente una rappresentazione di dati da un formato a un altro, il risultato è identico a quello ottenuto modificando un archivio dati in modo da cambiarne la forma. Un aspetto importante dell'approccio della costruzione funzionale riguarda il passaggio dei risultati delle query ai costruttori <xref:System.Xml.Linq.XDocument> e <xref:System.Xml.Linq.XElement>.  
  
 In molti casi, è possibile scrivere il codice di trasformazione in tempi ridotti rispetto a quelli richiesti per la modifica dell'archivio dati. Il codice è inoltre più affidabile e facile da gestire. In questi casi, anche se l'approccio della trasformazione può richiedere una maggiore potenza di elaborazione, si tratta di una soluzione più efficace per la modifica dei dati. Se gli sviluppatori hanno familiarità con l'approccio funzionale, il codice risultante è spesso più facile da comprendere. Risulta facile trovare il codice che modifica ogni parte dell'albero.  
  
 Molti programmatori DOM hanno una maggiore dimestichezza con l'approccio in cui un albero XML viene modificato sul posto, mentre il codice scritto con l'approccio funzionale potrebbe sembrare insolito agli sviluppatori che non hanno ancora compreso tale approccio. Se è necessario apportare solo una piccola modifica a un albero XML di grandi dimensioni, l'approccio in cui un albero viene modificato sul posto richiederà in molti casi meno tempo CPU.  
  
 In questo argomento viene illustrato un esempio implementato con entrambi gli approcci.  
  
## <a name="transforming-attributes-into-elements"></a>Trasformazione di attributi in elementi  
 Per questo esempio, si supponga di voler modificare il semplice documento XML seguente in modo che gli attributi diventino elementi. In questo argomento viene presentato dapprima l'approccio tradizionale della modifica sul posto e quindi l'approccio della costruzione funzionale.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<Root Data1="123" Data2="456">  
  <Child1>Content</Child1>  
</Root>  
```  
  
### <a name="modifying-the-xml-tree"></a>Modifica dell'albero XML  
 È possibile scrivere codice procedurale per creare elementi dagli attributi e quindi eliminare gli attributi, come segue:  
  
```csharp  
XElement root = XElement.Load("Data.xml");  
foreach (XAttribute att in root.Attributes()) {  
    root.Add(new XElement(att.Name, (string)att));  
}  
root.Attributes().Remove();  
Console.WriteLine(root);  
```  
  
 L'output del codice è il seguente:  
  
```xml  
<Root>  
  <Child1>Content</Child1>  
  <Data1>123</Data1>  
  <Data2>456</Data2>  
</Root>  
```  
  
### <a name="functional-construction-approach"></a>Approccio della costruzione funzionale  
 Al contrario, un approccio funzionale è costituito da codice per creare un nuovo albero, selezionando gli elementi e gli attributi dall'albero di origine e trasformandoli nel modo appropriato prima di aggiungerli nel nuovo albero. Di seguito è illustrato il risultato dell'approccio funzionale:  
  
```csharp  
XElement root = XElement.Load("Data.xml");  
XElement newTree = new XElement("Root",  
    root.Element("Child1"),  
    from att in root.Attributes()  
    select new XElement(att.Name, (string)att)  
);  
Console.WriteLine(newTree);  
```  
  
 In questo esempio viene restituito stesso lo stesso output XML del primo esempio. Si noti, tuttavia, che è possibile visualizzare la struttura risultante del nuovo codice XML nell'approccio funzionale. È quindi possibile vedere la creazione dell'elemento `Root`, il codice che effettua il pull dell'elemento `Child1` dall'albero di origine e il codice che trasforma gli attributi dell'albero di origine in elementi nel nuovo albero.  
  
 L'esempio funzionale in questo caso non è più breve del primo e in realtà non è neanche più semplice. Se tuttavia è necessario apportare molte modifiche a un albero XML, l'approccio non funzionale diventerà alquanto complesso e poco flessibile. Al contrario, quando si usa l'approccio funzionale, viene comunque creato l'XML desiderato, incorporando query ed espressioni nel modo appropriato, per inserire il contenuto desiderato. L'approccio funzionale restituisce codice più facile gestire.  
  
 Si noti che in questo caso le prestazioni dell'approccio funzionale potrebbero non essere uguali a quelle dell'approccio della modifica dell'albero. Il problema principale è che l'approccio funzionale crea più oggetti temporanei. Tuttavia, il problema è controbilanciato dalla maggiore produttività dei programmatori resa possibile da tale approccio.  
  
 Questo esempio è molto semplice, ma serve a illustrare le differenze concettuali tra i due approcci. L'approccio funzionale offre un aumento della produttività per la trasformazione di documenti XML di grandi dimensioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Modifica degli alberi XML (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
