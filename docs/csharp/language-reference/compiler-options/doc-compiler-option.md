---
title: -doc (opzioni del compilatore C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- FileProperties.BuildAction
- /doc
dev_langs:
- CSharp
helpviewer_keywords:
- comments, C# code
- XML documentation [C#], comments in source files
- doc compiler option [C#]
- Visual C#, XML documentation for
- -doc compiler option [C#]
- /doc compiler option [C#]
ms.assetid: 849eea59-c936-4311-bad8-d07404480f2a
caps.latest.revision: 19
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8addbbfe1e854feee560192292b713da4fc67e6c
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="doc-c-compiler-options"></a>/doc (opzioni del compilatore C#)
L'opzione **/doc** consente di inserire commenti per la documentazione in un file XML.  
  
## <a name="syntax"></a>Sintassi  
  
```console  
/doc:file  
```  
  
## <a name="arguments"></a>Argomenti  
 `file`  
 File di output in XML, con i commenti presenti nei file del codice sorgente della compilazione.  
  
## <a name="remarks"></a>Note  
 Nei file del codice sorgente è possibile elaborare e aggiungere al file XML i commenti di documentazione che precedono quanto segue:  
  
-   Tipi definiti dall'utente, ad esempio una [classe](../../../csharp/language-reference/keywords/class.md), un [delegato](../../../csharp/language-reference/keywords/delegate.md) o un'[interfaccia](../../../csharp/language-reference/keywords/interface.md)  
  
-   Membri quali un campo, un [evento](../../../csharp/language-reference/keywords/event.md), una [proprietà](../../../csharp/programming-guide/classes-and-structs/using-properties.md) o un metodo  
  
 Il primo output inserito nel file XML è quello del file di codice sorgente che contiene Main.  
  
 Per usare il file XML generato con la funzionalità [IntelliSense](https://docs.microsoft.com/visualstudio/ide/using-intellisense), assegnare al file XML lo stesso nome dell'assembly che si vuole supportare, quindi accertarsi che il file XML si trovi nella stessa directory dell'assembly. In questo modo, quando si farà riferimento all'assembly nel progetto Visual Studio, verrà trovato anche il file XML. Per altre informazioni, vedere [Inserimento di commenti al codice XML](https://docs.microsoft.com/visualstudio/ide/supplying-xml-code-comments).  
  
 Se non si esegue la compilazione con [/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md), in `file` saranno inclusi i tag \<assembly>\</assembly> che specificano il nome del file contenente il manifesto assembly per il file di output della compilazione.  
  
> [!NOTE]
>  L'opzione /doc può essere usata per tutti i file di input o, se definita in Impostazioni progetto, per tutti i file di un progetto. Per disabilitare la visualizzazione degli avvisi relativi ai commenti di documentazione per una sezione di codice o un file specifico, usare [#pragma warning](../../../csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning.md).  
  
 Per informazioni sulla generazione di documentazione da commenti presenti nel codice, vedere [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla scheda **Generazione**.  
  
3.  Modificare la proprietà **File di documentazione XML**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DocumentationFile%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 [C# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)  (Opzioni del compilatore C#)  
 [NIB Procedura: Modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
