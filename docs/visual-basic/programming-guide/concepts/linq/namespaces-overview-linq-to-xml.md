---
title: Panoramica di spazi dei nomi (LINQ to XML) | Documenti di Microsoft
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
ms.assetid: b8eb31fa-4b26-4acf-8050-6e705687f458
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
ms.openlocfilehash: cec2efd31c96af17ad717abaa8f4359210e99a78
ms.lasthandoff: 03/13/2017

---
# <a name="namespaces-overview-linq-to-xml"></a>Panoramica degli spazi dei nomi (LINQ to XML)
Questo argomento vengono presentati gli spazi dei nomi, <xref:System.Xml.Linq.XName>classe e la <xref:System.Xml.Linq.XNamespace>classe.</xref:System.Xml.Linq.XNamespace> </xref:System.Xml.Linq.XName>  
  
## <a name="xml-names"></a>Nomi XML  
 I nomi XML sono spesso causa di complessità nella programmazione XML. Un nome XML è composto da uno spazio dei nomi XML (detto anche URI dello spazio dei nomi XML) e da un nome locale. Uno spazio dei nomi XML è simile a uno spazio di nomi in un'applicazione basata su [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]. Consente infatti di qualificare in modo univoco i nomi di elementi e attributi e quindi di evitare conflitti di nomi tra le diverse parti di un documento XML. Dopo aver dichiarato uno spazio dei nomi XML, è possibile selezionare un nome locale che deve essere univoco all'interno di tale spazio dei nomi.  
  
 Un'altra peculiarità dei nomi XML in formato XML *i prefissi dello spazio dei nomi*. Sono i prefissi XML a costituire la causa di maggior complessità dei nomi XML. I prefissi consentono di creare un collegamento per uno spazio dei nomi XML al fine di rendere il documento XML più conciso e comprensibile. Tuttavia, il significato dei prefissi XML dipende dal contesto ed è proprio questo aspetto a renderli complessi. Ad esempio, è possibile associare il prefisso XML `aw` a un unico spazio dei nomi XML in un'unica parte di un albero XML e a uno spazio dei nomi XML diverso in una parte diversa dell'albero XML.  
  
 Quando si utilizza [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] con i valori letterali XML e Visual Basic, è necessario utilizzare i prefissi dello spazio dei nomi quando si lavora con documenti negli spazi dei nomi.  
  
 In [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], la classe che rappresenta i nomi XML è <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName> I nomi XML vengono frequentemente in tutta la [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] API, in cui è necessario un nome XML, è possibile trovare un <xref:System.Xml.Linq.XName>parametro.</xref:System.Xml.Linq.XName> Tuttavia, raramente lavorare direttamente con un <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName> <xref:System.Xml.Linq.XName>contiene una conversione implicita da stringa.</xref:System.Xml.Linq.XName>  
  
 Per ulteriori informazioni, vedere <xref:System.Xml.Linq.XNamespace>e <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XNamespace>  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di spazi dei nomi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md)
