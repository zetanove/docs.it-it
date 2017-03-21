---
title: Inferenza del tipo locale (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- local type inference
- vb.TypeInfer
dev_langs:
- VB
helpviewer_keywords:
- Option Infer statement
- local type inference [Visual Basic]
- implicitly-typed local variables [Visual Basic]
- variables [Visual Basic], type inference
- inference [Visual Basic]
- type inference [Visual Basic]
ms.assetid: b8307f18-2e56-4ab3-a45a-826873f400f6
caps.latest.revision: 43
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
ms.openlocfilehash: 2bb673ce871b8e875f62c373404a849c139ab598
ms.lasthandoff: 03/13/2017

---
# <a name="local-type-inference-visual-basic"></a>Inferenza del tipo di variabile locale (Visual Basic)
Il compilatore Visual Basic utilizza *inferenza del tipo* per determinare i tipi di dati delle variabili locali dichiarate senza un `As` clausola. Il compilatore deduce il tipo della variabile dal tipo dell'espressione di inizializzazione. In questo modo è possibile dichiarare variabili senza dichiarare in modo esplicito un tipo, come illustrato nell'esempio seguente. Come risultato le dichiarazioni, entrambi `num1` e `num2` sono fortemente tipizzati come integer.  
  
 [!code-vb[VbVbalrTypeInference n.&1;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_1.vb)]  
  
> [!NOTE]
>  Se non si desidera `num2` nell'esempio precedente sia tipizzato come un `Integer`, è possibile specificare un altro tipo utilizzando una dichiarazione come `Dim num3 As Object = 3` o `Dim num4 As Double = 3`.  
  
 Inferenza del tipo locale si applica a livello di routine. E non può essere utilizzato per dichiarare le variabili a livello di modulo (all'interno di una classe, struttura, modulo o interfaccia ma non all'interno di una routine o blocco). Se `num2` nell'esempio precedente fosse un campo di una classe anziché una variabile locale in una procedura, la dichiarazione genererebbe un errore con `Option Strict` e classificherebbe `num2` come un `Object` con `Option Strict` off. Analogamente, l'inferenza del tipo locale non si applica a variabili a livello di routine dichiarate come `Static`.  
  
## <a name="type-inference-vs-late-binding"></a>Inferenza del tipo e. L'associazione tardiva  
 Codice che utilizza l'inferenza del tipo è simile al codice che si basa sull'associazione tardiva. Tuttavia, l'inferenza del tipo tipizzare fortemente la variabile anziché lasciarla come `Object`. Il compilatore utilizza l'inizializzatore di variabile per determinare il tipo della variabile in fase di compilazione per produrre codice con associazione anticipata. Nell'esempio precedente, `num2`, come `num1`, tipizzato come un `Integer`.  
  
 Il comportamento delle variabili con associazione anticipata differisce da quello di variabili ad associazione tardiva, per cui il tipo è noto solo in fase di esecuzione. Sapere in anticipo il tipo consente al compilatore di identificare i problemi prima dell'esecuzione, in modo preciso della memoria ed eseguire altre ottimizzazioni. Associazione anticipata consente inoltre l'ambiente di sviluppo integrato (IDE) di IntelliSense consentono di ottenere informazioni sui membri di un oggetto di Visual Basic. È preferibile per le prestazioni anche l'associazione anticipata. In questo modo tutti i dati archiviati in una variabile ad associazione tardiva devono essere incluso come tipo `Object`, e l'accesso ai membri del tipo in fase di esecuzione rende più lento il programma.  
  
## <a name="examples"></a>Esempi  
 L'inferenza del tipo si verifica quando una variabile locale viene dichiarata senza una `As` clausola ed è stato inizializzato. Il compilatore utilizza il tipo di valore iniziale assegnato come il tipo della variabile. Ad esempio, ognuna delle righe di codice seguente dichiara una variabile di tipo `String`.  
  
 [!code-vb[VbVbalrTypeInference n.&2;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_2.vb)]  
  
 Il codice seguente illustra due modalità equivalenti per creare una matrice di interi.  
  
 [!code-vb[VbVbalrTypeInference n.&3;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_3.vb)]  
  
 È consigliabile usare l'inferenza del tipo per determinare il tipo di una variabile di controllo del ciclo. Nel codice seguente, il compilatore deduce che `number` è un `Integer` poiché `someNumbers2` dell'esempio precedente è una matrice di interi.  
  
 [!code-vb[VbVbalrTypeInference n.&4;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_4.vb)]  
  
 Inferenza del tipo locale può essere utilizzato `Using` istruzioni per stabilire il tipo del nome della risorsa, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrTypeInference&#7;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_5.vb)]  
  
 Il tipo di una variabile può essere dedotte anche dai valori restituiti delle funzioni, come illustrato nell'esempio seguente. Entrambi `pList1` e `pList2` sono costituiti da matrici di processi perché `Process.GetProcesses` restituisce una matrice di processi.  
  
 [!code-vb[VbVbalrTypeInference n.&5;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/local-type-inference_6.vb)]  
  
## <a name="option-infer"></a>Option Infer  
 `Option Infer`Consente di specificare se l'inferenza del tipo locale è consentito in un determinato file. Per consentire o bloccare l'opzione, digitare una delle seguenti istruzioni all'inizio del file.  
  
 `Option Infer On`  
  
 `Option Infer Off`  
  
 Se non si specifica un valore per `Option Infer` nel codice, il valore predefinito del compilatore è `Option Infer On`. Per i progetti aggiornati da [!INCLUDE[vb_orcas_long](../../../../visual-basic/misc/includes/vb_orcas_long_md.md)] o precedenti, il valore predefinito del compilatore è `Option Infer Off`.  
  
 Se il valore impostato per `Option Infer` in un file è in conflitto con il valore impostato nell'IDE o sulla riga di comando, il valore nel file ha precedenza.  
  
 Per ulteriori informazioni, vedere [Option Infer Statement](../../../../visual-basic/language-reference/statements/option-infer-statement.md) e [pagina Compila, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic).  
  
## <a name="restrictions"></a>Restrizioni  
 L'inferenza del tipo può essere utilizzato solo per variabili locali statiche. non può essere usato per determinare il tipo di classe campi, proprietà o funzioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Associazione anticipata e tardiva](../../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)   
 [Per ogni corso... Next (istruzione)](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [For... Next (istruzione)](../../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Istruzione Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [/optioninfer](../../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
