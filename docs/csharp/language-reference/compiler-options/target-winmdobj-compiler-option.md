---
title: -target:winmdobj (opzioni del compilatore C# ) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 1819a045-659d-498a-9457-c466e902986f
caps.latest.revision: 15
author: BillWagner
ms.author: wiwagn
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 7581ec18db0d2741452b47ad6200482b63c102be
ms.lasthandoff: 03/13/2017

---
# <a name="targetwinmdobj-c-compiler-options"></a>/target:winmdobj (opzioni del compilatore C#)
Se si usa l'opzione del compilatore **/target:winmdobj**, viene creato un file intermedio con estensione winmdobj che è possibile convertire in un file binario di Windows Runtime (winmd). Il file con estensione winmd può quindi essere utilizzato dai programmi C++ e JavaScript, oltre ai programmi di linguaggi gestiti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/target:winmdobj  
```  
  
## <a name="remarks"></a>Note  
 L'impostazione **winmdobj** segnala al compilatore che è richiesto un modulo intermedio. In risposta, Visual Studio consente di compilare la libreria di classi C# come file con estensione winmdobj. Il file con estensione winmdobj può quindi essere inserito dallo strumento di esportazione <xref:Microsoft.Build.Tasks.WinMDExp> per produrre un file di metadati Windows (winmd). Il file con estensione winmd contiene il codice della libreria originale e i metadati di WinMD utilizzati da JavaScript o C++ e da Windows Runtime.  
  
 L'output di un file compilato usando l'opzione del compilatore **/target:winmdobj** è progettato per essere usato solo come input dell'utilità di esportazione WimMDExp. Al file con estensione winmdobj non viene fatto riferimento direttamente.  
  
 A meno che non si usi l'opzione [/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md), il nome del file di output corrisponderà al nome del primo file di input. Non è richiesto un metodo [principale](../../../csharp/programming-guide/main-and-command-args/index.md).  
  
 Se si specifica l'opzione /target:winmdobj da un prompt dei comandi, tutti i file fino alla successiva opzione **/out** o [/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md) vengono usati per creare il programma per Windows.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-ide-for-a-windows-store-app"></a>Per impostare l'opzione del compilatore nell'IDE di Visual Studio per un'applicazione Windows Store  
  
1.  In **Esplora soluzioni** aprire il menu di scelta rapida per il progetto e scegliere **Proprietà**.  
  
2.  Scegliere la scheda **Applicazione**.  
  
3.  Nell'elenco **Tipo di output** scegliere **File WinMD**.  
  
     L'opzione **File WinMD** è disponibile solo per i modelli di applicazione [!INCLUDE[win8_appname_long](../../../csharp/includes/win8_appname_long_md.md)].  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## <a name="example"></a>Esempio  
 Il seguente comando consente di compilare `filename.cs` in un file intermedio con estensione winmdobj.  
  
```  
csc /target:winmdobj filename.cs  
```  
  
## <a name="see-also"></a>Vedere anche  
 [-target (opzioni del compilatore C#)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [Opzioni del compilatore C#](../../../csharp/language-reference/compiler-options/index.md)
