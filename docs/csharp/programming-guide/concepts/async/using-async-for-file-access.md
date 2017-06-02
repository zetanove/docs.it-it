---
title: "Uso della funzionalità Async per l&quot;accesso ai file (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: bb018fea-5313-4c80-ab3f-7c24b2145bd9
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 9aaf49c685498bce451eb53a35a56d8a8fde928c
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="using-async-for-file-access-c"></a>Uso della funzionalità Async per l'accesso ai file (C#)
È possibile usare la funzionalità Async per accedere ai file. Con la funzionalità Async è possibile chiamare i metodi asincroni senza usare callback o suddividere il codice in più metodi o espressioni lambda. Per rendere asincrono il codice sincrono, è sufficiente chiamare un metodo asincrono anziché un metodo sincrono e aggiungere alcune parole chiave al codice.  
  
 È opportuno considerare i seguenti motivi per l'aggiunta della modalità asincrona alle chiamate di accesso ai file:  
  
-   La modalità asincrona rende più reattive le applicazioni dell'interfaccia utente perché il thread dell'interfaccia utente che avvia l'operazione può eseguire altre operazioni. Se il thread dell'interfaccia utente deve eseguire codice che richiede molto tempo (ad esempio, più di 50 millisecondi), l'interfaccia utente può bloccarsi fino al completamento dell'I/O e il thread dell'interfaccia utente può nuovamente elaborare l'input di tastiera e mouse e altri eventi.  
  
-   La modalità asincrona migliora la scalabilità di ASP.NET e di altre applicazioni basate su server, riducendo la necessità di thread. Se l'applicazione usa un thread dedicato per ogni risposta e vengono gestite contemporaneamente mille richieste, sono necessari mille thread. Le operazioni asincrone non richiedono spesso l'uso di un thread durante l'attesa. Usano brevemente il thread di completamento di I/O esistente alla fine.  
  
-   La latenza di un'operazione di accesso ai file può essere molto bassa nelle condizioni attuali, ma aumentare notevolmente in futuro. Ad esempio, un file può essere spostato in tutt'altra parte del mondo.  
  
-   Il sovraccarico aggiuntivo dovuto all'uso della funzionalità Async è ridotto.  
  
-   Le attività asincrone possono essere facilmente eseguite in parallelo.  
  
## <a name="running-the-examples"></a>Esecuzione degli esempi  
 Per eseguire gli esempi in questo argomento, è possibile creare un'**applicazione WPF** o un'**applicazione Windows Form** e quindi aggiungere un **pulsante**. Nell'evento `Click` del pulsante aggiungere una chiamata al primo metodo in ogni esempio.  
  
 Negli esempi seguenti includere le istruzioni `using` indicate di seguito.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Diagnostics;  
using System.IO;  
using System.Text;  
using System.Threading.Tasks;  
```  
  
## <a name="use-of-the-filestream-class"></a>Uso della classe FileStream  
 Negli esempi di questo argomento viene usata la classe <xref:System.IO.FileStream>, che ha un'opzione che determina la generazione di I/O asincrono a livello di sistema operativo. L'opzione consente di evitare il blocco di un thread del pool di thread in molti casi. Per abilitare questa opzione, specificare l'argomento `useAsync=true` o `options=FileOptions.Asynchronous` nella chiamata al costruttore.  
  
 Non è possibile usare questa opzione con oggetti <xref:System.IO.StreamReader> e <xref:System.IO.StreamWriter> se questi vengono aperti direttamente tramite l'indicazione di un percorso. È tuttavia possibile usare questa opzione se si fornisce loro un oggetto <xref:System.IO.Stream> aperto dalla classe <xref:System.IO.FileStream>. Si noti che le chiamate asincrone sono più veloci nelle applicazioni dell'interfaccia utente anche se un thread del pool di thread è bloccato, poiché il thread dell'interfaccia utente non è bloccato durante l'attesa.  
  
## <a name="writing-text"></a>Scrittura di testo  
 Nell'esempio seguente viene scritto un testo in un file. Ad ogni istruzione await il metodo termina immediatamente. Completato l'I/O del file, il metodo riprende in corrispondenza dell'istruzione che segue l'istruzione await. Si noti che il modificatore async si trova nella definizione dei metodi che usano l'istruzione await.  
  
```csharp  
public async void ProcessWrite()  
{  
    string filePath = @"temp2.txt";  
    string text = "Hello World\r\n";  
  
    await WriteTextAsync(filePath, text);  
}  
  
