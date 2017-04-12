---
title: Esempio di righe di comando di compilazione (Visual Basic) | Documenti di Microsoft
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
- command line, compilers
- compilation, command-line
- command-line compilers
- compiling source code, from command line
- Visual Basic compiler, sample command lines
ms.assetid: 5bfbb487-5f47-4267-969a-39dfb917beeb
caps.latest.revision: 14
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 918787b3377f2e5a636a6b098046ac2f455efcdd
ms.lasthandoff: 03/13/2017

---
# <a name="sample-compilation-command-lines-visual-basic"></a>Esempi di righe di comando di compilazione (Visual Basic)
In alternativa alla compilazione [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] programmi dall'interno [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)], è possibile compilare dalla riga di comando per generare file di libreria a collegamento dinamico (DLL) o eseguibili (.exe).  
  
 Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore da riga di comando supporta un set completo di opzioni che controllano i file di input e outpui, assembly e il debug e le opzioni per il preprocessore. Ogni opzione è disponibile in due formati intercambiabili: `-``option` e `/``option`. Questa documentazione viene visualizzato soltanto il `/``option` form.  
  
 Nella tabella seguente sono elencate alcune righe di comando di esempio che è possibile modificare per uso personale.  
  
|Per|Usare|  
|--------|---------|  
|Compilare i file. vb e creare File.exe|`vbc /reference:Microsoft.VisualBasic.dll File.vb`|  
|Compilare i file. vb e creare file. dll|`vbc /target:library File.vb`|  
|Compilare i file. vb e creare My.exe|`vbc /out:My.exe File.vb`|  
|Compilare tutti [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] file nella directory corrente, con le ottimizzazioni e `DEBUG` simbolo definito, generando File2.exe|`vbc /define:DEBUG=1 /optimize /out:File2.exe *.vb`|  
|Compilare tutti [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] file nella directory corrente, generando una versione di debug di File2. dll senza visualizzare il logo o avvisi|`vbc /target:library /out:File2.dll /nowarn /nologo /debug *.vb`|  
|Compilare tutti [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] file nella directory corrente in qualcosa. dll|`vbc /target:library /out:Something.dll *.vb`|  
  
 Durante la compilazione dalla riga di comando, è necessario fare esplicitamente riferimento Microsoft [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] libreria di runtime tramite il `/reference` l'opzione del compilatore.  
  
> [!TIP]
>  Quando si compila un progetto utilizzando l'IDE di Visual Studio, è possibile visualizzare informazioni su associata **vbc** comando con le opzioni del compilatore nella finestra di output. Per visualizzare queste informazioni, aprire il [la finestra di dialogo Opzioni, progetti e soluzioni, compila ed Esegui](https://docs.microsoft.com/visualstudio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run), quindi impostare il **livello di dettaglio di output di compilazione progetto MSBuild** a **normale** o un livello di dettaglio superiore. Per altre informazioni, vedere [Procedura: Visualizzare, salvare e configurare file di log di compilazione](http://msdn.microsoft.com/library/75d38b76-26d6-4f43-bbe7-cbacd7cc81e7).  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Compilazione condizionale](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
