---
title: -lib (opzioni del compilatore C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /lib
dev_langs:
- CSharp
helpviewer_keywords:
- lib compiler option [C#]
- -lib compiler option [C#]
- /lib compiler option [C#]
ms.assetid: b0efcc88-e8aa-4df4-a00b-8bdef70b7673
caps.latest.revision: 16
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
ms.openlocfilehash: 27bcca456a7a5c884c33de6429e06c94afc9536a
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="lib-c-compiler-options"></a>/lib (opzioni del compilatore C#)
L'opzione **/lib** specifica la posizione degli assembly a cui si fa riferimento tramite l'opzione [/reference (opzioni del compilatore C#)](../../../csharp/language-reference/compiler-options/reference-compiler-option.md).  
  
## <a name="syntax"></a>Sintassi  
  
```console  
/lib:dir1[,dir2]  
```  
  
## <a name="arguments"></a>Argomenti  
 `dir1`  
 Directory in cui il compilatore può effettuare la ricerca se un assembly cui viene fatto riferimento non si trova nella cartella di lavoro corrente (quella da cui si chiama il compilatore) o nella directory di sistema di Common Language Runtime.  
  
 `dir2`  
 Una o più directory aggiuntive in cui effettuare la ricerca dei riferimenti agli assembly. Separare i nomi delle directory aggiuntive con una virgola, senza inserire spazi.  
  
## <a name="remarks"></a>Note  
 La ricerca dei riferimenti non completi agli assembly viene operata nell'ordine seguente:  
  
1.  Directory di lavoro corrente, ovvero la directory da cui viene chiamato il compilatore.  
  
2.  Directory di sistema di Common Language Runtime.  
  
3.  Directory specificate da **/lib**.  
  
4.  Directory specificate dalla variabile di ambiente LIB.  
  
 Per specificare un riferimento a un assembly, usare **/reference**.  
  
 L'opzione**/lib** è di tipo additivo: se viene specificata più volte, ogni nuovo valore verrà aggiunto a eventuali valori precedenti.  
  
 In alternativa a **/lib**, è possibile copiare nella directory di lavoro tutti gli assembly necessari. Sarà quindi sufficiente passare a **/reference** il nome dell'assembly. In seguito sarà possibile eliminare gli assembly dalla directory di lavoro. Dal momento che il percorso dell'assembly dipendente non è specificato nel manifesto dell'assembly, sarà possibile avviare l'applicazione sul computer di destinazione perché trovi e usi l'assembly nella Global Assembly Cache.  
  
 Il fatto che nel compilatore sia possibile fare riferimento all'assembly non implica che Common Language Runtime sarà in grado di trovare e caricare l'assembly in fase di runtime. Per informazioni dettagliate sulla modalità di ricerca degli assembly a cui viene fatto riferimento in fase di esecuzione, vedere [Come il runtime individua gli assembly](../../../framework/deployment/how-the-runtime-locates-assemblies.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la finestra di dialogo **Pagine delle proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Percorso riferimenti**.  
  
3.  Modificare il contenuto della casella di riepilogo.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.ReferencePath%2A>.  
  
## <a name="example"></a>Esempio  
 Compilare t2.cs per creare un file con estensione exe. Verranno cercati i riferimenti agli assembly nella directory di lavoro e nella directory radice dell'unità C.  
  
```console  
csc /lib:c:\ /reference:t2.dll t2.cs  
```  
  
## <a name="see-also"></a>Vedere anche  
 [C# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)  (Opzioni del compilatore C#)  
 [NIB Procedura: Modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
