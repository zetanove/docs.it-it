---
title: "Procedura: definire più versioni di una routine (Visual Basic) | Documenti di Microsoft"
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
- procedures, defining
- Visual Basic code, procedures
- procedures, overloading
- procedures, multiple versions
- procedure overloading, multiple versions
ms.assetid: 71ccdd66-1b00-4b66-bee4-6926c0d696f4
caps.latest.revision: 14
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
ms.openlocfilehash: 0228083ce00a0f552227fd7ae8f0f5a24f65148e
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-define-multiple-versions-of-a-procedure-visual-basic"></a>Procedura: definire più versioni di una routine (Visual Basic)
È possibile definire una routine in più versioni da *overload* quest'ultima, usando lo stesso nome ma un elenco di parametri diversi per ogni versione. Lo scopo dell'overload è definire più versioni strettamente correlate di una procedura senza la necessità di distinguere per nome.  
  
 Per ulteriori informazioni, vedere [overload di routine](./procedure-overloading.md).  
  
### <a name="to-define-multiple-versions-of-a-procedure"></a>Per definire più versioni di una routine  
  
1.  Scrivere un `Sub` o `Function` istruzione di dichiarazione per ogni versione della procedura di cui si desidera definire. Utilizzare lo stesso nome di procedura in ogni dichiarazione.  
  
2.  Far precedere il `Sub` o `Function` (parola chiave) in ogni dichiarazione con la [overload](../../../../visual-basic/language-reference/modifiers/overloads.md) (parola chiave). È possibile omettere `Overloads` nelle dichiarazioni, ma se si include in una di queste dichiarazioni, è necessario includerlo in ogni dichiarazione.  
  
3.  Dopo ogni istruzione di dichiarazione, scrivere codice procedure per gestire il caso specifico in cui il codice chiamante fornisce argomenti corrispondenti elenco di parametri di quella versione. Non è necessario testare per i parametri che ha fornito il codice chiamante. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]passa il controllo alla versione corrispondente della routine.  
  
4.  Terminare ogni versione della routine con il `End Sub` o `End Function` istruzione nel modo appropriato.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente definisce una `Sub` procedura per registrare una transazione al saldo del cliente. Usa il `Overloads` (parola chiave) per definire due versioni della routine, una che accetta il cliente per nome e l'altra per numero di conto.  
  
 [!code-vb[VbVbcnProcedures&#72;](./codesnippet/VisualBasic/how-to-define-multiple-versions-of-a-procedure_1.vb)]  
  
 Il codice chiamante può ottenere l'identificazione del cliente come un `String` o `Integer`, quindi utilizzare la stessa istruzione di chiamata in entrambi i casi.  
  
 Per informazioni sulla chiamata di queste versioni di `post` procedura, vedere [procedura: chiamare una routine di overload](./how-to-call-an-overloaded-procedure.md).  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Assicurarsi che le versioni di overload con lo stesso nome di procedura ma un elenco di parametri diverso.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Le procedure di risoluzione](./troubleshooting-procedures.md)   
 [Procedura: eseguire l'Overload di una routine che accetta parametri facoltativi](./how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [Procedura: eseguire l'Overload di una routine che accetta un numero indefinito di parametri](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [Considerazioni sull'overload di routine](./considerations-in-overloading-procedures.md)   
 [Risoluzione dell'overload](./overload-resolution.md)
