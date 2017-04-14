---
title: "Procedure consigliate per l&#39;hosting in Internet Information Services (IIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0834768e-9665-46bf-86eb-d4b09ab91af5
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# Procedure consigliate per l&#39;hosting in Internet Information Services (IIS)
In questo argomento vengono illustrate alcune procedure consigliate per l'hosting di servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
## Implementazione di servizi WCF come DLL  
 L'implementazione di un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] come DLL distribuita alla directory \\bin di un'applicazione Web consente di riutilizzare il servizio al di fuori del modello dell'applicazione Web, ad esempio in un ambiente di test in cui Internet Information Services \(IIS\) potrebbe non essere distribuito.  
  
## Host di servizi in applicazioni ospitate da IIS  
 Non utilizzare API indipendenti imperative per creare nuovi host di servizi che ascoltano sulla rete trasporti non supportati a livello nativo dall'ambiente host IIS \(ad esempio, [!INCLUDE[iis601](../../../../includes/iis601-md.md)] per ospitare servizi TCP, perché la comunicazione TCP non è supportata a livello nativo su [!INCLUDE[iis601](../../../../includes/iis601-md.md)]\).Questo approccio non è consigliato.Gli host di servizi creati in modo imperativo non sono conosciuti all'interno dell'ambiente host IIS.Il punto critico è il fatto che l'elaborazione eseguita da servizi creati in modo imperativo non viene considerata da IIS quando determina se il pool di applicazioni host è inattivo.Di conseguenza, le applicazioni con host di servizi creati in modo imperativo hanno un ambiente host IIS che elimina bruscamente i processi host IIS.  
  
## URI ed endpoint ospitati da IIS  
 Gli endpoint per un servizio ospitato da IIS devono essere configurati tramite URI \(Uniform Resource Identifier\), non tramite indirizzi assoluti.Ciò garantisce che l'indirizzo endpoint rientri nel set di indirizzi URI che appartengono all'applicazione host e assicurano che l'attivazione basata su messaggi si verifichi come previsto.  
  
## Riciclo del processo e della gestione dello stato  
 L'ambiente host IIS è ottimizzato per servizi che non mantengono lo stato locale in memoria.IIS ricicla il processo host in risposta a numerosi eventi esterni e interni, causando la perdita di qualsiasi stato volatile archiviato esclusivamente in memoria.I servizi ospitati in IIS devono archiviare il proprio stato fuori dal processo \(ad esempio, in un database\) o in una cache in memoria che può essere ricreata facilmente se si verifica un evento di riciclo dell'applicazione.  
  
> [!NOTE]
>  I protocolli utilizzati da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per l'affidabilità e la sicurezza a livello di messaggi utilizzano lo stato nella memoria volatile.Le sessioni affidabili e le sessioni di sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] potrebbero terminare in modo imprevisto a causa dei ricicli delle applicazioni.Le applicazioni ospitate da IIS che si avvalgono di questi protocolli devono dipendere da qualcosa che non sia la chiave di sessione fornita da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per correlare lo stato a livello di applicazione \(ad esempio, un costrutto a livello di applicazione o un'intestazione di correlazione personalizzata\) oppure devono disabilitare il riciclo del processo IIS per l'applicazione ospitata.  
  
## Ottimizzazione delle prestazioni in scenari di livello intermedio  
 Per ottimizzare le prestazioni in uno *scenario di livello intermedio*, un servizio che chiama altri servizi in risposta ai messaggi in ingresso, creare una volta l'istanza del client del servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nel servizio remoto e riutilizzarla in più richieste in entrata.La creazione di un'istanza dei client del servizio di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è un'operazione dispendiosa per quanto riguarda l'esecuzione di una chiamata del servizio su un'istanza client preesistente e gli scenari di livello intermedio offrono notevoli vantaggi a livello di prestazioni memorizzando nella cache i client remoti tra le richieste.I client del servizio di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono thread\-safe, pertanto non è necessario sincronizzare l'accesso a un client su più thread.  
  
 Gli scenari di livello intermedio offrono vantaggi a livello di prestazioni anche utilizzando le API asincrone generate dall'opzione `svcutil /a`.L'opzione `/a` fa sì che [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) generi metodi `BeginXXX/EndXXX` per ogni operazione del servizio, il che consente di eseguire su thread in background chiamate potenzialmente di lunga durata a servizi remoti.  
  
## WCF in scenari multihomed o con nomi multipli  
 È possibile distribuire servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] all'interno di una Web farm IIS, in cui un set di computer condividono un nome esterno comune \(ad esempio http:\/\/www.contoso.com\) ma sono indirizzati individualmente tramite nomi host diversi \(ad esempio, http:\/\/www.contoso.com potrebbe indirizzare il traffico a due computer diversi denominati http:\/\/machine1.internal.contoso.com e http:\/\/machine2.internal.contoso.com\).Questo scenario di distribuzione è supportato pienamente da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ma richiede la configurazione speciale del sito Web IIS che ospita servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per visualizzare il nome host corretto \(esterno\) nei metadati del servizio \(Web Services Description Language\).  
  
 Per assicurare che nei metadati del servizio generati da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] venga visualizzato il nome host corretto, configurare l'identità predefinita per il sito Web IIS che ospita servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in modo che venga utilizzato un nome host esplicito.I computer che risiedono all'interno della farm www.contoso.com, ad esempio, devono utilizzare un'associazione del sito IIS di \*:80:www.contoso.com per HTTP e \*:443:www.contoso.com per HTTPS.  
  
 È possibile configurare le associazioni del sito Web IIS utilizzando lo snap\-in IIS Microsoft Management Console \(MMC\).  
  
