---
title: Costruzione funzionale (LINQ to XML) (C#) | Microsoft Docs
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
ms.assetid: 57a82bcf-de03-4f1c-a0c8-9a76e989d542
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
ms.openlocfilehash: aa522bb2c9d1c570aff237a76fc745bad52c8bfc
ms.lasthandoff: 03/13/2017

---
# <a name="functional-construction-linq-to-xml-c"></a>Costruzione funzionale (LINQ to XML) (C#)
In [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è disponibile una potente funzionalità per la creazione di elementi XML, denominata *costruzione funzionale*. Per costruzione funzionale si intende la possibilità di creare una struttura ad albero XML in un'unica istruzione.  
  
 Diverse funzionalità importanti dell'interfaccia di programmazione [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] consentono la costruzione funzionale:  
  
-   Il costruttore <xref:System.Xml.Linq.XElement> accetta vari tipi di argomenti come contenuto. Ad esempio, è possibile passare un altro oggetto <xref:System.Xml.Linq.XElement>, che diventa un elemento figlio. È possibile passare un oggetto <xref:System.Xml.Linq.XAttribute> che diventa un attributo dell'elemento. Oppure è possibile passare qualsiasi altro tipo di oggetto, che viene convertito in una stringa e diventa il contenuto di testo dell'elemento.  
  
-   Il costruttore <xref:System.Xml.Linq.XElement> accetta una matrice `params` di tipo <xref:System.Object>, quindi è possibile passare qualsiasi numero di oggetti al costruttore. In questo modo è possibile creare un elemento con contenuto complesso.  
  
-   Se un oggetto implementa <xref:System.Collections.Generic.IEnumerable%601>, la raccolta nell'oggetto viene enumerata e vengono aggiunti tutti gli elementi della raccolta. Se la raccolta contiene oggetti <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XAttribute>, ogni elemento della raccolta viene aggiunto separatamente. Questo aspetto è importante perché consente di passare i risultati di una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] al costruttore.  
  
 Queste funzionalità consentono di scrivere codice per creare un albero XML. Di seguito è riportato un esempio:  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),  
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
```  
  
 Queste funzionalità consentono anche di scrivere codice che usa i risultati di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] per creare un albero XML. Di seguito è riportato un esempio:  
  
```csharp  
XElement srcTree = new XElement("Root",  
    new XElement("Element", 1),  
    new XElement("Element", 2),  
    new XElement("Element", 3),  
    new XElement("Element", 4),  
    new XElement("Element", 5)  
);  
XElement xmlTree = new XElement("Root",  
    new XElement("Child", 1),  
    new XElement("Child", 2),  
    from el in srcTree.Elements()  
    where (int)el > 2  
    select el  
);  
Console.WriteLine(xmlTree);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Element>3</Element>  
  <Element>4</Element>  
  <Element>5</Element>  
</Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di alberi XML (C#)](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees.md)
