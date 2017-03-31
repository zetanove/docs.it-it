---
title: 'Procedura: Estendere la procedura dettagliata asincrona usando Task.WhenAll (C#) | Microsoft Docs'
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
ms.assetid: f6927ef2-dc6c-43f8-bc82-bbeac42de423
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: cf538f555c9b1636980fb68ca1c132504112d9fb
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-extend-the-async-walkthrough-by-using-taskwhenall-c"></a>Procedura: Estendere la procedura dettagliata asincrona usando Task.WhenAll (C#)
È possibile migliorare le prestazioni della soluzione asincrona in [Procedura dettagliata: accesso al Web tramite async e await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md) tramite il metodo <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>. Questo metodo mette in attesa più operazioni asincrone, rappresentate come una raccolta di attività.  
  
 Si noti che nella procedura dettagliata i siti Web vengono scaricati a velocità diverse. A volte un sito Web è molto lento e causa il ritardo di tutti i download rimanenti. Quando si eseguono le soluzioni asincrone compilate nella procedura dettagliata, è possibile terminare il programma con facilità se non si vuole attendere. Un'opzione migliore consiste nell'avviare tutti i download contemporaneamente e consentire a quelli più veloci di continuare senza attendere il termine di quello più lento.  
  
 Si applica il metodo `Task.WhenAll` a una raccolta di attività. L'applicazione di `WhenAll` restituisce una singola attività che non viene completata fino quando non vengono completate tutte le attività nella raccolta. Le attività vengono eseguite in parallelo, ma non vengono creati thread aggiuntivi. Il completamento delle attività può avvenire in qualsiasi ordine.  
  
