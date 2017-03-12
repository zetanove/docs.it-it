---
title: "Compilazione dalla riga di comando con csc.exe | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "compilazioni [C#]"
  - "riga di comando [C#]"
ms.assetid: 66e70056-dd20-453c-a9b3-507e0478b015
caps.latest.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 28
---
# Compilazione dalla riga di comando con csc.exe
È possibile richiamare il compilatore C# digitando il nome del relativo file eseguibile (csc.exe) da un prompt dei comandi.  
  
 Se si utilizza il **Prompt dei comandi di Visual Studio** finestra, tutte le variabili di ambiente necessarie sono impostate automaticamente. In Windows 7, è possibile accedere dalla finestra di **avviare** menu aprendo Microsoft Visual Studio *versione*cartella \Visual Studio Tools. In Windows 8, il prompt dei comandi di Visual Studio viene chiamato il **Developer Command Prompt for VS2012**, ed è possibile trovarlo cercandolo dalla schermata Start.  
  
 Se si usa una finestra del Prompt dei comandi standard, è necessario modificare il percorso prima di poter richiamare csc.exe da qualsiasi sottodirectory del computer. È inoltre necessario eseguire vsvars32.bat per impostare le variabili di ambiente necessarie per supportare le compilazioni da riga di comando. Per ulteriori informazioni su vsvars32. bat, incluse le istruzioni su come trovare ed eseguire, vedere [procedura: impostare le variabili di ambiente per Visual Studio riga di comando](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md).  
  
 Se si lavora in un computer che dispone solo di [!INCLUDE[winsdklong](../../../csharp/language-reference/compiler-options/includes/winsdklong-md.md)], è possibile utilizzare il compilatore c# al **prompt dei comandi SDK**, che viene visualizzato dal **Microsoft .NET Framework SDK** opzione di menu.  
  
 È inoltre possibile utilizzare MSBuild per compilare programmi C# a livello di codice. Per ulteriori informazioni, vedere [MSBuild](/visual-studio/msbuild/msbuild1).  
  
 Il file eseguibile csc.exe è si trova in genere \Framework\\*versione* cartella nella directory di Windows. La posizione del file può variare in base all'esatta configurazione di un determinato computer. Se nel computer sono installate più versioni di .NET Framework, saranno disponibili più versioni di questo file. Per ulteriori informazioni su tali installazioni, vedere [Determinazione della versione di .NET Framework di installazione](http://msdn.microsoft.com/it-it/1a87cc6a-1c4b-4c38-b878-faa9b3beae3c).  
  
> [!TIP]
>  Quando si compila un progetto utilizzando l'IDE di Visual Studio, è possibile visualizzare il **csc** comando e le relative opzioni del compilatore associate nella **Output** finestra. Per visualizzare queste informazioni, seguire le istruzioni in [procedura: visualizzazione, salvare e configurare i file di Log compilare](../Topic/How%20to:%20View,%20Save,%20and%20Configure%20Build%20Log%20Files.md) per modificare il livello di dettaglio dei dati nel Registro di **normale** o **dettagliato**. Al termine della ricompilazione del progetto, cercare il **Output** finestra **csc** per trovare la chiamata del compilatore c#.  
  
 **In questo argomento**  
  
-   [Regole per la sintassi della riga di comando](#vcconcommand-linebuildinganchor1)  
  
-   [Esempi di righe di comando](#vcconcommand-linebuildinganchor2)  
  
-   [Differenze tra Output del compilatore C++ e il compilatore c#](#vcconcommand-linebuildinganchor3)  
  
##  <a name="a-namevcconcommand-linebuildinganchor1a-rules-for-command-line-syntax-for-the-c-compiler"></a><a name="vcconcommand-linebuildinganchor1"></a> Regole per la sintassi della riga di comando per il compilatore c#  
 Il compilatore c# utilizza le regole seguenti quando interpreta gli argomenti forniti alla riga di comando del sistema operativo:  
  
-   Gli argomenti sono delimitati da spazi vuoti, ovvero da uno spazio o da una tabulazione.  
  
-   L'accento circonflesso (^) non è riconosciuto come carattere di escape o delimitatore. Il carattere viene gestito dal parser della riga di comando nel sistema operativo prima di essere passato alla matrice argv nel programma.  
  
-   Una stringa racchiusa tra virgolette doppie ("stringa") viene interpretata come un unico argomento, a prescindere dallo spazio vuoto che è contenuto all'interno. Una stringa tra virgolette può essere incorporata in un argomento.  
  
-   Le virgolette doppie precedute da una barra rovesciata (\\") viene interpretato come un carattere di virgolette doppie (").  
  
-   Le barre rovesciate vengono interpretate letteralmente, a meno che non precedano virgolette doppie.  
  
-   Se un numero pari di barre rovesciate è seguito da un segno di virgolette doppie, una barra rovesciata viene inserita nella matrice argv per ogni coppia di barre rovesciate e le virgolette doppie viene interpretata come un delimitatore di stringa.  
  
-   Se un numero dispari di barre rovesciate è seguito da un segno di virgolette doppie, una barra rovesciata viene inserita nella matrice argv per ogni coppia di barre rovesciate e le virgolette doppie "escape" per la barra rovesciata rimanente. In questo modo un valore letterale virgolette doppie (") devono essere aggiunti argv.  
  
##  <a name="a-namevcconcommand-linebuildinganchor2a-sample-command-lines-for-the-c-compiler"></a><a name="vcconcommand-linebuildinganchor2"></a> Righe di comando di esempio per il compilatore c#  
  
-   Consente di compilare File.cs producendo File.exe:  
  
    ```  
    csc File.cs   
    ```  
  
-   Consente di compilare File.cs generando file. dll:  
  
    ```  
    csc /target:library File.cs  
    ```  
  
-   Consente di compilare File.cs e crea My.exe:  
  
    ```  
    csc /out:My.exe File.cs  
    ```  
  
-   Consente di compilare tutti i file c# nella directory corrente, con le ottimizzazioni attive e definisce il simbolo di DEBUG. L'output è File2.exe:  
  
    ```  
    csc /define:DEBUG /optimize /out:File2.exe *.cs  
    ```  
  
-   Consente di compilare tutti i file c# della directory corrente generando una versione di debug di File2. dll. Nessun logo e nessun avviso viene visualizzato:  
  
    ```  
    csc /target:library /out:File2.dll /warn:0 /nologo /debug *.cs  
    ```  
  
-   Consente di compilare tutti i file c# nella directory corrente in Something. xyz (una DLL):  
  
    ```  
    csc /target:library /out:Something.xyz *.cs  
    ```  
  
##  <a name="a-namevcconcommand-linebuildinganchor3a-differences-between-c-compiler-and-c-compiler-output"></a><a name="vcconcommand-linebuildinganchor3"></a> Differenze tra Output del compilatore C++ e il compilatore c#  
 In seguito al richiamo del compilatore C# non viene creato alcun file oggetto con estensione obj. I file di output vengono creati direttamente. Di conseguenza, il compilatore c# non è necessario un linker.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni del compilatore c#](../../../csharp/language-reference/compiler-options/index.md)   
 [Opzioni del compilatore c# elencate in ordine alfabetico](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)   
 [Opzioni del compilatore c# elencate per categoria](../../../csharp/language-reference/compiler-options/listed-by-category.md)   
 [Main () e gli argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md)   
 [Argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/command-line-arguments.md)   
 [Procedura: visualizzare gli argomenti della riga di comando](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)   
 [Procedura: accedere agli argomenti della riga di comando utilizzando foreach](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)   
 [Valori restituiti da Main](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)