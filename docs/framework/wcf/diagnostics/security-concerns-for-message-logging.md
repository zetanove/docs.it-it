---
title: "Problemi di sicurezza per la registrazione dei messaggi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21f513f2-815b-47f3-85a6-03c008510038
caps.latest.revision: 17
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 17
---
# Problemi di sicurezza per la registrazione dei messaggi
In questo argomento viene illustrato come evitare che i dati riservati vengano esposti nei log dei messaggi e come proteggere gli eventi generati dalla registrazione dei messaggi.  
  
## Problemi di sicurezza  
  
### Registrazione di informazioni riservate  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] non modifica nessun dato nelle intestazioni specifiche dell'applicazione e nel corpo.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] inoltre non tiene traccia delle informazioni personali nelle intestazioni specifiche dell'applicazione o nei dati del corpo.  
  
 Quando la registrazione dei messaggi è abilitata, le informazioni personali contenute nelle intestazioni specifiche dell'applicazione, ad esempio una stringa di query, e le informazioni contenute nel corpo, ad esempio un numero di carta di credito, possono divenire visibili nei log.Il distributore dell'applicazione è responsabile dell'applicazione del controllo di accesso sui file di log e di configurazione.Se non si desidera che questo tipo di informazioni sia visibile, è necessario disabilitare la registrazione oppure filtrare parte dei dati se si intende condividere i file registro.  
  
 I suggerimenti seguenti consentono di impedire che il contenuto di un file di log venga esposto per errore:  
  
-   Accertarsi che i file di log siano protetti da elenchi di controllo di accesso \(ACL, Access Control Lists\) in scenari sia WebHost che indipendenti.  
  
-   Scegliere un'estensione di file che non sia troppo facilmente disponibile quando si utilizza una richiesta Web.L'estensione xml, ad esempio, non è una scelta sicura.Per un elenco di estensioni disponibili, consultare il manuale dell'amministratore di Internet Information Services \(IIS\).  
  
-   Specificare un percorso assoluto per il file di log, che non deve essere contenuto nella directory pubblica della radice virtuale di WebHost, per evitare che venga consultato da un interessato esterno mediante un browser Web.  
  
 Per impostazione predefinita, le chiavi e le informazioni personali, ad esempio nome utente e password, non sono registrate in tracce e messaggi registrati.Un amministratore del computer, tuttavia, può utilizzare l'attributo `enableLoggingKnownPII` nell'elemento `machineSettings` del file Machine.config per consentire alle applicazioni in esecuzione sul computer di registrare informazioni personali note \(PII\).La procedura viene illustrata nella configurazione seguente:  
  
```  
<configuration>  
   <system.serviceModel>  
      <machineSettings enableLoggingKnownPii="true"/>  
   </system.serviceModel>  
</configuration>   
```  
  
 I distributori di applicazioni possono quindi utilizzare l'attributo `logKnownPii` nel file App.config o Web.config per abilitare la registrazione di informazioni personali come segue:  
  
```  
<system.diagnostics>  
  <sources>  
      <source name="System.ServiceModel.MessageLogging"  
        logKnownPii="true">  
        <listeners>  
                 <add name="messages"  
                 type="System.Diagnostics.XmlWriterTraceListener"  
                 initializeData="c:\logs\messages.svclog" />  
          </listeners>  
      </source>  
    </sources>  
</system.diagnostics>  
```  
  
 La registrazione di informazioni personali viene abilitata solo quando entrambe le impostazioni sono `true`.La combinazione di due opzioni consente la registrazione di informazioni personali note per ogni applicazione.  
  
> [!IMPORTANT]
>  In [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] i flag `logEntireMessage` e `logKnownPii` devono essere impostati su `true` nel file Web.config o nel file App.config per abilitare la registrazione delle informazioni personali, come mostrato nel seguente esempio `<system.serviceModel><messageLogging logEntireMessage="true" logKnownPii="true" …`.  
  
 Tenere presente che se si specificano due o più origini personalizzate in un file di configurazione, solo gli attributi della prima origine vengono letti.Gli altri vengono ignorati.Questo implica che, per il file App.config seguente, le informazioni personali non vengono registrate per entrambe le origini anche se la registrazione di informazioni personali è abilitata in modo esplicito per la seconda origine.  
  
