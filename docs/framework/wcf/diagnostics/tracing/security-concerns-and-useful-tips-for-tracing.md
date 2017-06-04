---
title: "Problemi di sicurezza e suggerimenti utili per la traccia | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 88bc2880-ecb9-47cd-9816-39016a07076f
caps.latest.revision: 11
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 11
---
# Problemi di sicurezza e suggerimenti utili per la traccia
In questo argomento viene descritto come proteggere informazioni riservate e vengono elencati suggerimenti utili durante l'utilizzo di WebHost.  
  
## Utilizzo di un listener di traccia personalizzato con WebHost  
 Nello scrivere listener di traccia personalizzati, tenere presente la possibilità che le tracce vadano perse nel caso di un servizio Host Web.Durante il riciclo, WebHost arresta il processo reale e subentra un duplicato.È necessario, tuttavia, che i due processi possano ancora accedere alla stessa risorsa, a seconda del tipo di listener.In questo caso, `XmlWriterTraceListener` crea un nuovo file di traccia per il secondo processo mentre Traccia eventi di Windows gestisce più processi nella stessa sessione e dà accesso allo stesso file.Se il listener personalizzato non fornisce funzionalità analoghe, è possibile che le tracce vadano perse quando il file è bloccato dai due processi.  
  
 È inoltre importante tenere presente che un listener di traccia personalizzato può inviare tracce e messaggi in transito, ad esempio, a un database remoto.Il distributore di applicazioni deve configurare listener personalizzati con il controllo di accesso appropriato.È inoltre necessario applicare un controllo di sicurezza a qualsiasi informazione personale potenzialmente esposta nel percorso remoto.  
  
## Registrazione di informazioni riservate  
 Le tracce contengono intestazioni di messaggio quando un messaggio è nell'ambito.Quando la funzionalità di traccia è abilitata, le informazioni personali contenute nelle intestazioni specifiche dell'applicazione, ad esempio una stringa di query, e le informazioni contenute nel corpo, ad esempio un numero di carta di credito, possono divenire visibili nei log.Il distributore dell'applicazione è responsabile dell'attivazione del controllo di accesso nei file di configurazione e di traccia.Se non si desidera che questo tipo di informazioni sia visibile, è necessario disabilitare la traccia oppure filtrare parte dei dati se si intende condividere i log di traccia.  
  
 I suggerimenti seguenti consentono di impedire che il contenuto di un file di traccia venga esposto per errore:  
  
-   Accertarsi che i file di log siano protetti da elenchi di controllo di accesso \(ACL, Access Control Lists\) in scenari sia WebHost che indipendenti.  
  
-   Scegliere un'estensione di file che non sia troppo facilmente disponibile quando si utilizza una richiesta Web.L'estensione xml, ad esempio, non è una scelta sicura.Per un elenco di estensioni disponibili, consultare il manuale dell'amministratore di IIS.  
  
-   Specificare un percorso assoluto per il file di log, che non deve essere contenuto nella directory pubblica della radice virtuale di WebHost, per evitare che venga consultato da un interessato esterno mediante un browser Web.  
  
 Per impostazione predefinita, le chiavi e le informazioni personali, ad esempio nome utente e password, non sono registrate in tracce e messaggi registrati.Un amministratore del computer, tuttavia, può utilizzare l'attributo `enableLoggingKnownPII` nell'elemento `machineSettings` del file Machine.config per consentire alle applicazioni in esecuzione sul computer di registrare informazioni personali note come segue:  
  
```  
<configuration>  
   <system.ServiceModel>  
      <machineSettings enableLoggingKnownPii="Boolean"/>  
   </system.ServiceModel>  
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
            <add name="xml" />  
         </listeners>  
      </source>  
  </sources>  
</system.diagnostics>  
```  
  
 Se l'elemento `<machineSettings enableLoggingKnownPii="Boolean"/>` esiste al di fuori del file Machine.config, il sistema genera un'eccezione <xref:System.Configuration.ConfigurationErrorsException>.  
  
 Le modifiche diventano effettive solo dopo l'avvio o il riavvio dell'applicazione.Un evento viene registrato all'avvio quando entrambi gli attributi sono impostati su `true`.Un evento viene inoltre registrato se `logKnownPii` è impostato su `true` ma `enableLoggingKnownPii` è `false`.  
  
 Per ulteriori informazioni sulla registrazione di informazioni personali, vedere l'esempio [Blocco della sicurezza delle informazioni personali](../../../../../docs/framework/wcf/samples/pii-security-lockdown.md).  
  
 L'amministratore del computer e il distributore di applicazioni devono prestare molta attenzione durante l'utilizzo di queste due opzioni.Se la registrazione di informazioni personali è abilitata, vengono registrate chiavi di sicurezza e informazioni personali.Se è disabilitata, i dati riservati e le informazioni specifiche dell'applicazione vengono comunque registrati nell'intestazione e nel corpo dei messaggi.Per una discussione più approfondita sulla privacy e la protezione delle informazioni personali esposte, vedere la pagina [Privacy dell'utente](http://go.microsoft.com/fwlink/?LinkID=94647) \(la pagina potrebbe essere in inglese\).  
  
 L'indirizzo IP del mittente del messaggio, inoltre, viene registrato una volta per ogni connessione per trasporti orientati alla connessione e una volta per ogni messaggio inviato diversamente.Ciò avviene senza il consenso del mittente.Questa registrazione, tuttavia, avviene solo ai livelli di traccia Informazioni o Dettagliato, ovvero i livelli non predefiniti né consigliati in produzione, tranne che per il debug attivo.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)