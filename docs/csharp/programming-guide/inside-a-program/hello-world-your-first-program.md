---
title: Hello World -- Il primo programma (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: get-started-article
f1_keywords:
- cs.program
- vs.csharp.startpage.firstapplication
dev_langs:
- CSharp
helpviewer_keywords:
- examples [C#], Hello World
- Hello World example [C#]
ms.assetid: 6493182a-b0b6-4539-a719-518a168cb730
caps.latest.revision: 39
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
ms.openlocfilehash: 21abcf70cce2d6c9052629ce60d08e9ec6ac16e7
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="hello-world----your-first-program-c-programming-guide"></a>Hello World -- Il primo programma (Guida per programmatori C#)
La procedura seguente crea una versione C# del programma "Hello World!" tradizionale. Il programma visualizza la stringa `Hello World!`  
  
 Per altri esempi di concetti introduttivi, vedere [Introduzione a Visual C# e Visual Basic](https://docs.microsoft.com/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic).  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-and-run-a-console-application"></a>Per creare ed eseguire un'applicazione console  
  
1.  Avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Nuovo**, **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Espandere **Installati**, **Modelli** e **Visual C#** e scegliere **Applicazione console**.  
  
4.  Nella casella **Nome** specificare un nome per il progetto e quindi scegliere il pulsante **OK**.  
  
     Il nuovo progetto verrà visualizzato in **Esplora soluzioni**.  
  
5.  Se Program.cs non è aperto nell'**Editor di codice**, aprire il menu di scelta rapida per **Program.cs** in **Esplora soluzioni** e selezionare **Visualizza codice**.  
  
6.  Sostituire il contenuto di Program.cs con il codice seguente.  
  
     [!code-cs[csProgGuide#21](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_1.cs)]  
  
7.  Premere F5 per eseguire il progetto. Viene visualizzata una finestra del prompt dei comandi che contiene la riga `Hello World!`  
  
 Successivamente, vengono esaminate le parti importanti del programma.  
  
## <a name="comments"></a>Commenti  
 La prima riga contiene un commento. I caratteri `//` convertono il resto della riga in un commento.  
  
 [!code-cs[csProgGuide#32](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_2.cs)]  
  
 È anche possibile commentare un blocco di testo racchiudendolo tra i caratteri `/*` e `*/`, come illustrato nell'esempio riportato di seguito.  
  
 [!code-cs[csProgGuide#33](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_3.cs)]  
  
## <a name="main-method"></a>Metodo Main  
 È necessario che un'applicazione console C# contenga un metodo `Main`, in cui il controllo inizia e finisce. Il metodo `Main` consente di creare oggetti e di eseguire altri metodi.  
  
 Il metodo `Main` è un metodo di tipo [static](../../../csharp/language-reference/keywords/static.md) che si trova all'interno di una classe o di uno struct. Nell'esempio "Hello World!" precedente si trovava in una classe denominata `Hello`. È possibile dichiarare il metodo `Main` in uno dei modi seguenti:  
  
-   Può restituire un valore `void`.  
  
     [!code-cs[csProgGuideMain#12](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_4.cs)]  
  
-   Può restituire anche un valore intero.  
  
     [!code-cs[csProgGuideMain#13](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_5.cs)]  
  
-   Con entrambi i tipi restituiti, può accettare argomenti.  
  
     [!code-cs[csProgGuideMain#19](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_6.cs)]  
  
     -oppure-  
  
     [!code-cs[csProgGuideMain#18](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_7.cs)]  
  
 Il parametro del metodo `Main`, `args`, è una matrice `string` che contiene gli argomenti della riga di comando usati per richiamare il programma. A differenza di C++, la matrice non include il nome del file eseguibile con estensione exe.  
  
 Per altre informazioni sull'uso degli argomenti della riga di comando, vedere gli esempi in [Main() e argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/index.md) e [Procedura: Creare e usare assembly dalla riga di comando](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4).  
  
 La chiamata a <xref:System.Console.ReadKey%2A> alla fine del metodo `Main` evita che la finestra della console si chiuda prima che sia possibile leggere l'output quando si esegue il programma in modalità di debug, premendo F5.  
  
## <a name="input-and-output"></a>Input e output  
 In genere i programmi C# usano i servizi di input/output offerti dalla libreria run-time di .NET Framework. L'istruzione `System.Console.WriteLine("Hello World!");` usa il metodo <xref:System.Console.WriteLine%2A>. Questo è uno dei metodi di output della classe <xref:System.Console> nella libreria di runtime. Visualizza il parametro di tipo stringa sul flusso di output standard seguito da una nuova riga. Sono disponibili altri metodi <xref:System.Console> per diverse operazioni di input e output. Se si include la direttiva `using System;` all'inizio del programma, è possibile usare direttamente le classi e i metodi <xref:System> senza specificarne il nome completo. Ad esempio, è possibile chiamare `Console.WriteLine` anziché `System.Console.WriteLine`:  
  
 [!code-cs[csProgGuide#1](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_8.cs)]  
  
 [!code-cs[csProgGuide#23](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/hello-world-your-first-program_9.cs)]  
  
 Per altre informazioni sui metodi di input/output, vedere <xref:System.IO>.  
  
## <a name="command-line-compilation-and-execution"></a>Esecuzione e compilazione da riga di comando  
 È possibile compilare il programma "Hello World!" usando la riga di comando invece dell'ambiente di sviluppo integrato (IDE, Integrated Development Environment) di Visual Studio.  
  
#### <a name="to-compile-and-run-from-a-command-prompt"></a>Per compilare ed eseguire codice a un prompt dei comandi  
  
1.  Incollare il codice della procedura precedente in un editor di testo e salvare il file come file di testo. Denominare il file `Hello.cs`. I file del codice sorgente di C# usano l'estensione `.cs`.  
  
2.  Eseguire una delle procedure seguenti per aprire una finestra al prompt dei comandi:  
  
    -   In Windows 8 nella schermata **Start** cercare `Developer Command Prompt` e toccare o selezionare **Prompt dei comandi per gli sviluppatori per VS2012**.  
  
         Viene visualizzata una finestra del prompt dei comandi per gli sviluppatori.  
  
    -   In Windows 7 aprire il menu **Start**, espandere la cartella della versione corrente di Visual Studio, aprire il menu di scelta rapida per **Strumenti di Visual Studio** e selezionare **Prompt dei comandi per gli sviluppatori per VS2012**.  
  
         Viene visualizzata una finestra del prompt dei comandi per gli sviluppatori.  
  
    -   Abilitare le compilazioni da riga di comando da una finestra del prompt dei comandi standard.  
  
         Vedere [How to: Set Environment Variables for the Visual Studio Command Line](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md) (Procedura: Impostare le variabili di ambiente per la riga di comando di Visual Studio).  
  
3.  Nella finestra del prompt dei comandi passare alla cartella che contiene il file `Hello.cs`.  
  
4.  Immettere il comando seguente per compilare `Hello.cs`.  
  
     `csc Hello.cs`  
  
     Se il programma non presenta errori di compilazione, viene creato un file eseguibile denominato `Hello.exe`.  
  
5.  Nella finestra del prompt dei comandi immettere il comando seguente per eseguire il programma:  
  
     `Hello`  
  
 Per altre informazioni sul compilatore C# e le relative opzioni, vedere [C# Compiler Options](../../../csharp/language-reference/compiler-options/index.md) (Opzioni del compilatore C#).
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Contenuto di un programma C#](../../../csharp/programming-guide/inside-a-program/index.md)   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)   
 [\<Applicazioni di esempio di C#](http://msdn.microsoft.com/en-us/9a9d7aaa-51d3-4224-b564-95409b0f3e15)   
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Main() e argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/index.md)   
 [Getting Started with Visual C# and Visual Basic](https://docs.microsoft.com/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic) (Introduzione a Visual C# e Visual Basic)
