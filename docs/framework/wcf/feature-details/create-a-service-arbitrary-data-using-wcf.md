---
title: "Procedura: creare un servizio che accetti dati arbitrari usando il modello di programmazione REST WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e566c15a-b600-4e4a-be3a-4af43e767dae
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Procedura: creare un servizio che accetti dati arbitrari usando il modello di programmazione REST WCF
Talvolta gli sviluppatori devono disporre del controllo completo sulla modalità di restituzione dei dati da un'operazione del servizio, ad esempio quando il formato dei dati restituiti da un'operazione del servizio non è supportato da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. In questo argomento viene illustrato l'uso del modello di programmazione REST di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per creare un servizio in grado di ricevere dati arbitrari.  
  
### <a name="to-implement-the-service-contract"></a>Per implementare il contratto di servizio  
  
1.  Definire il contratto di servizio. L'operazione che riceve i dati arbitrari deve avere un parametro di tipo <xref:System.IO.Stream>. Il parametro deve inoltre essere l'unico passato nel corpo della richiesta. L'operazione descritta in questo esempio accetta anche un parametro filename che viene passato nell'URL della richiesta. È possibile specificare che un parametro viene passato all'interno dell'URL specificando un <xref:System.UriTemplate> nel <xref:System.ServiceModel.Web.WebInvokeAttribute>. In questo caso l'URI usato per chiamare questo metodo termina con "UploadFile/Some-Filename". La parte "{filename}" del modello di URI specifica che il parametro filename per l'operazione viene passato nell'URI usato per chiamare l'operazione.  
  
    ```  
     [ServiceContract]  
    public interface IReceiveData  
    {  
        [WebInvoke(UriTemplate = "UploadFile/{fileName}")]  
        void UploadFile(string fileName, Stream fileContents);  
    }  
    ```  
  
2.  Implementare il contratto di servizio Il contratto dispone di un solo metodo, `UploadFile`, che riceve un file di dati arbitrari in un flusso. L'operazione legge il flusso conteggiando il numero di byte letti, quindi visualizza il nome file e il numero di byte letti.  
  
    ```  
    public class RawDataService : IReceiveData  
    {  
        public void UploadFile(string fileName, Stream fileContents)  
        {  
            byte[] buffer = new byte[10000];  
            int bytesRead, totalBytesRead = 0;  
            do  
            {  
                bytesRead = fileContents.Read(buffer, 0, buffer.Length);  
                totalBytesRead += bytesRead;  
            } while (bytesRead > 0);  
            Console.WriteLine("Service: Received file {0} with {1} bytes", fileName, totalBytesRead);  
        }  
    }  
    ```  
  
### <a name="to-host-the-service"></a>Per ospitare il servizio  
  
1.  Creare un'applicazione console per ospitare il servizio.  
  
    ```  
    class Program  
    {  
       static void Main(string[] args)  
       {  
       }  
    }  
  
    ```  
  
2.  Creare una variabile per contenere l'indirizzo di base per il servizio all'interno del metodo `Main`.  
  
    ```  
    string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
    ```  
  
3.  Creare un <xref:System.ServiceModel.ServiceHost> istanza per il servizio che specifica la classe del servizio e l'indirizzo di base.  
  
    ```  
    ServiceHost host = new ServiceHost(typeof(RawDataService), new Uri(baseAddress));  
    ```  
  
4.  Aggiungere un endpoint che specifichi il contratto, <xref:System.ServiceModel.WebHttpBinding>, e <xref:System.ServiceModel.Description.WebHttpBehavior>.  
  
    ```  
    host.AddServiceEndpoint(typeof(IReceiveData), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
    ```  
  
5.  Aprire l’host del servizio. Il servizio è ora pronto a ricevere le richieste.  
  
    ```  
    host.Open();  
    Console.WriteLine("Host opened");  
    ```  
  
### <a name="to-call-the-service-programmatically"></a>Per chiamare il servizio a livello di programmazione  
  
1.  Creare un <xref:System.Net.HttpWebRequest> con l'URI utilizzato per chiamare il servizio. Nel codice l'indirizzo di base è combinato con `“/UploadFile/Text”`. La parte `“UploadFile”` dell'URI specifica l'operazione da chiamare. La parte `“Test.txt”` dell'URI specifica il parametro filename da passare all'operazione `UploadFile`. Entrambi questi elementi vengono mappati al <xref:System.UriTemplate> applicato al contratto dell'operazione.  
  
    ```  
    HttpWebRequest req = (HttpWebRequest)HttpWebRequest.Create(baseAddress + "/UploadFile/Test.txt");  
  
    ```  
  
