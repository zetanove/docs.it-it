---
title: "Accesso ai servizi WCF con un&#39;applicazione client Windows Store | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e2002ef4-5dee-4a54-9d87-03b33d35fc52
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Accesso ai servizi WCF con un&#39;applicazione client Windows Store
In Windows 8 è stato introdotto un nuovo tipo di applicazione denominato applicazioni Windows Store. Queste applicazioni sono progettate in base a un'interfaccia del touchscreen. .NET Framework 4.5 consente alle applicazioni Windows Store di chiamare i servizi WCF.  
  
## Supporto WCF nelle applicazioni Windows Store  
 Un subset di funzionalità WCF è disponibile in un'applicazione Windows Store. Per altre informazioni, vedere le sezioni seguenti.  
  
> [!IMPORTANT]
>  Usare le API di diffusione WinRT anziché quelle esposte da WCF. Per altre informazioni, vedere [API di diffusione WinRT](http://go.microsoft.com/fwlink/?LinkId=236265)  
  
> [!WARNING]
>  L'uso di Aggiungi riferimento al servizio per aggiungere il riferimento di un servizio Web a un componente Windows Runtime non è supportato.  
  
### Associazioni supportate  
 Nelle applicazioni Windows Store sono supportate le associazioni WCF seguenti:  
  
1.  <xref:System.ServiceModel.BasicHttpBinding>  
  
2.  <xref:System.ServiceModel.NetTcpBinding>  
  
3.  <xref:System.ServiceModel.NetHttpBinding>  
  
4.  <xref:System.ServiceModel.CustomBinding>  
  
 Nelle applicazioni Windows Store sono supportati gli elementi di associazione seguenti:  
  
1.  <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>  
  
2.  <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>  
  
3.  <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement>  
  
4.  <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>  
  
5.  <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>  
  
6.  <xref:System.ServiceModel.Channels.TcpTransportBindingElement>  
  
7.  <xref:System.ServiceModel.Channels.HttpTransportBindingElement>  
  
8.  <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
9. <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>  
  
 Sono supportate sia la codifica testo sia quella binaria. Inoltre, sono supportate tutte le modalità di trasferimento WCF. Per altre informazioni, vedere [Trasferimento dei messaggi di flusso](../../../../docs/framework/wcf/feature-details/streaming-message-transfer.md).  
  
### Aggiungi riferimento al servizio  
 Per chiamare un servizio WCF da un'applicazione Windows Store, usare la funzionalità Aggiungi riferimento al servizio di Visual Studio 2012. Si noteranno alcune modifiche di tale funzionalità quando eseguita in un'applicazione Windows Store. Innanzitutto non viene generato alcun file di configurazione. Nelle applicazioni Windows Store non vengono usati i file di configurazione, pertanto devono essere configurati nel codice. Questo codice di configurazione è disponibile nel file References.cs generato da Aggiungi riferimento al servizio. Per visualizzarlo, accertarsi di selezione "Mostra tutti i file" in Esplora soluzioni. Il file si trova nei riferimenti al servizio, quindi nei nodi Reference.svcmap del progetto. Tutte le operazioni generate per i servizi WCF in un'applicazione Windows Store saranno asincrone mediante il modello asincrono basato su attività. Per altre informazioni, vedere [Modello asincrono basato su attività](http://msdn.microsoft.com/magazine/ff959203.aspx).  
  
 Poiché la configurazione viene generata nel codice, tutte le modifiche apportate al file Reference.cs verranno sovrascritte ogni volta che il riferimento al servizio viene aggiornato. Per risolvere questa situazione, il codice di configurazione viene generato all'interno di un metodo parziale, che è possibile implementare nella classe proxy del client. Il metodo parziale viene dichiarato come riportato di seguito:  
  
```csharp  
static partial void Configure(System.ServiceModel.Description.ServiceEndpoint serviceEndpoint, System.ServiceModel.Description.ClientCredentials clientCredentials);  
  
```  
  
 È quindi possibile implementare questo metodo parziale e modificare l'associazione o l'endpoint nella classe proxy del client come segue:  
  
```csharp  
public partial class Service1Client : System.ServiceModel.ClientBase<MetroWcfClient.ServiceRefMultiEndpt.IService1>, MetroWcfClient.ServiceRefMultiEndpt.IService1 { static partial void Configure(System.ServiceModel.Description.ServiceEndpoint serviceEndpoint, System.ServiceModel.Description.ClientCredentials clientCredentials) { if (serviceEndpoint.Name == ServiceRefMultiEndpt.Service1Client.EndpointConfiguration.BasicHttpBinding_IService1.ToString()) { serviceEndpoint.Binding.SendTimeout = new System.TimeSpan(0, 1, 0); } else if (serviceEndpoint.Name == ServiceRefMultiEndpt.Service1Client.EndpointConfiguration.BasicHttpBinding_IService11.ToString()) { serviceEndpoint.Binding.SendTimeout = new System.TimeSpan(0, 1, 0); clientCredentials.UserName.UserName = "username1"; clientCredentials.UserName.Password = "password"; } else if (serviceEndpoint.Name == ServiceRefMultiEndpt.Service1Client.EndpointConfiguration.NetTcpBinding_IService1.ToString()) { serviceEndpoint.Binding.Name = "MyTcpBinding"; serviceEndpoint.Address = new System.ServiceModel.EndpointAddress("net.tcp://localhost/tcp"); } } }  
  
```  
  
### Serializzazione  
 Nelle applicazioni Windows Store sono supportati i serializzatori seguenti:  
  
1.  DataContractSerializer  
  
2.  DataContractJsonSerializer  
  
3.  XmlSerializer  
  
> [!WARNING]
>  XmlDictionaryWriter.Write \(DateTime\) consente ora di scrivere un oggetto DateTime come stringa.  
  
### Sicurezza  
 Nelle applicazioni Windows Store sono supportate le modalità di sicurezza seguenti:  
  
1.  <xref:System.ServiceModel.SecurityMode>  
  
2.  <xref:System.ServiceModel.SecurityMode>  
  
3.  <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredentials>  
  
4.  <xref:System.ServiceModel.SecurityMode.TransportCredentialOnly>  
  
 Nelle applicazioni Windows Store sono supportati i tipi di credenziali client seguenti:  
  
1.  None  
  
2.  Basic  
  
3.  Digest  
  
4.  Negotiate  
  
5.  NTLM  
  
6.  Windows  
  
7.  Username \(sicurezza del messaggio\)  
  
8.  Windows \(sicurezza del trasporto\)  
  
 Per consentire alle applicazioni Windows Store di accedere e inviare le credenziali di Windows predefinite, è necessario abilitare questa funzionalità nel file Package.appmanifest. Aprire il file e selezionare la scheda delle funzionalità, quindi scegliere le credenziali di Windows predefinite. In questo modo le applicazioni possono connettersi alle risorse Intranet che richiedono le credenziali del dominio.  
  
> [!IMPORTANT]
>  Per consentire alle applicazioni Windows Store di effettuare chiamate su più computer, è necessario abilitare un'altra funzionalità denominata "Rete casa\/lavoro". Anche questa impostazione è disponibile nella scheda delle funzionalità del file Package.appmanifest. Selezionare la casella di controllo Rete casa\/lavoro. In questo modo viene fornito l'accesso in ingresso e in uscita dell'applicazione in uso alle reti delle posizioni affidabili dell'utente come casa e lavoro. Le porte critiche in ingresso sono sempre bloccate. Per accedere ai servizi su Internet è inoltre necessario abilitare la funzionalità Internet \(client\).  
  
### Varie  
 L'uso delle classi seguenti è supportato per le applicazioni Windows Store:  
  
1.  <xref:System.ServiceModel.ChannelFactory>  
  
2.  <xref:System.ServiceModel.DuplexChannelFactory>  
  
3.  <xref:System.ServiceModel.CallbackBehaviorAttribute>  
  
### Definizione dei contratti di servizio  
 Si consiglia di definire solo operazioni del servizio asincrone mediante il modello asincrono basato su attività. In questo modo viene garantita la risposta delle applicazioni Windows Store durante la chiamata a un'operazione del servizio.  
  
> [!WARNING]
>  Sebbene non venga generata alcuna eccezione se si definisce un'operazione sincrona, è consigliabile definire solo le operazioni asincrone.  
  
### Chiamata dei servizi WCF da applicazioni Windows Store  
 Come detto in precedenza, tutte le configurazioni devono essere eseguite nel codice nel metodo GetBindingForEndpoint della classe proxy generata. La chiamata di un'operazione del servizio viene effettuata in modo analogo al metodo asincrono basato su attività, come illustrato nel seguente frammento di codice.  
  
```csharp  
void async SomeMethod() { ServiceClient proxy = new ServiceClient(); Task<T> results = await proxy.CallAsync(param1, param2); T result = results.Result; if (result.Success) { // Do something with result } }  
  
```  
  
 Si noti l'uso della parola chiave async nel metodo con cui si effettua la chiamata asincrona e la parola chiave await quando viene chiamato il metodo asincrono.  
  
## Vedere anche  
 [WCF nel blog delle app di Windows Store](http://blogs.msdn.com/b/piyushjo/archive/2011/09/22/wcf-in-win8-metro-styled-apps-absolutely-supported.aspx)   
 [Client e sicurezza di Windows Store WCF](http://blogs.msdn.com/b/piyushjo/archive/2011/10/11/calling-a-wcf-service-from-a-metro-application-adding-security.aspx)   
 [App e chiamate tra computer di Windows Store](http://blogs.msdn.com/b/piyushjo/archive/2011/10/22/calling-a-wcf-service-from-a-metro-application-cross-machine-scenario.aspx)   
 [Chiamata di un servizio WCF distribuito in Azure da un'app di Windows Store](http://blogs.msdn.com/b/piyushjo/archive/2011/10/22/calling-a-wcf-service-from-a-metro-application-cross-machine-scenario.aspx)   
 [Programmazione delle funzionalità di sicurezza di WCF](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)   
 [Associazioni](../../../../docs/framework/wcf/bindings.md)