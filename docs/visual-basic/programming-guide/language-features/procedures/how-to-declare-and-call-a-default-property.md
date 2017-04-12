---
title: "Procedura: dichiarare e chiamare una proprietà predefinita in Visual Basic | Documenti di Microsoft"
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
- defaults, properties
- properties [Visual Basic], default
- procedures, defining
- default properties, in Visual Basic
- Visual Basic code, procedures
- Visual Basic code, properties
- default properties
ms.assetid: 68b4026e-09ef-4613-808e-f6287494ff63
caps.latest.revision: 23
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
ms.openlocfilehash: ce98e7fe72a395f6c4cde481feaa60be28c6fcc3
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-declare-and-call-a-default-property-in-visual-basic"></a>Procedura: dichiarare e chiamare una proprietà predefinita in Visual Basic
Oggetto *predefiniti delle proprietà* è una proprietà di classe o struttura che il codice può accedere senza specificarla. Quando il codice chiamante assegna una classe o struttura ma non una proprietà e il contesto consente l'accesso a una proprietà, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] risolve l'accesso a tale classe o una proprietà predefinita della struttura, se presente.  
  
 Una classe o struttura può avere al massimo una proprietà predefinita. Tuttavia, è possibile eseguire l'overload di una proprietà predefinita e dispone di più di una versione di esso.  
  
 Per ulteriori informazioni, vedere [predefinito](../../../../visual-basic/language-reference/modifiers/default.md).  
  
### <a name="to-declare-a-default-property"></a>Per dichiarare una proprietà predefinita  
  
1.  Dichiarare le proprietà in modo normale. Non si specifica il `Shared` o `Private` (parola chiave).  
  
2.  Includere il `Default` parola chiave nella dichiarazione di proprietà.  
  
3.  Specificare almeno un parametro per la proprietà. È possibile definire una proprietà predefinita che non accetta almeno un argomento.  
  
     [!code-vb[VbVbcnProcedures n.&17;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_1.vb)]  
  
### <a name="to-call-a-default-property"></a>Per chiamare una proprietà predefinita  
  
1.  Dichiarare una variabile di tipo classe o struttura che lo contiene.  
  
     [!code-vb[VbVbcnProcedures&#16;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_2.vb)]  
  
2.  Utilizzare il nome della variabile da solo in un'espressione in cui è in genere necessario includere il nome della proprietà.  
  
     [!code-vb[VbVbcnProcedures numero&21;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_3.vb)]  
  
3.  Seguire il nome della variabile con un elenco di argomenti racchiuso tra parentesi. Una proprietà predefinita deve accettare almeno un argomento.  
  
     [!code-vb[VbVbcnProcedures&#20;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_4.vb)]  
  
4.  Per recuperare il valore della proprietà predefinito, utilizzare il nome di variabile con un elenco di argomenti, in un'espressione o in seguito uguali (`=`) accedere in un'istruzione di assegnazione.  
  
     [!code-vb[VbVbcnProcedures&#15;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_5.vb)]  
  
5.  Per impostare il valore della proprietà predefinito, utilizzare il nome di variabile con un elenco di argomenti, sul lato sinistro di un'istruzione di assegnazione.  
  
     [!code-vb[VbVbcnProcedures&#14;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_6.vb)]  
  
6.  È sempre possibile specificare il nome della proprietà predefinita con il nome della variabile, così come si farebbe per accedere a qualsiasi altra proprietà.  
  
     [!code-vb[&#19; VbVbcnProcedures](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_7.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente dichiara una proprietà predefinita in una classe.  
  
 [!code-vb[VbVbcnProcedures&#12;](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_8.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come chiamare la proprietà predefinita `myProperty` sulla classe `class1`. Le istruzioni di assegnazione di tre valori memorizzati in `myProperty`e <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>chiamata legge i valori.</xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>  
  
 [!code-vb[13 VbVbcnProcedures](./codesnippet/VisualBasic/how-to-declare-and-call-a-default-property_9.vb)]  
  
 L'utilizzo più comune di una proprietà predefinita è la <xref:Microsoft.VisualBasic.Collection.Item%2A>proprietà in varie classi di raccolta.</xref:Microsoft.VisualBasic.Collection.Item%2A>  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Proprietà predefinite può determinare un lieve riduzione del numero di caratteri del codice sorgente, ma può rendere il codice più difficili da leggere. Se il codice chiamante non ha familiarità con la classe o struttura, quando fa riferimento al nome di classe o struttura non può essere determinato se il riferimento accede la classe o struttura o una proprietà predefinita. Ciò può causare errori del compilatore o meno evidenti della logica di runtime.  
  
 Piuttosto, è possibile ridurre il rischio di errori di proprietà predefiniti utilizzando sempre la [istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) per impostare il tipo di compilatore controllo `On`.  
  
 Se si intende utilizzare una classe predefinita o una struttura nel codice, è necessario determinare se esiste una proprietà predefinita e in tal caso, il relativo nome novità.  
  
 A causa di questi svantaggi, è consigliabile non definire le proprietà predefinite. Per la leggibilità del codice, si deve anche considerare fare sempre riferimento a tutte le proprietà in modo esplicito, incluse quelle predefinite.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà (routine)](./property-procedures.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Property (istruzione)](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Impostazione predefinita](../../../../visual-basic/language-reference/modifiers/default.md)   
 [Differenze tra proprietà e variabili in Visual Basic](./differences-between-properties-and-variables.md)   
 [Procedura: creare una proprietà](./how-to-create-a-property.md)   
 [Procedura: dichiarare una proprietà con livelli di accesso misti](./how-to-declare-a-property-with-mixed-access-levels.md)   
 [Procedura: chiamare una routine di proprietà](./how-to-call-a-property-procedure.md)   
 [Procedura: inserire un valore in una proprietà](./how-to-put-a-value-in-a-property.md)   
 [Procedura: Ottenere un valore da una proprietà](./how-to-get-a-value-from-a-property.md)
