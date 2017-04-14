---
title: "Uso di flussi nella rete | Microsoft Docs"
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
  - "richiesta di dati da Internet, flussi"
  - "Servizi di rete"
  - "risposta a richiesta Internet, flussi"
  - "risorse di rete, funzionalità di flusso"
  - "ricezione di dati, funzionalità di flusso"
  - "Risorse di rete"
  - "invio di dati, funzionalità di flusso"
  - "download delle risorse Internet, flussi"
  - "flussi, funzionalità"
  - "Internet, flussi"
  - "flussi"
ms.assetid: 02b05fba-7235-45ce-94e5-060436ee0875
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Uso di flussi nella rete
Le risorse di rete sono rappresentate in .NET Framework come flusso.  Considerare i flussi genere, .NET Framework offre le funzionalità seguenti:  
  
-   Un metodo comune per inviare e ricevere i dati Web.  Qualsiasi l'effettivo contenuto del file — HTML, XML, o qualsiasi altro elemento — l'applicazione utilizzerà <xref:System.IO.Stream.Write%2A?displayProperty=fullName> e <xref:System.IO.Stream.Read%2A?displayProperty=fullName> per inviare e ricevere i dati.  
  
-   Compatibilità con i flussi tramite .NET Framework.  I flussi vengono utilizzati in.NET Framework, che include un'infrastruttura dettagliata per gestirli.  Ad esempio, è possibile modificare un'applicazione che legge i dati XML da <xref:System.IO.FileStream> per leggere i dati da <xref:System.Net.Sockets.NetworkStream> anziché modificando solo le poche righe di codice che consentono di inizializzare il flusso.  Le principali differenze tra la classe **NetworkStream** e altri flussi in **NetworkStream** non è seekable, la proprietà <xref:System.Net.Sockets.NetworkStream.CanSeek%2A> restituisce sempre **false**e i metodi <xref:System.Net.Sockets.NetworkStream.Position%2A> e <xref:System.Net.Sockets.NetworkStream.Seek%2A> generano <xref:System.NotSupportedException>.  
  
-   Elaborazione di dati come arrivo.  I flussi forniscono accesso ai dati quando arriva dalla rete, anziché forzare l'applicazione attendere un intero set di dati da scaricare.  
  
 Lo spazio dei nomi <xref:System.Net.Sockets> contiene una classe **NetworkStream** che implementa la classe <xref:System.IO.Stream> in modo specifico per l'utilizzo con le risorse di rete.  Le classi nello spazio dei nomi <xref:System.Net.Sockets> utilizzare la classe **NetworkStream** per rappresentare i flussi.  
  
 Per inviare i dati alla rete utilizzando il flusso restituito, chiamare <xref:System.Net.WebRequest.GetRequestStream%2A> nel <xref:System.Net.WebRequest>.  **WebRequest** invierà le intestazioni di richiesta al server; è quindi possibile inviare dati alla risorsa di rete chiamando <xref:System.IO.Stream.BeginWrite%2A>, <xref:System.IO.Stream.EndWrite%2A>il metodo, o <xref:System.IO.Stream.Write%2A> nel flusso restituito.  Alcuni protocolli, ad esempio HTTP, può essere necessario impostare le proprietà specifiche del protocollo inviare dati.  Le esempio di codice seguente viene illustrato come impostare le proprietà HTTP\- specifiche per inviare i dati.  Si presuppone che `sendData` variabile contenga dati per l'invio e che `sendLength` variabile è il numero di byte dei dati da inviare.  
  
```csharp  
HttpWebRequest request =   
   (HttpWebRequest) WebRequest.Create("http://www.contoso.com/");  
request.Method = "POST";  
request.ContentLength = sendLength;  
try  
{  
   Stream sendStream = request.GetRequestStream();  
   sendStream.Write(sendData,0,sendLength);  
   sendStream.Close();  
}  
catch  
{  
   // Handle errors . . .  
}  
  
```  
  
```vb  
Dim request As HttpWebRequest = _  
   CType(WebRequest.Create("http://www.contoso.com/"), HttpWebRequest)  
request.Method = "POST"  
request.ContentLength = sendLength  
Try  
   Dim sendStream As Stream = request.GetRequestStream()  
   sendStream.Write(sendData, 0, sendLength)  
   sendStream.Close()  
Catch  
   ' Handle errors . . .  
End Try  
```  
  
 Per ricevere i dati dalla rete, chiamare <xref:System.Net.WebResponse.GetResponseStream%2A> nel <xref:System.Net.WebResponse>.  È quindi possibile leggere i dati dalla risorsa di rete chiamando <xref:System.IO.Stream.BeginRead%2A>, <xref:System.IO.Stream.EndRead%2A>il metodo, o <xref:System.IO.Stream.Read%2A> nel flusso restituito.  
  
 Nei flussi dalle risorse di rete, tenere presente i seguenti punti:  
  
-   La proprietà **CanSeek** restituisce sempre **false** poiché la classe **NetworkStream** non può modificare la posizione nel flusso.  i metodi **Position** e **Seek** generano **NotSupportedException**.  
  
-   Quando si utilizza **WebRequest** e **WebResponse**, le istanze del flusso creato chiamando **GetResponseStream** sono di sola lettura e le istanze del flusso creato chiamando **GetRequestStream** sono di sola scrittura.  
  
-   Utilizzare la classe <xref:System.IO.StreamReader> per rendere il codice più semplice.  Nell'esempio di codice riportato **StreamReader** per leggere un flusso ASCII\- codificato **WebResponse** nell'esempio non viene mostrata la richiesta\).  
  
-   La chiamata a **GetResponse** può bloccare se le risorse di rete non sono disponibili.  È necessario utilizzare una richiesta asincrona con i metodi <xref:System.Net.WebRequest.EndGetResponse%2A> e <xref:System.Net.WebRequest.BeginGetResponse%2A>.  
  
-   La chiamata a **GetRequestStream** può bloccarsi mentre la connessione al server viene creata.  È necessario utilizzare una richiesta asincrona del flusso dei metodi <xref:System.Net.WebRequest.EndGetRequestStream%2A> e <xref:System.Net.WebRequest.BeginGetRequestStream%2A>.  
  
```csharp  
// Create a response object.  
WebResponse response = request.GetResponse();  
// Get a readable stream from the server.  
StreamReader sr =   
   new StreamReader(response.GetResponseStream(), Encoding.ASCII);  
// Use the stream. Remember when you are through with the stream to close it.  
sr.Close();  
```  
  
```vb  
' Create a response object.  
Dim response As WebResponse = request.GetResponse()  
' Get a readable stream from the server.  
Dim sr As _   
   New StreamReader(response.GetResponseStream(), Encoding.ASCII)  
' Use the stream. Remember when you are through with the stream to close it.  
sr.Close()  
```  
  
## Vedere anche  
 [Procedura: Richiedere dati con la classe WebRequest](../../../docs/framework/network-programming/how-to-request-data-using-the-webrequest-class.md)   
 [Richiesta di dati](../../../docs/framework/network-programming/requesting-data.md)