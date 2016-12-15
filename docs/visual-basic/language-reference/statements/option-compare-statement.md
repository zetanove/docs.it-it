---
title: "Option Compare Statement | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Compare"
  - "vb.OptionCompare"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "case sensitivity, Option Compare statement"
  - "Compare keyword"
  - "binary comparison"
  - "strings [Visual Basic], returning from functions"
  - "binary comparison, Option Compare statement"
  - "strings [Visual Basic], comparing"
  - "string comparison [Visual Basic], Option Compare statement"
  - "Text keyword, Option Compare statement"
  - "Binary keyword, Option Compare statement"
  - "string comparison [Visual Basic], sorting data"
  - "Option Compare statement"
  - "text [Visual Basic], comparing"
ms.assetid: 54e8eeeb-3b0d-4fb9-acce-fbfbd5975f6e
caps.latest.revision: 37
caps.handback.revision: 37
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Option Compare Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Dichiara il metodo di confronto predefinito da usare durante il confronto dei dati di tipo stringa.  
  
## Sintassi  
  
```  
Option Compare { Binary | Text }  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`Binary`|Parametro facoltativo.  Consente di eseguire confronti tra stringhe basati su un criterio di ordinamento derivato dalle rappresentazioni binarie interne dei caratteri.<br /><br /> Questo tipo di confronto è particolarmente utile se le stringhe possono contenere caratteri che non devono essere interpretati come testo.  In questo caso, non è consigliabile consentire che il confronto sia falsato da equivalenze alfabetiche, ad esempio dalla mancata distinzione tra maiuscole e minuscole.|  
|`Text`|Parametro facoltativo.  Consente di eseguire confronti tra stringhe basati su un criterio di ordinamento testuale senza distinzione tra maiuscole e minuscole determinato dalle impostazioni locali del sistema.<br /><br /> Questo tipo di confronto è utile se le stringhe contengono tutti caratteri di testo e si vuole confrontarle prendendo in considerazione le equivalenze alfabetiche, quali la mancata distinzione tra maiuscole e minuscole e le lettere strettamente correlate.  Ad esempio, è possibile considerare le lettere `A` e `a` equivalenti e fare in modo che le lettere `Ä` e `ä` precedano `B` e `b`.|  
  
## Note  
 Se usato, è necessario includere l'istruzione `Option Compare` in un file prima di tutte le altre istruzioni del codice sorgente.  
  
 L'istruzione `Option Compare` specifica il metodo di confronto tra stringhe \(`Binary` o `Text`\).  Il metodo di confronto del testo predefinito è `Binary`.  
  
 Un confronto `Binary` confronta il valore numerico Unicode di ogni carattere in ciascuna stringa.  Un confronto `Text` confronta ogni carattere Unicode in base al relativo significato lessicale nelle impostazioni cultura correnti.  
  
 Il criterio di ordinamento di Microsoft Windows è determinato dalla tabella codici.  Per altre informazioni, vedere [Tabelle codici](/visual-cpp/c-runtime-library/code-pages).  
  
 Nell'esempio seguente i caratteri nella tabella codici \(ANSI 1252\) per le lingue inglese ed europee vengono ordinati usando `Option Compare Binary`, che determina un tipico ordinamento binario.  
  
 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`  
  
 Se gli stessi caratteri nella stessa tabella codici venissero ordinati con `Option Compare Text`, si otterrebbe il seguente ordinamento testuale.  
  
 `(A=a) < (À = à) < (B=b) < (E=e) < (Ê = ê) < (Z=z) < (Ø = ø)`  
  
## Quando non è presente un'istruzione Option Compare  
 Se nel codice sorgente non è presente un'istruzione `Option Compare`, si usa l'impostazione **Option Compare** disponibile in [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic).  Se si usa il compilatore a riga di comando, viene usata l'impostazione specificata dall'opzione del compilatore [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md).  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
#### Per impostare Option Compare nell'IDE  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per altre informazioni, vedere [NIB: Managing Project Properties with the Project Designer](http://msdn.microsoft.com/it-it/983f3c18-832f-4666-afec-74b716ff3e0e).  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Impostare il valore della casella **Option Compare**.  
  
 Quando si crea un progetto, l'impostazione **Option Compare** nella scheda **Compila** viene impostata con il valore dell'impostazione **Option Compare** della finestra di dialogo **Opzioni**.  Per modificare questa impostazione, scegliere **Opzioni** dal menu **Strumenti**.  Nella finestra di dialogo **Opzioni** espandere **Progetti e soluzioni**, quindi fare clic su **Impostazioni predefinite di Visual Basic**.  L'impostazione predefinita iniziale in **Impostazioni predefinite di Visual Basic** è **Binario**.  
  
#### Per impostare Option Compare sulla riga di comando  
  
-   Includere l'opzione del compilatore [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md) nel comando **vbc**.  
  
## Esempio  
 Nell'esempio seguente viene usata l'istruzione `Option Compare` per impostare il confronto binario come metodo predefinito per il confronto tra stringhe.  Per usare questo codice, rimuovere il commento dall'istruzione `Option Compare Binary` e inserirlo all'inizio del file di origine.  
  
 [!code-vb[VbVbalrStatements#45](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-compare-statement_1.vb)]  
  
## Esempio  
 Nell'esempio seguente viene usata l'istruzione `Option Compare` per impostare il criterio di ordinamento del testo senza distinzione tra maiuscole e minuscole come metodo predefinito per il confronto tra stringhe.  Per usare questo codice, rimuovere il commento dall'istruzione `Option Compare Text` e inserirlo all'inizio del file di origine.  
  
 [!code-vb[VbVbalrStatements#46](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-compare-statement_2.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Strings.InStr%2A>   
 <xref:Microsoft.VisualBasic.Strings.InStrRev%2A>   
 <xref:Microsoft.VisualBasic.Strings.Replace%2A>   
 <xref:Microsoft.VisualBasic.Strings.Split%2A>   
 <xref:Microsoft.VisualBasic.Strings.StrComp%2A>   
 [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [Comparison Operators](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Comparison Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Like Operator](../../../visual-basic/language-reference/operators/like-operator.md)   
 [Funzioni stringa](../../../visual-basic/language-reference/functions/string-functions.md)   
 [Option Explicit Statement](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md)