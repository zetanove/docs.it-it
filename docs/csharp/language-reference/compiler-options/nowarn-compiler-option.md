---
title: -nowarn (opzioni del compilatore C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /nowarn
dev_langs:
- CSharp
helpviewer_keywords:
- nowarn compiler option [C#]
- /nowarn compiler option [C#]
- -nowarn compiler option [C#]
ms.assetid: 6dcbc5e8-ae67-4566-9df3-f63cfdd9c4e4
caps.latest.revision: 24
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
ms.openlocfilehash: 34152b6e7247ac112bcc9c725402b8c9a5d631ed
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="nowarn-c-compiler-options"></a>/nowarn (opzioni del compilatore C#)
L'opzione **/nowarn** impedisce al compilatore di visualizzare uno o più avvisi. Separare più numeri di avviso con una virgola.  
  
## <a name="syntax"></a>Sintassi  
  
```console  
/nowarn:number1[,number2,...]  
```  
  
## <a name="arguments"></a>Argomenti  
 `number1`, `number2`  
 Il numero o i numeri degli avvisi che il compilatore non deve visualizzare.  
  
## <a name="remarks"></a>Note  
 Specificare solo la parte numerica dell'identificatore dell'avviso. Ad esempio, per eliminare l'avviso CS0028 è possibile specificare `/nowarn:28`.  
  
 Il compilatore ignorerà automaticamente i numeri di avviso passati a `/nowarn` validi nelle versioni precedenti ma rimossi dal compilatore. Ad esempio, CS0679 era valido nel compilatore in Visual Studio .NET 2002 ma è stato rimosso successivamente.  
  
 Gli avvisi seguenti non possono essere eliminati dall'opzione `/nowarn`:  
  
-   Avviso del compilatore (livello 1) CS2002  
  
-   Avviso del compilatore (livello 1) CS2023  
  
-   Avviso del compilatore (livello 1) CS2029  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto. Per informazioni dettagliate, vedere [Pagina Compilazione, Creazione progetti (C#)](https://docs.microsoft.com/visualstudio/ide/reference/build-page-project-designer-csharp).  
  
2.  Fare clic sulla pagina delle proprietà **Compilazione**.  
  
3.  Modificare la proprietà **Non visualizzare avvisi**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 [C# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)  (Opzioni del compilatore C#)  
 [NIB Procedura: Modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Errori del compilatore C#](../../../csharp/language-reference/compiler-messages/index.md)
