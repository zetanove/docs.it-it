---
title: "Procedura: inserire un valore in una proprietà (Visual Basic) | Documenti di Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- property values
- Visual Basic code, procedures
- values, properties
- Visual Basic code, properties
- properties [Visual Basic], values
ms.assetid: c39401e5-b5fc-4439-8f31-ed640f7ce6ed
caps.latest.revision: 13
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e3b2336589b525756a92cb3e26ab6c1950118b01
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-put-a-value-in-a-property-visual-basic"></a>Procedura: inserire un valore in una proprietà (Visual Basic)
Archiviare un valore in una proprietà inserendo il nome della proprietà sul lato sinistro di un'istruzione di assegnazione.  
  
 La proprietà `Set` procedure archivia un valore, ma non viene chiamato esplicitamente in base al nome. Utilizzare la proprietà esattamente come si utilizzerebbe una variabile. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]effettua le chiamate alle routine della proprietà.  
  
### <a name="to-store-a-value-in-a-property"></a>Per archiviare un valore in una proprietà  
  
1.  Utilizzare il nome della proprietà sul lato sinistro di un'istruzione di assegnazione.  
  
     Nell'esempio seguente imposta il valore della [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] `TimeOfDay` proprietà mezzogiorno, la chiamata in modo implicito il `Set` procedura.  
  
     [!code-vb[VbVbcnProcedures&#11;](./codesnippet/VisualBasic/how-to-put-a-value-in-a-property_1.vb)]  
  
2.  Se la proprietà accetta argomenti, seguire il nome della proprietà con le parentesi per racchiudere l'elenco di argomenti. Se non sono presenti argomenti, è possibile omettere le parentesi.  
  
3.  Inserire gli argomenti nell'elenco di argomenti all'interno delle parentesi, separati da virgole. Assicurarsi di inserire gli argomenti nello stesso ordine in cui la proprietà definisce i parametri corrispondenti.  
  
4.  Il valore generato sul lato destro dell'istruzione di assegnazione è archiviato nella proprietà.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A></xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A>   
 [Proprietà (routine)](./property-procedures.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Property (istruzione)](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Differenze tra proprietà e variabili in Visual Basic](./differences-between-properties-and-variables.md)   
 [Procedura: creare una proprietà](./how-to-create-a-property.md)   
 [Procedura: dichiarare una proprietà con livelli di accesso misti](./how-to-declare-a-property-with-mixed-access-levels.md)   
 [Procedura: chiamare una routine di proprietà](./how-to-call-a-property-procedure.md)   
 [Procedura: dichiarare e chiamare una proprietà predefinita in Visual Basic](./how-to-declare-and-call-a-default-property.md)   
 [Procedura: Ottenere un valore da una proprietà](./how-to-get-a-value-from-a-property.md)
