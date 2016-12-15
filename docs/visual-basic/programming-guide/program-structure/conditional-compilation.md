---
title: "Conditional Compilation in Visual Basic | Microsoft Docs"
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
  - "conditional compilation, about conditional compilation"
  - "compilation, conditional"
ms.assetid: 9c35e55e-7eee-44fb-a586-dad1f1884848
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Conditional Compilation in Visual Basic
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nella *compilazione condizionale*, blocchi particolari di codice in un programma vengono compilati in modo selettivo, mentre altri vengono ignorati.  
  
 È possibile, ad esempio, scrivere istruzioni di debug per confrontare la velocità di metodi diversi per compiere la stessa attività di programmazione o localizzare un'applicazione in più lingue.  Le istruzioni di compilazione condizionale sono progettate per essere eseguite in fase di compilazione, non di esecuzione.  
  
 Per indicare blocchi di codice da compilare in modo condizionale, utilizzare la direttiva `#If...Then...#Else`.  Per creare, ad esempio, una versione in francese e in tedesco della stessa applicazione dallo stesso codice sorgente, incorporare segmenti di codice specifici per la piattaforma nelle istruzioni `#If...Then` utilizzando le costanti predefinite `FrenchVersion` e `GermanVersion`.  L'esempio seguente illustra come eseguire questa operazione:  
  
 [!code-vb[VbVbalrConditionalComp#5](../../../visual-basic/language-reference/directives/codesnippet/VisualBasic/conditional-compilation_1.vb)]  
  
 Se si imposta il valore della costante di compilazione condizionale `FrenchVersion` su `True` in fase di compilazione, viene compilato il codice condizionale per la versione francese.  Se si imposta il valore della costante `GermanVersion` su `True`, il compilatore utilizza la versione tedesca.  Se nessuno dei due valori è impostato su `True`, viene eseguito il codice contenuto nell'ultimo blocco `Else`.  
  
> [!NOTE]
>  Il completamento automatico non funziona quando si effettuano operazioni di modifica del codice e si utilizzano direttive di compilazione condizionale se il codice non fa parte della diramazione corrente.  
  
## Dichiarazione di costanti di compilazione condizionale  
 È possibile impostare le costanti di compilazione condizionale in tre modi:  
  
-   In **Progettazione progetti**  
  
-   Nella riga di comando quando si utilizza il compilatore della riga di comando  
  
-   Nel codice  
  
 Le costanti di compilazione condizionale hanno un ambito di validità speciale e non è possibile accedere a esse dal codice standard.  L'ambito di validità di una costante di compilazione condizionale dipende dal modo in cui viene impostata.  Nella tabella seguente viene indicato l'ambito di validità delle costanti dichiarate utilizzando ciascuna delle tre modalità menzionate sopra.  
  
|||  
|-|-|  
|Modalità di impostazione della costante|Ambito di validità della costante|  
|**Progettazione progetti**|Pubblico rispetto a tutti i file del progetto|  
|Riga di comando|Pubblico rispetto a tutti i file passati al compilatore della riga di comando|  
|Istruzione`#Const` nel codice|Privato rispetto al file nel quale viene dichiarato|  
  
||  
|-|  
|Per impostare le costanti in Progettazione progetti|  
|-   Prima di creare il file eseguibile, impostare le costanti nella finestra di dialogo **Progettazione progetti** seguendo la procedura illustrata nella sezione [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67).|  
  
||  
|-|  
|Per impostare le costanti sulla riga di comando|  
|-   Utilizzare l'opzione **\/d** per inserire le costanti di compilazione condizionale, come nell'esempio che segue:<br />     `vbc MyProj.vb /d:conFrenchVersion=–1:conANSI=0`<br />     Non è necessario inserire spazi tra l'opzione **\/d** e la prima costante.  Per ulteriori informazioni, vedere [\/define](../../../visual-basic/reference/command-line-compiler/define.md).<br />     Le dichiarazioni sulla riga di comando eseguono l'override delle dichiarazioni inserite nella finestra di dialogo **Progettazione progetti**, ma non le cancellano.  Gli argomenti impostati nella finestra di dialogo **Progettazione progetti** rimangono validi per le compilazioni successive.<br />     Quando le costanti vengono scritte direttamente nel codice, non esistono regole precise circa la loro collocazione, in quanto il loro ambito di validità è l'intero modulo nel quale sono dichiarate.|  
  
||  
|-|  
|Per impostare le costanti nel codice|  
|-   Inserire le costanti nel blocco di dichiarazione del modulo nel quale sono utilizzate.  Questo agevola l'organizzazione e la facilità di lettura del codice.|  
  
## Argomenti correlati  
  
|||  
|-|-|  
|Titolo|Descrizione|  
|[Struttura del programma e convenzioni di scrittura del codice](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)|Vengono forniti suggerimenti per semplificare la lettura e la gestione del codice.|  
  
## Riferimento  
 [\#Const Directive](../../../visual-basic/language-reference/directives/const-directive.md)  
  
 [\#If...Then...\#Else Directives](../../../visual-basic/language-reference/directives/if-then-else-directives.md)  
  
 [\/define](../../../visual-basic/reference/command-line-compiler/define.md)