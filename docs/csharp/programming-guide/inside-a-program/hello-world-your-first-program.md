---
title: "Hello World -- Il primo programma (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "get-started-article"
f1_keywords: 
  - "cs.program"
  - "vs.csharp.startpage.firstapplication"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "esempi [C#], Hello World"
  - "Hello World (esempio) [C#]"
ms.assetid: 6493182a-b0b6-4539-a719-518a168cb730
caps.latest.revision: 39
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 39
---
# Hello World -- Il primo programma (Guida per programmatori C#)
La routine riportata di seguito crea una versione C\# del tradizionale programma "Hello World\!".  Il programma visualizza la stringa `Hello World!`  
  
 Per ulteriori esempi sui concetti introduttivi, vedere [Guida introduttiva a Visual C\# e Visual Basic](/visual-studio/ide/getting-started-with-visual-csharp-and-visual-basic).  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### Per creare ed eseguire un'applicazione console  
  
1.  Avviare Visual Studio.  
  
2.  Nella barra dei menu, scegliere **File**, **Nuovo**, **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto**.  
  
3.  Espandere **Installato**, **Modelli**, **Visual C\#** e **Applicazione console**.  
  
4.  Nella casella **Nome** specificare un nome per il progetto, quindi scegliere il pulsante **OK**.  
  
     Il nuovo progetto verrà visualizzato in **Esplora soluzioni**.  
  
5.  Se Program.cs non è aperto nell'**Editor codice**, aprire il menu di scelta rapida per **Program.cs** in **Esplora soluzioni**, quindi selezionare **Visualizza codice**.  
  
6.  Sostituire il contenuto di Program.jcs con il codice seguente.  
  
     [!code-cs[csProgGuide#21](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/csProgGuide/progGuide.cs#21)]  
  
7.  Premere il tasto F5 per eseguire il progetto.  Viene visualizzata una finestra dei prompt dei comandi contenente la riga `Hello World!`  
  
 Vengono quindi presi in esame gli aspetti principali di questo programma.  
  
## Commenti  
 La prima riga contiene un commento.  I caratteri `//` convertono il resto della riga in un commento.  
  
 [!code-cs[csProgGuide#32](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/csProgGuide/progGuide.cs#32)]  
  
 È anche possibile commentare un blocco di testo racchiudendolo tra i caratteri `/*` e `*/`.  Questa operazione viene mostrata nell'esempio seguente.  
  
 [!code-cs[csProgGuide#33](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/csProgGuide/progGuide.cs#33)]  
  
## Metodo Main  
 Un'applicazione console C\# deve contenere un metodo `Main`, nel quale il controllo ha inizio e fine.  Il metodo `Main` è il metodo in cui si creano oggetti e si eseguono altri metodi.  
  
 Il metodo `Main` è un metodo [statiche](../../../csharp/language-reference/keywords/static.md) all'interno di una classe o di una struct.  Nel precedente esempio di "Hello World\!" si trova all'interno della classe `Hello`.  È possibile dichiarare il metodo `Main` in uno dei modi seguenti:  
  
-   Può restituire `void`.  
  
     [!code-cs[csProgGuideMain#12](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/hello-world-your-first-p_4.cs)]  
  
-   Può inoltre restituire un integer.  
  
     [!code-cs[csProgGuideMain#13](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/hello-world-your-first-p_5.cs)]  
  
-   Con entrambi i tipi restituiti, può accettare argomenti.  
  
     [!code-cs[csProgGuideMain#19](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/hello-world-your-first-p_6.cs)]  
  
     In alternativa  
  
     [!code-cs[csProgGuideMain#18](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/hello-world-your-first-p_7.cs)]  
  
 Il parametro `args` del metodo `Main` è una matrice di oggetti `string` che contiene gli argomenti della riga di comando utilizzata per richiamare il programma.  Diversamente da C\+\+, la matrice non include il nome del file eseguibile \(.exe\).  
  
 Per ulteriori informazioni sull'utilizzo degli argomenti della riga di comando, vedere gli esempi riportati in [Main\(\) e argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md) e [Procedura: Creare e usare assembly dalla riga di comando](../Topic/How%20to:%20Create%20and%20Use%20Assemblies%20Using%20the%20Command%20Line%20\(C%23%20and%20Visual%20Basic\).md).  
  
 La chiamata a <xref:System.Console.ReadKey%2A> alla fine del metodo `Main` impedisce la chiusura della finestra della console e consente quindi di leggere l'output, quando si esegue il programma in modalità di debug premendo F5.  
  
## Input e output  
 In genere nei programmi C\# vengono utilizzati i servizi di input\/output forniti dalla libreria di runtime di .NET Framework.  L'istruzione `System.Console.WriteLine("Hello World!");`, in cui viene utilizzato il metodo <xref:System.Console.WriteLine%2A>,  Questo è uno dei metodi di output della classe <xref:System.Console> nella libreria di runtime.  e visualizza il parametro di tipo stringa sul flusso di output standard seguito da una nuova riga.  Altri metodi <xref:System.Console> sono disponibili per varie operazioni di input e output.  Se si include la direttiva `using System;` all'inizio del programma, è possibile utilizzare direttamente i metodi e le classi <xref:System> senza assegnare loro nomi completi.  È ad esempio possibile chiamare `Console.WriteLine` anziché `System.Console.WriteLine`:  
  
 [!code-cs[csProgGuide#1](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/csProgGuide/using.cs#1)]  
  
 [!code-cs[csProgGuide#23](../../../csharp/programming-guide/inside-a-program/codesnippet/csharp/csProgGuide/progGuide.cs#23)]  
  
 Per ulteriori informazioni sui metodi di input\/output, vedere <xref:System.IO>.  
  
## Compilazione ed esecuzione della riga di comando  
 È possibile compilare il programma "Hello, World\!" utilizzando la riga di comando invece dell'ambiente di sviluppo integrato \(IDE\) di Visual Studio.  
  
#### Per compilare ed eseguire da un prompt dei comandi  
  
1.  Incollare il codice dalla routine precedente in qualsiasi editor di testo, quindi salvare il file come file di testo.  Denominare il file `Hello.cs`.  I file del codice sorgente C\# utilizzano l'estensione `.cs`.  
  
2.  Eseguire una delle operazioni seguenti per aprire una finestra del prompt dei comandi:  
  
    -   In Windows 8 nella schermata **Start**, cercare `Prompt dei comandi per gli sviluppatori`, quindi tocca o selezionare **Prompt dei comandi per gli sviluppatori per VS2012**.  
  
         Viene visualizzata una finestra del prompt dei comandi per lo sviluppatore.  
  
    -   In Windows 7 aprire il menu **Start**, espandere la cartella della versione corrente di Visual Studio, aprire il menu di scelta rapida per **Visual Studio Tools**, quindi selezionare **Prompt dei comandi per gli sviluppatori per VS2012**.  
  
         Viene visualizzata una finestra del prompt dei comandi per lo sviluppatore.  
  
    -   Attivare le compilazioni da riga di comando da una finestra del prompt dei comandi standard.  
  
         Vedere [How to: Set Environment Variables for the Visual Studio Command Line](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md).  
  
3.  Nella finestra del prompt dei comandi passare alla cartella contenente il file `Hello.cs`.  
  
4.  Per compilare `Hello.cs`, immettere il comando seguente.  
  
     `csc Hello.cs`  
  
     Se il programma non presenta errori di compilazione, viene creato un file eseguibile denominato `Hello.exe`.  
  
5.  Nella finestra del prompt dei comandi immettere il seguente comando per eseguire il programma:  
  
     `Hello`  
  
 Per ulteriori informazioni sul compilatore C\# e le relative opzioni, vedere [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md).  
  
## Capitoli del libro rappresentati  
 [Scrittura di un programma in C\#](http://go.microsoft.com/fwlink/?LinkId=221227) in [Avvio a Visual C\# 2010](http://go.microsoft.com/fwlink/?LinkId=221214)  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Contenuto di un programma C\#](../../../csharp/programming-guide/inside-a-program/index.md)   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)   
 [\<paveover\>C\# Sample Applications](http://msdn.microsoft.com/it-it/9a9d7aaa-51d3-4224-b564-95409b0f3e15)   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Main\(\) e argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)   
 [Guida introduttiva a Visual C\# e Visual Basic](/visual-studio/ide/getting-started-with-visual-csharp-and-visual-basic)