---
title: "Option Infer Statement | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.OptionInfer"
  - "vb.Infer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "variables [Visual Basic], declaring"
  - "Option Infer statement"
  - "Infer keyword"
  - "declaring variables, inferred"
  - "inferred variable declaration"
ms.assetid: 4ad3e6e9-8f5b-4209-a248-de22ef6e4652
caps.latest.revision: 72
caps.handback.revision: 72
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Option Infer Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Abilita l'uso dell'inferenza del tipo di variabile locale nelle variabili dichiaranti.  
  
## Sintassi  
  
```  
Option Infer { On | Off }  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`On`|Parametro facoltativo.  Abilita l'inferenza del tipo di variabile locale.|  
|`Off`|Parametro facoltativo.  Disabilita l'inferenza del tipo di variabile locale.|  
  
## Note  
 Per impostare `Option Infer` in un file, digitare `Option Infer On` oppure `Option Infer Off` all'inizio del file, prima di qualsiasi altro codice sorgente.  Se il valore impostato per `Option Infer` in un file è in conflitto con il valore impostato nell'IDE o sulla riga di comando, il valore nel file ha precedenza.  
  
 Quando si imposta `Option Infer` su `On`, è possibile dichiarare variabili locali senza dichiarare in modo esplicito un tipo di dati.  Tramite l'inferenza, il compilatore deriva il tipo di dati di una variabile dal tipo della relativa espressione di inizializzazione.  
  
 Nella figura seguente, l'istruzione `Option Infer` è abilitata.  La variabile nella dichiarazione `Dim someVar = 2` viene dichiarata come Integer in base all'inferenza del tipo.  
  
 ![Visualizzazione IntelliSense della dichiarazione](../../../visual-basic/language-reference/statements/media/optioninferasinteger.png "optionInferAsInteger")  
IntelliSense quando Option Infer è attivato  
  
 Nella figura seguente, l'istruzione `Option Infer` è disabilitata.  La variabile nella dichiarazione `Dim someVar = 2` viene dichiarata come `Object` in base all'inferenza del tipo.  In questo esempio, l'impostazione **Option Strict** viene impostata su **Off** nella [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic).  
  
 ![Visualizzazione IntelliSense della dichiarazione](../../../visual-basic/language-reference/statements/media/optioninferasobject.png "optionInferAsObject")  
IntelliSense quando Option Infer è disabilitato  
  
> [!NOTE]
>  Quando una variabile viene dichiarata come `Object`, il tipo di runtime può essere modificato mentre il programma è in esecuzione.  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] esegue operazioni chiamate conversione *boxing* e conversione *unboxing* per convertire tra `Object` e un tipo di valore, il che rende l'esecuzione più lenta.  Per informazioni sulle conversioni boxing e unboxing, vedere [Visual Basic Language Specification](../../../visual-basic/reference/language-specification.md).  
  
 L'inferenza del tipo si applica a livello di routine e non si applica all'esterno di una routine in una classe, una struttura, un modulo o un'interfaccia.  
  
 Per altre informazioni, vedere [Local Type Inference](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).  
  
## Quando non è presente un'istruzione Option Infer  
 Se nel codice sorgente non è presente un'istruzione `Option Infer`, si usa l'impostazione **Option Infer** disponibile in [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic).  Se si usa il compilatore della riga di comando, viene usata l'opzione del compilatore [\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md).  
  
#### Per impostare Option Infer nell'IDE  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per altre informazioni, vedere [NIB: Managing Project Properties with the Project Designer](http://msdn.microsoft.com/it-it/983f3c18-832f-4666-afec-74b716ff3e0e).  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Impostare il valore nella casella **Option infer**.  
  
 Quando si crea un nuovo progetto, l'impostazione **Option Infer** nella scheda **Compila** viene definita in base all'impostazione **Option Infer** nella finestra di dialogo **Impostazioni predefinite di Visual Basic**.  Per accedere alla finestra di dialogo **Impostazioni predefinite di Visual Basic**, scegliere **Opzioni** dal menu **Strumenti**.  Nella finestra di dialogo **Opzioni** espandere **Progetti e soluzioni**, quindi fare clic su **Impostazioni predefinite di Visual Basic**.  L'impostazione predefinita iniziale in **Impostazioni predefinite di Visual Basic** è `On`.  
  
#### Per impostare Option Infer nella riga di comando  
  
-   Includere l'opzione del compilatore [\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md) nel comando **vbc**.  
  
## Tipi di dati e valori predefiniti  
 Nella tabella seguente vengono descritti i risultati di varie combinazioni della specifica del tipo di dati e dell'inizializzatore in un'istruzione `Dim`.  
  
|||||  
|-|-|-|-|  
|Tipo di dati specificato?|Inizializzatore specificato?|Esempio|Risultato|  
|No|No|`Dim qty`|Se `Option Strict` è disabilitato \(impostazione predefinita\), la variabile è impostata su `Nothing`.<br /><br /> Se `Option Strict` è abilitato, si verifica un errore in fase di compilazione.|  
|No|Sì|`Dim qty = 5`|Se `Option Infer` è abilitato \(impostazione predefinita\), alla variabile viene assegnato il tipo di dati dell'inizializzatore.  Vedere [Local Type Inference](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).<br /><br /> Se le istruzioni `Option Infer` e `Option Strict` sono disabilitate, il tipo di dati accettato dalla variabile è `Object`.<br /><br /> Se `Option Infer` è disabilitato e `Option Strict` è abilitato, si verifica un errore in fase di compilazione.|  
|Sì|No|`Dim qty As Integer`|La variabile viene inizializzata sul valore predefinito per il tipo di dati.  Per altre informazioni, vedere [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md).|  
|Sì|Sì|`Dim qty  As Integer = 5`|Se il tipo di dati dell'inizializzatore non è convertibile nel tipo di dati specificato, si verifica un errore in fase di compilazione.|  
  
## Esempio  
 Gli esempi seguenti illustrano come l'istruzione `Option Infer` permette di usare inferenza del tipo di variabile locale.  
  
 [!code-vb[VbVbalrTypeInference#6](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/option-infer-statement_1.vb)]  
  
## Esempio  
 L'esempio seguente dimostra che il tipo di runtime può differire quando una variabile viene identificata come `Object`.  
  
 [!code-vb[VbVbalrTypeInference#11](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/option-infer-statement_2.vb)]  
  
## Vedere anche  
 [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Local Type Inference](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Compare Statement](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Option Explicit Statement](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)   
 [\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [Boxing e unboxing](../../../csharp/programming-guide/types/boxing-and-unboxing.md)