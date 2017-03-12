---
title: "How to: Define Multiple Versions of a Procedure (Visual Basic) | Microsoft Docs"
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
  - "procedures, defining"
  - "Visual Basic code, procedures"
  - "procedures, overloading"
  - "procedures, multiple versions"
  - "procedure overloading, multiple versions"
ms.assetid: 71ccdd66-1b00-4b66-bee4-6926c0d696f4
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# How to: Define Multiple Versions of a Procedure (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile definire una routine in più versioni eseguendone l'*overload* utilizzando lo stesso nome ma un elenco di parametri differente per ogni versione.  Lo scopo dell'overload è definire più versioni strettamente correlate di una routine senza doverle distinguere per nome.  
  
 Per ulteriori informazioni, vedere [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md).  
  
### Per definire più versioni di una routine  
  
1.  Scrivere un'istruzione di dichiarazione `Sub` o `Function` per ogni versione della routine da definire.  Utilizzare lo stesso nome di routine in ogni dichiarazione.  
  
2.  Far precedere la parola chiave `Sub` o `Function` in ogni dichiarazione dalla parola chiave [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md).  Facoltativamente, è possibile omettere `Overloads` nelle dichiarazioni, ma se tale parola chiave viene inclusa in una di queste, è necessario includerla in tutte.  
  
3.  Dopo ogni istruzione di dichiarazione, scrivere un codice di routine che consenta di gestire il caso specifico in cui il codice chiamante fornisce argomenti corrispondenti all'elenco di parametri di tale versione.  Non è necessario verificare quali siano i parametri forniti dal codice chiamante.  In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] il controllo viene passato alla versione corrispondente della routine.  
  
4.  Far terminare ogni versione della routine con l'istruzione `End Sub` o `End Function`, a seconda dei casi.  
  
## Esempio  
 Nell'esempio seguente viene definita una routine `Sub` per l'invio di una transazione relativa al saldo di un cliente.  Viene utilizzata la parola chiave `Overloads` per definire due versioni della routine, una che accetta il cliente per nome e l'altra per numero di conto.  
  
 [!code-vb[VbVbcnProcedures#72](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-define-multiple-v_1.vb)]  
  
 Il codice chiamante può ottenere l'identificazione del cliente come `String` o `Integer` e quindi utilizzare la stessa istruzione di chiamata in entrambi i casi.  
  
 Per informazioni sulle modalità di chiamata di queste versioni della routine `post`, vedere [How to: Call an Overloaded Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-overloaded-procedure.md).  
  
## Compilazione del codice  
 Verificare che tutte le versioni di overload abbiano lo stesso nome di routine ma un elenco di parametri differente.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Troubleshooting Procedures](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [How to: Overload a Procedure that Takes Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [How to: Overload a Procedure that Takes an Indefinite Number of Parameters](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [Considerations in Overloading Procedures](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)   
 [Overload Resolution](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)