> [!IMPORTANT]
>  Le procedure seguenti descrivono le estensioni per le applicazioni asincrone che sono state sviluppate in [Procedura dettagliata: accesso al Web tramite async e await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md). È possibile sviluppare le applicazioni completando la procedura dettagliata o scaricando il codice da [Developer Code Samples](http://go.microsoft.com/fwlink/?LinkId=255191) (Esempi di codice per gli sviluppatori).  
>   
>  Per eseguire l'esempio, è necessario avere Visual Studio 2012 o versioni successive installate nel computer.  
  
### <a name="to-add-taskwhenall-to-your-geturlcontentsasync-solution"></a>Per aggiungere Task.WhenAll alla soluzione GetURLContentsAsync  
  
1.  Aggiungere il metodo `ProcessURLAsync` per la prima applicazione che è stata sviluppata in [Procedura dettagliata: accesso al Web tramite async e await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).  
  
    -   Se è stato scaricato il codice da [Developer Code Samples](http://go.microsoft.com/fwlink/?LinkId=255191) (Esempi di codice per gli sviluppatori), aprire il progetto AsyncWalkthrough e aggiungere `ProcessURLAsync` nel file MainWindow.xaml.cs.  
  
    -   Se il codice è stato sviluppato completando la procedura dettagliata, aggiungere `ProcessURLAsync` all'applicazione che include il metodo `GetURLContentsAsync`. Il file MainWindow.xaml.cs per questa applicazione è il primo esempio nella sezione dedicata agli esempi di codice della procedura dettagliata.  
  
     Il metodo `ProcessURLAsync` consente di consolidare le azioni nel corpo del ciclo `foreach` in `SumPageSizesAsync` nella procedura dettagliata originale. Il metodo scarica in modo asincrono il contenuto di un sito Web specificato come matrice di byte e quindi visualizza e restituisce la lunghezza della matrice di byte.  
  
    ```csharp  
    private async Task<int> ProcessURLAsync(string url)  
    {  
        var byteArray = await GetURLContentsAsync(url);  
        DisplayResults(url, byteArray);  
        return byteArray.Length;  
    }  
    ```  
  
2.  Impostare come commento o eliminare il ciclo `foreach` in `SumPageSizesAsync`, come illustrato nel codice seguente.  
  
    ```csharp  
    //var total = 0;  
    //foreach (var url in urlList)  
    //{  
    //    byte[] urlContents = await GetURLContentsAsync(url);  
  
    //    // The previous line abbreviates the following two assignment statements.  
    //    // GetURLContentsAsync returns a Task<T>. At completion, the task  
    //    // produces a byte array.  
    //    //Task<byte[]> getContentsTask = GetURLContentsAsync(url);  
    //    //byte[] urlContents = await getContentsTask;  
  
    //    DisplayResults(url, urlContents);  
  
    //    // Update the total.            
    //    total += urlContents.Length;  
    //}  
    ```  
  
3.  Creare una raccolta di attività. Il codice seguente definisce una [query](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d) che, quando eseguita dal metodo <xref:System.Linq.Enumerable.ToArray%2A>, crea una raccolta di attività che scarica il contenuto di ogni sito Web. Le attività vengono avviate quando viene valutata la query.  
  
     Aggiungere il codice seguente al metodo `SumPageSizesAsync` dopo la dichiarazione di `urlList`.  
  
    ```csharp  
    // Create a query.   
    IEnumerable<Task<int>> downloadTasksQuery =   
        from url in urlList select ProcessURLAsync(url);  
  
    // Use ToArray to execute the query and start the download tasks.  
    Task<int>[] downloadTasks = downloadTasksQuery.ToArray();  
    ```  
  
4.  Applicare `Task.WhenAll` alla raccolta di attività, `downloadTasks`. `Task.WhenAll` restituisce una singola attività che termina al completamento di tutte le attività della raccolta.  
  
     Nell'esempio seguente, l'espressione `await` mette in attesa il completamento della singola attività restituita da `WhenAll`. L'espressione restituisce una matrice di numeri interi, dove ogni numero intero rappresenta la lunghezza di un sito Web scaricato. Aggiungere il codice seguente a `SumPageSizesAsync`, dopo il codice aggiunto nel passaggio precedente.  
  
    ```csharp  
    // Await the completion of all the running tasks.  
    int[] lengths = await Task.WhenAll(downloadTasks);  
  
    //// The previous line is equivalent to the following two statements.  
    //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);  
    //int[] lengths = await whenAllTask;  
    ```  
  
5.  Infine, usare il metodo <xref:System.Linq.Enumerable.Sum%2A> per calcolare la somma delle lunghezze di tutti i siti Web. Aggiungere la riga seguente a `SumPageSizesAsync`.  
  
    ```csharp  
    int total = lengths.Sum();  
    ```  
  
### <a name="to-add-taskwhenall-to-the-httpclientgetbytearrayasync-solution"></a>Per aggiungere Task.WhenAll alla soluzione HttpClient.GetByteArrayAsync  
  
1.  Aggiungere la versione seguente di `ProcessURLAsync` alla seconda applicazione sviluppata in [Procedura dettagliata: accesso al Web tramite async e await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).  
  
    -   Se è stato scaricato il codice da [Developer Code Samples](http://go.microsoft.com/fwlink/?LinkId=255191) (Esempi di codice per gli sviluppatori), aprire il progetto AsyncWalkthrough_HttpClient e aggiungere `ProcessURLAsync` nel file MainWindow.xaml.cs.  
  
    -   Se il codice è stato sviluppato completando la procedura dettagliata, aggiungere `ProcessURLAsync` all'applicazione che usa il metodo `HttpClient.GetByteArrayAsync`. Il file MainWindow.xaml.cs per questa applicazione è il secondo esempio nella sezione dedicata agli esempi di codice della procedura dettagliata.  
  
     Il metodo `ProcessURLAsync` consente di consolidare le azioni nel corpo del ciclo `foreach` in `SumPageSizesAsync` nella procedura dettagliata originale. Il metodo scarica in modo asincrono il contenuto di un sito Web specificato come matrice di byte e quindi visualizza e restituisce la lunghezza della matrice di byte.  
  
     L'unica differenza rispetto al metodo `ProcessURLAsync` nella procedura precedente consiste nell'usare l'istanza <xref:System.Net.Http.HttpClient>, `client`.  
  
    ```csharp  
    async Task<int> ProcessURL(string url, HttpClient client)  
    {  
        byte[] byteArray = await client.GetByteArrayAsync(url);  
        DisplayResults(url, byteArray);  
        return byteArray.Length;  
    }  
    ```  
  
2.  Impostare come commento o eliminare il ciclo `For Each` o `foreach` in `SumPageSizesAsync`, come illustrato nel codice seguente.  
  
    ```csharp  
    //var total = 0;  
    //foreach (var url in urlList)  
    //{  
    //    // GetByteArrayAsync returns a Task<T>. At completion, the task  
    //    // produces a byte array.  
    //    byte[] urlContent = await client.GetByteArrayAsync(url);  
  
    //    // The previous line abbreviates the following two assignment  
    //    // statements.  
    //    Task<byte[]> getContentTask = client.GetByteArrayAsync(url);  
    //    byte[] urlContent = await getContentTask;  
  
    //    DisplayResults(url, urlContent);  
  
    //    // Update the total.  
    //    total += urlContent.Length;  
    //}  
    ```  
  
3.  Definire una [query](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d) che, quando eseguita dal metodo <xref:System.Linq.Enumerable.ToArray%2A>, crea una raccolta di attività che scarica il contenuto di ogni sito Web. Le attività vengono avviate quando viene valutata la query.  
  
     Aggiungere il codice seguente al metodo `SumPageSizesAsync` dopo la dichiarazione di `client` e `urlList`.  
  
    ```csharp  
    // Create a query.  
    IEnumerable<Task<int>> downloadTasksQuery =   
        from url in urlList select ProcessURL(url, client);  
  
    // Use ToArray to execute the query and start the download tasks.  
    Task<int>[] downloadTasks = downloadTasksQuery.ToArray();  
    ```  
  
4.  In seguito applicare `Task.WhenAll` alla raccolta di attività, `downloadTasks`. `Task.WhenAll` restituisce una singola attività che termina al completamento di tutte le attività della raccolta.  
  
     Nell'esempio seguente, l'espressione `await` mette in attesa il completamento della singola attività restituita da `WhenAll`. Al termine dell'operazione, l'espressione `await` restituisce una matrice di numeri interi, dove ogni numero intero rappresenta la lunghezza di un sito Web scaricato. Aggiungere il codice seguente a `SumPageSizesAsync`, dopo il codice aggiunto nel passaggio precedente.  
  
    ```csharp  
    // Await the completion of all the running tasks.  
    int[] lengths = await Task.WhenAll(downloadTasks);  
  
    //// The previous line is equivalent to the following two statements.  
    //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);  
    //int[] lengths = await whenAllTask;  
    ```  
  
5.  Infine, usare il metodo <xref:System.Linq.Enumerable.Sum%2A> per ottenere la somma delle lunghezze di tutti i siti Web. Aggiungere la riga seguente a `SumPageSizesAsync`.  
  
    ```csharp  
    int total = lengths.Sum();
    ```  
  
### <a name="to-test-the-taskwhenall-solutions"></a>Per testare le soluzioni Task.WhenAll  
  
-   Per tutte le soluzioni, premere F5 per eseguire il programma e scegliere il pulsante **Start**. L'output dovrebbe essere simile all'output delle soluzioni asincrone in [Procedura dettagliata: accesso al Web tramite async e await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md). Tuttavia, si noti che i siti Web vengono visualizzati ogni volta in un ordine diverso.  
  
## <a name="example"></a>Esempio  
 Il codice seguente illustra le estensioni per il progetto che usa il metodo `GetURLContentsAsync` per scaricare il contenuto dal Web.  
  
```csharp  
// Add the following using directives, and add a reference for System.Net.Http.  
using System.Net.Http;  
using System.IO;  
using System.Net;  
  
namespace AsyncExampleWPF_WhenAll  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
        }  
  
        private async void startButton_Click(object sender, RoutedEventArgs e)  
        {  
            resultsTextBox.Clear();  
  
            // Two-step async call.  
            Task sumTask = SumPageSizesAsync();  
            await sumTask;  
  
            // One-step async call.  
            //await SumPageSizesAsync();  
  
            resultsTextBox.Text += "\r\nControl returned to startButton_Click.\r\n";  
        }  
  
        private async Task SumPageSizesAsync()  
        {  
            // Make a list of web addresses.  
            List<string> urlList = SetUpURLList();  
  
            // Create a query.   
            IEnumerable<Task<int>> downloadTasksQuery =   
                from url in urlList select ProcessURLAsync(url);  
  
            // Use ToArray to execute the query and start the download tasks.  
            Task<int>[] downloadTasks = downloadTasksQuery.ToArray();  
  
            // You can do other work here before awaiting.  
  
            // Await the completion of all the running tasks.  
            int[] lengths = await Task.WhenAll(downloadTasks);  
  
            //// The previous line is equivalent to the following two statements.  
            //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);  
            //int[] lengths = await whenAllTask;  
  
            int total = lengths.Sum();  
  
            //var total = 0;  
            //foreach (var url in urlList)  
            //{  
            //    byte[] urlContents = await GetURLContentsAsync(url);  
  
            //    // The previous line abbreviates the following two assignment statements.  
            //    // GetURLContentsAsync returns a Task<T>. At completion, the task  
            //    // produces a byte array.  
            //    //Task<byte[]> getContentsTask = GetURLContentsAsync(url);  
            //    //byte[] urlContents = await getContentsTask;  
  
            //    DisplayResults(url, urlContents);  
  
            //    // Update the total.            
            //    total += urlContents.Length;  
            //}  
  
            // Display the total count for all of the websites.  
            resultsTextBox.Text +=  
                string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
        }  
  
        private List<string> SetUpURLList()  
        {  
            List<string> urls = new List<string>   
            {   
                "http://msdn.microsoft.com",  
                "http://msdn.microsoft.com/library/windows/apps/br211380.aspx",  
                "http://msdn.microsoft.com/library/hh290136.aspx",  
                "http://msdn.microsoft.com/library/ee256749.aspx",  
                "http://msdn.microsoft.com/library/hh290138.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/dd470362.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            };  
            return urls;  
        }  
  
        // The actions from the foreach loop are moved to this async method.  
        private async Task<int> ProcessURLAsync(string url)  
        {  
            var byteArray = await GetURLContentsAsync(url);  
            DisplayResults(url, byteArray);  
            return byteArray.Length;  
        }  
  
        private async Task<byte[]> GetURLContentsAsync(string url)  
        {  
            // The downloaded resource ends up in the variable named content.  
            var content = new MemoryStream();  
  
            // Initialize an HttpWebRequest for the current URL.  
            var webReq = (HttpWebRequest)WebRequest.Create(url);  
  
            // Send the request to the Internet resource and wait for  
            // the response.  
            using (WebResponse response = await webReq.GetResponseAsync())  
            {  
                // Get the data stream that is associated with the specified url.  
                using (Stream responseStream = response.GetResponseStream())  
                {  
                    await responseStream.CopyToAsync(content);  
                }  
            }  
  
            // Return the result as a byte array.  
            return content.ToArray();  
  
        }  
  
        private void DisplayResults(string url, byte[] content)  
        {  
            // Display the length of each website. The string format   
            // is designed to be used with a monospaced font, such as  
            // Lucida Console or Global Monospace.  
            var bytes = content.Length;  
            // Strip off the "http://".  
            var displayURL = url.Replace("http://", "");  
            resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
  
        }  
    }  
}  
```  
  
## <a name="example"></a>Esempio  
 Il codice seguente illustra le estensioni per il progetto che usa il metodo `HttpClient.GetByteArrayAsync` per scaricare il contenuto dal Web.  
  
```csharp  
// Add the following using directives, and add a reference for System.Net.Http.  
using System.Net.Http;  
using System.IO;  
using System.Net;  
  
namespace AsyncExampleWPF_HttpClient_WhenAll  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
        }  
  
        private async void startButton_Click(object sender, RoutedEventArgs e)  
        {  
            resultsTextBox.Clear();  
  
            // One-step async call.  
            await SumPageSizesAsync();  
  
            // Two-step async call.  
            //Task sumTask = SumPageSizesAsync();  
            //await sumTask;  
  
            resultsTextBox.Text += "\r\nControl returned to startButton_Click.\r\n";  
        }  
  
        private async Task SumPageSizesAsync()  
        {  
            // Make a list of web addresses.  
            List<string> urlList = SetUpURLList();  
  
            // Declare an HttpClient object and increase the buffer size. The  
            // default buffer size is 65,536.  
            HttpClient client = new HttpClient() { MaxResponseContentBufferSize = 1000000 };  
  
            // Create a query.  
            IEnumerable<Task<int>> downloadTasksQuery =   
                from url in urlList select ProcessURL(url, client);  
  
            // Use ToArray to execute the query and start the download tasks.  
            Task<int>[] downloadTasks = downloadTasksQuery.ToArray();  
  
            // You can do other work here before awaiting.  
  
            // Await the completion of all the running tasks.  
            int[] lengths = await Task.WhenAll(downloadTasks);  
  
            //// The previous line is equivalent to the following two statements.  
            //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);  
            //int[] lengths = await whenAllTask;  
  
            int total = lengths.Sum();  
  
            //var total = 0;  
            //foreach (var url in urlList)  
            //{  
            //    // GetByteArrayAsync returns a Task<T>. At completion, the task  
            //    // produces a byte array.  
            //    byte[] urlContent = await client.GetByteArrayAsync(url);  
  
            //    // The previous line abbreviates the following two assignment  
            //    // statements.  
            //    Task<byte[]> getContentTask = client.GetByteArrayAsync(url);  
            //    byte[] urlContent = await getContentTask;  
  
            //    DisplayResults(url, urlContent);  
  
            //    // Update the total.  
            //    total += urlContent.Length;  
            //}  
  
            // Display the total count for all of the web addresses.  
            resultsTextBox.Text +=  
                string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
        }  
  
        private List<string> SetUpURLList()  
        {  
            List<string> urls = new List<string>   
            {   
                "http://msdn.microsoft.com",  
                "http://msdn.microsoft.com/library/hh290136.aspx",  
                "http://msdn.microsoft.com/library/ee256749.aspx",  
                "http://msdn.microsoft.com/library/hh290138.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/dd470362.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            };  
            return urls;  
        }  
  
        // The actions from the foreach loop are moved to this async method.  
        async Task<int> ProcessURL(string url, HttpClient client)  
        {  
            byte[] byteArray = await client.GetByteArrayAsync(url);  
            DisplayResults(url, byteArray);  
            return byteArray.Length;  
        }  
  
        private void DisplayResults(string url, byte[] content)  
        {  
            // Display the length of each web site. The string format   
            // is designed to be used with a monospaced font, such as  
            // Lucida Console or Global Monospace.  
            var bytes = content.Length;  
            // Strip off the "http://".  
            var displayURL = url.Replace("http://", "");  
            resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>   
 [Procedura dettagliata: accesso al Web tramite async e await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)

