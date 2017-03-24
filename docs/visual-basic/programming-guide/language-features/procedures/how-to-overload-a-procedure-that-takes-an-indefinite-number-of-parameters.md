---
title: 'Procedura: eseguire l&quot;Overload di una routine che accetta un numero indefinito di parametri (Visual Basic) | Documenti di Microsoft'
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
- procedures, parameters
- procedure overloading, indefinite number of parameters
- procedures, defining
- Visual Basic code, procedures
- procedure parameters
- procedures, overloading
- procedures, multiple versions
ms.assetid: c7042de2-2422-4039-94e8-ac298896af69
caps.latest.revision: 18
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
ms.openlocfilehash: c7e09bd482e35c7ce7f28a6cc7de0379b7cc89f6
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters-visual-basic"></a>Procedura: eseguire l'overload di una routine che accetta un numero indefinito di parametri (Visual Basic)
Se una routine include un [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) parametro, non è possibile definire una versione di overload che accetta una matrice unidimensionale per la matrice di parametri. Per ulteriori informazioni, vedere "Overload impliciti per un parametro ParamArray" in [Considerations in Overloading Procedures](./considerations-in-overloading-procedures.md).  
  
### <a name="to-overload-a-procedure-that-takes-a-variable-number-of-parameters"></a>Eseguire l'overload che accetta un numero variabile di parametri  
  
1.  Verificare che la stored procedure e la chiamata di codice logica beneficerà overload versioni con più di un `ParamArray` parametro. Vedere "Overload e ParamArray" in [considerazioni sull'overload di routine](./considerations-in-overloading-procedures.md).  
  
2.  Determinare il numero di valori forniti la routine deve accettare nella parte variabile all'elenco di parametri. Potrebbero essere inclusi nel caso di alcun valore, e può includere il caso di una matrice unidimensionale.  
  
3.  Per ogni numero accettabile di valori forniti, scrivere un `Sub` o `Function` istruzione di dichiarazione che definisce l'elenco di parametri corrispondenti. Non utilizzare il `Optional` o `ParamArray` (parola chiave) in questa versione di overload.  
  
4.  In ogni dichiarazione far precedere il `Sub` o `Function` (parola chiave) con il [overload](../../../../visual-basic/language-reference/modifiers/overloads.md) (parola chiave).  
  
5.  Dopo ogni dichiarazione, scrivere il codice della routine che deve essere eseguita quando il codice chiamante fornisce valori corrispondenti all'elenco di parametri della dichiarazione.  
  
6.  Terminare ciascuna routine con il `End Sub` o `End Function` istruzione nel modo appropriato.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrata una routine definita con un [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) parametro e un set equivalente di routine di overload.  
  
 [!code-vb[VbVbcnProcedures&#69;](./codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters_1.vb)]  
  
 [!code-vb[VbVbcnProcedures&#70;](./codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters_2.vb)]  
  
 Impossibile eseguire l'overload di una routine con un elenco di parametri che accetta una matrice unidimensionale per la matrice di parametri. Tuttavia, è possibile utilizzare le firme degli altri overload impliciti. Le seguenti dichiarazioni illustrare questo concetto.  
  
 [!code-vb[VbVbcnProcedures&#71;](./codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters_3.vb)]  
  
 Il codice nelle versioni di overload non è necessario verificare se il codice chiamante ha fornito uno o più valori per il `ParamArray` parametro, in caso affermativo, il numero. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]passa il controllo alla versione corrispondente all'elenco di argomenti chiamante.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Poiché una routine con un `ParamArray` parametro è equivalente a un set di versioni di overload, è possibile eseguire l'overload di una routine con un elenco di parametri corrispondente a uno di questi overload impliciti. Per ulteriori informazioni, vedere [Considerations in Overloading Procedures](./considerations-in-overloading-procedures.md).  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Quando gestisce una matrice che può essere di grandi dimensioni in modo indefinito, sussiste il rischio di sovraccaricare capacità interna dell'applicazione. Se si accetta una matrice di parametri, si deve verificare la lunghezza della matrice passato al codice chiamante ed eseguire i passaggi appropriati, se è troppo grande per l'applicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Parametri facoltativi](./optional-parameters.md)   
 [Matrici di parametri](./parameter-arrays.md)   
 [Overload di routine](./procedure-overloading.md)   
 [Le procedure di risoluzione](./troubleshooting-procedures.md)   
 [Procedura: definire più versioni di una routine](./how-to-define-multiple-versions-of-a-procedure.md)   
 [Procedura: chiamare una routine di overload](./how-to-call-an-overloaded-procedure.md)   
 [Procedura: eseguire l'Overload di una routine che accetta parametri facoltativi](./how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [Risoluzione dell'overload](./overload-resolution.md)
