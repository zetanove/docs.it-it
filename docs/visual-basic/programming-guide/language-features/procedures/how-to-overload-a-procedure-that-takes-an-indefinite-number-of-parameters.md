---
title: "How to: Overload a Procedure that Takes an Indefinite Number of Parameters (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "procedures, parameters"
  - "procedure overloading, indefinite number of parameters"
  - "procedures, defining"
  - "Visual Basic code, procedures"
  - "procedure parameters"
  - "procedures, overloading"
  - "procedures, multiple versions"
ms.assetid: c7042de2-2422-4039-94e8-ac298896af69
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# How to: Overload a Procedure that Takes an Indefinite Number of Parameters (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Se una routine include un parametro [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md), non è possibile definire una versione di overload che accetta una matrice unidimensionale per la matrice di parametri.  Per ulteriori informazioni, vedere "Overload impliciti per un parametro ParamArray" in [Considerations in Overloading Procedures](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md).  
  
### Per eseguire l'overload di una routine che accetta un numero variabile di parametri  
  
1.  Assicurarsi che per la logica della routine e del codice chiamante i vantaggi derivanti dall'utilizzo di versioni di overload siano maggiori rispetto a quelli derivanti dall'uso di un parametro `ParamArray`.  Per informazioni, vedere "Overload e ParamArray" in [Considerations in Overloading Procedures](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md).  
  
2.  Determinare il numero di valori specificati che la routine deve accettare nella parte variabile dell'elenco dei parametri.  È possibile che non sia disponibile alcun valore o che sia presente una sola matrice unidimensionale.  
  
3.  Per ogni numero accettabile di valori forniti, scrivere un'istruzione per la dichiarazione `Sub` o `Function` che definisca l'elenco di parametri corrispondente.  Non utilizzare la parola chiave `Optional` o `ParamArray` in questa versione di overload.  
  
4.  In ogni dichiarazione inserire la parola chiave [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md) prima della parola chiave `Sub` o `Function` .  
  
5.  Dopo ogni dichiarazione scrivere il codice della routine da eseguire quando il codice chiamante fornisce valori corrispondenti all'elenco dei parametri della dichiarazione.  
  
6.  Terminare ciascuna routine con l'istruzione `End Sub` o `End Function` nel modo appropriato.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono illustrati una routine definita con un parametro [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) e quindi un insieme equivalente di routine di overload.  
  
 [!code-vb[VbVbcnProcedures#69](./codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters_1.vb)]  
  
 [!code-vb[VbVbcnProcedures#70](./codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters_2.vb)]  
  
 Non è possibile eseguire l'overload di una routine di questo tipo con un elenco di parametri che accetta una matrice unidimensionale per la matrice di parametri.  È invece possibile utilizzare le firme di altri overload impliciti.  Questa situazione viene illustrata nelle dichiarazioni seguenti.  
  
 [!code-vb[VbVbcnProcedures#71](./codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters_3.vb)]  
  
 Il codice nelle versioni di overload non deve verificare se il codice chiamante ha fornito uno o più valori per il parametro `ParamArray` e, in caso affermativo, il numero di valori.  In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] il controllo viene passato alla versione che corrisponde all'elenco di argomenti di chiamata.  
  
## Compilazione del codice  
 Poiché una routine con un parametro `ParamArray` equivale a un insieme di versioni di overload, non è possibile eseguire l'overload di una routine di questo tipo con un elenco di parametri corrispondente a uno di questi overload impliciti.  Per ulteriori informazioni, vedere [Considerations in Overloading Procedures](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md).  
  
## Sicurezza di .NET Framework  
 Ogni volta che viene utilizzata una matrice che può essere di dimensioni indefinite, esiste il rischio di sovraccarico della capacità interna dell'applicazione.  Se si accetta una matrice di parametri, è necessario verificare la lunghezza della matrice passata dal codice chiamante ed effettuare le operazioni appropriate nel caso in cui fosse troppo grande per l'applicazione.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [Parameter Arrays](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Troubleshooting Procedures](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [How to: Define Multiple Versions of a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md)   
 [How to: Call an Overloaded Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-overloaded-procedure.md)   
 [How to: Overload a Procedure that Takes Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [Overload Resolution](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)