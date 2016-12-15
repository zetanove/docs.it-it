---
title: "How to: Overload a Procedure that Takes Optional Parameters (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
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
  - "procedures, parameters"
  - "procedure overloading, optional parameters"
  - "procedures, defining"
  - "Visual Basic code, procedures"
  - "procedure parameters"
  - "procedures, overloading"
  - "procedures, multiple versions"
ms.assetid: 825f9d56-4cde-43fd-993a-b9171717e2eb
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Overload a Procedure that Takes Optional Parameters (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Se una routine include uno o più parametri [Optional](../../../../visual-basic/language-reference/modifiers/optional.md), non è possibile definire una versione di overload che corrisponda a uno dei relativi overload impliciti.  Per ulteriori informazioni, vedere "Overload impliciti per i parametri facoltativi" in [Considerations in Overloading Procedures](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md).  
  
## Un parametro facoltativo  
  
#### Per eseguire l'overload di una routine che accetta un parametro facoltativo  
  
1.  Scrivere un'istruzione di dichiarazione `Sub` o `Function` che includa il parametro facoltativo nell'elenco di parametri.  Non utilizzare la parola chiave `Optional` in questa versione di overload.  
  
2.  Far precedere la parola chiave `Sub` o `Function` dalla parola chiave [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md).  
  
3.  Scrivere il codice della routine da eseguire quando il codice chiamante fornisce l'argomento facoltativo.  
  
4.  Far terminare la routine con l'istruzione `End Sub` o `End Function`, nel modo appropriato.  
  
5.  Scrivere una seconda istruzione di dichiarazione identica alla prima, con l'eccezione che non includerà il parametro facoltativo nell'elenco di parametri.  
  
6.  Scrivere il codice della routine da eseguire quando il codice chiamante non fornisce l'argomento facoltativo.  Far terminare la routine con l'istruzione `End Sub` o `End Function`, nel modo appropriato.  
  
     Nell'esempio seguente viene illustrata una routine definita con un parametro facoltativo, un set equivalente di due routine di overload e infine esempi sia della versione di overload valida che di quella non valida.  
  
     [!code-vb[VbVbcnProcedures#59](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-optional-parameters_1.vb)]  
  
     [!code-vb[VbVbcnProcedures#60](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-optional-parameters_2.vb)]  
  
     [!code-vb[VbVbcnProcedures#61](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-optional-parameters_3.vb)]  
  
## Più parametri facoltativi  
 Per una routine con più parametri facoltativi, sono generalmente necessarie più di due versioni di overload.  Se, ad esempio, sono presenti due parametri facoltativi e il codice chiamante può fornirne oppure ometterne uno indipendentemente dall'altro, sono necessarie quattro versioni di overload, una per ogni possibile combinazione di argomenti forniti.  
  
 La complessità dell'overload cresce con l'aumentare del numero dei parametri facoltativi.  A meno che alcune combinazioni di argomenti forniti non siano accettabili, per N parametri facoltativi sono necessarie 2 ^ N versioni di overload.  A seconda della natura della routine, è possibile che la chiarezza della logica giustifichi l'attività aggiuntiva di definizione di tutte le versioni di overload.  
  
#### Per eseguire l'overload di una routine che accetta più parametri facoltativi  
  
1.  Stabilire quali combinazioni di argomenti facoltativi specificati sono accettabili per la logica della routine.  È possibile che una combinazione non sia accettabile in caso di dipendenza reciproca di due parametri facoltativi.  Se, ad esempio, un parametro accetta il nome di un coniuge\/partner e un altro ne accetta l'età, una combinazione di argomenti che specifica l'età ma omette il nome risulta inaccettabile.  
  
2.  Per ogni combinazione accettabile di argomenti facoltativi forniti, scrivere un'istruzione di dichiarazione `Sub` o `Function` che definisca il corrispondente elenco di parametri.  Non utilizzare la parola chiave `Optional`.  
  
3.  In ogni dichiarazione inserire la parola chiave [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md) prima della parola chiave `Sub` o `Function` .  
  
4.  Dopo ogni dichiarazione, scrivere il codice della routine da eseguire quando il codice chiamante fornisce un elenco di argomenti corrispondente all'elenco di parametri di tale dichiarazione.  
  
5.  Terminare ciascuna routine con l'istruzione `End Sub` o `End Function` nel modo appropriato.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [Parameter Arrays](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Troubleshooting Procedures](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [How to: Define Multiple Versions of a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md)   
 [How to: Call an Overloaded Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-overloaded-procedure.md)   
 [How to: Overload a Procedure that Takes an Indefinite Number of Parameters](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [Overload Resolution](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)