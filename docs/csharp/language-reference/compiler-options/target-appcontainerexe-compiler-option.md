---
title: -target:appcontainerexe (opzioni del compilatore C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: e7e62229-23ea-4e53-bef5-380d951bf95f
caps.latest.revision: 13
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
ms.openlocfilehash: 168771506692308bc9b031df5c059e58e8d190b1
ms.lasthandoff: 03/13/2017

---
# <a name="targetappcontainerexe-c-compiler-options"></a>/target:appcontainerexe (opzioni del compilatore C#)
Se si usa l'opzione del compilatore **/target:appcontainerexe**, il compilatore crea un file eseguibile di Windows (exe) che deve essere eseguito in un contenitore di app. Questa opzione equivale a [/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md), ma è progettata per le app [!INCLUDE[win8_appname_long](../../../csharp/includes/win8_appname_long_md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
/target:appcontainerexe  
```  
  
## <a name="remarks"></a>Note  
 Per richiedere che l'app venga eseguita in un contenitore di app, questa opzione imposta un bit nel file [eseguibile di tipo PE](http://go.microsoft.com/fwlink/p/?LinkId=236960). Quando questo bit è impostato, viene generato un errore se il metodo CreateProcess tenta di avviare il file eseguibile all'esterno di un contenitore di app.  
  
 A meno che non si usi l'opzione [/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md), il nome del file di output corrisponderà al nome del file di input contenente il metodo [Main](../../../csharp/programming-guide/main-and-command-args/index.md).  
  
 Quando si specifica questa opzione da un prompt dei comandi, tutti i file fino alla successiva opzione **/out** o **/target** vengono usati per creare il file eseguibile.  
  
### <a name="to-set-this-compiler-option-in-the-ide"></a>Per impostare l'opzione del compilatore nell'IDE  
  
1.  In **Esplora soluzioni** aprire il menu di scelta rapida per il progetto e scegliere **Proprietà**.  
  
2.  Nell'elenco **Tipo di output** della scheda **Applicazione** scegliere **Applicazione Windows Store**.  
  
     Questa opzione è disponibile solo per i modelli di app [!INCLUDE[win8_appname_long](../../../csharp/includes/win8_appname_long_md.md)].  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## <a name="example"></a>Esempio  
 Il seguente comando consente di compilare `filename.cs` in un file eseguibile di Windows che può essere eseguito solo in un contenitore di app.  
  
```  
csc /target:appcontainerexe filename.cs  
```  
  
## <a name="see-also"></a>Vedere anche  
 [/target (opzioni del compilatore C#)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [/target:winexe (opzioni del compilatore C#)](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md)   
 [Opzioni del compilatore C#](../../../csharp/language-reference/compiler-options/index.md)
