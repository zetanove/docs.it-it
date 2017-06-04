---
title: "Procedura: Richiedere dati con la classe WebRequest | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "download delle risorse Internet, procedura"
  - "richiesta di dati da Internet, procedura"
  - "WebRequest (classe), ricezione di dati"
  - "ricezione di dati, con la classe WebRequest"
  - "Internet, richiesta di dati"
ms.assetid: 368b8d0f-dc5e-4469-a8b8-b2adbf5dd800
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# Procedura: Richiedere dati con la classe WebRequest
La procedura riportata di seguito vengono descritti i passaggi necessari per richiedere una risorsa da un server, ad esempio, una pagina Web o da un file.  La risorsa deve essere identificata da un URI.  
  
### I dati della richiesta da un server host  
  
1.  Creare un'istanza <xref:System.Net.WebRequest> chiamando <xref:System.Net.WebRequest.Create%2A> con l'uri della risorsa.  
  
    ```csharp  
    WebRequest request = WebRequest.Create("http://www.contoso.com/");  
    ```  
  
    ```vb  
    Dim request as WebRequest = WebRequest.Create("http://www.contoso.com/")  
  
    ```  
  
    > [!NOTE]
    >  .NET Framework fornisce classi specifiche del protocollo derivate da **WebRequest** e da **WebResponse** per gli URI che iniziano con “HTTP: „, “https:'' “, " FTP: „ e “file: „.  Per accedere alle risorse mediante altri protocolli, è necessario implementare classi specifiche del protocollo che derivano da **WebRequest** e da **WebResponse**.  Per ulteriori informazioni, vedere [Programmazione di protocolli di collegamento](../../../docs/framework/network-programming/programming-pluggable-protocols.md).  
  
2.  Impostare i valori delle proprietà necessarie in **WebRequest**.  Ad esempio, attivare l'autenticazione, impostare la proprietà **Credentials** un'istanza della classe <xref:System.Net.NetworkCredential>.  
  
    ```csharp  
    request.Credentials = CredentialCache.DefaultCredentials;  
    ```  
  
    ```vb  
    request.Credentials = CredentialCache.DefaultCredentials  
    ```  
  
     Nella maggior parte dei casi, la classe **WebRequest** è sufficiente per ricevere i dati.  Tuttavia, se è necessario impostare le proprietà specifiche del protocollo, è necessario eseguire il cast al tipo **WebRequest** protocollo specifico.  Ad esempio, per accedere ad accedere a proprietà specifiche HTTP <xref:System.Net.HttpWebRequest>, eseguire il cast **WebRequest** un riferimento **HttpWebRequest**.  Le esempio di codice seguente viene illustrato come impostare la proprietà HTTP\- specifica <xref:System.Net.HttpWebRequest.UserAgent%2A>.  
  
    ```csharp  
    ((HttpWebRequest)request).UserAgent = ".NET Framework Example Client";  
    ```  
  
    ```vb  
    Ctype(request,HttpWebRequest).UserAgent = ".NET Framework Example Client"  
  
    ```  
  
3.  Per inviare la richiesta al server, chiamare <xref:System.Net.HttpWebRequest.GetResponse%2A>.  Il tipo effettivo dell'oggetto restituito **WebResponse** è determinato dalla combinazione di URI richiesto.  
  
    ```csharp  
    WebResponse response = request.GetResponse();  
    ```  
  
    ```vb  
    Dim response As WebResponse = request.GetResponse()  
  
    ```  
  
    > [!NOTE]
    >  Al termine di un oggetto <xref:System.Net.WebResponse>, è necessario chiamare il metodo <xref:System.Net.WebResponse.Close%2A>.  In alternativa, se è stato ottenuto il flusso di risposte dall'oggetto di risposta, è possibile chiudere il flusso chiamando il metodo <xref:System.IO.Stream.Close%2A?displayProperty=fullName>.  Se non si chiude la risposta o il flusso, l'applicazione può esaurirsi le connessioni al server e diventare impossibile elaborare le richieste aggiuntive.  
  
