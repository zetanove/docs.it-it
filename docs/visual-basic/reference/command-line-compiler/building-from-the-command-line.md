---
title: Compilazione dalla riga di comando (Visual Basic) | Documenti di Microsoft
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
- builds [Visual Basic], command-line
- Visual Basic compiler, about Visual Basic compiler
- command line [Visual Basic], compilers
- command line [Visual Basic], building from
- command line [Visual Basic], builds
- compilers, invoking from command line
- command-line builds
- compiling source code
- command-line compilers, Visual Basic
- command line [Visual Basic], Visual Basic
ms.assetid: e61947e9-a42e-4717-a699-5f70a98cdd03
caps.latest.revision: 13
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
ms.openlocfilehash: 49f84c221e18457ab46534ca46da7c4764a8ee40
ms.lasthandoff: 03/13/2017

---
# <a name="building-from-the-command-line-visual-basic"></a>Compilazione dalla riga di comando (Visual Basic)
Oggetto [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] progetto è costituito da uno o più file di origine separato. Durante il processo noto come compilazione, questi file vengono riuniti in un pacchetto, ovvero un singolo file eseguibile che può essere eseguito come un'applicazione.  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce un compilatore della riga di comando come alternativa alla compilazione dei programmi dall'interno di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] ambiente di sviluppo integrato (IDE). Il compilatore della riga di comando è progettato per situazioni che non richiedono il set completo di funzionalità nell'IDE, ad esempio, quando si utilizza o scrive codice per computer con spazio di archiviazione o memoria limitate sul sistema.  
  
 Durante la compilazione dalla riga di comando, è necessario fare esplicitamente riferimento Microsoft [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] libreria di runtime tramite il `/reference` l'opzione del compilatore.  
  
 Per compilare file di origine dall'interno di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] IDE, scegliere il **compilare** comando il **compilare** menu.  
  
> [!TIP]
>  Quando si compila i file di progetto utilizzando l'IDE di Visual Studio, è possibile visualizzare informazioni su associata **vbc** comando e le opzioni nella finestra di output. Per visualizzare queste informazioni, aprire il [la finestra di dialogo Opzioni, progetti e soluzioni, compila ed Esegui](https://docs.microsoft.com/visualstudio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run), quindi impostare il **livello di dettaglio di output di compilazione progetto MSBuild** a **normale** o un livello di dettaglio superiore. Per altre informazioni, vedere [Procedura: Visualizzare, salvare e configurare file di log di compilazione](http://msdn.microsoft.com/library/75d38b76-26d6-4f43-bbe7-cbacd7cc81e7).  
  
 È possibile compilare file di progetto (vbproj) in un prompt dei comandi utilizzando MSBuild. Per ulteriori informazioni, vedere [da riga di comando](https://docs.microsoft.com/visualstudio/msbuild/msbuild-command-line-reference) e [procedura dettagliata: utilizzo di MSBuild](http://msdn.microsoft.com/library/b8a8b866-bb07-4abf-b9ec-0b40d281c310).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Procedura:Richiamare il compilatore da riga di comando](../../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md)  
 Viene descritto come richiamare il compilatore della riga di comando al prompt di MS-DOS o da una sottodirectory specifica.  
  
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 Fornisce un elenco delle righe di comando di esempio che è possibile modificare per uso personale.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)  
 Fornisce elenchi di opzioni del compilatore, organizzati in ordine alfabetico o in base allo scopo.  
  
 [Compilazione condizionale](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)  
 Viene descritto come compilare particolari sezioni di codice.  
  
 [Compilazione e pulizia di progetti e soluzioni in Visual Studio](https://docs.microsoft.com/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio)  
 Viene descritto come organizzare gli elementi verranno inclusi nelle diverse compilazioni, scegliere le proprietà del progetto e assicurarsi che i progetti vengano compilati nell'ordine corretto.
