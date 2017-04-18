---
title: Riferimenti per F# Interactive (fsi.exe)
description: Riferimenti per F# Interactive (fsi.exe)
keywords: visual f#, f#, programmazione funzionale
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 36af8d1b-dc08-4a37-9497-d23c0a0ac11c
translationtype: Human Translation
ms.sourcegitcommit: 0a01ec92a90d99fafaacbd3f71f5177e5cf94a68
ms.openlocfilehash: 87980bada62b568ec8795ab3566089f1bb510652
ms.lasthandoff: 04/05/2017

---

# <a name="interactive-programming-with-f"></a>Programmazione interattiva con F# #

> [!NOTE]
Questo articolo illustra attualmente solo l'esperienza per Windows.  Verrà riscritto.

> [!NOTE]
Il collegamento al riferimento per l'API porta a MSDN.  Il riferimento all'API in Microsoft Docs (docs.microsoft.com) non è completo.

F# Interactive (fsi.exe) viene usato per eseguire il codice di F# in modo interattivo alla console o per eseguire script F#. In altre parole, F# Interactive esegue un REPL (Read, Evaluate, Print Loop) per il linguaggio F#.

Per eseguire F# Interactive dalla console, eseguire fsi.exe.  Il file fsi.exe si trova in "c:\Programmi (x86)\Microsoft SDKs\F#\<versione>\Framework\<versione>\". Per informazioni sulle opzioni da riga di comando disponibili, vedere [Opzioni di F# Interactive](fsharp-interactive-options.md).

Per eseguire F# Interactive in Visual Studio, è possibile fare clic sul pulsante **F# Interactive** appropriato sulla barra degli strumenti oppure premere i tasti **CTRL+ALT+F**. Questa operazione comporterà l'apertura della finestra interattiva, una finestra degli strumenti che esegue una sessione di F# Interactive. È anche possibile selezionare parti di codice che si vuole eseguire nella finestra interattiva e quindi premere **ALT + INVIO**. F# Interactive viene avviato in una finestra degli strumenti denominata **F# Interactive**. Quando si usa questa combinazione di tasti, assicurarsi che sia selezionata la finestra dell'editor.

Sia che si utilizzi la console o Visual Studio, viene visualizzato un prompt dei comandi e l'interprete attende l'input. Immettere il codice come si farebbe in un file di codice. Per compilare ed eseguire il codice, immettere due punti e virgola (**;;**) per terminare una o più righe di input.

F# Interactive prova a compilare il codice e, in caso contrario, esegue il codice e stampa la firma dei tipi e dei valori compilati. Se si verificano errori, l'interprete stampa i messaggi di errore.

Il codice immesso nella stessa sessione ha accesso a qualsiasi costrutto immesso in precedenza, per consentire la compilazione di programmi. Un buffer completo nella finestra degli strumenti consente di copiare il codice in un file, se necessario.

Se eseguito in Visual Studio, F# Interactive viene eseguito in modo indipendente dal progetto. In questo modo, ad esempio, non è possibile usare costrutti definiti nel progetto in F# Interactive a meno che non sia possibile copiare il codice per la funzione nella finestra interattiva.

Se è aperto un progetto che fa riferimento ad alcune librerie, è possibile fare riferimento a tali librerie in F# Interactive con **Esplora soluzioni**. Per fare riferimento a una libreria in F# Interactive, espandere il nodo **Riferimenti**, aprire il menu di scelta rapida della libreria e scegliere **Invia a F# Interactive**.

È possibile controllare gli argomenti della riga di comando (opzioni) di F# Interactive modificando le impostazioni. Nel menu **Strumenti** selezionare **Opzioni**, quindi espandere **Strumenti F#**. Le due impostazioni che è possibile modificare sono le opzioni di F# Interactive e l'impostazione **F# Interactive a 64 bit**, che è rilevante solo se si esegue F# Interactive in un computer a 64 bit. Con questa impostazione si determina se si desidera eseguire la versione a 64 bit dedicata di fsi.exe o di fsianycpu.exe, in cui si usa l'architettura del computer per determinare se l'esecuzione avviene come processo a 32 bit o 64 bit.


