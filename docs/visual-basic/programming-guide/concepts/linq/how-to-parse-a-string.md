---
title: 'Procedura: analizzare una stringa (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 896e1b4b-f9bd-4975-8bc1-55b6badce1ac
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
ms.openlocfilehash: d062efd2e207f5db39e3be044450fd3f9a5d9e11
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-parse-a-string-visual-basic"></a>Procedura: analizzare una stringa (Visual Basic)
In questo argomento viene illustrato come creare una struttura ad albero XML in c#.  
  
## <a name="example"></a>Esempio  
 È possibile analizzare una stringa in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] utilizzando il `XElement.Parse` metodo. Tuttavia, è preferibile utilizzare valori letterali XML, come illustrato nel codice riportato di seguito, perché i valori letterali XML non comportano gli stessi problemi di prestazioni di analisi XML da una stringa.  
  
 Usando valori letterali XML, è possibile copiare e incollare l'XML nel programma [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
> [!NOTE]
>  L'analisi di testo o il caricamento di un documento XML da un file di testo è un processo meno efficiente della costruzione funzionale. Se si inizializza un albero XML dal codice, il tempo CPU richiesto per la costruzione funzionale è inferiore rispetto all'analisi di testo.  
  
```vb  
Dim contacts as XElement = _  
    <Contacts>  
        <Contact>  
            <Name>Patrick Hines</Name>  
            <Phone Type="home">206-555-0144</Phone>  
            <Phone Type="work">425-555-0145</Phone>  
            <Address>  
            <Street1>123 Main St</Street1>  
            <City>Mercer Island</City>  
            <State>WA</State>  
            <Postal>68042</Postal>  
            </Address>  
            <NetWorth>10</NetWorth>  
        </Contact>  
        <Contact>  
            <Name>Gretchen Rivas</Name>  
            <Phone Type="mobile">206-555-0163</Phone>  
            <Address>  
            <Street1>123 Main St</Street1>  
            <City>Mercer Island</City>  
            <State>WA</State>  
            <Postal>68042</Postal>  
            </Address>  
            <NetWorth>11</NetWorth>  
        </Contact>  
    </Contacts>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Analisi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/parsing-xml.md)
