---
title: -reference (opzioni del compilatore C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /reference
dev_langs:
- CSharp
helpviewer_keywords:
- /r compiler option [C#]
- reference compiler option [C#]
- r compiler option [C#]
- /reference compiler option [C#]
- -r compiler option [C#]
- metadata import [C#]
- public type information [C#]
- -reference compiler option [C#]
ms.assetid: 8d13e5b0-abf6-4c46-bf71-2daf2cd0a6c4
caps.latest.revision: 28
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
ms.sourcegitcommit: 7e33ed084c560470a486ebbb25035a59ddc18565
ms.openlocfilehash: 11bb7fc9490879714542bfbd77a81d58e7d8e8ed
ms.contentlocale: it-it
ms.lasthandoff: 03/31/2017

---
# <a name="reference-c-compiler-options"></a>/reference (opzioni del compilatore C#)
Con l'opzione **/reference** il compilatore importa nel progetto corrente le informazioni sui tipi [public](../../../csharp/language-reference/keywords/public.md) disponibili nel file specificato e consente quindi di fare riferimento ai metadati dai file di assembly specificati.  
  
## <a name="syntax"></a>Sintassi  
  
```console  
/reference:[alias=]filename  
/reference:filename  
```  
  
## <a name="arguments"></a>Argomenti  
 `filename`  
 Nome di un file contenente il manifesto di un assembly. Per importare più file, specificare un'opzione **/Reference** per ogni file.  
  
 `alias`  
 Identificatore C# valido che rappresenta uno spazio dei nomi di primo livello contenente tutti gli spazi dei nomi dell'assembly.  
  
## <a name="remarks"></a>Note  
 Per importare da più file, includere un'opzione **/reference** per ogni file.  
  
 È necessario che i file importati contengano un manifesto e che il file di output sia stato compilato specificando un'opzione [/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) diversa da [/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md).  
  
 **/r** rappresenta la versione abbreviata di **/reference**.  
  
 Usare [/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md) per importare metadati da un file di output che non contiene un manifesto dell'assembly.  
  
 Se si fa riferimento a un assembly (assembly A) che fa a sua volta riferimento a un secondo assembly (assembly B), è necessario fare riferimento all'assembly B nei casi seguenti:  
  
-   Se un tipo dell'assembly A eredita da un tipo o implementa un'interfaccia dell'assembly B.  
  
-   Se si chiama un campo, una proprietà, un evento o un metodo che presenta un tipo restituito o un tipo di parametro proveniente dall'assembly B.  
  
 Per specificare la directory in cui si trovano uno o più assembly cui si fa riferimento, usare [/lib](../../../csharp/language-reference/compiler-options/lib-compiler-option.md). Nell'argomento dedicato a **/lib** sono indicate anche le directory in cui il compilatore ricerca gli assembly.  
  
 Perché il compilatore sia in grado di riconoscere un tipo in un assembly e non in un modulo, è necessario imporre la risoluzione del tipo stesso. A questo scopo, è possibile definire un'istanza del tipo. La risoluzione dei nomi dei tipi in un assembly può avvenire anche con altre modalità. Se, ad esempio, si eredita da un tipo in un assembly, il nome del tipo sarà riconosciuto dal compilatore.  
  
 In alcuni casi è necessario fare riferimento a due versioni diverse dello stesso componente da un unico assembly. A questo scopo, usare l'opzione di secondo livello alias dell'opzione **/Reference** per ogni file, in modo che sia possibile distinguere tra le due versioni. Questo alias verrà usato come qualificatore per il nome del componente, quindi risolto nel componente stesso in uno dei file.  
  
 Per impostazione predefinita, viene usato il file di risposta csc (.rsp), che fa riferimento agli assembly .NET Framework di uso comune. Usare [/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md) se non si vuole che il compilatore usi csc.rsp.  
  
> [!NOTE]
> In Visual Studio usare la finestra di dialogo **Aggiungi riferimento**. Per altre informazioni, vedere [Procedura: Aggiungere o rimuovere riferimenti mediante Gestione riferimenti](https://docs.microsoft.com/en-us/visualstudio/ide/how-to-add-or-remove-references-by-using-the-reference-manager). Per garantire un comportamento equivalente tra l'aggiunta di riferimenti usare `/reference` e aggiungere riferimenti tramite la finestra di dialogo **Aggiungi riferimento**, impostando la proprietà **Incorpora tipi di interoperabilità** su **False** per l'assembly che si vuole aggiungere. Per questa proprietà il valore predefinito è **True**.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come usare la funzionalità [extern alias](../../../csharp/language-reference/keywords/extern-alias.md).  
  
 Il file di origine viene compilato e i metadati vengono importati dai file `grid.dll` e `grid20.dll`, compilati in precedenza. Nelle due DLL sono presenti versioni distinte dello stesso componente. Usare due opzioni **/reference** con opzioni alias per compilare il file di origine. Le opzioni sono analoghe alle seguenti:  
  
 /reference:GridV1=grid.dll e /reference:GridV2=grid20.dll  
  
 In questo modo vengono impostati gli alias esterni "GridV1" e "GridV2", da usare nel programma tramite un'istruzione extern:  
  
```csharp  
extern alias GridV1;  
extern alias GridV2;  
// Using statements go here.  
```  
  
 Una volta completate queste operazioni, è possibile fare riferimento al controllo griglia dal file grid.dll aggiungendo il prefisso GridV1 al nome del controllo, come riportato di seguito:  
  
```csharp  
GridV1::Grid  
```  
  
 È anche possibile fare riferimento al controllo griglia dal file grid20.dll aggiungendo il prefisso GridV2 al nome del controllo, come riportato di seguito:  
  
```csharp  
GridV2::Grid   
```  
  
## <a name="see-also"></a>Vedere anche  
 [C# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)  (Opzioni del compilatore C#)  
 [NIB Procedura: Modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