private async Task WriteTextAsync(string filePath, string text)  
{  
    byte[] encodedText = Encoding.Unicode.GetBytes(text);  
  
    using (FileStream sourceStream = new FileStream(filePath,  
        FileMode.Append, FileAccess.Write, FileShare.None,  
        bufferSize: 4096, useAsync: true))  
    {  
        await sourceStream.WriteAsync(encodedText, 0, encodedText.Length);  
    };  
}  
```  
  
 L'esempio originale usa l'istruzione `await sourceStream.WriteAsync(encodedText, 0, encodedText.Length);`, che è una contrazione delle due istruzioni seguenti:  
  
```csharp  
Task theTask = sourceStream.WriteAsync(encodedText, 0, encodedText.Length);  
await theTask;  
```  
  
 La prima istruzione restituisce un'attività e determina l'avvio dell'elaborazione dei file. La seconda istruzione con await induce il metodo a terminare immediatamente e restituire un'attività diversa. Al termine dell'elaborazione dei file l'esecuzione torna quindi all'istruzione che segue await. Per altre informazioni, vedere [Flusso di controllo in programmi asincroni (C#)](../../../../csharp/programming-guide/concepts/async/control-flow-in-async-programs.md).  
  
## <a name="reading-text"></a>Lettura di testo  
 Nell'esempio seguente viene letto del testo da un file. Il testo viene memorizzato nel buffer e, in questo caso, inserito in un oggetto <xref:System.Text.StringBuilder>. A differenza dell'esempio precedente, la valutazione di await produce un valore. Il metodo <xref:System.IO.Stream.ReadAsync%2A> restituisce un <xref:System.Threading.Tasks.Task> \< <xref:System.Int32>>. Pertanto la valutazione dell'attesa produce un valore `Int32` (`numRead`) dopo il completamento dell'operazione. Per altre informazioni, vedere [Tipi restituiti asincroni (C#)](../../../../csharp/programming-guide/concepts/async/async-return-types.md).  
  
```csharp  
public async void ProcessRead()  
{  
    string filePath = @"temp2.txt";  
  
    if (File.Exists(filePath) == false)  
    {  
        Debug.WriteLine("file not found: " + filePath);  
    }  
    else  
    {  
        try  
        {  
            string text = await ReadTextAsync(filePath);  
            Debug.WriteLine(text);  
        }  
        catch (Exception ex)  
        {  
            Debug.WriteLine(ex.Message);  
        }  
    }  
}  
  
private async Task<string> ReadTextAsync(string filePath)  
{  
    using (FileStream sourceStream = new FileStream(filePath,  
        FileMode.Open, FileAccess.Read, FileShare.Read,  
        bufferSize: 4096, useAsync: true))  
    {  
        StringBuilder sb = new StringBuilder();  
  
        byte[] buffer = new byte[0x1000];  
        int numRead;  
        while ((numRead = await sourceStream.ReadAsync(buffer, 0, buffer.Length)) != 0)  
        {  
            string text = Encoding.Unicode.GetString(buffer, 0, numRead);  
            sb.Append(text);  
        }  
  
        return sb.ToString();  
    }  
}  
```  
  
## <a name="parallel-asynchronous-io"></a>I/O asincrono parallelo  
 Nell'esempio seguente viene illustrata l'elaborazione parallela per la scrittura di 10 file di testo. Per ogni file, il metodo <xref:System.IO.Stream.WriteAsync%2A> restituisce un'attività che successivamente viene aggiunta a un elenco di attività. L'istruzione `await Task.WhenAll(tasks);` termina il metodo e riprende all'interno del metodo quando l'elaborazione dei file è completata per tutte le attività.  
  
 L'esempio chiude tutte le istanze di <xref:System.IO.FileStream> in un blocco `finally` dopo il completamento delle attività. Se invece ogni oggetto `FileStream` è stato creato in un'istruzione `using`, è possibile che l'oggetto `FileStream` venga eliminato prima del completamento dell'attività.  
  
 Si noti che qualsiasi miglioramento delle prestazioni è dovuto quasi interamente all'elaborazione parallela e non all'elaborazione asincrona. I vantaggi dell'asincronia sono che l'elaborazione non blocca più thread e non blocca il thread dell'interfaccia utente.  
  
```csharp  
public async void ProcessWriteMult()  
{  
    string folder = @"tempfolder\";  
    List<Task> tasks = new List<Task>();  
    List<FileStream> sourceStreams = new List<FileStream>();  
  
    try  
    {  
        for (int index = 1; index <= 10; index++)  
        {  
            string text = "In file " + index.ToString() + "\r\n";  
  
            string fileName = "thefile" + index.ToString("00") + ".txt";  
            string filePath = folder + fileName;  
  
            byte[] encodedText = Encoding.Unicode.GetBytes(text);  
  
            FileStream sourceStream = new FileStream(filePath,  
                FileMode.Append, FileAccess.Write, FileShare.None,  
                bufferSize: 4096, useAsync: true);  
  
            Task theTask = sourceStream.WriteAsync(encodedText, 0, encodedText.Length);  
            sourceStreams.Add(sourceStream);  
  
            tasks.Add(theTask);  
        }  
  
        await Task.WhenAll(tasks);  
    }  
  
    finally  
    {  
        foreach (FileStream sourceStream in sourceStreams)  
        {  
            sourceStream.Close();  
        }  
    }  
}  
```  
  
 Quando si usano i metodi <xref:System.IO.Stream.WriteAsync%2A> e <xref:System.IO.Stream.ReadAsync%2A>, è possibile specificare uno struct <xref:System.Threading.CancellationToken>, che consente di annullare l'operazione nel corso del flusso. Per altre informazioni, vedere [Ottimizzazione dell'app asincrona (C#)](../../../../csharp/programming-guide/concepts/async/fine-tuning-your-async-application.md) e [Annullamento in thread gestiti](../../../../standard/threading/cancellation-in-managed-threads.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione asincrona con async e await (C#)](../../../../csharp/programming-guide/concepts/async/index.md)   
 [Tipi restituiti asincroni (C#)](../../../../csharp/programming-guide/concepts/async/async-return-types.md)   
 [Flusso di controllo in programmi asincroni (C#)](../../../../csharp/programming-guide/concepts/async/control-flow-in-async-programs.md)
