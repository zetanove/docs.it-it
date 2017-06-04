---
title: "Duplex durevole | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e76d1a1-f3d8-4a0f-8746-4a322cdff6eb
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Duplex durevole
In questo esempio viene illustrato come impostare e configurare lo scambio durevole di messaggi duplex utilizzando le attività di messaggistica in [!INCLUDE[wf](../../../../includes/wf-md.md)].Un scambio durevole di messaggi duplex è un scambio di messaggi bidirezionale che si verifica in un lungo periodo di tempo.È possibile che la durata dello scambio di messaggi sia superiore alla durata del canale di comunicazione e alla durata in memoria delle istanze del servizio.  
  
## Dettagli dell'esempio  
 In questo esempio due servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] implementati tramite [!INCLUDE[wf2](../../../../includes/wf2-md.md)] vengono configurati per l'utilizzo di un scambio durevole di messaggi duplex.Lo scambio durevole di messaggi duplex è composto da due messaggi unidirezionali inviati tramite MSMQ e correlati utilizzando lo [scambio del contesto di .NET](http://go.microsoft.com/fwlink/?LinkID=166059).I messaggi vengono inviati tramite le attività di messaggistica <xref:System.ServiceModel.Activities.Send> e <xref:System.ServiceModel.Activities.Receive>.Lo scambio del contesto di .NET viene utilizzato per specificare l'indirizzo di callback nei messaggi inviati.Entrambi i servizi sono ospitati tramite i servizi Attivazione processo Windows \(WAS\) e sono configurati per abilitare la persistenza delle istanze dei servizi.  
  
 Il primo servizio \(Service1.xamlx\) invia una richiesta al servizio di invio \(Service2.xamlx\) per l'esecuzione di un'operazione.Al termine, per indicare che l'operazione è stata completata, Service2.xamlx restituisce una notifica a Service1.xamlx.Un'applicazione console del flusso di lavoro configura le code su cui i servizi sono in ascolto e invia il messaggio di avvio per l'attivazione di Service1.xamlx.Una volta che Service1.xamlx ha ricevuto da Service2.xamlx la notifica che l'operazione richiesta è stata completata, il risultato viene salvato da Service1.xamlx in un file XML.In attesa del messaggio di callback, Service1.xamlx salva in modo permanente lo stato dell'istanza utilizzando l'oggetto <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior> predefinito.Service2.xamlx salva in modo permanente lo stato dell'istanza come parte del completamento dell'operazione richiesta da Service1.xamlx.  
  
 Per fare in modo che venga utilizzato lo scambio del contesto di .NET su MSMQ, entrambi i servizi sono configurati per l'utilizzo di un'associazione personalizzata costituita da <xref:System.ServiceModel.Channels.ContextBindingElement> e <xref:System.ServiceModel.Channels.MsmqTransportBindingElement>.Un indirizzo di callback viene specificato con <xref:System.ServiceModel.Channels.ContextBindingElement> ed è incluso in un'intestazione del contesto di callback con tutti i messaggi inviati utilizzando un'associazione personalizzata.Nel codice seguente viene definita l'associazione personalizzata.  
  
```xml  
<configuration>  
     <system.serviceModel>  
          …  
          <bindings>  
               <customBinding>  
                    <binding name="netMsmqContextBinding">  
                         <context clientCallbackAddress="net.msmq://localhost/private/DurableDuplex/Service1.xamlx"/>  
                         <msmqTransport exactlyOnce="False">  
                              <msmqTransportSecurity msmqAuthenticationMode="None" msmqProtectionLevel="None"/>  
                         </msmqTransport>  
                    </binding>  
               </customBinding>  
          </bindings>  
          …  
     </system.serviceModel>  
</configuration>  
  
```  
  
> [!NOTE]
>  L'associazione utilizzata da questo esempio non è sicura.In caso di distribuzione dell'applicazione è necessario configurare l'associazione in base ai requisiti di sicurezza dell'applicazione stessa.  
  
> [!NOTE]
>  Le code utilizzate in questo esempio non sono transazionali.Per un esempio che illustra come configurare gli scambi di messaggi utilizzando code di transazioni di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere l'esempio [Attivazione MSMQ](../../../../docs/framework/wcf/samples/msmq-activation.md).  
  
 Per l'invio del messaggio da Service1.xamlx a Service2.xamlx viene utilizzato un endpoint client configurato con l'indirizzo di Service2.xamlx e con l'associazione personalizzata definita precedentemente.Il callback da Service2.xamlx a Service1.xamlx viene inviato utilizzando un endpoint client senza indirizzo configurato in modo esplicito, perché l'indirizzo viene rilevato dal contesto di callback inviato da Service1.xamlx.Nel codice seguente vengono definiti gli endpoint client.  
  
```xml  
<?xml version="1.0"?>  
<configuration>  
     <system.serviceModel>  
          …  
          <client>  
               <endpoint address="net.msmq://localhost/private/DurableDuplex/Service2.xamlx" binding="customBinding" bindingConfiguration="netMsmqContextBinding" contract="IDoWork"/>  
               <endpoint binding="customBinding" bindingConfiguration="netMsmqContextBinding" contract="INotify"/>  
          </client>  
          …  
     </system.serviceModel>  
</configuration>  
  
```  
  
 Nell'esempio di codice seguente vengono esposti endpoint tramite questa associazione personalizzata modificando il mapping del protocollo predefinito per gli indirizzi di base net.msmq, in modo che venga utilizzata l'associazione personalizzata.  
  
