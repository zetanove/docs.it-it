---
title: /netcf | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /netcf
- netcf
dev_langs:
- VB
helpviewer_keywords:
- -netcf compiler option [Visual Basic]
- netcf compiler option [Visual Basic]
- /netcf compiler option [Visual Basic]
ms.assetid: db7cfa59-c315-401c-a59b-0daf355343d6
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
ms.openlocfilehash: d8e2328eb5434ea0e73238709c429975ae29e6d0
ms.lasthandoff: 03/13/2017

---
# <a name="netcf"></a>/netcf
Imposta il compilatore in modo che punti a [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
/netcf  
```  
  
## <a name="remarks"></a>Note  
 Il `/netcf` opzione il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore alla destinazione di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)] anziché l'intero [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]. Funzionalità di linguaggio che è presente solo nella versione completa [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] è disabilitato.  
  
 Il `/netcf` opzione è progettata per essere utilizzato con [/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md). Le funzionalità di linguaggio disabilitate da `/netcf` sono le stesse funzionalità di linguaggio non presenti nel file di destinazione con `/sdkpath`.  
  
> [!NOTE]
>  Il `/netcf` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando. Il `/netcf` opzione viene impostata quando un [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] dispositivo progetto viene caricato.  
  
 Il `/netcf` opzione consente di modificare le funzionalità del linguaggio seguenti:  
  
-   Il [End \<parola chiave > istruzione](../../../visual-basic/language-reference/statements/end-keyword-statement.md) (parola chiave), che termina l'esecuzione di un programma, è disabilitato. Il seguente programma compilato ed eseguito senza `/netcf` ma non riesce in fase di compilazione con `/netcf`.  
  
     [!code-vb[VbVbalrCompiler&#34;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/netcf_1.vb)]  
  
-   L'associazione tardiva, in tutti i form, è disabilitata. Quando vengono rilevati gli scenari di associazione tardiva riconosciuti, vengono generati errori in fase di compilazione. Il seguente programma compilato ed eseguito senza `/netcf` ma non riesce in fase di compilazione con `/netcf`.  
  
     [!code-vb[VbVbalrCompiler&#35;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/netcf_2.vb)]  
  
-   Il [Auto](../../../visual-basic/language-reference/modifiers/auto.md), [Ansi](../../../visual-basic/language-reference/modifiers/ansi.md), e [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md) modificatori sono disabilitati. La sintassi di [l'istruzione Declare](../../../visual-basic/language-reference/statements/declare-statement.md) istruzione viene inoltre modificata in `Declare Sub|Function name Lib "library" [Alias "alias"] [([arglist])]`. Il codice seguente viene illustrato l'effetto di `/netcf` su una compilazione.  
  
     [!code-vb[VbVbalrCompiler&#36;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/netcf_3.vb)]  
  
-   Utilizzando le parole chiave Visual Basic 6.0 che sono stati rimossi dalla [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] genera un errore diverso quando `/netcf` viene utilizzato. Ciò influisce sui messaggi di errore per le parole chiave seguenti:  
  
    -   `Open`  
  
    -   `Close`  
  
    -   `Put`  
  
    -   `Print`  
  
    -   `Write`  
  
    -   `Input`  
  
    -   `Lock`  
  
    -   `Unlock`  
  
    -   `Seek`  
  
    -   `Width`  
  
    -   `Name`  
  
    -   `FreeFile`  
  
    -   `EOF`  
  
    -   `Loc`  
  
    -   `LOF`  
  
    -   `Line`  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `Myfile.vb` con il [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)], con le versioni di mscorlib. dll e Microsoft.VisualBasic.dll trovato nella directory di installazione predefinita di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)] nell'unità C. In genere, si utilizzerà la versione più recente di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)].  
  
```  
vbc /netcf /sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)
