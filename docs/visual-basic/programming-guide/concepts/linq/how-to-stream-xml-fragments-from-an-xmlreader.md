---
title: 'Procedura: flusso di frammenti XML da un XmlReader (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: f67ce598-4a12-4dcb-9a07-24deca02a111
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
ms.openlocfilehash: c9c60bb4730ef6569390f76f63c40a2cbd1c9524
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-stream-xml-fragments-from-an-xmlreader-visual-basic"></a>Procedura: flusso di frammenti XML da un XmlReader (Visual Basic)
Quando è necessario elaborare file XML di grandi dimensioni, potrebbe risultare impossibile caricare in memoria l'intero albero XML. Questo argomento viene illustrato come eseguire il flusso di frammenti tramite un <xref:System.Xml.XmlReader>.</xref:System.Xml.XmlReader>  
  
 Uno dei modi più efficaci per usare un <xref:System.Xml.XmlReader>leggere <xref:System.Xml.Linq.XElement>oggetti consiste nello scrivere un metodo dell'asse personalizzato.</xref:System.Xml.Linq.XElement> </xref:System.Xml.XmlReader> Un metodo dell'asse restituisce in genere una raccolta, ad esempio <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>, come illustrato nell'esempio di questo argomento.</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> Nel metodo dell'asse personalizzato, dopo aver creato il frammento XML chiamando il <xref:System.Xml.Linq.XNode.ReadFrom%2A>metodo, restituire la raccolta usando `yield return`.</xref:System.Xml.Linq.XNode.ReadFrom%2A> In questo modo si fornisce la semantica di esecuzione posticipata al metodo dell'asse personalizzato.  
  
 Quando si crea un albero XML da un <xref:System.Xml.XmlReader>oggetto, il <xref:System.Xml.XmlReader>deve essere posizionato su un elemento.</xref:System.Xml.XmlReader> </xref:System.Xml.XmlReader> Il <xref:System.Xml.Linq.XNode.ReadFrom%2A>metodo non restituisce fino a quando non letto il tag di chiusura dell'elemento.</xref:System.Xml.Linq.XNode.ReadFrom%2A>  
  
 Se si desidera creare un albero parziale, è possibile creare un'istanza di un <xref:System.Xml.XmlReader>, posizionare il lettore sul nodo che si desidera convertire in un <xref:System.Xml.Linq.XElement>struttura ad albero e quindi creare il <xref:System.Xml.Linq.XElement>oggetto.</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XElement> </xref:System.Xml.XmlReader>  
  
 L'argomento [procedura: flusso di frammenti XML con accesso a informazioni di intestazione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-stream-xml-fragments-with-access-to-header-information.md) contiene informazioni e un esempio su come trasmettere un documento più complesso.  
  
 L'argomento [procedura: eseguire lo Streaming Transform di grandi dimensioni documenti XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-perform-streaming-transform-of-large-xml-documents.md) contiene un esempio dell'utilizzo di LINQ to XML per trasformare documenti XML molto grandi mantenendo un footprint di memoria di piccole dimensioni.  
  
## <a name="example"></a>Esempio  
 In questo esempio viene creato un metodo dell'asse personalizzato. È possibile sottoporlo a query tramite una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]. Il metodo dell'asse personalizzato `StreamRootChildDoc` è progettato specificamente per leggere un documento contenente un elemento `Child` ripetuto.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 Questo esempio produce il seguente output:  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 In questo esempio il documento di origine è molto piccolo. Tuttavia, anche contenesse milioni di elementi `Child`, il footprint di memoria di questo esempio sarebbe comunque ridotto.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura dettagliata: Implementazione di IEnumerable(Of T) in Visual Basic](../../../../visual-basic/programming-guide/language-features/control-flow/walkthrough-implementing-ienumerable-of-t.md)   
 [Analisi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/parsing-xml.md)
