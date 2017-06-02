---
title: "&lt;participants&gt; di WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d99dbddc-0057-4e18-8e42-f91411d39970
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;participants&gt; di WCF
Configurare un elenco di partecipanti del rilevamento che ascoltano i record di rilevamento generati direttamente durante la fase di esecuzione e li elaborano in base alle impostazioni configurate.  Tali impostazioni includono la scrittura in un output specifico, ad esempio file, console, ETW, l'elaborazione\/aggregazione dei record o qualsiasi altra combinazione che potrebbe essere richiesta.  
  
 Per altre informazioni sul rilevamento del flusso di lavoro e sui partecipanti del rilevamento, vedere [Rilevamento e traccia del flusso di lavoro](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md) e [Partecipanti del rilevamento](../../../../../docs/framework/windows-workflow-foundation//tracking-participants.md).  
  
## Sintassi  
  
```vb  
  
<tracking>   
   <participants>   
      <add name="String"   
           profileName="String"  
           type="String" />   
   </participants>   
</tracking>  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/add-of-participants.md)|Contiene impostazioni per un partecipante del rilevamento.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<tracking\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/tracking.md)|Rappresenta una sezione di configurazione per la definizione delle impostazioni di rilevamento di un servizio flusso di lavoro.|  
  
## Note  
 I partecipanti del rilevamento vengono usati per ottenere i dati di rilevamento generati dal flusso di lavoro e archiviarli in supporti differenti.  Analogamente, è anche possibile eseguire qualsiasi operazione di post\-elaborazione sui record di rilevamento all'interno del partecipante del rilevamento.  
  
 Più partecipanti del rilevamento possono usare simultaneamente gli eventi di rilevamento.  Ogni partecipante del rilevamento può essere associato a un profilo di rilevamento diverso.  
  
 Viene fornito un partecipante del rilevamento standard che scrive i record di rilevamento in una sessione ETW.  Il partecipante viene configurato su un servizio flusso di lavoro aggiungendo un comportamento specifico del rilevamento in un file di configurazione.  L'abilitazione di un partecipante del rilevamento ETW consente la visualizzazione dei record di rilevamento nel Visualizzatore eventi.  Se tale partecipante non soddisfa i propri requisiti, è anche possibile scrivere un partecipante del rilevamento personalizzato.  
  
## Esempio  
 Nell'esempio di configurazione seguente viene mostrato il partecipante del rilevamento ETW standard configurato nel file Web.config.  
  
 L'ID del provider usato dal partecipante del rilevamento ETW per scrivere i record di rilevamento in ETW è definito nella sezione `<diagnostics>`.  Al partecipante di rilevamento è associato un profilo per specificare i record di rilevamento che ha sottoscritto.  Tale profilo è definito dall'attributo `profileName` dell'elemento `<add>`.  Dopo aver definito tali elementi, il partecipante del rilevamento viene aggiunto al comportamento del servizio `<etwTracking>`,  che aggiungerà i partecipanti del rilevamento selezionati alle estensioni dell'istanza del flusso di lavoro, in modo che inizino a ricevere i record di rilevamento.  
  
```  
  
<configuration>   
  <system.web>   
    <compilation targetFrameworkMoniker=".NETFramework,Version=v4.0"/>   
  </system.web>   
  <system.serviceModel>   
    <diagnostics etwProviderId="52A3165D-4AD9-405C-B1E8-7D9A257EAC9F" />                
    <tracking>   
      <participants>   
        <add name="EtwTrackingParticipant"   
             type="System.Activities.Tracking.EtwTrackingParticipant, System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35"   
             profileName="HealthMonitoring_Tracking_Profile"/>   
      </participants>   
    </tracking>   
    <behaviors>   
      <serviceBehaviors>   
        <behavior>   
          <etwTracking profileName="Sample Tracking Profile"/>  
        </behavior>   
      </serviceBehaviors>   
    </behaviors>   
  </system.serviceModel>   
</configuration>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Activities.Tracking.Configuration.TrackingSection>   
 <xref:System.ServiceModel.Activities.Description.EtwTrackingBehavior>   
 <xref:System.ServiceModel.Activities.Configuration.EtwTrackingBehavior>   
 [Rilevamento e traccia del flusso di lavoro](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)   
 [Partecipanti del rilevamento](../../../../../docs/framework/windows-workflow-foundation//tracking-participants.md)