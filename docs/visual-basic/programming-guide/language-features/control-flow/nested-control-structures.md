---
title: Annidati strutture di controllo (Visual Basic) | Documenti di Microsoft
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
- Visual Basic code, control flow
- control structures, nested
- conditional statements, nested
- statements [Visual Basic], control flow
- control flow, nested control statements
- structures, nested control
- nested control statements
ms.assetid: cf60b061-65d9-44a8-81f2-b0bdccd23a05
caps.latest.revision: 20
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 4afc0afc2ad63d03f2c4251640d3682b2b184504
ms.lasthandoff: 03/13/2017

---
# <a name="nested-control-structures-visual-basic"></a>Strutture di controllo annidate (Visual Basic)
È possibile inserire istruzioni di controllo all'interno di altre istruzioni di controllo, ad esempio un `If...Then...Else` blocco all'interno di un `For...Next` ciclo. Un'istruzione di controllo inserita in un'altra istruzione di controllo è detto *nidificate*.  
  
## <a name="nesting-levels"></a>Livelli di annidamento  
 In strutture di controllo [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] possono essere nidificate in un numero di livelli desiderato. È pratica comune per rendere più leggibile strutture annidate rientrare il corpo di ciascuna di esse. L'editor di sviluppo integrato (IDE) di ambiente esegue automaticamente questa.  
  
 Nell'esempio seguente, la procedura `sumRows` sommare gli elementi positivi di ogni riga della matrice.  
  
```  
Public Sub sumRows(ByVal a(,) As Double, ByRef r() As Double)  
    Dim i, j As Integer  
    For i = 0 To UBound(a, 1)  
        r(i) = 0  
        For j = 0 To UBound(a, 2)  
            If a(i, j) > 0 Then  
                r(i) = r(i) + a(i, j)  
            End If  
        Next j  
    Next i  
End Sub  
```  
  
 Nell'esempio precedente, il primo `Next` istruzione chiude il `For` ciclo e l'ultimo `Next` istruzione chiude esterna `For` ciclo.  
  
 Analogamente, nidificazione `If` istruzioni, il `End If` istruzioni vengono applicate automaticamente al più vicino prima `If` istruzione. Annidati `Do` cicli funzionano in modo simile, con più interna `Loop` corrispondente più interna `Do` istruzione.  
  
> [!NOTE]
>  Per molte strutture di controllo quando si fa clic su una parola chiave, vengono evidenziate tutte le parole chiave nella struttura. Ad esempio, quando fa clic su `If` in un `If...Then...Else` costruzione, tutte le istanze di `If`, `Then`, `ElseIf`, `Else`, e `End If` nella costruzione vengono evidenziati. Per passare alla parola chiave evidenziata successiva o precedente, premere CTRL + MAIUSC + freccia giù o CTRL + MAIUSC + freccia su.  
  
## <a name="nesting-different-kinds-of-control-structures"></a>Annidamento di tipi diversi di strutture di controllo  
 È possibile annidare un tipo di struttura di controllo all'interno di un altro tipo. Nell'esempio seguente viene utilizzato un `With` blocco all'interno di un `For Each` ciclo e nidificati `If` blocchi all'interno di `With` blocco.  
  
```  
For Each ctl As System.Windows.Forms.Control In Me.Controls  
    With ctl  
        .BackColor = System.Drawing.Color.Yellow  
        .ForeColor = System.Drawing.Color.Black  
        If .CanFocus Then  
            .Text = "Colors changed"  
            If Not .Focus() Then  
                ' Insert code to process failed focus.  
            End If  
        End If  
    End With  
Next ctl  
```  
  
## <a name="overlapping-control-structures"></a>Strutture di controllo sovrapposte  
 Non è possibile sovrapporre le strutture di controllo. Ciò significa che qualsiasi struttura annidata deve essere contenuta completamente nella successiva struttura più interna. Ad esempio, la disposizione seguente è valida perché il `For` ciclo termina prima del `With` termina.  
  
 ![Diagramma grafico di annidamento non valida](../../../../visual-basic/programming-guide/language-features/control-flow/media/nestexampleinvalid.gif "NestExampleInvalid")  
Annidamento non valida di per e con strutture  
  
 Il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore rileva tale controllo sovrapposto strutture e segnala un errore in fase di compilazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di controllo](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [Strutture decisionali](../../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [Cicli (strutture)](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Altre strutture di controllo](../../../../visual-basic/programming-guide/language-features/control-flow/other-control-structures.md)
