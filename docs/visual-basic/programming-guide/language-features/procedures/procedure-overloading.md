---
title: "Procedure Overloading (Visual Basic) | Microsoft Docs"
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
  - "signatures"
  - "Overloads keyword"
  - "hiding by signature"
  - "Visual Basic code, procedures"
  - "procedures, signatures for"
  - "procedures, overloading"
  - "procedures, multiple versions"
  - "parameters, lists"
  - "signatures, procedure"
  - "parameter lists"
  - "Visual Basic code, parameter lists"
  - "Shadows keyword"
  - "procedure overloading"
  - "procedures, parameter lists"
ms.assetid: fbc7fb18-e3b2-48b6-b554-64c00ed09d2a
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# Procedure Overloading (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

*Eseguire l'overload* di una routine significa definirla in più versioni, utilizzando lo stesso nome ma diversi elenchi di parametri.  Lo scopo dell'overload è definire più versioni strettamente correlate di una routine senza doverle distinguere per nome.  Questa operazione richiede la modifica dell'elenco di parametri.  
  
## Regole per l'overload  
 Quando si esegue l'overload di una routine, è necessario rispettare le seguenti regole:  
  
-   **Stesso nome**.  È necessario che ogni versione di overload utilizzi lo stesso nome di routine.  
  
-   **Firma diversa**.  È necessario che ogni versione di overload sia diversa dalle altre per almeno uno degli aspetti che seguono:  
  
    -   Numero di parametri  
  
    -   Ordine dei parametri  
  
    -   Tipi di dati dei parametri  
  
    -   Numero dei parametri di tipo \(per una routine generica\)  
  
    -   Tipo restituito \(solo per un operatore di conversione\)  
  
     L'insieme del nome di routine e degli elementi precedenti viene definito *firma* della routine.  Quando si chiama una routine di overload, il compilatore utilizza la firma per verificare la corrispondenza tra la chiamata e la definizione.  
  
-   **Elementi che non fanno parte della firma**.  Non è possibile eseguire l'overload di una routine senza modificare la firma.  In particolare, non è possibile eseguire l'overload di una routine modificando solo uno o più degli elementi che seguono:  
  
    -   Parole chiave di modificatori di routine, come `Public`, `Shared` e `Static`  
  
    -   Nomi dei parametri o dei parametri di tipo  
  
    -   Vincoli dei parametri di tipo \(per una routine generica\)  
  
    -   Parole chiave di modificatori di parametro, come `ByRef` e `Optional`  
  
    -   Eventuale restituzione di un valore  
  
    -   Tipo di dati del valore restituito \(fatta eccezione per gli operatori di conversione\)  
  
     Gli elementi riportati nell'elenco precedente non fanno parte della firma.  Sebbene non sia possibile utilizzarli per distinguere le versioni di overload, è possibile servirsene in modo vario nelle differenti versioni di overload adeguatamente differenziate dalle rispettive firme.  
  
-   **Argomenti ad associazione tardiva**.  Se si desidera passare una variabile oggetto ad associazione tardiva a una versione di overload, è necessario dichiarare il parametro appropriato come <xref:System.Object>.  
  
## Più versioni di una routine  
 Si supponga di scrivere una routine `Sub` per inviare una transazione relativa al saldo di un cliente e che si desideri potersi riferire al cliente tramite nome o tramite numero di conto.  Per rispondere a questa esigenza, è possibile definire due diverse routine `Sub`, come nell'esempio che segue:  
  
 [!code-vb[VbVbcnProcedures#73](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/procedure-overloading_1.vb)]  
  
### Versioni di overload  
 Un'alternativa consiste nell'esecuzione dell'overload di un singolo nome di routine.  È possibile utilizzare la parola chiave [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md) per definire una versione della routine per ogni elenco di parametri nel seguente modo:  
  
 [!code-vb[VbVbcnProcedures#72](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/procedure-overloading_2.vb)]  
  
#### Overload aggiuntivi  
 Se si desidera inoltre accettare l'importo di una transazione in `Decimal` o in `Single`, è possibile eseguire l'ulteriore overload di `post` per consentire tale variazione.  Se viene eseguita questa operazione per ognuno degli overload dell'esempio precedente, si ottengono quattro routine `Sub`, tutte con lo stesso nome ma con quattro diverse firme.  
  
## Vantaggi dell'overload  
 Il vantaggio dell'esecuzione dell'overload di una routine è rappresentato dalla flessibilità della chiamata.  Per utilizzare la routine `post` dichiarata nell'esempio precedente, il codice chiamante può ottenere l'identificazione del cliente in forma di `String` o di `Integer` e quindi chiamare la stessa routine in entrambi i casi.  Questa condizione è illustrata nell'esempio che segue.  
  
 [!code-vb[VbVbcnProcedures#56](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/procedure-overloading_3.vb)]  
  
 [!code-vb[VbVbcnProcedures#57](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/procedure-overloading_4.vb)]  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [How to: Define Multiple Versions of a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md)   
 [How to: Call an Overloaded Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-overloaded-procedure.md)   
 [How to: Overload a Procedure that Takes Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [How to: Overload a Procedure that Takes an Indefinite Number of Parameters](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [Considerations in Overloading Procedures](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)   
 [Overload Resolution](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)   
 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md)   
 [Tipi generici in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)