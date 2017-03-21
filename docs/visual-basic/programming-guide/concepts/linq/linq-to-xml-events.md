---
title: Eventi LINQ to XML (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 34923928-b99c-4004-956e-38f6db25e910
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2b7756845f155c4683015d54b41f2ecc09b29333
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-events-visual-basic"></a>Eventi LINQ to XML (Visual Basic)
[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]gli eventi consentono di ricevere una notifica quando un albero XML viene modificato.  
  
 È possibile aggiungere eventi a un'istanza di qualsiasi <xref:System.Xml.Linq.XObject>.</xref:System.Xml.Linq.XObject> Il gestore eventi riceverà quindi gli eventi per apportare modifiche a cui <xref:System.Xml.Linq.XObject>e dei relativi discendenti.</xref:System.Xml.Linq.XObject> Ad esempio, è possibile aggiungere un gestore eventi alla radice dell'albero e gestire tutte le modifiche apportate alla struttura da tale gestore.  
  
 Per esempi di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] gli eventi, vedere <xref:System.Xml.Linq.XObject.Changing>e <xref:System.Xml.Linq.XObject.Changed>.</xref:System.Xml.Linq.XObject.Changed> </xref:System.Xml.Linq.XObject.Changing>  
  
## <a name="types-and-events"></a>Tipi ed eventi  
 Con gli eventi è possibile usare i tipi seguenti:  
  
|Tipo|Descrizione|  
|----------|-----------------|  
|<xref:System.Xml.Linq.XObjectChange></xref:System.Xml.Linq.XObjectChange>|Specifica il tipo di evento quando viene generato un evento per un <xref:System.Xml.Linq.XObject>.</xref:System.Xml.Linq.XObject>|  
|<xref:System.Xml.Linq.XObjectChangeEventArgs></xref:System.Xml.Linq.XObjectChangeEventArgs>|Fornisce dati per il <xref:System.Xml.Linq.XObject.Changing>e <xref:System.Xml.Linq.XObject.Changed>gli eventi.</xref:System.Xml.Linq.XObject.Changed> </xref:System.Xml.Linq.XObject.Changing>|  
  
 Gli eventi seguenti vengono generati quando si modifica una struttura ad albero XML:  
  
|Evento|Descrizione|  
|-----------|-----------------|  
|<xref:System.Xml.Linq.XObject.Changing></xref:System.Xml.Linq.XObject.Changing>|Si verifica poco prima che il <xref:System.Xml.Linq.XObject>o dei relativi discendenti viene modificato.</xref:System.Xml.Linq.XObject>|  
|<xref:System.Xml.Linq.XObject.Changed></xref:System.Xml.Linq.XObject.Changed>|Si verifica quando un <xref:System.Xml.Linq.XObject>è stato modificato o uno qualsiasi dei relativi discendenti viene modificato.</xref:System.Xml.Linq.XObject>|  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 Gli eventi sono utili quando si desidera gestire alcune informazioni di aggregazione in un albero XML. Ad esempio, si desidera gestire un totale di fattura che corrisponde alla somma delle voci della fattura. In questo esempio vengono usati gli eventi per gestire il totale di tutti gli elementi figlio sotto l'elemento `Items` complesso.  
  
### <a name="code"></a>Codice  
  
```vb  
Module Module1  
    Dim WithEvents items As XElement = Nothing  
    Dim total As XElement = Nothing  
    Dim root As XElement = _  
            <Root>  
                <Total>0</Total>  
                <Items></Items>  
            </Root>  
  
    Private Sub XObjectChanged( _  
            ByVal sender As Object, _  
            ByVal cea As XObjectChangeEventArgs) _  
            Handles items.Changed  
        Select Case cea.ObjectChange  
            Case XObjectChange.Add  
                If sender.GetType() Is GetType(XElement) Then  
                    total.Value = CStr(CInt(total.Value) + _  
                            CInt((DirectCast(sender, XElement)).Value))  
                End If  
                If sender.GetType() Is GetType(XText) Then  
                    total.Value = CStr(CInt(total.Value) + _  
                            CInt((DirectCast(sender, XText)).Value))  
                End If  
            Case XObjectChange.Remove  
                If sender.GetType() Is GetType(XElement) Then  
                    total.Value = CStr(CInt(total.Value) - _  
                            CInt((DirectCast(sender, XElement)).Value))  
                End If  
                If sender.GetType() Is GetType(XText) Then  
                    total.Value = CStr(CInt(total.Value) - _  
                            CInt((DirectCast(sender, XText)).Value))  
                End If  
        End Select  
        Console.WriteLine("Changed {0} {1}", _  
                            sender.GetType().ToString(), _  
                            cea.ObjectChange.ToString())  
    End Sub  
  
    Sub Main()  
        total = root.<Total>(0)  
        items = root.<Items>(0)  
        items.SetElementValue("Item1", 25)  
        items.SetElementValue("Item2", 50)  
        items.SetElementValue("Item2", 75)  
        items.SetElementValue("Item3", 133)  
        items.SetElementValue("Item1", Nothing)  
        items.SetElementValue("Item4", 100)  
        Console.WriteLine("Total:{0}", CInt(total))  
        Console.WriteLine(root)  
    End Sub  
End Module  
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
 [LINQ to XML (Visual Basic) di programmazione avanzata](../../../../visual-basic/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
