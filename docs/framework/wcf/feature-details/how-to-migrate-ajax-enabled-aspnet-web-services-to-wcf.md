---
title: "Procedura: eseguire la migrazione di servizi Web ASP.NET compatibili AJAX a WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1428df4d-b18f-4e6d-bd4d-79ab3dd5147c
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Procedura: eseguire la migrazione di servizi Web ASP.NET compatibili AJAX a WCF
In questo argomento vengono illustrate le procedure per eseguire la migrazione di un servizio ASP.NET AJAX di base a un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] compatibile AJAX equivalente.  Verrà descritto come creare una versione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] funzionalmente equivalente a un servizio ASP.NET.AJAX.  I due servizi possono quindi essere utilizzati in modo affiancato, oppure il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può essere utilizzato al posto del servizio ASP.NET.AJAX.  
  
 La migrazione di un servizio ASP.NET.AJAX esistente in un servizio AJAX [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] offre i vantaggi seguenti:  
  
-   È possibile esporre il servizio AJAX come servizio SOAP tramite una minima configurazione aggiuntiva.  
  
-   Sarà possibile usufruire delle funzionalità di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] quali la traccia e così via.  
  
 Ai fini delle procedure seguenti si presuppone che venga utilizzato [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
 Il codice generato dalle procedure descritte in questo argomento viene fornito nell'esempio riportato dopo le procedure stesse.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'esposizione di un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tramite un endpoint compatibile con AJAX, vedere l'argomento [Procedura: aggiungere un endpoint ASP.NET AJAX con l'utilizzo della configurazione](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md).  
  
### Per creare e testare l'applicazione del servizio Web ASP.NET  
  