4.  È possibile accedere alle proprietà **WebResponse** o eseguire il cast **WebResponse** a un'istanza specifica del protocollo per leggere le proprietà specifiche del protocollo.  Ad esempio, per accedere ad accedere a proprietà specifiche HTTP <xref:System.Net.HttpWebResponse>, eseguire il cast **WebResponse** un riferimento **HttpWebResponse**.  Nel seguente esempio di codice seguente viene illustrato come visualizzare le informazioni sullo stato inviato con una risposta.  
  
    ```csharp  
    Console.WriteLine (((HttpWebResponse)response).StatusDescription);  
    ```  
  
    ```vb  
    Console.WriteLine(CType(response,HttpWebResponse).StatusDescription)  
    ```  
  
5.  Per ottenere il flusso che contiene i dati di risposta inviati dal server, utilizzare il metodo <xref:System.Net.HttpWebResponse.GetResponseStream%2A>**WebResponse**.  
  
    ```csharp  
    Stream dataStream = response.GetResponseStream ();  
    ```  
  
    ```vb  
    Dim dataStream As Stream = response.GetResponseStream()  
  
    ```  
  
6.  Dopo la lettura di dati dalla risposta, è necessario chiudere il flusso di risposte mediante il metodo **Stream.Close** o chiudere la risposta utilizzando il metodo **WebResponse.Close**.  Non è necessario chiamare il metodo **Close** sia nel flusso di risposte che in **WebResponse**, ma questa operazione non è danneggiato.  Chiamate **Stream.Close** di**WebResponse.Close** file alla chiusura della risposta.  
  
    ```csharp  
    response.Close();  
    ```  
  
    ```vb  
    response.Close()  
  
    ```  
  
## Esempio  
  
```csharp  
using System;  
using System.IO;  
using System.Net;  
using System.Text;  
  
namespace Examples.System.Net  
{  
    public class WebRequestGetExample  
    {  
        public static void Main ()  
        {  
            // Create a request for the URL.   
            WebRequest request = WebRequest.Create (  
              "http://www.contoso.com/default.html");  
            // If required by the server, set the credentials.  
            request.Credentials = CredentialCache.DefaultCredentials;  
            // Get the response.  
            WebResponse response = request.GetResponse ();  
            // Display the status.  
            Console.WriteLine (((HttpWebResponse)response).StatusDescription);  
            // Get the stream containing content returned by the server.  
            Stream dataStream = response.GetResponseStream ();  
            // Open the stream using a StreamReader for easy access.  
            StreamReader reader = new StreamReader (dataStream);  
            // Read the content.  
            string responseFromServer = reader.ReadToEnd ();  
            // Display the content.  
            Console.WriteLine (responseFromServer);  
            // Clean up the streams and the response.  
            reader.Close ();  
            response.Close ();  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Net  
Imports System.Text  
Namespace Examples.System.Net  
    Public Class WebRequestGetExample  
  
        Public Shared Sub Main()  
            ' Create a request for the URL.   
            Dim request As WebRequest = _  
              WebRequest.Create("http://www.contoso.com/default.html")  
            ' If required by the server, set the credentials.  
            request.Credentials = CredentialCache.DefaultCredentials  
            ' Get the response.  
            Dim response As WebResponse = request.GetResponse()  
            ' Display the status.  
            Console.WriteLine(CType(response,HttpWebResponse).StatusDescription)  
            ' Get the stream containing content returned by the server.  
            Dim dataStream As Stream = response.GetResponseStream()  
            ' Open the stream using a StreamReader for easy access.  
            Dim reader As New StreamReader(dataStream)  
            ' Read the content.  
            Dim responseFromServer As String = reader.ReadToEnd()  
            ' Display the content.  
            Console.WriteLine(responseFromServer)  
            ' Clean up the streams and the response.  
            reader.Close()  
            response.Close()  
        End Sub   
    End Class   
End Namespace  
```  
  
## Vedere anche  
 [Creazione di richieste Internet](../../../docs/framework/network-programming/creating-internet-requests.md)   
 [Uso di flussi nella rete](../../../docs/framework/network-programming/using-streams-on-the-network.md)   
 [Accesso a Internet con un proxy](../../../docs/framework/network-programming/accessing-the-internet-through-a-proxy.md)   
 [Richiesta di dati](../../../docs/framework/network-programming/requesting-data.md)   
 [Procedura: Inviare dati con la classe WebRequest](../../../docs/framework/network-programming/how-to-send-data-using-the-webrequest-class.md)