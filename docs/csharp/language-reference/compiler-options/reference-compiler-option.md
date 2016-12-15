---
title: "/reference (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/reference"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/r compiler option [C#]"
  - "reference compiler option [C#]"
  - "r compiler option [C#]"
  - "/reference compiler option [C#]"
  - "-r compiler option [C#]"
  - "metadata import [C#]"
  - "public type information [C#]"
  - "-reference compiler option [C#]"
ms.assetid: 8d13e5b0-abf6-4c46-bf71-2daf2cd0a6c4
caps.latest.revision: 28
caps.handback.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /reference (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Con l'opzione **\/reference**, il compilatore importa nel progetto corrente le informazioni sui tipi [public](../../../csharp/language-reference/keywords/public.md) disponibili nel file specificato e consente quindi di fare riferimento ai metadati dai file di assembly specificati.  
  
## Sintassi  
  
```  
/reference:[alias=]filename  
/reference:filename  
```  
  
## Argomenti  
 `filename`  
 Il nome di un file contenente un manifesto dell'assembly.  Per importare più file, specificare un'opzione **\/reference** per ciascun file.  
  
 `alias`  
 Un identificatore C\# valido che rappresenta uno spazio dei nomi di primo livello contenente tutti gli spazi dei nomi dell'assembly.  
  
## Note  
 Per importare da più file, specificare un'opzione **\/reference** per ciascun file.  
  
 È necessario che i file importati contengano un manifesto e che il file di output sia stato compilato specificando un'opzione [\/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) diversa da [\/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md).  
  
 **\/r** rappresenta la versione abbreviata di **\/reference**.  
  
 Utilizzare [\/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md) per importare metadati da un file di output che non contiene un manifesto assembly.  
  
 Se si fa riferimento a un assembly \(assembly A\) che fa a sua volta riferimento a un secondo assembly \(assembly B\), sarà necessario fare riferimento all'assembly B nei seguenti casi:  
  
-   Se un tipo dell'assembly A eredita da un tipo o implementa un'interfaccia dell'assembly B.  
  
-   Se si richiama un campo, una proprietà, un evento o un metodo che presenta un tipo restituito o un tipo di parametro proveniente dall'assembly B.  
  
 Per specificare la directory in cui si trova uno o più assembly cui si fa riferimento, utilizzare [\/lib](../../../csharp/language-reference/compiler-options/lib-compiler-option.md).  Nella descrizione di **\/lib** verranno indicate anche le directory in cui il compilatore ricerca gli assembly.  
  
 Perché il compilatore sia in grado di riconoscere un tipo in un assembly e non in un modulo, è necessario imporre la risoluzione del tipo stesso. A questo scopo, è possibile definire un'istanza del tipo.  La risoluzione dei nomi dei tipi in un assembly può avvenire anche con altre modalità. Se, ad esempio, si eredita da un tipo in un assembly, il nome del tipo sarà riconosciuto dal compilatore.  
  
 In alcuni casi è necessario fare riferimento a due versioni diverse dello stesso componente da un unico assembly.  A questo scopo, utilizzare l'opzione di secondo livello alias dell'opzione **\/reference** per ciascun file, in modo che sia possibile distinguere tra le due versioni.  Questo alias verrà utilizzato come qualificatore per il nome del componente, quindi risolto nel componente stesso in uno dei file.  
  
 Per impostazione predefinita, viene utilizzato il file di risposta csc \(.rsp\), che fa riferimento agli assembly .NET Framework di uso comune.  Utilizzare l'opzione del compilatore [\/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md) se non si desidera che il compilatore utilizzi il file csc.rsp.  
  
> [!NOTE]
>  In Visual Studio, usare la finestra di dialogo **Aggiungi riferimento**.  Per ulteriori informazioni, vedere [Procedura: aggiungere o rimuovere riferimenti utilizzando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/it-it/3bd75d61-f00c-47c0-86a2-dd1f20e231c9).  In Visual Studio 2010 e nelle versioni successive, verificare il comportamento equivalente tra l'aggiunta di riferimenti utilizzando `/reference` e utilizzando la finestra di dialogo **Aggiungi riferimento**, la proprietà **Incorpora tipi di interoperabilità** deve essere impostata su **False** per l'assembly che si stia aggiungendo.  **True** è il valore predefinito per quella proprietà.  
  
## Esempio  
 Nel seguente esempio viene illustrato come utilizzare la funzionalità [extern alias](../../../csharp/language-reference/keywords/extern-alias.md).  
  
 Il file di origine viene compilato e i metadati vengono importati dai file `grid.dll` e `grid20.dll`, ``  compilati in precedenza.  Nelle due DLL sono presenti versioni distinte dello stesso componente. Utilizzare due opzioni **\/reference** con opzioni di secondo livello alias per compilare il file di origine.  Le opzioni sono analoghe alle seguenti:  
  
 \/reference:GridV1\=grid.dll and \/reference:GridV2\=grid20.dll  
  
 In questo modo verranno impostati gli alias esterni "GridV1" e "GridV2", da utilizzare nel programma tramite un'istruzione extern:  
  
```  
extern alias GridV1;  
extern alias GridV2;  
// Using statements go here.  
```  
  
 Una volta completate queste operazioni, è possibile fare riferimento al controllo griglia dal file grid.dll aggiungendo il prefisso GridV1 al nome del controllo, come riportato di seguito:  
  
```  
GridV1::Grid  
```  
  
 È inoltre possibile fare riferimento al controllo griglia dal file grid20.dll aggiungendo il prefisso GridV2 al nome del controllo, come riportato di seguito:  
  
```  
GridV2::Grid   
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)