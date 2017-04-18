---
title: Utilizzo di spazi dei nomi globali (Visual Basic) (LINQ to XML) | Documenti di Microsoft
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
ms.assetid: 0a8064d5-e02f-4315-ad48-6deaa443a2f0
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
ms.openlocfilehash: e20d0c0b670d63ebe2be137a48dc1a1a9a861b9f
ms.lasthandoff: 03/13/2017

---
# <a name="working-with-global-namespaces-visual-basic-linq-to-xml"></a>Utilizzo di spazi dei nomi globali (Visual Basic) (LINQ to XML)
Una delle funzionalità chiave dei valori letterali XML in Visual Basic è la possibilità di dichiarare spazi dei nomi XML utilizzando il `Imports` istruzione. Tramite questa funzionalità, è possibile dichiarare uno spazio dei nomi XML che usa un prefisso oppure uno spazio dei nomi XML predefinito.  
  
 Questa funzionalità risulta utile in due situazioni. Innanzitutto gli spazi dei nomi dichiarati in valori letterali XML non vengono trasferiti nelle espressioni incorporate. La dichiarazione di spazi dei nomi globali riduce il numero di operazioni che è necessario eseguire per usare le espressioni incorporate con gli spazi dei nomi. In secondo luogo, è necessario dichiarare spazi dei nomi globali al fine di usare gli spazi dei nomi con le proprietà XML.  
  
 È possibile dichiarare spazi dei nomi globali a livello di progetto oppure a livello di modulo. In quest'ultimo caso gli spazi dei nomi eseguono l'override di quelli a livello di progetto. Infine è possibile eseguire l'override degli spazi dei nomi globali in un valore letterale XML.  
  
 Quando si usano i valori letterali o le proprietà XML incluse negli spazi dei nomi dichiarati a livello globale, è possibile visualizzare il nome espanso dei valori letterali o delle proprietà XML passandovi sopra con il mouse in Visual Studio. Il nome espanso verrà visualizzato in una descrizione comandi.  
  
 È possibile ottenere un <xref:System.Xml.Linq.XNamespace>oggetto che corrisponde a uno spazio dei nomi globale usando il `GetXmlNamespace` (metodo).</xref:System.Xml.Linq.XNamespace>  
  
## <a name="examples-of-global-namespaces"></a>Esempi di spazi dei nomi globali  
 Nell'esempio seguente viene dichiarato un spazio dei nomi globale predefinito usando il `Imports` istruzione, quindi viene utilizzato un valore letterale XML per inizializzare un <xref:System.Xml.Linq.XElement>oggetto nello spazio dei nomi:</xref:System.Xml.Linq.XElement>  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = <Root/>  
        Console.WriteLine(root)  
    End Sub  
End Module  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root xmlns="http://www.adventure-works.com" />  
```  
  
 Nell'esempio seguente viene dichiarato uno spazio dei nomi globale con un prefisso, quindi viene usato un valore letterale XML per inizializzare un elemento:  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = <aw:Root/>  
        Console.WriteLine(root)  
    End Sub  
End Module  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com" />  
```  
  
## <a name="global-namespaces-and-embedded-expressions"></a>Spazi dei nomi globali ed espressioni incorporate  
 Gli spazi dei nomi dichiarati in valori letterali XML non vengono trasferiti nelle espressioni incorporate. Nell'esempio seguente viene dichiarato uno spazio dei nomi predefinito. Viene quindi usata un'espressione incorporata per l'elemento `Child`.  
  
```vb  
Dim root As XElement = _  
    <Root xmlns="http://www.adventure-works.com">  
        <%= <Child/> %>  
    </Root>  
Console.WriteLine(root)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root xmlns="http://www.adventure-works.com">  
  <Child xmlns="" />  
</Root>  
```  
  
 Si noti che l'XML risultante include una dichiarazione di uno spazio dei nomi predefinito, per cui l'elemento `Child` non è incluso in alcuno spazio dei nomi.  
  
 È possibile ridichiarare lo spazio dei nomi nell'espressione incorporata, come segue:  
  
```vb  
Dim root As XElement = _  
    <Root xmlns="http://www.adventure-works.com">  
        <%= <Child xmlns="http://www.adventure-works.com"/> %>  
    </Root>  
Console.WriteLine(root)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root xmlns="http://www.adventure-works.com">  
  <Child xmlns="http://www.adventure-works.com" />  
</Root>  
```  
  
 Questa operazione è, tuttavia, piuttosto complessa. Un approccio più efficace è costituito dall'utilizzo dello spazio dei nomi predefinito globale, che consente di usare valori letterali XML senza dichiarare spazi dei nomi. L'XML risultante si troverà nello spazio dei nomi predefinito dichiarato a livello globale.  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = <Root>  
                                   <%= <Child/> %>  
                               </Root>  
        Console.WriteLine(root)  
    End Sub  
End Module  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root xmlns="http://www.adventure-works.com">  
  <Child />  
</Root>  
```  
  
## <a name="using-namespaces-with-xml-properties"></a>Utilizzo degli spazi dei nomi con proprietà XML  
 Se si usa un albero XML incluso in uno spazio dei nomi e si usano proprietà XML, è necessario usare uno spazio dei nomi globale in modi che anche le proprietà XML saranno incluse nello spazio dei nomi corretto. Nell'esempio seguente viene dichiarato un albero XML in uno spazio dei nomi. Viene quindi stampato il conteggio degli elementi `Child`.  
  
```vb  
Dim root As XElement = _  
    <Root xmlns="http://www.adventure-works.com">  
        <Child>content</Child>  
    </Root>  
Console.WriteLine(root.<Child>.Count())  
```  
  
 L'esempio indica che non sono presenti elementi `Child`. L'output è il seguente:  
  
```  
0  
```  
  
 Se tuttavia viene dichiarato uno spazio dei nomi globale predefinito, sia i valori letterali XML che la proprietà XML si trovano nello spazio dei nomi globale predefinito:  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <Root>  
                <Child>content</Child>  
            </Root>  
        Console.WriteLine(root.<Child>.Count())  
    End Sub  
End Module  
```  
  
 L'esempio indica che è presente un unico elemento `Child`. L'output è il seguente:  
  
```  
1  
```  
  
 Se si dichiara uno spazio dei nomi globale che ha un prefisso, è possibile usare il prefisso per i valori letterali e le proprietà XML:  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <aw:Child>content</aw:Child>  
            </aw:Root>  
        Console.WriteLine(root.<aw:Child>.Count())  
    End Sub  
End Module  
```  
  
## <a name="xnamespace-and-global-namespaces"></a>XNamespace e spazi dei nomi globali  
 È possibile ottenere un <xref:System.Xml.Linq.XNamespace>oggetto utilizzando il `GetXmlNamespace` metodo:</xref:System.Xml.Linq.XNamespace>  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = <aw:Root/>  
        Dim xn As XNamespace = GetXmlNamespace(aw)  
        Console.WriteLine(xn)  
    End Sub  
End Module  
```  
  
 Questo esempio produce il seguente output:  
  
```  
http://www.adventure-works.com  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di spazi dei nomi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md)