## I pool di applicazioni che sono in esecuzione in contesti utente diversi sovrascrivono gli assembly da altri account nella cartella temporanea  
 Per assicurare che i pool di applicazioni in esecuzione in contesti utente diversi non possano sovrascrivere gli assembly da altri account nella cartella temporanea dei file [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], utilizzare identità diverse e cartelle temporanee per le diverse applicazioni.Se si hanno, ad esempio, due applicazioni virtuali \/Application1 e \/ Application2, è possibile creare due pool Application, A e B, con due identità diverse.Il pool dell'applicazione A può essere eseguito sotto un'identità utente \(user1\) mentre il pool dell'applicazione B può essere eseguito sotto un'altra identità utente \(user2\). Configurare inoltre \/Application1 in modo che utilizzi A e \/Application2 in modo che utilizzi B.  
  
 In Web.config è possibile configurare la cartella temporanea utilizzando \<system.web\/compilation\/@tempFolder\>.Per \/Application1, può essere "c:\\tempForUser1" e per application2 può essere "c:\\tempForUser2".Concedere a queste due cartelle l'autorizzazione di scrittura corrispondente per le due identità.  
  
 Di conseguenza, user2 non può modificare la cartella di generazione del codice per \/application2 \(sotto c:\\tempForUser1\).  
  
## Abilitazione dell'elaborazione asincrona  
 Per impostazione predefinita, i messaggi inviati a un servizio di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitato in IIS 6.0 o versioni precedenti vengono processati in modo sincrono.In ASP.NET viene eseguita una chiamata a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nel relativo thread, vale a dire quello di lavoro di ASP.NET, e in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene utilizzato un altro thread per elaborare la richiesta.Poiché il thread di lavoro di ASP.NET viene mantenuto in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fino al completamento dell'elaborazione,le richieste vengono elaborate in modo sincrono.L'elaborazione asincrona delle richieste consente una scalabilità maggiore poiché riduce il numero di thread necessari per l'elaborazione stessa. In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] infatti non viene mantenuto il thread ASP.NET durante l'elaborazione della richiesta.L'utilizzo della modalità asincrona non è consigliato per computer che eseguono IIS 6.0 poiché non è possibile limitare le richieste in ingresso che espongono il server ad attacchi *Denial Of Service* \(DOS\).A partire da IIS 7.0, è stato introdotto un limite al numero di richieste simultanee, ovvero `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\2.0.50727.0]“MaxConcurrentRequestsPerCpu`.Grazie a questo nuovo limite, è possibile utilizzare l'elaborazione asincrona in modo sicuro.Per impostazione predefinita, in IIS 7.0 il gestore asincrono e il modulo sono registrati.Se l'elaborazione asincrona di richieste è stata disattivata, è possibile abilitarla manualmente nel file Web.config dell'applicazione.Le impostazioni da utilizzare dipendono dall'impostazione `aspNetCompatibilityEnabled`.Se `aspNetCompatibilityEnabled` è impostato su `false`, configurare <xref:System.ServiceModel.Activation.ServiceHttpModule> come illustrato nel frammento di configurazione seguente.  
  
```  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="false" />      
  </system.serviceModel>  
  <system.webServer>  
    <modules>  
      <remove name="ServiceModel"/>  
      <add name="ServiceModel"   
           preCondition="integratedMode,runtimeVersionv2.0"   
           type="System.ServiceModel.Activation.ServiceHttpModule, System.ServiceModel,Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>  
    </modules>  
    </system.webServer>  
  
```  
  
 Se `aspNetCompatibilityEnabled` è impostato su `true`, configurare <xref:System.ServiceModel.Activation.ServiceHttpHandlerFactory> come illustrato nel frammento di configurazione seguente.  
  
```  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true" />      
  </system.serviceModel>  
  <system.webServer>  
    <handlers>  
          <clear/>  
          <add name="TestAsyncHttpHandler"   
               path="*.svc"   
               verb="*"   
               type="System.ServiceModel.Activation.ServiceHttpHandlerFactory, System.ServiceModel, Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"           
               />  
    </handlers>      
  </system.webServer>  
  
```  
  
## Vedere anche  
 [Service Hosting Samples](http://msdn.microsoft.com/it-it/f703a3f6-0fba-418a-a92f-7ce75ccfa47e)   
 [Funzionalità di hosting di AppFabric](http://go.microsoft.com/fwlink/?LinkId=201276)