---
title: "Configurazione del rilevamento per un flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 905adcc9-30a0-4918-acd6-563f86db988a
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# Configurazione del rilevamento per un flusso di lavoro
Un flusso di lavoro può essere eseguito in tre modi:  
  
-   Ospitato nell'oggetto <xref:System.ServiceModel.Activities.WorkflowServiceHost>  
  
-   Eseguito come un oggetto <xref:System.Activities.WorkflowApplication>  
  
-   Eseguito direttamente usando l'oggetto <xref:System.Activities.WorkflowInvoker>  
  
 A seconda dell'opzione di hosting del flusso di lavoro, un partecipante del rilevamento può essere aggiunto tramite codice o un file di configurazione.  In questo argomento viene descritta la configurazione del rilevamento tramite l'aggiunta di un partecipante del rilevamento agli oggetti <xref:System.Activities.WorkflowApplication> e <xref:System.ServiceModel.Activities.WorkflowServiceHost> e viene illustrato come abilitare il rilevamento quando si usa l'oggetto <xref:System.Activities.WorkflowInvoker>.  
  
## Configurazione del rilevamento dell'applicazione flusso di lavoro  
 Un flusso di lavoro può essere eseguito usando la classe <xref:System.Activities.WorkflowApplication>.  In questo argomento viene illustrata la configurazione del rilevamento per un'applicazione flusso di lavoro di [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] tramite l'aggiunta di un partecipante del rilevamento all'host del flusso di lavoro <xref:System.Activities.WorkflowApplication>.  In questo caso, il flusso di lavoro viene eseguito come un'applicazione flusso di lavoro.  Quest'ultima viene configurata tramite codice \(anziché tramite un file di configurazione\), ovvero un file con estensione exe indipendente che usa la classe <xref:System.Activities.WorkflowApplication>.  Il partecipante del rilevamento viene aggiunto come estensione all'istanza <xref:System.Activities.WorkflowApplication>.  Tale operazione viene eseguita aggiungendo l'oggetto <xref:System.Activities.Tracking.TrackingParticipant> alla raccolta di estensioni per l'istanza WorkflowApplication.  
  
 Per un'applicazione flusso di lavoro, è possibile aggiungere l'estensione di comportamento <xref:System.Activities.Tracking.EtwTrackingParticipant> come mostrato nel codice seguente.  
  
```csharp  
LogActivity activity = new LogActivity();  
  
WorkflowApplication instance = new WorkflowApplication(activity);  
EtwTrackingParticipant trackingParticipant =  
    new EtwTrackingParticipant  
{  
  
        TrackingProfile = new TrackingProfile  
           {  
               Name = "SampleTrackingProfile",  
               ActivityDefinitionId = "ProcessOrder",  
               Queries = new WorkflowInstanceQuery  
               {  
                  States = { "*" }  
              }  
          }  
       };  
instance.Extensions.Add(trackingParticipant);  
  
```  
  
### Configurazione del rilevamento del servizio del flusso di lavoro  
 Un flusso di lavoro può essere esposto come servizio di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] nell'host del servizio <xref:System.ServiceModel.Activities.WorkflowServiceHost>.  <xref:System.ServiceModel.Activities.WorkflowServiceHost> è un'implementazione specifica di .NET ServiceHost per un servizio basato sul flusso di lavoro.  Contenuto della sezione viene illustrato come configurare il rilevamento per un servizio flusso di lavoro di [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] in esecuzione nell'oggetto <xref:System.ServiceModel.Activities.WorkflowServiceHost>.  Viene configurato tramite un file Web.config \(per un servizio ospitato sul Web\) o un file App.config \(per un servizio ospitato in un'applicazione autonoma, ad esempio un'applicazione console\) specificando un comportamento del servizio oppure, tramite codice, aggiungendo un comportamento specifico del rilevamento alla raccolta <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> per l'host del servizio.  
  
 Per un servizio del flusso di lavoro ospitato nell'oggetto <xref:System.ServiceModel.WorkflowServiceHost>, è possibile aggiungere l'oggetto <xref:System.Activities.Tracking.EtwTrackingParticipant> usando l'elemento \<`behavior`\> in un file di configurazione, come mostrato nell'esempio seguente.  
  
