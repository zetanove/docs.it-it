---
title: 'Procedura: trovare discendenti con un nome di elemento specifico (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 78915518-0d25-4051-ab55-929779989510
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 678622fe04ae971e7fed2cea182b21d895edaa1c
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-find-descendants-with-a-specific-element-name-visual-basic"></a>Procedura: trovare discendenti con un nome di elemento specifico (Visual Basic)
Talvolta si desidera individuare tutti i discendenti con un determinato nome. È possibile scrivere codice per scorrere tutti i discendenti, ma è più facile da utilizzare il <xref:System.Xml.Linq.XContainer.Descendants%2A>dell'asse.</xref:System.Xml.Linq.XContainer.Descendants%2A>  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente è illustrato come individuare discendenti in base al nome dell'elemento.  
  
```vb  
Dim root As XElement = _  
    <root>  
        <para>  
            <r>  
                <t>Some text </t>  
            </r>  
            <n>  
                <r>  
                    <t>that is broken up into </t>  
                </r>  
            </n>  
            <n>  
                <r>  
                    <t>multiple segments.</t>  
                </r>  
            </n>  
        </para>  
    </root>  
  
Dim textSegs As IEnumerable(Of String) = _  
    From seg In root...<t> _  
    Select seg.Value  
  
Dim str As String = textSegs.Aggregate( _  
    New StringBuilder, _  
    Function(sb, i) sb.Append(i), _  
    Function(sb) sb.ToString)  
  
Console.WriteLine(str)  
```  
  
 L'output del codice è il seguente:  
  
```  
Some text that is broken up into multiple segments.  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente è illustrata la stessa query per XML in uno spazio dei nomi. Per ulteriori informazioni, vedere [utilizzo di spazi dei nomi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md).  
  
```vb  
Imports <xmlns='http://www.adatum.com'>  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <root>  
                <para>  
                    <r>  
                        <t>Some text </t>  
                    </r>  
                    <n>  
                        <r>  
                            <t>that is broken up into </t>  
                        </r>  
                    </n>  
                    <n>  
                        <r>  
                            <t>multiple segments.</t>  
                        </r>  
                    </n>  
                </para>  
            </root>  
  
        Dim textSegs As IEnumerable(Of String) = _  
            From seg In root...<t> _  
            Select seg.Value  
  
        Dim str As String = textSegs.Aggregate( _  
            New StringBuilder, _  
            Function(sb, i) sb.Append(i), _  
            Function(sb) sb.ToString)  
  
        Console.WriteLine(str)  
    End Sub  
End Module  
```  
  
 L'output del codice è il seguente:  
  
```  
Some text that is broken up into multiple segments.  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XContainer.Descendants%2A></xref:System.Xml.Linq.XContainer.Descendants%2A>   
 [Query di base (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/basic-queries-linq-to-xml.md)
