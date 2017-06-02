---
title: Compilazione dalla riga di comando con csc.exe | Microsoft Docs
ms.date: 2017-04-19
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- builds [C#]
- command line [C#]
ms.assetid: 66e70056-dd20-453c-a9b3-507e0478b015
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
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: d90dc35fd985cbe35cfe86f7c299bd12aed11365
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="command-line-build-with-cscexe"></a>Compilazione dalla riga di comando con csc.exe
È possibile richiamare il compilatore C# digitando il nome del relativo file eseguibile (*csc.exe*) da un prompt dei comandi.

Se si usa la finestra **Prompt dei comandi per gli sviluppatori per Visual Studio**, tutte le variabili di ambiente necessarie sono impostate automaticamente. Per informazioni su come accedere a questo strumento, vedere [Developer Command Prompt for Visual Studio](../../../framework/tools/developer-command-prompt-for-vs.md) (Prompt dei comandi per gli sviluppatori per Visual Studio). 

Se si usa una finestra del prompt dei comandi standard, è necessario modificare il percorso prima di poter richiamare *csc.exe* da qualsiasi sottodirectory del computer. Si deve anche eseguire *vsvars32.bat* per impostare le variabili di ambiente necessarie per supportare le compilazioni da riga di comando. Per altre informazioni su *vsvars32.bat*, incluse istruzioni per trovare ed eseguire il file, vedere [How to: Set Environment Variables for the Visual Studio Command Line](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md) (Procedura: Impostare le variabili di ambiente per la riga di comando di Visual Studio).

Se nel computer in uso è disponibile solo [!INCLUDE[winsdklong](../../../csharp/language-reference/compiler-options/includes/winsdklong_md.md)], è possibile usare il compilatore C# al **Prompt dei comandi di SDK** che viene visualizzato dall'opzione di menu **Microsoft .NET Framework SDK**.

È inoltre possibile utilizzare MSBuild per compilare programmi C# a livello di codice. Per altre informazioni, vedere [MSBuild](/visualstudio/msbuild/msbuild).

Il file eseguibile *csc.exe* si trova in genere nella cartella Microsoft.NET\Framework\\*\<versione* della directory *Windows*. La posizione del file può variare in base all'esatta configurazione di un determinato computer. Se nel computer sono installate più versioni di .NET Framework, saranno disponibili più versioni di questo file. Per altre informazioni su queste installazioni, vedere [How to: determine which versions of the .NET Framework are installed](../../../framework/migration-guide/how-to-determine-which-versions-are-installed.md) (Procedura: Determinare le versioni di .NET Framework installate).

> [!TIP]
>  Quando si compila un progetto usando l'IDE di Visual Studio, è possibile visualizzare il comando **csc** e le relative opzioni del compilatore associate nella finestra **Output**. Per visualizzare queste informazioni, seguire le istruzioni in [Procedura: Visualizzare, salvare e configurare file di log di compilazione](/visualstudio/ide/how-to-view-save-and-configure-build-log-files#to-change-the-amount-of-information-included-in-the-build-log) per impostare il livello di dettaglio dei dati di log su **Normale** o **Dettagliato**. Al termine della ricompilazione del progetto, nella finestra **Output** cercare **csc** per trovare la chiamata del compilatore C#.

 **Contenuto dell'argomento**

- [Regole per la sintassi della riga di comando](#-rules-for-command-line-syntax-for-the-c-compiler)

- [Righe di comando di esempio](#sample-command-lines-for-the-c-compiler)

- [Differenze tra l'output del compilatore C# e l'output del compilatore C++](#differences-between-c-compiler-and-c-compiler-output)

## <a name="rules-for-command-line-syntax-for-the-c-compiler"></a>Regole per la sintassi della riga di comando per il compilatore C#

Il compilatore C# usa le regole seguenti per interpretare gli argomenti visualizzati nella riga di comando del sistema operativo:

- Gli argomenti sono delimitati da spazi vuoti, ovvero da uno spazio o da una tabulazione.

- L'accento circonflesso (^) non viene riconosciuto come carattere di escape o delimitatore. Il carattere viene gestito dal parser della riga di comando nel sistema operativo prima di essere passato alla matrice `argv` del programma.

- Una stringa racchiusa tra virgolette doppie ("string") viene interpretata come argomento singolo, indipendentemente dalla presenza di spazi al suo interno. Una stringa tra virgolette può essere incorporata in un argomento.

- Le virgolette doppie precedute da una barra rovesciata (\\") vengono interpretate come carattere letterale virgolette doppie (").

- Le barre rovesciate vengono interpretate letteralmente, a meno che non precedano virgolette doppie.

- Se un numero pari di barre rovesciate è seguito da virgolette doppie, viene inserita solo una barra rovesciata nella matrice `argv` per ogni coppia di barre rovesciate e le virgolette doppie vengono interpretate come delimitatore di stringa.

- Se un numero dispari di barre rovesciate è seguito da virgolette doppie, viene inserita solo una barra rovesciata nella matrice `argv` per ogni coppia di barre rovesciate e le virgolette doppie vengono "ignorate" dalla barra rovesciata rimanente. Questo determina l'aggiunta di un valore letterale virgolette doppie (") in `argv`.

## <a name="sample-command-lines-for-the-c-compiler"></a>Righe di comando di esempio per il compilatore C#

- Compila *File.cs* e crea *File.exe*:

```
csc File.cs 
```

- Compila *File.cs* e crea *File.dll*:

```
csc /target:library File.cs
```

- Compila *File.cs* e crea *My.exe*:

```
csc /out:My.exe File.cs
```

- Compila tutti i file C# della directory corrente con le ottimizzazioni attivate e definisce il simbolo DEBUG. L'output è il *File2.exe*:

```
csc /define:DEBUG /optimize /out:File2.exe *.cs
```

- Compila tutti i file C# della directory corrente generando una versione di debug del file *File2.dll*. Non viene visualizzato nessun logo e nessun avviso:

```
csc /target:library /out:File2.dll /warn:0 /nologo /debug *.cs
```

- Compila tutti i file C# della directory corrente creando un file *Something.xyz* (una DLL):

```
csc /target:library /out:Something.xyz *.cs
```

## <a name="differences-between-c-compiler-and-c-compiler-output"></a>Differenze tra output del compilatore C# e output del compilatore C++
Dopo il richiamo del compilatore C# non viene creato alcun file oggetto (*.obj*). I file di output vengono creati direttamente. Di conseguenza il compilatore C# non richiede un linker.

## <a name="see-also"></a>Vedere anche
 [C# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)  (Opzioni del compilatore C#)  
 [Opzioni del compilatore C# in ordine alfabetico](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)   
 [Opzioni del compilatore C# elencate per categoria](../../../csharp/language-reference/compiler-options/listed-by-category.md)   
 [Main() e argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/index.md)   
 [Argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/command-line-arguments.md)   
 [Procedura: Visualizzare gli argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [Procedura: Accedere agli argomenti della riga di comando usando foreach](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)   
 [Valori restituiti da Main()](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)