```  
  
<behaviors>  
   <serviceBehaviors>  
        <behavior>  
          <etwTracking profileName="Sample Tracking Profile" />  
        </behavior>              
   </serviceBehaviors>  
<behaviors>  
  
```  
  
 In alternativa, per un servizio del flusso di lavoro ospitato nell'oggetto <xref:System.ServiceModel.WorkflowServiceHost>, è possibile aggiungere l'estensione di comportamento <xref:System.Activities.Tracking.EtwTrackingParticipant> tramite il codice.  Per aggiungere un partecipante del rilevamento personalizzato, creare una nuova estensione di comportamento e aggiungerla all'oggetto <xref:System.ServiceModel.ServiceHost> come mostrato nel codice di esempio seguente.  
  
> [!NOTE]
>  Se si desidera visualizzare il codice di esempio in cui viene illustrato come creare un elemento del comportamento personalizzato che aggiunge un partecipante del rilevamento personalizzato, fare riferimento agli esempi di [Rilevamento](../../../docs/framework/windows-workflow-foundation/samples/tracking.md).  
  
```  
ServiceHost svcHost = new ServiceHost(typeof(WorkflowService), new   
                                 Uri("http://localhost:8001/Sample"));  
EtwTrackingBehavior trackingBehavior =   
    new EtwTrackingBehavior  
    {  
        ProfileName = "Sample Tracking Profile"  
    };  
svcHost.Description.Behaviors.Add(trackingBehavior);  
svcHost.Open();  
  
```  
  
 Il partecipante del rilevamento viene aggiunto all'host del servizio del flusso di lavoro come estensione al comportamento.  
  
 Nel codice di esempio seguente viene mostrato come leggere un profilo di rilevamento dal file di configurazione.  
  
```  
TrackingProfile GetProfile(string profileName, string displayName)  
        {  
            TrackingProfile trackingProfile = null;  
            TrackingSection trackingSection = (TrackingSection)WebConfigurationManager.GetSection("system.serviceModel/tracking");  
            if (trackingSection == null)   
            {  
                return null;  
            }  
  
            if (profileName == null)   
            {  
                profileName = "";  
            }  
  
            //Find the profile with the specified profile name in the list of profile found in config  
            var match = from p in new List<TrackingProfile>(trackingSection.TrackingProfiles)  
                        where (p.Name == profileName) && ((p.ActivityDefinitionId == displayName) || (p.ActivityDefinitionId == "*"))  
                        select p;  
  
            if (match.Count() == 0)  
            {  
                //return an empty profile  
                trackingProfile = new TrackingProfile()  
                {  
                    ActivityDefinitionId = displayName  
                };  
  
            }  
            else  
            {  
                trackingProfile = match.First();  
            }  
  
            return trackingProfile;  
  
```  
  
 In questo codice di esempio viene illustrato come aggiungere un profilo di rilevamento a un host del flusso di lavoro.  
  
```  
WorkflowServiceHost workflowServiceHost = serviceHostBase as WorkflowServiceHost;  
if (null != workflowServiceHost)  
{  
              string workflowDisplayName = workflowServiceHost.Activity.DisplayName;  
               TrackingProfile trackingProfile = GetProfile(this.profileName, workflowDisplayName);  
                workflowServiceHost.WorkflowExtensions.Add(()  => new EtwTrackingParticipant  {  
               TrackingProfile = trackingProfile  
                        });  
 }  
```  
  
