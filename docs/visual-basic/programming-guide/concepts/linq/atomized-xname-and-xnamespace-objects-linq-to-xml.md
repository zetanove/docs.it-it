---
title: Scomporre oggetti XName e XNamespace (LINQ to XML) (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 21ee7585-7df9-40b4-8c76-a12bb5f29bb3
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b08f3116f5acb404cf2c33072ec31fbaada4e7cb
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017


---
# <a name="atomized-xname-and-xnamespace-objects-linq-to-xml-visual-basic"></a>Scomporre oggetti XName e XNamespace (LINQ to XML) (Visual Basic)
<xref:System.Xml.Linq.XName>e <xref:System.Xml.Linq.XNamespace>sono oggetti *atomizzati*; ovvero, se contengono lo stesso nome completo, fanno riferimento allo stesso oggetto.</xref:System.Xml.Linq.XNamespace></xref:System.Xml.Linq.XName> Questo offre vantaggi a livello di prestazioni per le query: quando si confrontano due nomi atomizzati per verificarne l'uguaglianza, il linguaggio intermedio sottostante deve determinare solo se i due riferimenti puntano allo stesso oggetto. Il codice sottostante non deve eseguire confronti tra stringhe, che richiederebbero molto tempo.  
  
## <a name="atomization-semantics"></a>Semantica di atomizzazione  
 Atomizzazione significa che se due <xref:System.Xml.Linq.XName>gli oggetti hanno lo stesso nome locale e si trovano nello stesso spazio dei nomi, condividono la stessa istanza.</xref:System.Xml.Linq.XName> Nello stesso modo, se due <xref:System.Xml.Linq.XNamespace>gli oggetti hanno lo stesso URI dei nomi, condividono la stessa istanza.</xref:System.Xml.Linq.XNamespace>  
  
 Affinché una classe consenta gli oggetti atomizzati, il costruttore per la classe deve essere privato, non pubblico. Se il costruttore fosse pubblico, sarebbe possibile creare un oggetto non atomizzato. <xref:System.Xml.Linq.XName>E <xref:System.Xml.Linq.XNamespace>le classi implementano un operatore di conversione implicita per convertire una stringa in un <xref:System.Xml.Linq.XName>o <xref:System.Xml.Linq.XNamespace>.</xref:System.Xml.Linq.XNamespace> </xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XNamespace> </xref:System.Xml.Linq.XName> In questo modo è possibile ottenere un'istanza di questi oggetti. Non è possibile ottenere un'istanza tramite un costruttore, in quanto il costruttore è inaccessibile.  
  
 <xref:System.Xml.Linq.XName>e <xref:System.Xml.Linq.XNamespace>implementare anche gli operatori di uguaglianza e disuguaglianza, per determinare se i due oggetti confrontati sono riferimenti alla stessa istanza.</xref:System.Xml.Linq.XNamespace></xref:System.Xml.Linq.XName>  
  
## <a name="example"></a>Esempio  
 Il codice seguente vengono creati alcuni <xref:System.Xml.Linq.XElement>gli oggetti e viene dimostrato che i nomi identici condividono la stessa istanza.</xref:System.Xml.Linq.XElement>  
  
```vb  
Dim r1 As New XElement("Root", "data1")  
Dim r2 As XElement = XElement.Parse("<Root>data2</Root>")  
  
If DirectCast(r1.Name, Object) = DirectCast(r2.Name, Object) Then  
    Console.WriteLine("r1 and r2 have names that refer to the same instance.")  
Else  
    Console.WriteLine("Different")  
End If  
  
Dim n As XName = "Root"  
  
If DirectCast(n, Object) = DirectCast(r1.Name, Object) Then  
    Console.WriteLine("The name of r1 and the name in 'n' refer to the same instance.")  
Else  
    Console.WriteLine("Different")  
End If  
```  
  
 Questo esempio produce il seguente output:  
  
```  
r1 and r2 have names that refer to the same instance.  
The name of r1 and the name in 'n' refer to the same instance.  
```  
  
 Come accennato in precedenza, il vantaggio degli oggetti atomizzati è che quando si utilizza uno dei metodi dell'asse che accettano un <xref:System.Xml.Linq.XName>come parametro, il metodo dell'asse deve determinare solo che due nomi fanno riferimento alla stessa istanza per selezionare gli elementi desiderati.</xref:System.Xml.Linq.XName>  
  
 Nell'esempio seguente viene passato un <xref:System.Xml.Linq.XName>per il <xref:System.Xml.Linq.XContainer.Descendants%2A>chiamata al metodo, che quindi offre prestazioni migliori grazie al modello di atomizzazione.</xref:System.Xml.Linq.XContainer.Descendants%2A> </xref:System.Xml.Linq.XName>  
  
```vb  
Dim root As New XElement("Root", New XElement("C1", 1), New XElement("Z1", New XElement("C1", 2), New XElement("C1", 1)))  
  
Dim query = From e In root.Descendants("C1") Where CInt(e) = 1e  
  
For Each z As var In query  
    Console.WriteLine(z)  
Next  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<C1>1</C1>  
<C1>1</C1>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Prestazioni (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/performance-linq-to-xml.md)

