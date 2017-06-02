---
title: -addmodule (Opzioni del compilatore C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /addmodule
dev_langs:
- CSharp
helpviewer_keywords:
- /addmodule compiler option [C#]
- -addmodule compiler option [C#]
- addmodule compiler option [C#]
ms.assetid: ed604546-0dc2-4bd4-9a3e-610a8d973e58
caps.latest.revision: 13
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
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 614dbefbb472ef2cd03fcb1ba7a44f08c450bf4a
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="addmodule-c-compiler-options"></a>/addmodule (opzioni del compilatore C#)
Questa opzione aggiunge un modulo creato con l'opzione target:module nella compilazione in corso.  
  
## <a name="syntax"></a>Sintassi  
  
```console  
/addmodule:file[;file2]  
```  
  
## <a name="arguments"></a>Argomenti  
 `file`, `file2`  
 Un file di output che contiene i metadati. Il file non può contenere un manifesto dell'assembly. Per importare più di un file, separare i nomi dei file con una virgola o con un punto e virgola.  
  
## <a name="remarks"></a>Note  
 Tutti i moduli aggiunti con **/addmodule** devono essere nella stessa directory del file di output in fase di esecuzione. Ovvero, è possibile specificare un modulo in una directory in fase di compilazione, ma il modulo deve essere nella directory dell'applicazione in fase di esecuzione. Se il modulo non è nella directory dell'applicazione in fase di esecuzione, verrà restituita un'eccezione <xref:System.TypeLoadException>.  
  
 `file` non può contenere un assembly. Ad esempio, se il file di output è stato creato con [/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md), i relativi metadati possono essere importati con **/addmodule**.  
  
 Se il file di output è stato creato con un'opzione **/target** e non con un'opzione **/target:module**, i relativi metadati non possono essere importati con l'opzione **/addmodule**, ma con l'opzione [/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md).  
  
 L'opzione del compilatore non è disponibile in Visual Studio. Un progetto non può fare riferimento a un modulo. Inoltre, l'opzione del compilatore non può essere modificata a livello di codice.  
  
## <a name="example"></a>Esempio  
 Compilare un file di origine `input.cs` e aggiungere i metadati da `metad1.netmodule` e `metad2.netmodule` per creare `out.exe`:  
  
```console  
csc /addmodule:metad1.netmodule;metad2.netmodule /out:out.exe input.cs  
```  
  
## <a name="see-also"></a>Vedere anche  
 [C# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)  (Opzioni del compilatore C#)  
 [NIB Procedura: Modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Multifile Assemblies](../../../framework/app-domains/multifile-assemblies.md)  (Assembly su più file)  
 [Procedura: Compilare un assembly su più file](../../../framework/app-domains/how-to-build-a-multifile-assembly.md)
