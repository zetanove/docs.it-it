---
title: "Sviluppo del servizio del flusso di lavoro con priorit&#224; al contratto (&quot;contract-first&quot;) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5dbaa7b-005f-4330-848d-58ac4f42f093
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Sviluppo del servizio del flusso di lavoro con priorit&#224; al contratto (&quot;contract-first&quot;)
A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], [!INCLUDE[wf](../../../includes/wf-md.md)] offre una maggiore integrazione tra i servizi Web e i flussi di lavoro sotto forma di sviluppo di flussi di lavoro con priorità al contratto.Lo strumento di sviluppo di flussi di lavoro con priorità al contratto consente di progettare il contratto innanzitutto nel codice.Lo strumento consente di generare automaticamente un modello di attività nella casella degli strumenti per le operazioni nel contratto.In questo argomento viene fornita una panoramica del mapping di attività e proprietà di un servizio del flusso di lavoro agli attributi di un contratto di servizio.Per un esempio dettagliato della creazione di un servizio del flusso di lavoro con priorità al contratto \("contract\-first"\), vedere [Procedura: creare un servizio di flusso di lavoro che utilizza un contratto di servizio esistente](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow-service-that-consumes-an-existing-service-contract.md).  
  
## In questo argomento  
  
-   [Mapping degli attributi del contratto di servizio agli attributi del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#MappingAttributes)  
  
    -   [Attributi del contratto di servizio](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#ServiceContract)  
  
    -   [Attributi del contratto dell'operazione](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#OperationContract)  
  
    -   [Attributi del contratto del messaggio](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#MessageContract)  
  
    -   [Attributi del contratto dei dati](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#DataContract)  
  
    -   [Attributi del contratto di errore](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#FaultContract)  
  
-   [Ulteriori informazioni di implementazione e di supporto](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#AdditionalSupport)  
  
    -   [Funzionalità non supportate del contratto di servizio](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#UnsupportedFeatures)  
  
    -   [Generazione di attività di messaggistica configurate](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#ActivityGeneration)  
  
##  <a name="MappingAttributes"></a> Mapping degli attributi del contratto di servizio agli attributi del flusso di lavoro  
 Le tabelle nelle sezioni seguenti specificano gli attributi e le proprietà WCF e il relativo mapping alle attività e alle proprietà di messaggistica in un flusso di lavoro con priorità al contratto \("contract\-first"\).  
  
-   [Attributi del contratto di servizio](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#ServiceContract)  
  
-   [Attributi del contratto dell'operazione](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#OperationContract)  
  
-   [Attributi del contratto del messaggio](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#MessageContract)  
  
-   [Attributi del contratto dei dati](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#DataContract)  
  
-   [Attributi del contratto di errore](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#FaultContract)  
  
###  <a name="ServiceContract"></a> Attributi del contratto di servizio  
  
|Nome proprietà|Supportato|Descrizione|Convalida WF|  
|--------------------|----------------|-----------------|------------------|  
|CallbackContract|No|Ottiene o imposta il tipo di contratto di callback quando il contratto è duplex.|\(N\/D\)|  
|ConfigurationName|No|Consente di ottenere o impostare il nome utilizzato per individuare il servizio in un file di configurazione dell'applicazione.|\(N\/D\)|  
|HasProtectionLevel|Sì|Ottiene un valore che indica se al membro è stato assegnato un livello di protezione.|Receive.ProtectionLevel non deve essere null.|  
|Name|Sì|Ottiene o imposta il nome dell'elemento \<portType\> in WSDL \(Web Services Description Language\).|Receive.ServiceContractName.LocalName deve corrispondere.|  
|Spazio dei nomi|Sì|Ottiene o imposta lo spazio dei nomi dell'elemento \<portType\> in WSDL \(Web Services Description Language\).|Receive.ServiceContractName.NameSpace deve corrispondere.|  
|ProtectionLevel|Sì|Specifica se l'associazione del contratto deve supportare il valore della proprietà ProtectionLevel.|Receive.ProtectionLevel deve corrispondere.|  
|SessionMode|No|Consente di ottenere o impostare un valore che stabilisce se le sessioni sono consentite, non consentite oppure obbligatorie.|\(N\/D\)|  
|TypeId|No|Se implementato in una classe derivata, ottiene un identificatore univoco per l'attributo\(ereditato dall'attributo\).|\(N\/D\)|  
  
 Inserire qui il corpo della sottosezione.  
  
###  <a name="OperationContract"></a> Attributi del contratto dell'operazione  
  
|Nome proprietà|Supportato|Descrizione|Convalida WF|  
|--------------------|----------------|-----------------|------------------|  
|Azione|Sì|Consente di ottenere o impostare l'azione WS\-Addressing del messaggio di richiesta.|Receive.Action deve corrispondere.|  
|AsyncPattern|No|Indica che un'operazione è implementata in modo asincrono utilizzando una coppia costituita dai metodi Begin\<nomeMetodo\> e End\<nomeMetodo\> in un contratto di servizio.|\(N\/D\)|  
|HasProtectionLevel|Sì|Ottiene un valore che indica se i messaggi di questa operazione devono essere crittografati o firmati o se devono presentare entrambi i meccanismi di protezione.|Receive.ProtectionLevel non deve essere null.|  
|IsInitiating|No|Ottiene o imposta un valore che indica se il metodo implementa un'operazione in grado di avviare una sessione nel server \(se tale sessione esiste\).|\(N\/D\)|  
|IsOneWay|Sì|Ottiene o imposta un valore che indica se l'operazione restituisce un messaggio di risposta.|\(Nessun SendReply per Receive OPPURE nessun ReceiveReply per Send\).|  
|IsTerminating|No|Ottiene o imposta un valore che indica se l'operazione di servizio causa la chiusura della sessione da parte del server dopo l'invio di un eventuale messaggio di risposta.|\(N\/D\)|  
|Name|Sì|Ottiene o imposta il nome dell'operazione.|Receive.OperationName deve corrispondere.|  
|ProtectionLevel|Sì|Ottiene o imposta un valore che specifica se i messaggi di un'operazione devono essere crittografati o firmati o se devono presentare entrambi i meccanismi di sicurezza.|Receive.ProtectionLevel deve corrispondere.|  
|ReplyAction|Sì|Ottiene o imposta il valore dell'azione SOAP del messaggio di risposta dell'operazione.|SendReply.Action deve corrispondere.|  
|TypeId|No|Se implementato in una classe derivata, ottiene un identificatore univoco per l'attributo\(ereditato dall'attributo\).|\(N\/D\)|  
  
###  <a name="MessageContract"></a> Attributi del contratto del messaggio  
  
|Nome proprietà|Supportato|Descrizione|Convalida WF|  
|--------------------|----------------|-----------------|------------------|  
|HasProtectionLevel|Sì|Ottiene un valore che indica se per il messaggio è specificato un livello di protezione.|Nessuna convalida \(Receive.Content e SendReply.Content devono corrispondere al tipo di contratto di messaggio\).|  
|IsWrapped|Sì|Ottiene o imposta un valore che specifica se il corpo del messaggio contiene un elemento wrapper.|Nessuna convalida \(Receive.Content e SendReply.Content devono corrispondere al tipo di contratto di messaggio\).|  
|ProtectionLevel|No|Ottiene o imposta un valore che specifica se il messaggio deve essere crittografato o firmato o se deve presentare entrambi i meccanismi di sicurezza.|\(N\/D\)|  
|TypeId|Sì|Se implementato in una classe derivata, ottiene un identificatore univoco per l'attributo\(ereditato dall'attributo\).|Nessuna convalida \(Receive.Content e SendReply.Content devono corrispondere al tipo di contratto di messaggio\).|  
|WrapperName|Sì|Ottiene o imposta il nome dell'elemento wrapper del corpo del messaggio.|Nessuna convalida \(Receive.Content e SendReply.Content devono corrispondere al tipo di contratto di messaggio\).|  
|WrapperNamespace|No|Ottiene o imposta lo spazio dei nomi dell'elemento wrapper del corpo del messaggio.|\(N\/D\)|  
  
###  <a name="DataContract"></a> Attributi del contratto dei dati  
  
|Nome proprietà|Supportato|Descrizione|Convalida WF|  
|--------------------|----------------|-----------------|------------------|  
|IsReference|No|Ottiene o imposta un valore che indica se mantenere i dati del riferimento all'oggetto.|\(N\/D\)|  
|Name|Sì|Ottiene o imposta il nome del contratto dati per il tipo.|Nessuna convalida \(Receive.Content e SendReply.Content devono corrispondere al tipo di contratto di messaggio\).|  
|Spazio dei nomi|Sì|Ottiene o imposta lo spazio dei nomi del contratto dati per il tipo.|Nessuna convalida \(Receive.Content e SendReply.Content devono corrispondere al tipo di contratto di messaggio\).|  
|TypeId|No|Se implementato in una classe derivata, ottiene un identificatore univoco per l'attributo\(ereditato dall'attributo\).|\(N\/D\)|  
  
###  <a name="FaultContract"></a> Attributi del contratto di errore  
  
|Nome proprietà|Supportato|Descrizione|Convalida WF|  
|--------------------|----------------|-----------------|------------------|  
|Azione|Sì|Consente di ottenere o impostare l'azione del messaggio di errore SOAP specificato come parte del contratto dell'operazione.|SendReply.Action deve corrispondere.|  
|DetailType|Sì|Consente di ottenere il tipo di un oggetto serializzabile contenente le informazioni sull'errore.|SendReply.Content deve corrispondere al tipo.|  
|HasProtectionLevel|No|Ottiene un valore che indica se al messaggio di errore SOAP è stato assegnato un livello di protezione.|\(N\/D\)|  
|Name|No|Consente di ottenere o impostare il nome del messaggio di errore in WSDL \(Web Services Description Language\).|\(N\/D\)|  
|Spazio dei nomi|No|Consente di ottenere o impostare lo spazio dei nomi dell'errore SOAP.|\(N\/D\)|  
|ProtectionLevel|No|Consente di specificare il livello di protezione che l'associazione deve applicare all'errore SOAP.|\(N\/D\)|  
|TypeId|No|Se implementato in una classe derivata, ottiene un identificatore univoco per l'attributo\(ereditato dall'attributo\).|\(N\/D\)|  
  
##  <a name="AdditionalSupport"></a> Ulteriori informazioni di implementazione e di supporto  
  
-   [Funzionalità non supportate del contratto di servizio](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#UnsupportedFeatures)  
  
-   [Generazione di attività di messaggistica configurate](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md#ActivityGeneration)  
  
###  <a name="UnsupportedFeatures"></a> Funzionalità non supportate del contratto di servizio  
  
-   L'utilizzo delle attività della libreria TPL \(Task Parallel Library\) nei contratti non è supportato.  
  
-   L'ereditarietà nei contratti di servizio non è supportata.  
  
###  <a name="ActivityGeneration"></a> Generazione di attività di messaggistica configurate  
 Sono stati aggiunti due metodi statici pubblici alle attività <xref:System.ServiceModel.Activities.SendReply> e <xref:System.ServiceModel.Activities.Receive> per supportare la generazione di attività preconfigurate del messaggio durante l'utilizzo dei servizi dei flussi di lavoro con priorità al contratto \("contract\-first"\).  
  
-   <xref:System.ServiceModel.Activities.Receive.FromOperationDescription%2A?displayProperty=fullName>  
  
-   <xref:System.ServiceModel.Activities.SendReply.FromOperationDescription%2A?displayProperty=fullName>  
  
 L'attività generata da questi metodi deve passare la convalida del contratto e quindi questi metodi vengono utilizzati internamente come parte della logica di convalida per <xref:System.ServiceModel.Activities.Receive> e <xref:System.ServiceModel.Activities.SendReply>.<xref:System.ServiceModel.Activities.Receive.OperationName%2A>, <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A>, <xref:System.ServiceModel.Activities.Receive.Action%2A>, <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A>, <xref:System.ServiceModel.Activities.Receive.ProtectionLevel%2A> e <xref:System.ServiceModel.Activities.Receive.KnownTypes%2A> sono tutti preconfigurati per corrispondere al contratto importato.Nella pagina delle proprietà di contenuto per le attività nella finestra di progettazione del flusso di lavoro, anche le sezioni **Messaggio** o **Parametri** sono preconfigurate in base al contratto.  
  
 I contratti di errore WCF vengono gestiti anche tramite la restituzione di un set separato di attività <xref:System.ServiceModel.Activities.SendReply> configurate per ognuno degli errori che vengono visualizzati in <xref:System.ServiceModel.Description.OperationDescription.Faults%2A> <xref:System.ServiceModel.Description.FaultDescriptionCollection>.  
  
 Per altre parti di <xref:System.ServiceModel.Description.OperationDescription> che non sono attualmente supportate dai servizi WF \(ad esempioi comportamenti di WebGet\/WebInvoke o i comportamenti di operazioni personalizzate\) l'API ignorerà questi valori come parte della generazione e della configurazione.Non verranno generate eccezioni.