```  
<system.diagnostics>  
   <sources>  
      <source name="System.ServiceModel.MessageLogging"  
              logKnownPii="false">  
              <listeners>  
                 <add name="messages"  
                      type="System.Diagnostics.XmlWriterTraceListener"  
                      initializeData="c:\logs\messages.svclog" />  
              </listeners>  
            </source>  
      <source name="System.ServiceModel"   
              logKnownPii="true">  
              <listeners>  
                 <add name="traces"  
                      type="System.Diagnostics.XmlWriterTraceListener"  
                      initializeData="c:\logs\traces.svclog" />  
              </listeners>  
      </source>  
   </sources>  
</system.diagnostics>  
```  
  
 Se l'elemento `<machineSettings enableLoggingKnownPii="Boolean"/>` esiste al di fuori del file Machine.config, il sistema genera un'eccezione <xref:System.Configuration.ConfigurationErrorsException>.  
  
 Le modifiche diventano effettive solo dopo l'avvio o il riavvio dell'applicazione.Un evento viene registrato all'avvio quando entrambi gli attributi sono impostati su `true`.Un evento viene inoltre registrato se `logKnownPii` è impostato su `true` ma `enableLoggingKnownPii` è `false`.  
  
 L'amministratore del computer e il distributore di applicazioni devono prestare molta attenzione durante l'utilizzo di queste due opzioni.Se la registrazione di informazioni personali è abilitata, vengono registrate chiavi di sicurezza e informazioni personali.Se è disabilitata, i dati riservati e le informazioni specifiche dell'applicazione vengono comunque registrati nell'intestazione e nel corpo dei messaggi.Per una discussione più approfondita sulla privacy e la protezione di informazioni personali, vedere la pagina [Privacy dell'utente](http://go.microsoft.com/fwlink/?LinkID=94647) \(il contenuto potrebbe essere in inglese\).  
  
> [!CAUTION]
>  Le PII non sono nascoste nei messaggi in formato non valido.Tali messaggi vengono registrati così come sono, senza alcuna modifica.Gli attributi menzionati prima non hanno alcun effetto su questa situazione.  
  
### Listener di traccia personalizzato  
 L'aggiunta di un listener di traccia personalizzato sull'origine della traccia di registrazione messaggi è un privilegio che deve essere limitato all'amministratore.Tale limitazione è dovuta al fatto che i listener personalizzati dannosi possono essere configurati per inviare messaggi in modalità remota, con la conseguente divulgazione di informazioni riservate.Se, inoltre, si configura un listener personalizzato affinché invii messaggi in rete, ad esempio a un database remoto, è necessario applicare un controllo di accesso appropriato sui registri dei messaggi nel computer remoto.  
  
## Eventi generati dalla registrazione dei messaggi  
 Di seguito vengono elencati tutti gli eventi emessi dalla registrazione dei messaggi.  
  
-   Registrazioni messaggi attiva: questo evento viene emesso quando la registrazione messaggi è abilitata nella configurazione, o tramite WMI.Il contenuto dell'evento è "Registrazione messaggi attivata.È possibile che le informazioni riservate vengano registrate in forma non crittografata, anche se crittografate durante la trasmissione, ad esempio i corpi dei messaggi".  
  
-   Registrazioni messaggi disattivata: questo evento viene emesso quando la registrazione messaggi è disabilitata tramite WMI.Il contenuto dell'evento è "Registrazione messaggi disattivata".  
  
-   Registrazione informazioni personali note attiva: questo evento viene generato quando la registrazione di informazioni personali note è abilitata.Ciò accade quando l'attributo `enableLoggingKnownPii` nell'elemento `machineSettings` del file Machine.config è impostato su `true` e l'attributo `logKnownPii` dell'elemento `source` nel file App.config o nel file Web.config è impostato su `true`.  
  
-   Registrazione informazioni personali note non consentita: questo evento viene emesso quando la registrazione delle informazioni personali note non è consentita.Ciò accade quando l'attributo `logKnownPii` dell'elemento `source` nel file App.config o nel file Web.config è impostato su `true`, ma l'attributo `enableLoggingKnownPii` nell'elemento `machineSettings` del file Machine.config è impostato su `false`.Non viene generata alcuna eccezione.  
  
 Questi eventi possono essere visualizzati nello strumento Visualizzatore eventi in dotazione con Windows.Per ulteriori informazioni in merito, vedere [Registrazione eventi](../../../../docs/framework/wcf/diagnostics/event-logging/index.md).  
  
## Vedere anche  
 [Registrazione messaggi](../../../../docs/framework/wcf/diagnostics/message-logging.md)   
 [Problemi di sicurezza e suggerimenti utili per la traccia](../../../../docs/framework/wcf/diagnostics/tracing/security-concerns-and-useful-tips-for-tracing.md)