2.  Impostare il <xref:System.Net.HttpWebRequest.Method%2A> proprietà del <xref:System.Net.HttpWebRequest> a `POST` e <xref:System.Net.HttpWebRequest.ContentType%2A> proprietà `“text/plain”`. In questo modo si comunica al servizio che il codice sta inviando dati in formato testo normale.  
  
    ```  
    req.Method = "POST";  
    req.ContentType = "text/plain";  
    ```  
  
3.  Chiamare <xref:System.Net.HttpWebRequest.GetRequestStream%2A> per ottenere il flusso di richiesta, creare i dati da inviare, scrivere tali dati nel flusso di richiesta e chiudere il flusso.  
  
    ```  
    Stream reqStream = req.GetRequestStream();  
    byte[] fileToSend = new byte[12345];  
    for (int i = 0; i < fileToSend.Length; i++)  
       {  
           fileToSend[i] = (byte)('a' + (i % 26));  
       }  
    reqStream.Write(fileToSend, 0, fileToSend.Length);  
    reqStream.Close();  
    ```  
  
4.  Ottenere la risposta dal servizio chiamando <xref:System.Net.HttpWebRequest.GetResponse%2A> e visualizzare i dati della risposta nella console.  
  
    ```  
    HttpWebResponse resp = (HttpWebResponse)req.GetResponse();  
    Console.WriteLine("Client: Receive Response HTTP/{0} {1} {2}", resp.ProtocolVersion, (int)resp.StatusCode, resp.StatusDescription);  
  
    ```  
  
5.  Chiudere l'host del servizio.  
  
    ```  
    host.Close();  
    ```  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un elenco completo del codice per questo esempio.  
  
```  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.ServiceModel;  
using System.ServiceModel.Web;  
using System.ServiceModel.Description;  
using System.IO;  
using System.Net;  
  
namespace ReceiveRawData  
{  
    [ServiceContract]  
    public interface IReceiveData  
    {  
        [WebInvoke(UriTemplate = "UploadFile/{fileName}")]  
        void UploadFile(string fileName, Stream fileContents);  
    }  
    public class RawDataService : IReceiveData  
    {  
        public void UploadFile(string fileName, Stream fileContents)  
        {  
            byte[] buffer = new byte[10000];  
            int bytesRead, totalBytesRead = 0;  
            do  
            {  
                bytesRead = fileContents.Read(buffer, 0, buffer.Length);  
                totalBytesRead += bytesRead;  
            } while (bytesRead > 0);  
            Console.WriteLine("Service: Received file {0} with {1} bytes", fileName, totalBytesRead);  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
            ServiceHost host = new ServiceHost(typeof(RawDataService), new Uri(baseAddress));  
            host.AddServiceEndpoint(typeof(IReceiveData), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
            host.Open();  
            Console.WriteLine("Host opened");  
  
            HttpWebRequest req = (HttpWebRequest)HttpWebRequest.Create(baseAddress + "/UploadFile/Test.txt");  
            req.Method = "POST";  
            req.ContentType = "text/plain";  
            Stream reqStream = req.GetRequestStream();  
            byte[] fileToSend = new byte[12345];  
            for (int i = 0; i < fileToSend.Length; i++)  
            {  
                fileToSend[i] = (byte)('a' + (i % 26));  
            }  
            reqStream.Write(fileToSend, 0, fileToSend.Length);  
            reqStream.Close();  
            HttpWebResponse resp = (HttpWebResponse)req.GetResponse();  
            Console.WriteLine("Client: Receive Response HTTP/{0} {1} {2}", resp.ProtocolVersion, (int)resp.StatusCode, resp.StatusDescription);  
            host.Close();  
  
        }  
    }  
}  
  
```  
  
<!-- TODO: review snippet reference  [!CODE [Microsoft.Win32.RegistryKey#4](Microsoft.Win32.RegistryKey#4)]  -->  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
  
-   Durante la compilazione del codice, fare riferimento a System.ServiceModel.dll e System.ServiceModel.Web.dll.  
  
## <a name="see-also"></a>Vedere anche  
 [UriTemplate e UriTemplateTable](../../../../docs/framework/wcf/feature-details/uritemplate-and-uritemplatetable.md)   
 [Modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)   
 [Cenni preliminari sul modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)