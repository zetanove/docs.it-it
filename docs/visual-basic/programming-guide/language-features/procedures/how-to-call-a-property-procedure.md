---
title: 'Procedura: chiamare una routine (Visual Basic) | Documenti di Microsoft'
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
- Visual Basic code, procedures
- Visual Basic code, properties
- procedures, calling
- properties [Visual Basic], property procedures
- procedure calls, property procedures
ms.assetid: 96bc4d74-d9c3-4b7a-954d-58ac8553cd94
caps.latest.revision: 16
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
ms.openlocfilehash: 7dd3d53f602886f65c951de34b915b2672b1a817
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-a-property-procedure-visual-basic"></a>Procedura: chiamare una routine di proprietà (Visual Basic)
Chiamare una routine di proprietà mediante l'archiviazione di un valore nella proprietà o recuperarne il valore. Si accede alla proprietà esattamente come si accede a una variabile.  
  
 La proprietà `Set` procedura archivia un valore e il relativo `Get` procedura recupera il valore. Tuttavia, non chiamare in modo esplicito queste procedure in base al nome. Utilizzare la proprietà in un'istruzione di assegnazione o un'espressione, così come viene archiviato o recuperare il valore di una variabile. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]effettua le chiamate alle routine della proprietà.  
  
### <a name="to-call-a-propertys-get-procedure"></a>Per chiamare routine Get della proprietà  
  
1.  Utilizzare il nome della proprietà in un'espressione simile a quello è necessario utilizzare un nome di variabile. È possibile utilizzare una proprietà in qualsiasi punto è possibile utilizzare una variabile o costante.  
  
     -oppure-  
  
     Utilizzare il nome della proprietà seguente uguali (`=`) accedere in un'istruzione di assegnazione.  
  
     Nell'esempio seguente viene letto il valore della <xref:Microsoft.VisualBasic.DateAndTime.Now%2A>proprietà, in modo implicito chiamando il relativo `Get` procedura.</xref:Microsoft.VisualBasic.DateAndTime.Now%2A>  
  
     [!code-vb[VbVbalrDateProperties n.&4;](./codesnippet/VisualBasic/how-to-call-a-property-procedure_1.vb)]  
  
2.  Se la proprietà accetta argomenti, seguire il nome della proprietà con le parentesi per racchiudere l'elenco di argomenti. Se non sono presenti argomenti, è possibile omettere le parentesi.  
  
3.  Inserire gli argomenti nell'elenco di argomenti all'interno delle parentesi, separati da virgole. Assicurarsi di inserire gli argomenti nello stesso ordine in cui la proprietà definisce i parametri corrispondenti.  
  
 Il valore della proprietà fa parte dell'espressione come una variabile o costante viene archiviato nella variabile o proprietà sul lato sinistro dell'istruzione di assegnazione.  
  
### <a name="to-call-a-propertys-set-procedure"></a>Per chiamare una proprietà dell'insieme di procedure  
  
1.  Utilizzare il nome della proprietà sul lato sinistro di un'istruzione di assegnazione.  
  
     Nell'esempio seguente imposta il valore della <xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A>proprietà, in modo implicito la chiamata di `Set` procedura.</xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A>  
  
     [!code-vb[VbVbcnProcedures&#11;](./codesnippet/VisualBasic/how-to-call-a-property-procedure_2.vb)]  
  
2.  Se la proprietà accetta argomenti, seguire il nome della proprietà con le parentesi per racchiudere l'elenco di argomenti. Se non sono presenti argomenti, è possibile omettere le parentesi.  
  
3.  Inserire gli argomenti nell'elenco di argomenti all'interno delle parentesi, separati da virgole. Assicurarsi di inserire gli argomenti nello stesso ordine in cui la proprietà definisce i parametri corrispondenti.  
  
 Il valore generato sul lato destro dell'istruzione di assegnazione è archiviato nella proprietà.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà (routine)](./property-procedures.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Property (istruzione)](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Differenze tra proprietà e variabili in Visual Basic](./differences-between-properties-and-variables.md)   
 [Procedura: creare una proprietà](./how-to-create-a-property.md)   
 [Procedura: dichiarare una proprietà con livelli di accesso misti](./how-to-declare-a-property-with-mixed-access-levels.md)   
 [Procedura: dichiarare e chiamare una proprietà predefinita in Visual Basic](./how-to-declare-and-call-a-default-property.md)   
 [Procedura: inserire un valore in una proprietà](./how-to-put-a-value-in-a-property.md)   
 [Procedura: ottenere un valore da una proprietà](./how-to-get-a-value-from-a-property.md)   
 [Get (istruzione)](../../../../visual-basic/language-reference/statements/get-statement.md)   
 [Istruzione Set](../../../../visual-basic/language-reference/statements/set-statement.md)
