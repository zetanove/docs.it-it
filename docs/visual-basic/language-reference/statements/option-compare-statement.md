---
title: Option Compare (istruzione) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Compare
- vb.OptionCompare
dev_langs:
- VB
helpviewer_keywords:
- case sensitivity, Option Compare statement
- Compare keyword
- binary comparison
- strings [Visual Basic], returning from functions
- binary comparison, Option Compare statement
- strings [Visual Basic], comparing
- string comparison [Visual Basic], Option Compare statement
- Text keyword, Option Compare statement
- Binary keyword, Option Compare statement
- string comparison [Visual Basic], sorting data
- Option Compare statement
- text [Visual Basic], comparing
ms.assetid: 54e8eeeb-3b0d-4fb9-acce-fbfbd5975f6e
caps.latest.revision: 37
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8b1b077a8818315e52ada6b08ff1e1ced9bbd17c
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="option-compare-statement"></a>Istruzione Option Compare
Dichiara il metodo di confronto predefinito da usare durante il confronto dei dati di tipo stringa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Option Compare { Binary | Text }  
```  
  
## <a name="parts"></a>Parti  
  
|Termine|Definizione|  
|---|---|  
|`Binary`|Parametro facoltativo. Consente di eseguire confronti tra stringhe basati su un criterio di ordinamento derivato dalle rappresentazioni binarie interne dei caratteri.<br /><br /> Questo tipo di confronto è particolarmente utile se le stringhe possono contenere caratteri che non devono essere interpretati come testo. In questo caso, non è consigliabile consentire che il confronto sia falsato da equivalenze alfabetiche, ad esempio dalla mancata distinzione tra maiuscole e minuscole.|  
|`Text`|Parametro facoltativo. Consente di eseguire confronti tra stringhe basati su un criterio di ordinamento testuale senza distinzione tra maiuscole e minuscole determinato dalle impostazioni locali del sistema.<br /><br /> Questo tipo di confronto è utile se le stringhe contengono tutti caratteri di testo e si vuole confrontarle prendendo in considerazione le equivalenze alfabetiche, quali la mancata distinzione tra maiuscole e minuscole e le lettere strettamente correlate. Ad esempio, è possibile considerare le lettere `A` e `a` equivalenti e fare in modo che le lettere `Ä` e `ä` precedano `B` e `b`.|  
  
## <a name="remarks"></a>Note  
 Se usato, è necessario includere l'istruzione `Option Compare` in un file prima di tutte le altre istruzioni del codice sorgente.  
  
 L'istruzione `Option Compare` specifica il metodo di confronto tra stringhe (`Binary` o `Text`).  Il metodo di confronto del testo predefinito è `Binary`.  
  
 Un confronto `Binary` confronta il valore numerico Unicode di ogni carattere in ciascuna stringa. Un confronto `Text` confronta ogni carattere Unicode in base al relativo significato lessicale nelle impostazioni cultura correnti.  
  
 Il criterio di ordinamento di Microsoft Windows è determinato dalla tabella codici. Per altre informazioni, vedere [Tabelle codici](https://docs.microsoft.com/cpp/c-runtime-library/code-pages).  
  
 Nell'esempio seguente i caratteri nella tabella codici (ANSI 1252) per le lingue inglese ed europee vengono ordinati usando `Option Compare Binary`, che determina un tipico ordinamento binario.  
  
 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`  
  
 Se gli stessi caratteri nella stessa tabella codici venissero ordinati con `Option Compare Text`, si otterrebbe il seguente ordinamento testuale.  
  
 `(A=a) < (À = à) < (B=b) < (E=e) < (Ê = ê) < (Z=z) < (Ø = ø)`  
  
## <a name="when-an-option-compare-statement-is-not-present"></a>Quando non è presente un'istruzione Option Compare  
 Se il codice sorgente non contiene un `Option Compare` istruzione, il **Option Compare** impostazione per il [pagina Compila, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic) viene utilizzato. Se si utilizza il compilatore della riga di comando, l'impostazione specificata per il [/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md) viene utilizzata l'opzione del compilatore.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
#### <a name="to-set-option-compare-in-the-ide"></a>Per impostare Option Compare nell'IDE  
  
1.  In **Esplora**, selezionare un progetto. Nel **progetto** menu, fare clic su **proprietà**. Per ulteriori informazioni, vedere [NIB: gestione di proprietà del progetto con Progettazione](http://msdn.microsoft.com/en-us/983f3c18-832f-4666-afec-74b716ff3e0e).  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Impostare il valore di **Option Compare** casella.  
  
 Quando si crea un progetto, il **Option Compare** impostazione per il **compilare** scheda è impostata sul **Option Compare** impostazione nel **opzioni** la finestra di dialogo. Per modificare questa impostazione, scegliere il **strumenti** menu, fare clic su **opzioni**. Nel **opzioni** finestra di dialogo espandere **progetti e soluzioni**, quindi fare clic su **impostazioni predefinite di Visual Basic**. L'impostazione predefinita iniziale in **impostazioni predefinite di Visual Basic** è **binario**.  
  
#### <a name="to-set-option-compare-on-the-command-line"></a>Per impostare Option Compare sulla riga di comando  
  
-   Includere il [/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md) opzione del compilatore di **vbc** comando.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene usata l'istruzione `Option Compare` per impostare il confronto binario come metodo predefinito per il confronto tra stringhe. Per usare questo codice, rimuovere il commento dall'istruzione `Option Compare Binary` e inserirlo all'inizio del file di origine.  
  
 [!code-vb[N. VbVbalrStatements&45;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-compare-statement_1.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene usata l'istruzione `Option Compare` per impostare il criterio di ordinamento del testo senza distinzione tra maiuscole e minuscole come metodo predefinito per il confronto tra stringhe. Per usare questo codice, rimuovere il commento dall'istruzione `Option Compare Text` e inserirlo all'inizio del file di origine.  
  
 [!code-vb[VbVbalrStatements n.&46;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-compare-statement_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Strings.InStr%2A></xref:Microsoft.VisualBasic.Strings.InStr%2A>   
 <xref:Microsoft.VisualBasic.Strings.InStrRev%2A></xref:Microsoft.VisualBasic.Strings.InStrRev%2A>   
 <xref:Microsoft.VisualBasic.Strings.Replace%2A></xref:Microsoft.VisualBasic.Strings.Replace%2A>   
 <xref:Microsoft.VisualBasic.Strings.Split%2A></xref:Microsoft.VisualBasic.Strings.Split%2A>   
 <xref:Microsoft.VisualBasic.Strings.StrComp%2A></xref:Microsoft.VisualBasic.Strings.StrComp%2A>   
 [/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [Operatori di confronto](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Operatori di confronto in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [LIKE (operatore)](../../../visual-basic/language-reference/operators/like-operator.md)   
 [Funzioni stringa](../../../visual-basic/language-reference/functions/string-functions.md)   
 [Istruzione Option Explicit](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Istruzione Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md)
