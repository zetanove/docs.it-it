---
title: Costruzione funzionale (LINQ to XML) (Visual Basic) | Documenti di Microsoft
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
ms.assetid: feac4273-39ab-43ae-bab7-4059c807a785
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9fa8cb3c97a1e23a863296c828c82b240e9ab5db
ms.lasthandoff: 03/13/2017

---
# <a name="functional-construction-linq-to-xml-visual-basic"></a>Costruzione funzionale (LINQ to XML) (Visual Basic)
[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]fornisce un potente strumento per creare elementi XML chiamati *costruzione funzionale*. Per costruzione funzionale si intende la possibilità di creare una struttura ad albero XML in un'unica istruzione.  
  
 Diverse funzionalità importanti dell'interfaccia di programmazione [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] consentono la costruzione funzionale:  
  
-   Il <xref:System.Xml.Linq.XElement>costruttore accetta vari tipi di argomenti per il contenuto.</xref:System.Xml.Linq.XElement> Ad esempio, è possibile passare un altro <xref:System.Xml.Linq.XElement>oggetto, che diventa un elemento figlio.</xref:System.Xml.Linq.XElement> È possibile passare un <xref:System.Xml.Linq.XAttribute>oggetto, che diventa un attributo dell'elemento.</xref:System.Xml.Linq.XAttribute> Oppure è possibile passare qualsiasi altro tipo di oggetto, che viene convertito in una stringa e diventa il contenuto di testo dell'elemento.  
  
-   Il <xref:System.Xml.Linq.XElement>costruttore accetta un `params` matrice di tipo <xref:System.Object>, in modo che è possibile passare qualsiasi numero di oggetti al costruttore.</xref:System.Object> </xref:System.Xml.Linq.XElement> In questo modo è possibile creare un elemento con contenuto complesso.  
  
-   Se un oggetto implementa <xref:System.Collections.Generic.IEnumerable%601>, la raccolta nell'oggetto viene enumerata e vengono aggiunti tutti gli elementi nella raccolta.</xref:System.Collections.Generic.IEnumerable%601> Se la raccolta contiene <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XAttribute>oggetti, ogni elemento nella raccolta viene aggiunto separatamente.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> Questo è importante perché consente di passare i risultati di una [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query al costruttore.  
  
 Di seguito è riportato un esempio:  
  
 Queste funzionalità consentono di scrivere codice utilizzando i valori letterali XML per creare una struttura ad albero XML, nonché di scrivere codice che utilizza i risultati di [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] esegue una query quando si crea una struttura ad albero XML:  
  
```vb  
Dim srcTree As XElement = _  
    <Root>  
        <Element>1</Element>  
        <Element>2</Element>  
        <Element>3</Element>  
        <Element>4</Element>  
        <Element>5</Element>  
    </Root>  
Dim xmlTree As XElement = _  
    <Root>  
        <Child>1</Child>  
        <Child>2</Child>  
        <%= From el In srcTree.Elements() _  
            Where CInt(el) > 2 _  
            Select el %>  
    </Root>  
Console.WriteLine(xmlTree)  
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
 [Creazione di strutture ad albero XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)