```  
<configuration>  
     <system.serviceModel>  
          <protocolMapping>  
               <add scheme="net.msmq" binding="customBinding" bindingConfiguration="netMsmqContextBinding"/>  
          </protocolMapping>  
          …  
     </system.serviceModel>  
</configuration>  
  
```  
  
 Nell'esempio di codice seguente viene abilitata la persistenza per entrambi i servizi aggiungendo agli stessi il comportamento <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> e specificando la stringa di connessione per il database di persistenza.  
  
```xml  
<?xml version="1.0"?>  
<configuration>  
    <system.serviceModel>  
          …  
          <behaviors>  
               <serviceBehaviors>  
                    <behavior>  
                         <serviceDebug includeExceptionDetailInFaults="True"/>  
                         <serviceMetadata httpGetEnabled="True"/>  
                         <sqlWorkflowInstanceStore connectionString="Data Source=.\SQLEXPRESS;Initial Catalog=DefaultSampleStore;Integrated Security=True"/>  
                    </behavior>  
               </serviceBehaviors>  
          </behaviors>  
     </system.serviceModel>  
</configuration>  
  
```  
  
## Requisiti di sistema  
 Per questo esempio sono richiesti i componenti seguenti.  
  
1.  Internet Information Services.  
  
2.  Internet Information Services \-\> Compatibilità di gestione con IIS 6.0 \-\> Compatibilità metabase di IIS e configurazione di IIS 6.0.  
  
3.  Servizi World Wide Web \-\> Funzionalità di sviluppo di applicazioni \-\> ASP.NET.  
  
4.  Microsoft Message Queuing \(MSMQ\) Server.  
  
#### Per utilizzare questo esempio  
  
1.  Impostare il database di persistenza e la directory dei risultati.  
  
    1.  Aprire un prompt dei comandi di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
    2.  Passare alla cartella di questo esempio ed eseguire Setup.cmd.  
  
2.  Impostare l'applicazione virtuale.  
  
    1.  Da un prompt dei comandi di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] registrare ASP.NET tramite il comando seguente:  
  
        ```  
        aspnet_regiis -i  
        ```  
  
    2.  Eseguire [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] con le autorizzazioni di amministratore facendo clic con il pulsante destro del mouse su [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] e scegliendo **Esegui come amministratore**.  
  
    3.  Tramite [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file DurableDuplex.sln.  
  
3.  Impostare le code del servizio:  
  
    1.  Per eseguire il client DurableDuplex, premere CTRL\+F5.  
  
    2.  Aprire la console **Gestione computer** eseguendo `Compmgmt.msc` da un prompt dei comandi.  
  
    3.  Espandere **Servizi e applicazioni**, **Accodamento messaggi**,**Code private**.  
  
    4.  Fare clic con il pulsante destro del mouse sulle code durableduplex\/service1.xamlx e durableduplex\/service2.xamlx e scegliere **Proprietà**.  
  
    5.  Selezionare la scheda **Sicurezza** e consentire le autorizzazioni **Ricevi messaggio**, **Visualizza messaggio** e **Invia messaggio** a tutti gli utenti per entrambe code.  
  
    6.  Aprire Gestione Internet Information Services \(IIS\).  
  
    7.  Passare a **Server**, **Siti**, **Sito Web predefinito**, **private**, **Duplex durevole** e selezionare **Opzioni avanzate**.  
  
    8.  Impostare **Protocolli abilitati** su **http,net.msmq**.  
  
4.  Eseguire l'esempio.  
  
    1.  Passare a http:\/\/localhost\/private\/durableduplex\/service1.xamlx e http:\/\/localhost\/private\/durableduplex\/service2.xamlx per assicurarsi che entrambi i servizi siano in esecuzione.  
  
    2.  Premere F5 per eseguire DurableDuplexClient.  
  
         Quando lo scambio durevole di messaggi duplex è completato, viene salvato un file result.xml nella cartella C:\\Inbox contenente il risultato dello scambio di messaggi.  
  
#### Per eseguire la pulizia \(facoltativo\)  
  
1.  Eseguire Cleanup.cmd.  
  
    1.  Aprire un prompt dei comandi di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
    2.  Passare alla cartella di questo esempio ed eseguire Cleanup.cmd.  
  
2.  Rimuovere l'applicazione virtuale per i servizi.  
  
    1.  Aprire Gestione Internet Information Services \(IIS\) eseguendo `Inetmgr.exe` da un prompt dei comandi.  
  
    2.  Passare al sito Web predefinito e rimuovere la directory virtuale **private**.  
  
3.  Rimuovere le code impostate per questo esempio.  
  
    1.  Aprire la console Gestione computer eseguendo `Compmgmt.msc` da un prompt dei comandi.  
  
    2.  Espandere **Servizi e applicazioni**, **Accodamento messaggi**, **Code private**.  
  
    3.  Eliminare le code durableduplex\/service1.xamlx e durableduplex\/service2.xamlx.  
  
4.  Rimuovere la directory C:\\Inbox.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Services\DurableDuplex`  
  
## Vedere anche