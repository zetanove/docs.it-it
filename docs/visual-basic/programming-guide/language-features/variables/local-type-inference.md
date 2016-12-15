---
title: "Local Type Inference (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "local type inference"
  - "vb.TypeInfer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Option Infer statement"
  - "local type inference [Visual Basic]"
  - "implicitly-typed local variables [Visual Basic]"
  - "variables [Visual Basic], type inference"
  - "inference [Visual Basic]"
  - "type inference [Visual Basic]"
ms.assetid: b8307f18-2e56-4ab3-a45a-826873f400f6
caps.latest.revision: 43
caps.handback.revision: 43
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Local Type Inference (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Il compilatore in Visual Basic utilizza un'*inferenza dei tipi* per determinare i tipi di dati delle variabili locali dichiarate senza una clausola `As`.  Tramite l'inferenza, il compilatore deduce il tipo della variabile dal tipo dell'espressione di inizializzazione  Questo consente di dichiarare le variabili senza dichiarare in modo esplicito un tipo, come illustrato nell'esempio seguente. Come conseguenza delle dichiarazioni, `num1` e `num2` sono fortemente tipizzati come Integer.  
  
 [!code-vb[VbVbalrTypeInference#1](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_1.vb)]  
  
> [!NOTE]
>  Se non si desidera che `num2` nell'esempio precedente sia tipizzato come un `Integer`, è possibile specificare un altro tipo utilizzando una dichiarazione come `Dim num3 As Object = 3` o `Dim num4 As Double = 3`.  
  
 L'inferenza del tipo di variabile locale si applica a livello di routine.  Non può essere utilizzata per dichiarare variabili a livello di modulo \(all'interno di una classe, una struttura, un modulo o un'interfaccia ma non all'interno di una routine o di un blocco\).  Se `num2` nell'esempio precedente fosse un campo di una classe anziché una variabile locale in una routine, la dichiarazione genererebbe un errore con `Option Strict` on e classificherebbe `num2` come `Object` con `Option Strict` off.  In modo analogo, l'inferenza del tipo di variabile locale non è applicabile alle variabili a livello di routine dichiarate come `Static`.  
  
## Inferenza del tipo eassociazione tardiva  
 Il codice che utilizza l'inferenza dei tipi è simile al codice basato sull'associazione tardiva.  Tuttavia, l'inferenza dei tipi digita può tipizzare fortemente la variabile anziché lasciarla come `Object`.  Il compilatore utilizza l'inizializzatore della variabile per determinare in fase di compilazione il tipo di variabile per produrre codice con associazione anticipata.  Nell'esempio precedente `num2`, come `num1`, è tipizzato come `Integer`.  
  
 Il comportamento delle variabili con associazione anticipata differisce da quello delle variabili con associazione tardiva per le quali il tipo è noto solo in fase di esecuzione .  Conoscere il tipo in anticipo consente al compilatore di identificare i problemi prima dell'esecuzione, di allocare la memoria con precisione e di eseguire altre ottimizzazioni.  L'associazione anticipata consente anche all'ambiente di sviluppo integrato \(IDE\) di Visual Basic di fornire la guida di IntelliSense per i membri di un oggetto.  L'associazione anticipata è preferibile anche in termini di prestazioni.  Perché su tutti i dati archiviati in una variabile ad associazione tardiva deve essere eseguito il wrapping come tipi `Object`e l'accesso in fase di esecuzione ai membri del tipo rende più lento il programma.  
  
## Esempi  
 L'inferenza del tipo si verifica quando una variabile locale viene dichiarata senza una clausola `As` e inizializzata.  Il compilatore utilizza il tipo del valore iniziale assegnato come tipo della variabile.  Ognuna delle righe di codice seguenti dichiara ad esempio una variabile di tipo `String`.  
  
 [!code-vb[VbVbalrTypeInference#2](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_2.vb)]  
  
 Nel codice seguente vengono illustrate due modalità equivalenti per creare una matrice di Integer.  
  
 [!code-vb[VbVbalrTypeInference#3](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_3.vb)]  
  
 È possibile utilizzare l'inferenza del tipo per determinare il tipo di una variabile di controllo del ciclo.  Nel codice seguente il compilatore deduce che `number` è un `Integer`, perché `someNumbers2` nell'esempio precedente è una matrice di Integer.  
  
 [!code-vb[VbVbalrTypeInference#4](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_4.vb)]  
  
 L'inferenza dei tipi locali può essere utilizzata nelle istruzioni `Using` per definire il tipo del nome della risorsa, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrTypeInference#7](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_5.vb)]  
  
 Il tipo di una variabile può anche essere dedotto dai valori restituiti da funzioni, come illustrato nell'esempio seguente.  Sia `pList1` che `pList2` sono matrici di processi perché `Process.GetProcesses` restituisce una matrice di processi.  
  
 [!code-vb[VbVbalrTypeInference#5](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_6.vb)]  
  
## Option Infer  
 `Option Infer` consente di specificare se l'inferenza del tipo di variabile locale è consentita in un particolare file.  Per abilitare o bloccare l'opzione, digitare una delle istruzioni seguenti all'inizio del file.  
  
 `Option Infer On`  
  
 `Option Infer Off`  
  
 Se non si specifica un valore per `Option Infer` nel codice, il valore predefinito del compilatore è `Option Infer On`.  Per i progetti aggiornati da [!INCLUDE[vb_orcas_long](../../../../visual-basic/misc/includes/vb_orcas_long_md.md)] o versioni precedenti, il valore predefinito del compilatore è `Option Infer Off`.  
  
 Se il valore impostato per `Option Infer` in un file è in conflitto con il valore impostato nell'IDE o sulla riga di comando, il valore nel file ha precedenza.  
  
 Per ulteriori informazioni, vedere [Option Infer Statement](../../../../visual-basic/language-reference/statements/option-infer-statement.md) e [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic).  
  
## Restrizioni  
 L'inferenza dei tipi può essere utilizzata solo per variabili locali non statiche; non può essere utilizzata per determinare tipo di campi, proprietà, o funzioni di classi.  
  
## Vedere anche  
 [Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Early and Late Binding](../../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md)   
 [Istruzione For Each...Next](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [Istruzione For...Next](../../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Option Infer Statement](../../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [\/optioninfer](../../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)