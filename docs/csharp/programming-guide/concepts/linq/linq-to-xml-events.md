---
title: Eventi LINQ to XML (C#) | Microsoft Docs
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
ms.assetid: ce7de951-cba7-4870-9962-733eb01cd680
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f19439004a9551f5e13588201ca3aaf201620681
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-events-c"></a>Eventi LINQ to XML (C#)
Gli eventi [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] consentono di ricevere una notifica quando un albero XML viene modificato.  
  
 È possibile aggiungere eventi a un'istanza di qualsiasi <xref:System.Xml.Linq.XObject>. Il gestore eventi riceverà quindi gli eventi relativi alle modifiche apportate a <xref:System.Xml.Linq.XObject> e a tutti i relativi discendenti. Ad esempio, è possibile aggiungere un gestore eventi alla radice dell'albero e gestire tutte le modifiche apportate alla struttura da tale gestore.  
  
 Per esempi di eventi [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], vedere <xref:System.Xml.Linq.XObject.Changing> e <xref:System.Xml.Linq.XObject.Changed>.  
  
## <a name="types-and-events"></a>Tipi ed eventi  
 Con gli eventi è possibile usare i tipi seguenti:  
  
|Tipo|Descrizione|  
|----------|-----------------|  
|<xref:System.Xml.Linq.XObjectChange>|Specifica il tipo di evento quando viene generato un evento per <xref:System.Xml.Linq.XObject>.|  
|<xref:System.Xml.Linq.XObjectChangeEventArgs>|Specifica i dati per gli eventi <xref:System.Xml.Linq.XObject.Changing> e <xref:System.Xml.Linq.XObject.Changed>.|  
  
 Gli eventi seguenti vengono generati quando si modifica una struttura ad albero XML:  
  
|Evento|Descrizione|  
|-----------|-----------------|  
|<xref:System.Xml.Linq.XObject.Changing>|Si verifica poco prima che <xref:System.Xml.Linq.XObject> o uno qualsiasi dei relativi discendenti venga modificato.|  
|<xref:System.Xml.Linq.XObject.Changed>|Si verifica quando <xref:System.Xml.Linq.XObject> o uno qualsiasi dei relativi discendenti viene modificato.|  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 Gli eventi sono utili quando si desidera gestire alcune informazioni di aggregazione in un albero XML. Ad esempio, si desidera gestire un totale di fattura che corrisponde alla somma delle voci della fattura. In questo esempio vengono usati gli eventi per gestire il totale di tutti gli elementi figlio sotto l'elemento `Items` complesso.  
  
### <a name="code"></a>Codice  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Total", "0"),  
    new XElement("Items")  
);  
XElement total = root.Element("Total");  
XElement items = root.Element("Items");  
items.Changed += (object sender, XObjectChangeEventArgs cea) =>  
{  
    switch (cea.ObjectChange)  
    {  
        case XObjectChange.Add:  
            if (sender is XElement)  
                total.Value = ((int)total + (int)(XElement)sender).ToString();  
            if (sender is XText)  
                total.Value = ((int)total + (int)((XText)sender).Parent).ToString();  
            break;  
        case XObjectChange.Remove:  
            if (sender is XElement)  
                total.Value = ((int)total - (int)(XElement)sender).ToString();  
            if (sender is XText)  
                total.Value = ((int)total - Int32.Parse(((XText)sender).Value)).ToString();  
            break;  
    }  
    Console.WriteLine("Changed {0} {1}",  
      sender.GetType().ToString(), cea.ObjectChange.ToString());  
};  
items.SetElementValue("Item1", 25);  
items.SetElementValue("Item2", 50);  
items.SetElementValue("Item2", 75);  
items.SetElementValue("Item3", 133);  
items.SetElementValue("Item1", null);  
items.SetElementValue("Item4", 100);  
Console.WriteLine("Total:{0}", (int)total);  
Console.WriteLine(root);  
```  
  
### <a name="comments"></a>Commenti  
 L'output del codice è il seguente:  
  
```  
Changed System.Xml.Linq.XElement Add  
Changed System.Xml.Linq.XElement Add  
Changed System.Xml.Linq.XText Remove  
Changed System.Xml.Linq.XText Add  
Changed System.Xml.Linq.XElement Add  
Changed System.Xml.Linq.XElement Remove  
Changed System.Xml.Linq.XElement Add  
Total:308  
<Root>  
  <Total>308</Total>  
  <Items>  
    <Item2>75</Item2>  
    <Item3>133</Item3>  
    <Item4>100</Item4>  
  </Items>  
</Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione LINQ to XML avanzata (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