1.  Aprire [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  Scegliere **Nuovo** dal menu **File**, quindi **Progetto**, **Web** e infine **Applicazione servizio Web ASP.NET**.  
  
3.  Assegnare al progetto il nome `ASPHello`, quindi fare clic su **OK**.  
  
4.  Rimuovere il commento dalla riga nel file Service1.asmx.cs che contiene `System.Web.Script.Services.ScriptService]` per abilitare AJAX per questo servizio.  
  
5.  Scegliere **Compila soluzione** dal menu **Compila**.  
  
6.  Scegliere **Avvia senza eseguire debug** dal menu **Debug**.  
  
7.  Nella pagina Web generata, selezionare l'operazione `HelloWorld`.  
  
8.  Fare clic sul pulsante **Richiama** nella pagina di prova di `HelloWorld`.  Si dovrebbe ricevere la risposta XML seguente:  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <string xmlns="http://tempuri.org/">Hello World</string>  
    ```  
  
9. Questa risposta conferma che si dispone di un servizio ASP.NET.AJAX funzionante e, in particolare, che il servizio ha esposto un endpoint su Service1.asmx\/HelloWorld che risponde alle richieste HTTP POST e restituisce XML.  
  
     È ora possibile convertire il servizio per utilizzare un servizio AJAX [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
### Per creare un'applicazione di servizio AJAX WCF equivalente  
  
1.  Fare clic con il pulsante destro del mouse sul progetto **ASPHello** e scegliere **Aggiungi**, quindi **Nuovo elemento** e infine **Sevizio WCF compatibile AJAX**.  
  
2.  Assegnare al servizio il nome `WCFHello`, quindi fare clic su **Aggiungi**.  
  
3.  Aprire il file WCFHello.svc.cs.  
  
4.  Da Service1.asmx.cs, copiare l'implementazione seguente dell'operazione `HelloWorld`.  
  
    ```  
    public string HelloWorld()  
    {  
         return "Hello World";  
    }  
    ```  
  
5.  Incollare l'implementazione copiata dell'operazione `HelloWorld` nel file WCFHello.svc.cs al posto del codice seguente.  
  
    ```  
    public void DoWork()  
    {  
          // Add your operation implementation here  
          return;  
    }  
    ```  
  
6.  Specificare l'attributo `Namespace` per <xref:System.ServiceModel.ServiceContractAttribute> come `WCFHello`.  
  
    ```  
    [ServiceContract(Namespace="WCFHello")]  
    [AspNetCompatibilityRequirements(RequirementsMode=AspNetCompatibilityRequirementsMode.Required)]  
    public class WCFHello  
    { … }  
    ```  
  
7.  Aggiungere <xref:System.ServiceModel.Web.WebInvokeAttribute> all'operazione `HelloWorld` e impostare la proprietà <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A> affinché restituisca <xref:System.ServiceModel.Web.WebMessageFormat>.  Se non impostato, il tipo restituito predefinito è <xref:System.ServiceModel.Web.WebMessageFormat>.  
  
    ```  
    [OperationContract]  
    [WebInvoke(ResponseFormat=WebMessageFormat.Xml)]  
    public string HelloWorld()  
    {  
        return "Hello World";  
    }  
    ```  
  
8.  Scegliere **Compila soluzione** dal menu **Compila**.  
  
9. Aprire il file WCFHello.svc e selezionare **Avvia senza eseguire debug** dal menu **Debug**.  
  
10. Il servizio esporrà un endpoint su `WCFHello.svc/HelloWorld`, che risponde alle richieste HTTP POST.  Le richieste HTTP POST non possono essere sottoposte a test dal browser, ma l'endpoint restituisce l'XML seguente.  
  
    ```  
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Hello World</string>  
    ```  
  
11. `WCFHello.svc/HelloWorld` e gli endpoint `Service1.aspx/HelloWorld` sono ora funzionalmente equivalenti.  
  
## Esempio  
 Il codice che scaturisce dalle procedure descritte in questo argomento viene fornito nell'esempio seguente.  
  
```  
//This is the ASP.NET code in the Service1.asmx.cs file.  
  
using System;  
using System.Collections;  
using System.ComponentModel;  
using System.Data;  
using System.Linq;  
using System.Web;  
using System.Web.Services;  
using System.Web.Services.Protocols;  
using System.Xml.Linq;  
using System.Web.Script.Services;  
  
namespace ASPHello  
{  
    /// <summary>  
    /// Summary description for Service1.  
    /// </summary>  
    [WebService(Namespace = "http://tempuri.org/")]  
    [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]  
    [ToolboxItem(false)]  
    // To allow this Web Service to be called from script, using ASP.NET AJAX, uncomment the following line.   
    [System.Web.Script.Services.ScriptService]  
    public class Service1 : System.Web.Services.WebService  
    {  
  
        [WebMethod]  
        public string HelloWorld()  
        {  
            return "Hello World";  
        }  
    }  
}   
  
//This is the WCF code in the WCFHello.svc.cs file.  
using System;  
using System.Linq;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Activation;  
using System.ServiceModel.Web;  
  
namespace ASPHello  
{  
    [ServiceContract(Namespace = "WCFHello")]  
    [AspNetCompatibilityRequirements(RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]  
    public class WCFHello  
    {  
        // Add [WebInvoke] attribute to use HTTP GET.  
        [OperationContract]  
        [WebInvoke(ResponseFormat=WebMessageFormat.Xml)]  
        public string HelloWorld()  
        {  
            return "Hello World";  
        }  
  
        // Add more operations here and mark them with [OperationContract].  
    }  
}  
```  
  
 Il tipo <xref:System.Xml.XmlDocument> non è supportato da <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> perché non è serializzabile mediante <xref:System.Xml.Serialization.XmlSerializer>.  È possibile utilizzare un tipo <xref:System.Xml.Linq.XDocument> oppure serializzare <xref:System.Xml.XmlDocument.DocumentElement%2A>.  
  
 Se l'aggiornamento\/migrazione dei servizi Web ASMX vengono eseguiti side\-by\-side ai servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], evitare di eseguire il mapping di due tipi allo stesso nome sul client.  Se viene utilizzato lo stesso tipo sia in un <xref:System.Web.Services.WebMethodAttribute> che in un <xref:System.ServiceModel.ServiceContractAttribute>, nei serializzatori verrà generata un'eccezione:  
  
-   Se viene aggiunto per primo un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], la chiamata del metodo sul servizio Web ASMX provoca un'eccezione in <xref:System.Web.UI.ObjectConverter.ConvertValue%28System.Object%2CSystem.Type%2CSystem.String%29> perché la definizione di stile di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] dell'ordine nel proxy ha la precedenza.  
  
-   Se viene aggiunto per primo un servizio Web ASMX, la chiamata del metodo sul servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] provoca un'eccezione in <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> perché la definizione di stile del servizio Web dell'ordine nel proxy ha la precedenza.  
  
 Esistono differenze significative di comportamento tra <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> e <xref:System.Web.Script.Serialization.JavascriptSerializer> ASP.NET AJAX.  <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>, ad esempio, rappresenta un dizionario come una matrice di coppie chiave\/valore, mentre ASP.NET AJAX <xref:System.Web.Script.Serialization.JavascriptSerializer> rappresenta un dizionario come oggetti JSON effettivi.  Pertanto quello seguente è il dizionario rappresentato in ASP.NET AJAX.  
  
```  
Dictionary<string, int> d = new Dictionary<string, int>();  
d.Add(“one”, 1);  
d.Add(“two”, 2);  
```  
  
 Tale dizionario è rappresentato negli oggetti JSON come mostrato nell'elenco seguente:  
  
-   \[{"Key":"one","Value":1},{"Key":"two","Value":2}\] da <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>  
  
-   {“one”:1,”two”:2} da <xref:System.Web.Script.Serialization.JavascriptSerializer> ASP.NET AJAX.  
  
 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> è più potente perché può gestire dizionari in cui il tipo di chiave non è una stringa, mentre <xref:System.Web.Script.Serialization.JavascriptSerializer> non è in grado di farlo.  Quest'ultimo, tuttavia, è più favorevole a JSON.  
  
 Le differenze significative tra questi serializzatori sono riepilogate nella tabella seguente.  
  
|Categoria delle differenze|DataContractJsonSerializer|JavaScriptSerializer per ASP.NET AJAX|  
|--------------------------------|--------------------------------|-------------------------------------------|  
|Deserializzazione del buffer vuoto \(new byte\[0\]\) in <xref:System.Object> \(o <xref:System.Uri> o alcune altre classi\).|SerializationException|Null|  
|Serializzazione di <xref:System.DBNull.Value>|{} \(o {"\_\_type":"\#System"}\)|Null|  
|Serializzazione dei membri privati di tipi \[Serializable\].|serializzato|non serializzato|  
|Serializzazione delle proprietà pubbliche di tipi <xref:System.Runtime.Serialization.ISerializable>.|non serializzato|serializzato|  
|"Estensioni" di JSON|È conforme alla specifica JSON, che richiede le virgolette per i nomi dei membri di un oggetto \({"a":"hello"}\).|Supporta i nomi dei membri di un oggetto senza virgolette \({a:"hello"}\).|  
|Ora UTC \(Coordinated Universal Time\) <xref:System.DateTime>|Non supporta il formato "\\\/Date\(123456789U\)\\\/" o "\\\/Date\\\(\\d\+\(U&#124;\(\\\+\\\-\[\\d{4}\]\)\)?  \\\)\\\\\/\)".|Supporta i formati "\\\/Date\(123456789U\)\\\/" e "\\\/Date\\\(\\d\+\(U&#124;\(\\\+\\\-\[\\d{4}\]\)\)?  \\\)\\\\\/\)" come valori DateTime.|  
|Rappresentazione di dizionari|Una matrice di KeyValuePair\<K, V\>, gestisce tipi di chiave che non sono stringhe.|Come gli oggetti JSON effettivi, ma gestisce solo i tipi di chiave che sono stringhe.|  
|Caratteri di escape|Sempre con un carattere di escape barra \(\/\); non consente mai caratteri JSON non validi senza carattere di escape, ad esempio "\\n".|Con un carattere di escape barra \(\/\) per i valori DateTime.|  
  
## Vedere anche  
 [Procedura: aggiungere un endpoint ASP.NET AJAX con l'utilizzo della configurazione](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)