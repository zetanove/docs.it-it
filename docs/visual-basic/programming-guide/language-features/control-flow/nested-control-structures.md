---
title: "Nested Control Structures (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic code, control flow"
  - "control structures, nested"
  - "conditional statements, nested"
  - "statements [Visual Basic], control flow"
  - "control flow, nested control statements"
  - "structures, nested control"
  - "nested control statements"
ms.assetid: cf60b061-65d9-44a8-81f2-b0bdccd23a05
caps.latest.revision: 20
caps.handback.revision: 20
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Nested Control Structures (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

È possibile inserire istruzioni di controllo all'interno di altre istruzioni di controllo, ad esempio un blocco `If...Then...Else` all'interno di un ciclo `For...Next`.  Un'istruzione di controllo inserita in un'altra istruzione di controllo è detta *annidata*.  
  
## Livelli di annidamento  
 In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] le strutture di controllo possono essere annidate in un numero qualsiasi di livelli.  È pratica diffusa far rientrare il corpo di ogni struttura annidata per facilitarne la lettura.  Questa operazione viene eseguita automaticamente dall'editor dell'ambiente di sviluppo integrato \(IDE, Integrated Development Environment\).  
  
 Nell'esempio che segue viene utilizzata la routine `sumRows` per sommare gli elementi positivi di ogni riga della matrice.  
  
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
  
 Nell'esempio precedente la prima istruzione `Next` chiude il ciclo `For` interno mente l'ultima istruzione `Next` chiude il ciclo `For` esterno.  
  
 Analogamente, nelle istruzioni `If` annidate le istruzioni `End If` vengono applicate automaticamente all'istruzione `If` immediatamente precedente.  I cicli `Do` annidati hanno un funzionamento analogo in base al quale l'istruzione `Loop` più interna corrisponde all'istruzione `Do` più interna.  
  
> [!NOTE]
>  Per molte strutture di controllo quando si fa clic su una parola chiave, vengono evidenziate tutte le parole chiave nella struttura.  Ad esempio, quando si fa clic su `If` in una costruzione `If...Then...Else`, vengono evidenziate tutte le istanze di `If`, `Then`, `ElseIf`, `Else` e `End If` nella costruzione.  Per spostarsi alla parola chiave evidenziata successiva o precedente, premere CTRL\+MAIUSC\+FRECCIA GIÙ o CTRL\+MAIUSC\+FRECCIA SU.  
  
## Annidamento di tipi diversi di strutture di controllo  
 È possibile annidare un tipo di struttura di controllo all'interno di un'altra.  Nell'esempio che segue vengono utilizzati un blocco `With` all'interno di un ciclo `For Each` e i blocchi `If` annidati all'interno del blocco `With`.  
  
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
  
## Strutture di controllo sovrapposte  
 Non è possibile sovrapporre le strutture di controllo.  In altre parole, le strutture annidate devono essere contenute completamente nella successiva struttura più interna.  La seguente disposizione, ad esempio, non è valida in quanto il ciclo `For` termina prima del blocco `With` interno.  
  
 ![Diagramma grafico di annidamento non valida](../../../../visual-basic/programming-guide/language-features/control-flow/media/nestexampleinvalid.png "NestExampleInvalid")  
Annidamento non valido di strutture For e With  
  
 Il compilatore di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] rileva le strutture di controllo sovrapposte e segnala un errore in fase di compilazione.  
  
## Vedere anche  
 [Control Flow](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [Decision Structures](../../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [Loop Structures](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Other Control Structures](../../../../visual-basic/programming-guide/language-features/control-flow/other-control-structures.md)