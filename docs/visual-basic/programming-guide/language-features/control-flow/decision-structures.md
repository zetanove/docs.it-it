---
title: La decisione di strutture (Visual Basic) | Documenti di Microsoft
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
- statements [Visual Basic], control flow
- If statement, decision structures
- If statement, If...Then...Else
- control flow, decision structures
- decision structures
- conditional statements, decision structures
ms.assetid: 2e2e0895-4483-442a-b17c-26aead751ec2
caps.latest.revision: 29
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
ms.openlocfilehash: c69b487322dc75ae8d54f42c1c62f8f5cc35757d
ms.lasthandoff: 03/13/2017

---
# <a name="decision-structures-visual-basic"></a>Strutture decisionali (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Consente di condizioni di test ed eseguire operazioni diverse in base ai risultati del test. È possibile verificare una condizione è true o false per diversi valori di un'espressione o per diverse eccezioni generate quando si esegue una serie di istruzioni.  
  
 Nella figura seguente mostra una struttura decisionale che verifica la presenza di una condizione true ed esegue azioni diverse a seconda se è true o false.  
  
 ![Diagramma di flusso di un blocco If... Quindi... Costruzione else](../../../../visual-basic/programming-guide/language-features/control-flow/media/ifthenelse.gif "IfThenElse")  
Operazioni diverse quando una condizione è true e false  
  
## <a name="ifthenelse-construction"></a>If... Quindi... Costruzione else  
 `If...Then...Else`consentono di testare per una o più condizioni ed eseguire una o più istruzioni in base a ogni condizione. È possibile verificare le condizioni e intraprendere azioni nei modi seguenti:  
  
-   Eseguire una o più istruzioni se una condizione`True`  
  
-   Eseguire una o più istruzioni se una condizione`False`  
  
-   Eseguire alcune istruzioni se una condizione è `True` e altri in questo caso`False`  
  
-   Verificare una condizione aggiuntiva se la prima condizione è`False`  
  
 La struttura di controllo che offre tutte queste possibilità è la [se... Quindi... Istruzione else](../../../../visual-basic/language-reference/statements/if-then-else-statement.md). Se si dispone solo un test e un'istruzione per l'esecuzione, è possibile utilizzare una versione a riga singola. Se si dispone di un set di condizioni e azioni più complesso, è possibile utilizzare la versione più righe.  
  
## <a name="selectcase-construction"></a>Seleziona... Costruzione di case  
 Il `Select...Case` costruzione consente di valutare un'espressione una sola volta e di eseguire diversi set di istruzioni basate su diversi valori possibili. Per ulteriori informazioni, vedere [Seleziona... Case (istruzione)](../../../../visual-basic/language-reference/statements/select-case-statement.md).  
  
## <a name="trycatchfinally-construction"></a>Try... Catch... Infine costruzione  
 `Try...Catch...Finally`consentono di eseguire un set di istruzioni in un ambiente che mantiene il controllo se una qualsiasi di tali istruzioni genera un'eccezione. È possibile eseguire azioni diverse per le diverse eccezioni. È possibile specificare facoltativamente un blocco di codice da eseguire prima di terminare l'intera `Try...Catch...Finally` costruzione, indipendentemente dall'esito. Per ulteriori informazioni, vedere [Try... Catch... Istruzione finally](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
> [!NOTE]
>  Per molte strutture di controllo quando si fa clic su una parola chiave, vengono evidenziate tutte le parole chiave nella struttura. Ad esempio, quando fa clic su `If` in un `If...Then...Else` costruzione, tutte le istanze di `If`, `Then`, `ElseIf`, `Else`, e `End If` nella costruzione vengono evidenziati. Per passare alla parola chiave evidenziata successiva o precedente, premere CTRL + MAIUSC + freccia giù o CTRL + MAIUSC + freccia su.  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di controllo](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [Cicli (strutture)](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Altre strutture di controllo](../../../../visual-basic/programming-guide/language-features/control-flow/other-control-structures.md)   
 [Strutture di controllo annidate](../../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Operatore If](../../../../visual-basic/language-reference/operators/if-operator.md)