> [!NOTE]
>  Per altre informazioni sui profili di rilevamento, vedere [Profili di rilevamento](http://go.microsoft.com/fwlink/?LinkId=201310).  
  
### Configurazione del rilevamento tramite WorkflowInvoker  
 Per configurare il rilevamento per un flusso di lavoro eseguito usando l'oggetto <xref:System.Activities.WorkflowInvoker>, aggiungere il provider del rilevamento come estensione a un'istanza <xref:System.Activities.WorkflowInvoker>.  Il codice di esempio seguente proviene dall'esempio [Rilevamento personalizzato](../../../docs/framework/windows-workflow-foundation/samples/custom-tracking.md).  
  
```  
WorkflowInvoker invoker = new WorkflowInvoker(BuildSampleWorkflow());  
invoker.Extensions.Add(customTrackingParticipant);  
invoker.Invoke();  
  
```  
  
### Visualizzazione dei record di rilevamento in Visualizzatore eventi  
 Esistono due log del Visualizzatore eventi di particolare interesse per il rilevamento dell'esecuzione di WF: il log analitico e il log debug.  Entrambi i log sono disponibili sotto il nodo Microsoft&#124;Windows&#124;Server applicazioni\-Applicazioni.  I log presenti in questa sezione contengono gli eventi relativi una singola applicazione piuttosto che gli eventi che interessano l'intero sistema.  
  
 Gli eventi di traccia di debug vengono scritti nel log di debug.  Per raccogliere gli eventi di traccia di debug di WF nel Visualizzatore eventi, abilitare il log di debug.  
  
1.  Per aprire Visualizzatore eventi, fare clic su **Start**, quindi su **Esegui**. Nella finestra di dialogo Esegui, digitare `eventvwr`.  
  
2.  Nella finestra di dialogo Visualizzatore eventi, espandere il nodo **Registri applicazioni e servizi**.  
  
3.  Espandere i nodi **Microsoft**, **Windows** e **Server applicazioni\-Applicazioni**.  
  
4.  Fare clic con il pulsante destro del mouse sul nodo **Debug** sotto il nodo **Server applicazioni\-Applicazioni** e selezionare **Attiva log**.  
  
5.  Eseguire l'applicazione abilitata per il rilevamento per generare gli eventi di rilevamento.  
  
6.  Fare clic con il pulsante destro del mouse su **Debug** e selezionare **Aggiorna**. Gli eventi di traccia verranno visualizzati nel riquadro centrale.  
  
 In WF 4 è presente un partecipante del rilevamento mediante il quale vengono scritti i record di rilevamento in una sessione ETW \(Event Tracing for Windows\).  Il partecipante del rilevamento ETW viene configurato con un profilo di rilevamento per sottoscrivere i record di rilevamento.  Quando il rilevamento è abilitato, vengono generati record di rilevamento di errori su ETW.  Gli eventi di rilevamento ETW \(in un intervallo da 100 a 113\) corrispondenti agli eventi di rilevamento generati dal partecipante del rilevamento ETW vengono scritti nel log analitico.  
  
 Per visualizzare i record di rilevamento, attenersi alla seguente procedura.  
  
1.  Per aprire Visualizzatore eventi, fare clic su **Start**, quindi su **Esegui**. Nella finestra di dialogo Esegui, digitare `eventvwr`.  
  
2.  Nella finestra di dialogo Visualizzatore eventi, espandere il nodo **Registri applicazioni e servizi**.  
  
3.  Espandere i nodi **Microsoft**, **Windows** e **Server applicazioni\-Applicazioni**.  
  
4.  Fare clic con il pulsante destro del mouse sul nodo **Analitico** sotto il nodo **Server applicazioni\-Applicazioni** e selezionare **Attiva log**.  
  
5.  Eseguire l'applicazione abilitata per il rilevamento per generare record di rilevamento.  
  
6.  Fare clic con il pulsante destro del mouse sul nodo **Analitico** e scegliere **Aggiorna**. I record di rilevamento dovrebbero essere visibili nel riquadro centrale.  
  
 Nell'immagine seguente vengono mostrati gli eventi di rilevamento nel visualizzatore eventi.  
  
 ![Visualizzatore eventi con i record di traccia](../../../docs/framework/windows-workflow-foundation//media/trackingeventviewer.PNG "TrackingEventViewer")  
  
### Registrazione di un ID provider specifico dell'applicazione  
 Se gli eventi devono essere scritti in un registro applicazioni specifico, attenersi alla seguente procedura per registrare il nuovo manifesto del provider.  
  
1.  Dichiarare l'ID provider nel file di configurazione dell'applicazione.  
  
    ```  
    <system.serviceModel>  
        <diagnostics etwProviderId="2720e974-9fe9-477a-bb60-81fe3bf91eec"/>  
    </system.serviceModel>  
  
    ```  
  
2.  Copiare il file manifesto da %windir%\\Microsoft.NET\\Framework\\\<versione più recente di [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]\>\\Microsoft.Windows.ApplicationServer.Applications.man in un percorso temporaneo e rinominarlo Microsoft.Windows.ApplicationServer.Applications\_Provider1.man  
  
3.  Modificare il GUID del file manifesto con il nuovo GUID.  
  
    ```  
    <provider name="Microsoft-Windows-Application Server-Applications" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}"  
  
    ```  
  
4.  Modificare il nome del provider se non si desidera disinstallare il provider predefinito.  
  
    ```  
    <provider name="Microsoft-Windows-Application Server-Applications" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}"  
  
    ```  
  
5.  Se è stato modificato il nome del provider nel passaggio precedente, modificare i nomi dei canali nel file manifesto in base al nuovo nome del provider.  
  
    ```  
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Admin" chid="ADMIN_CHANNEL" symbol="ADMIN_CHANNEL" type="Admin" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ADMIN_CHANNEL.message)" />  
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Operational" chid="OPERATIONAL_CHANNEL" symbol="OPERATIONAL_CHANNEL" type="Operational" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.OPERATIONAL_CHANNEL.message)" />  
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Analytic" chid="ANALYTIC_CHANNEL" symbol="ANALYTIC_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ANALYTIC_CHANNEL.message)" />  
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Debug" chid="DEBUG_CHANNEL" symbol="DEBUG_CHANNEL" type="Debug" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.DEBUG_CHANNEL.message)" />  
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Perf" chid="PERF_CHANNEL" symbol="PERF_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.PERF_CHANNEL.message)" />  
  
    ```  
  
6.  Generare la DLL di risorse attenendosi ai passaggi seguenti.  
  
    1.  Installare Windows SDK.  Windows SDK include il compilatore di messaggi \([mc.exe](http://go.microsoft.com/fwlink/?LinkId=184606)\) e il compilatore di risorse \([rc.exe](http://go.microsoft.com/fwlink/?LinkId=184605)\).  
  
    2.  In un prompt dei comandi di Windows SDK, eseguire mc.exe nel nuovo file manifesto.  
  
        ```  
        mc.exe Microsoft.Windows.ApplicationServer.Applications_Provider1.man  
  
        ```  
  
    3.  Eseguire rc.exe nel file di risorse generato nel passaggio precedente.  
  
        ```  
        rc.exe  Microsoft.Windows.ApplicationServer.Applications_Provider1.rc  
  
        ```  
  
    4.  Creare un file cs vuoto denominato NewProviderReg.cs.  
  
    5.  Creare una DLL di risorse usando il compilatore C\#.  
  
        ```  
        csc /target:library /win32res:Microsoft.Windows.ApplicationServer.Applications_Provider1.res NewProviderReg.cs /out:Microsoft.Windows.ApplicationServer.Applications_Provider1.dll  
        ```  
  
    6.  Impostare il nome della DLL di risorse e messaggi nel file manifesto da `Microsoft.Windows.ApplicationServer.Applications.Provider1.man` al nuovo nome della DLL.  
  
        ```  
        <provider name="Microsoft-Windows-Application Server-Applications_Provider1" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}" symbol="Microsoft_Windows_ApplicationServer_ApplicationEvents" resourceFileName="<dll directory>\Microsoft.Windows.ApplicationServer.Applications_Provider1.dll" messageFileName="<dll directory>\Microsoft.Windows.ApplicationServer.Applications_Provider1.dll">  
  
        ```  
  
    7.  Usare [wevtutil](http://go.microsoft.com/fwlink/?LinkId=184608) per registrare il manifesto.  
  
        ```  
        wevtutil im Microsoft.Windows.ApplicationServer.Applications_Provider1.man  
        ```  
  
## Vedere anche  
 [Concetti di monitoraggio](http://go.microsoft.com/fwlink/?LinkId=201273)   
 [Monitoraggio delle applicazioni](http://go.microsoft.com/fwlink/?LinkId=201275)