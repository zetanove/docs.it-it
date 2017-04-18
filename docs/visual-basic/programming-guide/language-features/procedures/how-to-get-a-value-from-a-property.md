---
title: "Procedura: ottenere un valore da una proprietà (Visual Basic) | Documenti di Microsoft"
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
ms.assetid: 3954423e-6ab7-4a4c-b55c-a8d27be47891
caps.latest.revision: 11
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
ms.openlocfilehash: 7487e4cde724c46a193639f2ad116d25e4ff834c
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-get-a-value-from-a-property-visual-basic"></a>Procedura: ottenere un valore da una proprietà (Visual Basic)
Per recuperare il valore della proprietà, includendo il nome della proprietà in un'espressione.  
  
 La proprietà `Get` procedura recupera il valore, ma non viene chiamato esplicitamente in base al nome. Utilizzare la proprietà esattamente come si utilizzerebbe una variabile. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]effettua le chiamate alle routine della proprietà.  
  
### <a name="to-retrieve-a-value-from-a-property"></a>Per recuperare un valore da una proprietà  
  
1.  Utilizzare il nome della proprietà in un'espressione simile a quello è necessario utilizzare un nome di variabile. È possibile utilizzare una proprietà in qualsiasi punto è possibile utilizzare una variabile o costante.  
  
     -oppure-  
  
     Utilizzare il nome della proprietà seguente uguali (`=`) accedere in un'istruzione di assegnazione.  
  
     Nell'esempio seguente viene letto il valore della [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] `Now` proprietà, in modo implicito chiamando il relativo `Get` procedura.  
  
     [!code-vb[VbVbalrDateProperties n.&4;](./codesnippet/VisualBasic/how-to-get-a-value-from-a-property_1.vb)]  
  
2.  Se la proprietà accetta argomenti, seguire il nome della proprietà con le parentesi per racchiudere l'elenco di argomenti. Se non sono presenti argomenti, è possibile omettere le parentesi.  
  
3.  Inserire gli argomenti nell'elenco di argomenti all'interno delle parentesi, separati da virgole. Assicurarsi di inserire gli argomenti nello stesso ordine in cui la proprietà definisce i parametri corrispondenti.  
  
 Il valore della proprietà fa parte dell'espressione come una variabile o costante viene archiviato nella variabile o proprietà sul lato sinistro dell'istruzione di assegnazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Proprietà (routine)](./property-procedures.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Property (istruzione)](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Differenze tra proprietà e variabili in Visual Basic](./differences-between-properties-and-variables.md)   
 [Procedura: creare una proprietà](./how-to-create-a-property.md)   
 [Procedura: dichiarare una proprietà con livelli di accesso misti](./how-to-declare-a-property-with-mixed-access-levels.md)   
 [Procedura: chiamare una routine di proprietà](./how-to-call-a-property-procedure.md)   
 [Procedura: dichiarare e chiamare una proprietà predefinita in Visual Basic](./how-to-declare-and-call-a-default-property.md)   
 [Procedura: Inserire un valore in una proprietà](./how-to-put-a-value-in-a-property.md)