## <a name="scripting-with-f"></a>Esecuzione di script con F# #
Gli script hanno l'estensione di file **.fsx** o **.fsscript**. Anziché compilare il codice sorgente e quindi eseguire in un secondo momento l'assembly compilato, è possibile eseguire semplicemente **fsi.exe** e specificare il nome del file dello script del codice sorgente F#. F# Interactive legge il codice e lo esegue in tempo reale.


## <a name="differences-between-the-interactive-scripting-and-compiled-environments"></a>Differenze tra gli ambienti interattivi, di scripting e compilati
Quando si compila il codice in F# Interactive, con un'esecuzione interattiva o con un'esecuzione di uno script, viene definito il simbolo **INTERACTIVE**. Quando si compila il codice nel compilatore, viene definito il simbolo **COMPILED**. In questo modo, se il codice deve essere diverso in modalità interattiva e compilata, è possibile usare le direttive del preprocessore per la compilazione condizionale allo scopo di determinare quale usare.

Alcune direttive sono disponibili quando si eseguono script in F# Interactive, mentre non sono disponibili quando si esegue il compilatore. Nella tabella seguente sono riepilogate le direttive disponibili quando si usa F# Interactive.

|Direttiva|Descrizione|
|---------|-----------|
|**#help**|Visualizza informazioni sulle direttive disponibili.|
|**#I**|Specifica un percorso di ricerca assembly tra virgolette.|
|**#load**|Legge un file di origine, lo compila e lo esegue.|
|**#quit**|Termina una sessione di F# Interactive.|
|**#r**|Fa riferimento a un assembly.|
|**#time ["on"&#124;"off"]**|**#time** attiva o disattiva la visualizzazione di informazioni sulle prestazioni. Quando è attivato, F# Interactive misura il tempo reale, il tempo di CPU e le informazioni di Garbage Collection per ogni sezione di codice che viene interpretato ed eseguito.|

Quando si specificano file o percorsi in F# Interactive, è previsto un valore letterale di stringa. Quindi, file e percorsi devono essere racchiusi tra virgolette ed è necessario applicare i caratteri di escape consueti. È anche possibile usare il carattere @ in modo che F# Interactive interpreti una stringa che contiene un percorso come stringa letterale. In questo modo F# Interactive ignorerà i caratteri di escape.

Una delle differenze tra la modalità interattiva e quella compilata è la modalità di accesso agli argomenti della riga di comando. Nella modalità compilata, usare **System.Environment.GetCommandLineArgs**. Negli script, usare **fsi.CommandLineArgs**.

Il codice seguente illustra come creare una funzione che legga gli argomenti della riga di comando in uno script e anche come fare riferimento a un altro assembly da uno script. Il primo file di codice, **MyAssembly.fs**, è il codice per l'assembly a cui fa riferimento. Compilare questo file con la riga di comando **fsc -a MyAssembly.fs**, quindi eseguire il secondo file come script con la riga di comando **fsi --exec file1.fsx** test

```fsharp
// MyAssembly.fs
module MyAssembly
let myFunction x y = x + 2 * y
```

```fsharp
// file1.fsx
#r "MyAssembly.dll"

printfn "Command line arguments: "

for arg in fsi.CommandLineArgs do
    printfn "%s" arg

printfn "%A" (MyAssembly.myFunction 10 40)
```

L'output è indicato di seguito:

```
Command line arguments: 
file1.fsx
test
60
```

## <a name="related-topics"></a>Argomenti correlati

|Titolo|Descrizione|
|-----|-----------|
|[Opzioni di F# Interactive](fsharp-interactive-options.md)|Viene descritta la sintassi della riga di comando e le opzioni per F# Interactive, fsi.exe.|
|[Riferimento alla libreria di F# Interactive](https://msdn.microsoft.com/visualfsharpdocs/conceptual/fsharp-interactive-library-reference)|Viene descritta la funzionalità della libreria disponibile durante l'esecuzione di codice in F# Interactive.|
