---
title: "Riferimento dell&#39;evento di traccia analitica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "traccia analitica [WCF]. riferimento"
ms.assetid: e44540cf-44a1-4efc-b965-7fbfd2131d73
caps.latest.revision: 50
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 50
---
# Riferimento dell&#39;evento di traccia analitica
Nella tabella seguente vengono definiti i livelli di evento, gli identificatori e i messaggi associati alla traccia analitica di [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].  
  
## Riferimento dell'evento  
  
|ID evento|Livello dell'evento|Messaggio dell'evento|Parole chiave|  
|---------------|-------------------------|---------------------------|-------------------|  
|[131 \- BufferPoolAllocation](../../../../../docs/framework/wcf/diagnostics/etw/131-bufferpoolallocation.md)|Dettagliato|Allocazione di %1 byte da parte del pool.|Infrastruttura|  
|[132 \- BufferPoolChangeQuota](../../../../../docs/framework/wcf/diagnostics/etw/132-bufferpoolchangequota.md)|Dettagliato|BufferPool di dimensioni %1, modifica quota di %2.|Infrastruttura|  
|[133 \- ActionItemScheduled](../../../../../docs/framework/wcf/diagnostics/etw/133-actionitemscheduled.md)|Dettagliato|Callback utilità di pianificazione thread di IO richiamato.|Infrastruttura|  
|[134 \- ActionItemCallbackInvoked](../../../../../docs/framework/wcf/diagnostics/etw/134-actionitemcallbackinvoked.md)|Dettagliato|Callback utilità di pianificazione thread di IO richiamato.|Infrastruttura|  
|[201 \- ClientMessageInspectorAfterReceiveInvoked](../../../../../docs/framework/wcf/diagnostics/etw/201-clientmessageinspectorafterreceiveinvoked.md)|Informazioni|'AfterReceiveReply' richiamato dal dispatcher in un elemento ClientMessageInspector di tipo '%1'.|Troubleshooting, ServiceModel|  
|[202 \- ClientMessageInspectorBeforeSendInvoked](../../../../../docs/framework/wcf/diagnostics/etw/202-clientmessageinspectorbeforesendinvoked.md)|Informazioni|'BeforeSendRequest' richiamato dal dispatcher in un elemento ClientMessageInspector di tipo '%1'.|Troubleshooting, ServiceModel|  
|[203 \- ClientParameterInspectorAfterCallInvoked](../../../../../docs/framework/wcf/diagnostics/etw/203-clientparameterinspectoraftercallinvoked.md)|Informazioni|Il dispatcher ha richiamato 'AfterCall' in un ClientParameterInspector  di tipo '%1'.|Troubleshooting, ServiceModel|  
|[204 \- ClientParameterInspectorBeforeCallInvoked](../../../../../docs/framework/wcf/diagnostics/etw/204-clientparameterinspectorbeforecallinvoked.md)|Informazioni|'BeforeCall' richiamato dal dispatcher in un elemento ClientParameterInspector di tipo '%1'.|Troubleshooting, ServiceModel|  
|[205 \- OperationInvoked](../../../../../docs/framework/wcf/diagnostics/etw/205-operationinvoked.md)|Informazioni|Metodo '%1' richiamato da OperationInvoker.|EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[206 \- ErrorHandlerInvoked](../../../../../docs/framework/wcf/diagnostics/etw/206-errorhandlerinvoked.md)|Informazioni|ErrorHandler di tipo '%1' richiamato dal dispatcher con un'eccezione di tipo '%3'.  ErrorHandled \=\= '%2'.|Troubleshooting, ServiceModel|  
|[207 \- FaultProviderInvoked](../../../../../docs/framework/wcf/diagnostics/etw/207-faultproviderinvoked.md)|Informazioni|FaultProvider di tipo '%1' richiamato dal dispatcher con un'eccezione di tipo '%2'.|Troubleshooting, ServiceModel|  
|[208 \- MessageInspectorAfterReceiveInvoked](../../../../../docs/framework/wcf/diagnostics/etw/208-messageinspectorafterreceiveinvoked.md)|Informazioni|'AfterReceiveReply' richiamato dal dispatcher in un elemento MessageInspector di tipo '%1'.|Troubleshooting, ServiceModel|  
|[209 \- MessageInspectorBeforeSendInvoked](../../../../../docs/framework/wcf/diagnostics/etw/209-messageinspectorbeforesendinvoked.md)|Informazioni|'BeforeSendRequest' richiamato dal dispatcher in un elemento MessageInspector di tipo '%1'.|Troubleshooting, ServiceModel|  
|[210 \- MessageThrottleExceeded](../../../../../docs/framework/wcf/diagnostics/etw/210-messagethrottleexceeded.md)|Avviso|È stato raggiunto il limite di velocità '%1' di '%2'.|HealthMonitoring, EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[211 \- ParameterInspectorAfterCallInvoked](../../../../../docs/framework/wcf/diagnostics/etw/211-parameterinspectoraftercallinvoked.md)|Informazioni|Il dispatcher ha richiamato 'AfterCall' in un ParameterInspector di tipo '%1'.|Troubleshooting, ServiceModel|  
|[212 \- ParameterInspectorBeforeCallInvoked](../../../../../docs/framework/wcf/diagnostics/etw/212-parameterinspectorbeforecallinvoked.md)|Informazioni|Il dispatcher ha richiamato 'BeforeCall' in un ParameterInspector di tipo '%1'.|Troubleshooting, ServiceModel|  
|[213 \- ServiceHostStarted](../../../../../docs/framework/wcf/diagnostics/etw/213-servicehoststarted.md)|LogAlways|ServiceHost avviato: '%1'.|HealthMonitoring, EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[214 \- OperationCompleted](../../../../../docs/framework/wcf/diagnostics/etw/214-operationcompleted.md)|Informazioni|Chiamata al metodo '%1' da parte di OperationInvoker completata.  Durata della chiamata al metodo: '%2' ms.|HealthMonitoring, EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[215 \- MessageReceivedByTransport](../../../../../docs/framework/wcf/diagnostics/etw/215-messagereceivedbytransport.md)|Informazioni|Il trasporto ha ricevuto un messaggio da '%1'.|Troubleshooting, ServiceModel|  
|[216 \- MessageSentByTransport](../../../../../docs/framework/wcf/diagnostics/etw/216-messagesentbytransport.md)|Informazioni|Il trasporto ha inviato un messaggio a '%1'.|Troubleshooting, ServiceModel|  
|[217 \- ClientOperationPrepared](../../../../../docs/framework/wcf/diagnostics/etw/217-clientoperationprepared.md)|Informazioni|Esecuzione dell'operazione client '%1' definita nel contratto '%2'.  Il messaggio verrà inviato a '%3'.|Troubleshooting, ServiceModel|  
|[218 \- ClientOperationCompleted](../../../../../docs/framework/wcf/diagnostics/etw/218-clientoperationcompleted.md)|Informazioni|L'operazione client '%1' definita nel contratto '%2' è completa.  Il messaggio è stato inviato a '%3'.|Troubleshooting, ServiceModel|  
|[219 \- ServiceException](../../../../../docs/framework/wcf/diagnostics/etw/219-serviceexception.md)|Errore|Riscontrata un'eccezione non gestita di tipo '%2' durante l'elaborazione del messaggio.  ToString completo dell'eccezione: %1.|HealthMonitoring, EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[220 \- MessageSentToTransport](../../../../../docs/framework/wcf/diagnostics/etw/220-messagesenttotransport.md)|Informazioni|Il dispatcher ha inviato un messaggio al trasporto.  ID di correlazione \=\= '%1'.|EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[221 \- MessageReceivedFromTransport](../../../../../docs/framework/wcf/diagnostics/etw/221-messagereceivedfromtransport.md)|Informazioni|Il dispatcher ha ricevuto un messaggio dal trasporto.  ID di correlazione \=\= '%1'.|EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[222 \- OperationFailed](../../../../../docs/framework/wcf/diagnostics/etw/222-operationfailed.md)|Avviso|Il metodo '%1' ha generato un'eccezione non gestita quando è stato richiamato da OperationInvoker.  Durata della chiamata al metodo: '%2' ms.|HealthMonitoring, EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[223 \- OperationFaulted](../../../../../docs/framework/wcf/diagnostics/etw/223-operationfaulted.md)|Avviso|Il metodo '%1' ha generato FaultException quando è stato richiamato da OperationInvoker.  Durata della chiamata al metodo: '%2' ms.|HealthMonitoring, EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[224 \- MessageThrottleAtSeventyPercent](../../../../../docs/framework/wcf/diagnostics/etw/224-messagethrottleatseventypercent.md)|Avviso|Il limite di velocità '%1' di '%2' è al 70%.|HealthMonitoring, EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[226 \- IdleServicesClosed](../../../../../docs/framework/wcf/diagnostics/etw/226-idleservicesclosed.md)|LogAlways|%1 servizi inattivi su %2 servizi attivati chiusi totali.|HealthMonitoring WebHost|  
|[301 \- UserDefinedErrorOccurred](../../../../../docs/framework/wcf/diagnostics/etw/301-userdefinederroroccurred.md)|Errore|Nome:'%1', riferimento:'%2', payload:%3.|UserEvents, HealthMonitoring, EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[302 \- UserDefinedWarningOccurred](../../../../../docs/framework/wcf/diagnostics/etw/302-userdefinedwarningoccurred.md)|Avviso|Nome:'%1', riferimento:'%2', payload:%3.|UserEvents, HealthMonitoring, EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[303 \- UserDefinedInformationEventOccured](../../../../../docs/framework/wcf/diagnostics/etw/303-userdefinedinformationeventoccured.md)|Informazioni|Nome:'%1', riferimento:'%2', payload:%3.|UserEvents, HealthMonitoring, EndToEndMonitoring, Troubleshooting, ServiceModel|  
|[401\- StopSignPostEvent](../../../../../docs/framework/wcf/diagnostics/etw/401-stopsignpostevent.md)|Informazioni|Limite dell'attività.|Risoluzione dei problemi|  
|[402 \- StartSignpostEvent](../../../../../docs/framework/wcf/diagnostics/etw/402-startsignpostevent.md)|Informazioni|Limite dell'attività.|Risoluzione dei problemi|  
|[403 \- SuspendSignpostEvent](../../../../../docs/framework/wcf/diagnostics/etw/403-suspendsignpostevent.md)|Informazioni|Limite dell'attività.|Risoluzione dei problemi|  
|[404 \- ResumeSignpostEvent](../../../../../docs/framework/wcf/diagnostics/etw/404-resumesignpostevent.md)|Informazioni|Limite dell'attività.|Risoluzione dei problemi|  
|[451 \- MessageLogInfo](../../../../../docs/framework/wcf/diagnostics/etw/451-messageloginfo.md)|Informazioni|%1|Troubleshooting, WCFMessageLogging|  
|[452 \- MessageLogWarning](../../../../../docs/framework/wcf/diagnostics/etw/452-messagelogwarning.md)|Avviso|%1|Troubleshooting, WCFMessageLogging|  
|[499 \- TransferEmitted](../../../../../docs/framework/wcf/diagnostics/etw/499-transferemitted.md)|LogAlways|Emissione evento di trasferimento.|Troubleshooting, UserEvents, EndToEndMonitoring, ServiceModel, WFTracking, ServiceHost, WCFMessageLogging|  
|[501 \- CompilationStart](../../../../../docs/framework/wcf/diagnostics/etw/501-compilationstart.md)|Informazioni|Inizio compilazione|WebHost|  
|[502 \- CompilationStop](../../../../../docs/framework/wcf/diagnostics/etw/502-compilationstop.md)|Informazioni|Fine compilazione|WebHost|  
|[503 \- ServiceHostFactoryCreationStart](../../../../../docs/framework/wcf/diagnostics/etw/503-servicehostfactorycreationstart.md)|Informazioni|Inizio creazione ServiceHostFactory|WebHost|  
|[504 \- ServiceHostFactoryCreationStop](../../../../../docs/framework/wcf/diagnostics/etw/504-servicehostfactorycreationstop.md)|Informazioni|Fine creazione ServiceHostFactory|WebHost|  
|[505 \- CreateServiceHostStart](../../../../../docs/framework/wcf/diagnostics/etw/505-createservicehoststart.md)|Informazioni|Inizio CreateServiceHost|WebHost|  
|[506 \- CreateServiceHostStop](../../../../../docs/framework/wcf/diagnostics/etw/506-createservicehoststop.md)|Informazioni|Fine CreateServiceHost|WebHost|  
|[507 \- HostedTransportConfigurationManagerConfigInitStart](../../../../../docs/framework/wcf/diagnostics/etw/507-hostedtransportconfigurationmanagerconfiginitstart.md)|Informazioni|Inizio configurazione inizializzazione HostedTransportConfigurationManager|WebHost|  
|[508 \- HostedTransportConfigurationManagerConfigInitStop](../../../../../docs/framework/wcf/diagnostics/etw/508-hostedtransportconfigurationmanagerconfiginitstop.md)|Informazioni|Fine configurazione inizializzazione HostedTransportConfigurationManager|WebHost|  
|[509 \- ServiceHostOpenStart](../../../../../docs/framework/wcf/diagnostics/etw/509-servicehostopenstart.md)|Informazioni|Fine configurazione inizializzazione HostedTransportConfigurationManager|Host servizio|  
|[510 \- ServiceHostOpenStop](../../../../../docs/framework/wcf/diagnostics/etw/510-servicehostopenstop.md)|Informazioni|ServiceHostOpen completato.|Host servizio|  
|[513 \- WebHostRequestStart](../../../../../docs/framework/wcf/diagnostics/etw/513-webhostrequeststart.md)|Informazioni|Richiesta ricevuta con percorso virtuale '%2' da AppDomain '%1'.|WebHost|  
|[514 \- WebHostRequestStop](../../../../../docs/framework/wcf/diagnostics/etw/514-webhostrequeststop.md)|Informazioni|Arresto di WebHostRequest.|WebHost|  
|[601 \- CBAEntryRead](../../../../../docs/framework/wcf/diagnostics/etw/601-cbaentryread.md)|Dettagliato|Indirizzo relativo dell'elemento ServiceActivation elaborato:'%1', indirizzo relativo normalizzato '%2'.||  
|[602 \- CBAMatchFound](../../../../../docs/framework/wcf/diagnostics/etw/602-cbamatchfound.md)|Dettagliato|La richiesta in ingresso corrisponde a un elemento ServiceActivation con indirizzo '%1'.||  
|[603 \- AspNetRoutingService](../../../../../docs/framework/wcf/diagnostics/etw/603-aspnetroutingservice.md)|Dettagliato|La richiesta in ingresso corrisponde a un servizio WCF definito nella route ASP.NET con indirizzo %1.|RoutingServices|  
|[604 \- AspNetRoute](../../../../../docs/framework/wcf/diagnostics/etw/604-aspnetroute.md)|Dettagliato|È stata aggiunta una nuova route ASP.NET '%1' con serviceType '%2' e serviceHostFactoryType '%3'.|RoutingServices|  
|[605 \- IncrementBusyCount](../../../../../docs/framework/wcf/diagnostics/etw/605-incrementbusycount.md)|Dettagliato|Chiamato IncrementBusyCount.  Origine: %1|WebHost|  
|[606 \- DecrementBusyCount](../../../../../docs/framework/wcf/diagnostics/etw/606-decrementbusycount.md)|Dettagliato|Chiamato DecrementBusyCount.  Origine: %1|WebHost|  
|[701 \- ServiceChannelOpenStart](../../../../../docs/framework/wcf/diagnostics/etw/701-servicechannelopenstart.md)|Dettagliato|ServiceChannelOpen avviato.|WebHost|  
|[702 \- ServiceChannelOpenStop](../../../../../docs/framework/wcf/diagnostics/etw/702-servicechannelopenstop.md)|Informazioni|ServiceChannelOpen completato.|ServiceModel|  
|[703 \- ServiceChannelCallStart](../../../../../docs/framework/wcf/diagnostics/etw/703-servicechannelcallstart.md)|Informazioni|ServiceChannelCall avviato.|ServiceModel|  
|[704 \- ServiceChannelBeginCallStart](../../../../../docs/framework/wcf/diagnostics/etw/704-servicechannelbegincallstart.md)|Informazioni|Chiamate asincrone di ServiceChannel avviate.|ServiceModel|  
|[706 \- HttpSendMessageStart](../../../../../docs/framework/wcf/diagnostics/etw/706-httpsendmessagestart.md)|Dettagliato|Avvio HttpSendRequest.|HTTP|  
|[707 \- HttpSendStop](../../../../../docs/framework/wcf/diagnostics/etw/707-httpsendstop.md)|Dettagliato|Arresto HttpSendRequest.|HTTP|  
|[708 \- HttpMessageReceiveStart](../../../../../docs/framework/wcf/diagnostics/etw/708-httpmessagereceivestart.md)|Dettagliato|Messaggio ricevuto dal trasporto HTTP.|HTTP|  
|[709 \- DispatchMessageStart](../../../../../docs/framework/wcf/diagnostics/etw/709-dispatchmessagestart.md)|Informazioni|Invio messaggi avviato.|ServiceModel|  
|[710 \- HttpContextBeforeProcessAuthentication](../../../../../docs/framework/wcf/diagnostics/etw/710-httpcontextbeforeprocessauthentication.md)|Dettagliato|Avviare l'autenticazione per l'invio dei messaggi.|ServiceModel|  
|[711 \- DispatchMessageBeforeAuthorization](../../../../../docs/framework/wcf/diagnostics/etw/711-dispatchmessagebeforeauthorization.md)|Dettagliato|Avviare l'autorizzazione per l'invio dei messaggi|ServiceModel|  
|[712 \- DispatchMessageStop](../../../../../docs/framework/wcf/diagnostics/etw/712-dispatchmessagestop.md)|Informazioni|Invio messaggi completato|ServiceModel|  
|[715 \- ClientChannelOpenStart](../../../../../docs/framework/wcf/diagnostics/etw/715-clientchannelopenstart.md)|Informazioni|Avvio apertura ServiceChannel.|ServiceModel|  
|[716 \- ClientChannelOpenStop](../../../../../docs/framework/wcf/diagnostics/etw/716-clientchannelopenstop.md)|Informazioni|Arresto apertura ServiceChannel.|ServiceModel|  
|[717 \- HttpSendStreamedMessageStart](../../../../../docs/framework/wcf/diagnostics/etw/717-httpsendstreamedmessagestart.md)|Informazioni|Messaggio invio HttpSend avviato.|HTTP|  
|[1400 \- ChannelInitializationTimeout](../../../../../docs/framework/wcf/diagnostics/etw/1400-channelinitializationtimeout.md)|Errore|1%|ServiceModel|  
|[1401 \- CloseTimeout](../../../../../docs/framework/wcf/diagnostics/etw/1401-closetimeout.md)|Errore|1%|ServiceModel|  
|[1402 \- IdleTimeout](../../../../../docs/framework/wcf/diagnostics/etw/1402-idletimeout.md)|Errore|%1 Chiave pool di connessioni: %2|ServiceModel|  
|[1403 \- LeaseTimeout](../../../../../docs/framework/wcf/diagnostics/etw/1403-leasetimeout.md)|Informazioni|%1 Chiave pool di connessioni: %2|ServiceModel|  
|[1405 \- OpenTimeout](../../../../../docs/framework/wcf/diagnostics/etw/1405-opentimeout.md)|Errore|%1|ServiceModel|  
|[1406 \- ReceiveTimeout](../../../../../docs/framework/wcf/diagnostics/etw/1406-receivetimeout.md)|Errore|%1|ServiceModel|  
|[1407 \- SendTimeout](../../../../../docs/framework/wcf/diagnostics/etw/1407-sendtimeout.md)|Errore|%1|ServiceModel|  
|[1409 \- InactivityTimeout](../../../../../docs/framework/wcf/diagnostics/etw/1409-inactivitytimeout.md)|Informazioni|%1|ServiceModel|  
|[1416 \- MaxReceivedMessageSizeExceeded](../../../../../docs/framework/wcf/diagnostics/etw/1416-maxreceivedmessagesizeexceeded.md)|Errore|%1|Quota|  
|[1417 \- MaxSentMessageSizeExceeded](../../../../../docs/framework/wcf/diagnostics/etw/1417-maxsentmessagesizeexceeded.md)|Errore|%1|Quota|  
|[1418 \- MaxOutboundConnectionsPerEndpointExceeded](../../../../../docs/framework/wcf/diagnostics/etw/1418-maxoutboundconnectionsperendpointexceeded.md)|Informazioni|%1|Quota|  
|[1419 \- MaxPendingConnectionsExceeded](../../../../../docs/framework/wcf/diagnostics/etw/1419-maxpendingconnectionsexceeded.md)|Informazioni|%1|Quota|  
|[1420 \- ReaderQuotaExceeded](../../../../../docs/framework/wcf/diagnostics/etw/1420-readerquotaexceeded.md)|Errore|%1|Quota|  
|[1422 \- NegotiateTokenAuthenticatorStateCacheExceeded](../../../../../docs/framework/wcf/diagnostics/etw/1422-negotiatetokenauthenticatorstatecacheexceeded.md)|Errore|%1|Quota|  
|[1423 \- NegotiateTokenAuthenticatorStateCacheRatio](../../../../../docs/framework/wcf/diagnostics/etw/1423-negotiatetokenauthenticatorstatecacheratio.md)|Dettagliato|Percentuale della cache dello stato dell'autenticatore del token di negoziazione: %1\/%2|Quota|  
|[1424 \- SecuritySessionRatio](../../../../../docs/framework/wcf/diagnostics/etw/1424-securitysessionratio.md)|Dettagliato|Percentuale sessioni di sicurezza: %1\/%2|Quota|  
|[1430 \- PendingConnectionsRatio](../../../../../docs/framework/wcf/diagnostics/etw/1430-pendingconnectionsratio.md)|Dettagliato|Percentuale connessioni in sospeso: %1\/%2|Quota|  
|[1431 \- ConcurrentCallsRatio](../../../../../docs/framework/wcf/diagnostics/etw/1431-concurrentcallsratio.md)|Dettagliato|Percentuale sessioni simultanee: %1\/%2|Quota|  
|[1432 \- ConcurrentSessionsRatio](../../../../../docs/framework/wcf/diagnostics/etw/1432-concurrentsessionsratio.md)|Dettagliato|Percentuale sessioni simultanee: %1\/%2|Quota|  
|[1433 \- OutboundConnectionsPerEndpointRatio](../../../../../docs/framework/wcf/diagnostics/etw/1433-outboundconnectionsperendpointratio.md)|Dettagliato|Percentuale connessioni in uscita per endpoint: %1\/%2|Quota|  
|[1433 \- OutboundConnectionsPerEndpointRatio](../../../../../docs/framework/wcf/diagnostics/etw/1433-outboundconnectionsperendpointratio.md)|Dettagliato|Percentuale connessioni in uscita per endpoint: %1\/%2|Quota|  
|[1436 \- PendingMessagesPerChannelRatio](../../../../../docs/framework/wcf/diagnostics/etw/1436-pendingmessagesperchannelratio.md)|Dettagliato|Percentuale messaggi in sospeso per canale: %1\/%2|Quota|  
|[1438 \- ConcurrentInstancesRatio](../../../../../docs/framework/wcf/diagnostics/etw/1438-concurrentinstancesratio.md)|Dettagliato|Percentuale istanze simultanee: %1\/%2|Quota|  
|[1439 \- PendingAcceptsAtZero](../../../../../docs/framework/wcf/diagnostics/etw/1439-pendingacceptsatzero.md)|Informazioni|Zero accettazioni in sospeso rimaste|Quota|  
|[1441 \- MaxSessionSizeReached](../../../../../docs/framework/wcf/diagnostics/etw/1441-maxsessionsizereached.md)|Avviso|1%|Quota|  
|[1442 \- ReceiveRetryCountReached](../../../../../docs/framework/wcf/diagnostics/etw/1442-receiveretrycountreached.md)|Avviso|Numero tentativi di ricezione raggiunto nel messaggio MSMQ con ID '%1'|Quota|  
|[1443 \- MaxRetryCyclesExceededMsmq](../../../../../docs/framework/wcf/diagnostics/etw/1443-maxretrycyclesexceededmsmq.md)|Errore|Numero massimo cicli di nuovi tentativi superato nel messaggio MSMQ con ID '%1'|Quota|  
|[1445 \- ReadPoolMiss](../../../../../docs/framework/wcf/diagnostics/etw/1445-readpoolmiss.md)|Dettagliato|Creato nuovo '%1'|Quota|  
|[1446 \- WritePoolMiss](../../../../../docs/framework/wcf/diagnostics/etw/1446-writepoolmiss.md)|Dettagliato|Creato nuovo '%1'|Quota|  
|[1451 \- MaxRetryCyclesExceeded](../../../../../docs/framework/wcf/diagnostics/etw/1451-maxretrycyclesexceeded.md)|Errore|1%|Quota|  
|[3300 \- ReceiveContextCompleteFailed](../../../../../docs/framework/wcf/diagnostics/etw/3300-receivecontextcompletefailed.md)|Avviso|Impossibile completare %1.|Canale|  
|[3301 \- ReceiveContextAbandonFailed](../../../../../docs/framework/wcf/diagnostics/etw/3301-receivecontextabandonfailed.md)|Avviso|Impossibile abbandonare %1.|Canale|  
|[3303 \- ReceiveContextAbandonWithException](../../../../../docs/framework/wcf/diagnostics/etw/3303-receivecontextabandonwithexception.md)|Avviso|Contesto di ricezione non riuscito.|ServiceModel|  
|[3303 \- ReceiveContextAbandonWithException](../../../../../docs/framework/wcf/diagnostics/etw/3303-receivecontextabandonwithexception.md)|Informazioni|%1 è stato abbandonato con l'eccezione %2.|Canale|  
|[3305 \- ClientBaseCachedChannelFactoryCount](../../../../../docs/framework/wcf/diagnostics/etw/3305-clientbasecachedchannelfactorycount.md)|Informazioni|Il numero di channel factory memorizzato nella cache è: '%1'. È possibile memorizzare nella cache al massimo '%2' channel factory.|ServiceModel|  
|[3306 \- ClientBaseChannelFactoryAgedOutofCache](../../../../../docs/framework/wcf/diagnostics/etw/3306-clientbasechannelfactoryagedoutofcache.md)|Informazioni|Una channel factory è stata rimossa dalla cache perché è stato raggiunto il limite di '%1' della cache.|ServiceModel|  
|[3307 \- ClientBaseChannelFactoryCacheHit](../../../../../docs/framework/wcf/diagnostics/etw/3307-clientbasechannelfactorycachehit.md)|Informazioni|Channel factory corrispondente usata trovata nella cache.|ServiceModel|  
|[3308 \- ClientBaseUsingLocalChannelFactory](../../../../../docs/framework/wcf/diagnostics/etw/3308-clientbaseusinglocalchannelfactory.md)|Informazioni|Channel factory della cache non usata.  Memorizzazione nella cache disattivata.|ServiceModel|  
|[3309 \- QueryCompositionExecuted](../../../../../docs/framework/wcf/diagnostics/etw/3309-querycompositionexecuted.md)|Informazioni|Composizione query mediante '%1' eseguita sull'URI di richiesta: '%2'.|ServiceModel|  
|[3310 \- DispatchFailed](../../../../../docs/framework/wcf/diagnostics/etw/3310-dispatchfailed.md)|Errore|L'operazione '%1' è stata inviata con errori.|ServiceModel|  
|[3311 \- DispatchSuccessful](../../../../../docs/framework/wcf/diagnostics/etw/3311-dispatchsuccessful.md)|Informazioni|L'operazione '%1' è stata inviata correttamente.|ServiceModel|  
|[3312 \- MessageReadByEncoder](../../../../../docs/framework/wcf/diagnostics/etw/3312-messagereadbyencoder.md)|Informazioni|Un messaggio di dimensioni '%1' byte è stato letto dal codificatore.|Canale|  
|[3312 \- MessageReadByEncoder](../../../../../docs/framework/wcf/diagnostics/etw/3312-messagereadbyencoder.md)|Informazioni|Un messaggio di dimensioni '%1' byte è stato scritto dal codificatore.|Canale|  
|[3314 \- SessionIdleTimeout](../../../../../docs/framework/wcf/diagnostics/etw/3314-sessionidletimeout.md)|Errore|Interruzione sessione per canale di inattività nell'URI:'%1'.|ServiceModel|  
|[3319 \- SocketAcceptEnqueued](../../../../../docs/framework/wcf/diagnostics/etw/3319-socketacceptenqueued.md)|Dettagliato|Accettazione connessione avviata.|TCP|  
|[3320 \- SocketAccepted](../../../../../docs/framework/wcf/diagnostics/etw/3320-socketaccepted.md)|Dettagliato|ListenerId:%1 accettato SocketId:%2.|TCP|  
|[3321 \- ConnectionPoolMiss](../../../../../docs/framework/wcf/diagnostics/etw/3321-connectionpoolmiss.md)|Dettagliato|Il pool per %1 non ha nessuna connessione disponibile e %2 connessioni occupate.|Canale|  
|[3322 \- DispatchFormatterDeserializeRequestStart](../../../../../docs/framework/wcf/diagnostics/etw/3322-dispatchformatterdeserializerequeststart.md)|Dettagliato|Il dispatcher ha avviato la deserializzazione del messaggio di richiesta.|ServiceModel|  
|[3323 \- DispatchFormatterDeserializeRequestStop](../../../../../docs/framework/wcf/diagnostics/etw/3323-dispatchformatterdeserializerequeststop.md)|Dettagliato|Il dispatcher ha completato la deserializzazione del messaggio di richiesta.|ServiceModel|  
|[3324 \- DispatchFormatterSerializeReplyStart](../../../../../docs/framework/wcf/diagnostics/etw/3324-dispatchformatterserializereplystart.md)|Dettagliato|Il dispatcher ha avviato la serializzazione del messaggio di risposta.|ServiceModel|  
|[3325 \- DispatchFormatterSerializeReplyStop](../../../../../docs/framework/wcf/diagnostics/etw/3325-dispatchformatterserializereplystop.md)|Dettagliato|Il dispatcher ha completato la serializzazione del messaggio di risposta.|ServiceModel|  
|[3326 \- ClientFormatterSerializeRequestStart](../../../../../docs/framework/wcf/diagnostics/etw/3326-clientformatterserializerequeststart.md)|Dettagliato|Serializzazione richiesta del client avviata.|ServiceModel|  
|[3327 \- ClientFormatterSerializeRequestStop](../../../../../docs/framework/wcf/diagnostics/etw/3327-clientformatterserializerequeststop.md)|Dettagliato|Il cliente ha completato la serializzazione del messaggio di richiesta.|ServiceModel|  
|[3328 \- ClientFormatterDeserializeReplyStart](../../../../../docs/framework/wcf/diagnostics/etw/3328-clientformatterdeserializereplystart.md)|Dettagliato|Il client ha avviato la deserializzazione del messaggio di risposta.|ServiceModel|  
|[3329 \- ClientFormatterDeserializeReplyStop](../../../../../docs/framework/wcf/diagnostics/etw/3329-clientformatterdeserializereplystop.md)|Dettagliato|Il client ha completato la deserializzazione del messaggio di risposta.|ServiceModel|  
|[3330 \- SecurityNegotiationStart](../../../../../docs/framework/wcf/diagnostics/etw/3330-securitynegotiationstart.md)|Dettagliato|Negoziazione di sicurezza avviata.|Sicurezza|  
|[3331 \- SecurityNegotiationStop](../../../../../docs/framework/wcf/diagnostics/etw/3331-securitynegotiationstop.md)|Dettagliato|Negoziazione di sicurezza completata.|Sicurezza|  
|[3332 \- SecurityTokenProviderOpened](../../../../../docs/framework/wcf/diagnostics/etw/3332-securitytokenprovideropened.md)|Dettagliato|Apertura SecurityTokenProvider completata.|Sicurezza|  
|[3333 \- OutgoingMessageSecured](../../../../../docs/framework/wcf/diagnostics/etw/3333-outgoingmessagesecured.md)|Dettagliato|Messaggio in uscita protetto.|Sicurezza|  
|[3334 \- IncomingMessageVerified](../../../../../docs/framework/wcf/diagnostics/etw/3334-incomingmessageverified.md)|Dettagliato|Messaggio in ingresso verificato.|Security ServiceModel|  
|[3335 \- GetServiceInstanceStart](../../../../../docs/framework/wcf/diagnostics/etw/3335-getserviceinstancestart.md)|Dettagliato|Recupero istanza del servizio avviato.|ServiceModel|  
|[3336 \- GetServiceInstanceStop](../../../../../docs/framework/wcf/diagnostics/etw/3336-getserviceinstancestop.md)|Dettagliato|Istanza del servizio recuperata.|ServiceModel|  
|[3337 \- ChannelReceiveStart](../../../../../docs/framework/wcf/diagnostics/etw/3337-channelreceivestart.md)|Dettagliato|ChannelHandlerId:%1 \- Ciclo ricezione messaggio avviato.|Canale|  
|[3338 \- ChannelReceiveStop](../../../../../docs/framework/wcf/diagnostics/etw/3338-channelreceivestop.md)|Dettagliato|ChannelHandlerId:%1 \- Ciclo ricezione messaggio arrestato.|Canale|  
|[3339 \- ChannelFactoryCreated](../../../../../docs/framework/wcf/diagnostics/etw/3339-channelfactorycreated.md)|Dettagliato|ChannelFactory creata.|ServiceModel|  
|[3340 \- PipeConnectionAcceptStart](../../../../../docs/framework/wcf/diagnostics/etw/3340-pipeconnectionacceptstart.md)|Dettagliato|Accettazione connessione pipe avviata su %1.|Canale|  
|[3341 \- PipeConnectionAcceptStop](../../../../../docs/framework/wcf/diagnostics/etw/3341-pipeconnectionacceptstop.md)|Dettagliato|Connessione pipe accettata.|Canale|  
|[3342 \- EstablishConnectionStart](../../../../../docs/framework/wcf/diagnostics/etw/3342-establishconnectionstart.md)|Dettagliato|Attivazione della connessione avviata per %1.|Canale|  
|[3343 \- EstablishConnectionStop](../../../../../docs/framework/wcf/diagnostics/etw/3343-establishconnectionstop.md)|Dettagliato|Connessione stabilita.|Canale|  
|[3345 \- SessionPreambleUnderstood](../../../../../docs/framework/wcf/diagnostics/etw/3345-sessionpreambleunderstood.md)|Dettagliato|Preambolo sessione per '%1' riconosciuto.|Canale|  
|[3346 \- ConnectionReaderSendFault](../../../../../docs/framework/wcf/diagnostics/etw/3346-connectionreadersendfault.md)|Errore|Invio errore '%1' da parte del lettore di connessione.|Canale|  
|[3347 \- SocketAcceptClosed](../../../../../docs/framework/wcf/diagnostics/etw/3347-socketacceptclosed.md)|Dettagliato|Accettazione socket chiusa.|TCP|  
|[3348 \- ServiceHostFaulted](../../../../../docs/framework/wcf/diagnostics/etw/3348-servicehostfaulted.md)|Critical|Errore host del servizio.|TCP|  
|[3349 \- ListenerOpenStart](../../../../../docs/framework/wcf/diagnostics/etw/3349-listeneropenstart.md)|Dettagliato|Apertura listener per '%1'.|Canale|  
|[3350 \- ListenerOpenStop](../../../../../docs/framework/wcf/diagnostics/etw/3350-listeneropenstop.md)|Dettagliato|Apertura listener completata.|Canale|  
|[3351 \- ServerMaxPooledConnectionsQuotaReached](../../../../../docs/framework/wcf/diagnostics/etw/3351-servermaxpooledconnectionsquotareached.md)|Dettagliato|Quota massima connessioni server in pool di server raggiunta.|Quota|  
|[3352 \- TcpConnectionTimedOut](../../../../../docs/framework/wcf/diagnostics/etw/3352-tcpconnectiontimedout.md)|Errore|SocketId:%1: all'indirizzo remoto %2 scaduto.|TCP|  
|[3353 \- TcpConnectionResetError](../../../../../docs/framework/wcf/diagnostics/etw/3353-tcpconnectionreseterror.md)|Avviso|SocketId:%1 all'indirizzo remoto %2 con errore di reimpostazione della connessione.|TCP|  
|[3354 \- ServiceSecurityNegotiationCompleted](../../../../../docs/framework/wcf/diagnostics/etw/3354-servicesecuritynegotiationcompleted.md)|Dettagliato|Negoziazione di sicurezza del servizio completata.|Sicurezza|  
|[3355 \- SecurityNegotiationProcessingFailure](../../../../../docs/framework/wcf/diagnostics/etw/3355-securitynegotiationprocessingfailure.md)|Errore|Elaborazione della negoziazione di sicurezza non riuscita.|Sicurezza|  
|[3356 \- SecurityIdentityVerificationSuccess](../../../../../docs/framework/wcf/diagnostics/etw/3356-securityidentityverificationsuccess.md)|Dettagliato|Verifica di sicurezza completata.|Sicurezza|  
|[3357 \- SecurityIdentityVerificationFailure](../../../../../docs/framework/wcf/diagnostics/etw/3357-securityidentityverificationfailure.md)|Errore|Verifica di sicurezza non riuscita.|Sicurezza|  
|[3358 \- PortSharingDuplicatedSocket](../../../../../docs/framework/wcf/diagnostics/etw/3358-portsharingduplicatedsocket.md)|Dettagliato|Socket duplicato per %1.|ActivationServices|  
|[3359 \- SecurityImpersonationSuccess](../../../../../docs/framework/wcf/diagnostics/etw/3359-securityimpersonationsuccess.md)|Dettagliato|Rappresentazione sicurezza riuscita.|Sicurezza|  
|[3360 \- SecurityImpersonationFailure](../../../../../docs/framework/wcf/diagnostics/etw/3360-securityimpersonationfailure.md)|Avviso|Rappresentazione sicurezza non riuscita.|Sicurezza|  
|[3361 \- HttpChannelRequestAborted](../../../../../docs/framework/wcf/diagnostics/etw/3361-httpchannelrequestaborted.md)|Avviso|Richiesta canale HTTP interrotta.|HTTP|  
|[3362 \- HttpChannelResponseAborted](../../../../../docs/framework/wcf/diagnostics/etw/3362-httpchannelresponseaborted.md)|Avviso|Risposta canale HTTP interrotta.|HTTP|  
|[3363 \- HttpAuthFailed](../../../../../docs/framework/wcf/diagnostics/etw/3363-httpauthfailed.md)|Avviso|Autenticazione HTTP non riuscita.|HTTP|  
|[3364 \- SharedListenerProxyRegisterStart](../../../../../docs/framework/wcf/diagnostics/etw/3364-sharedlistenerproxyregisterstart.md)|Dettagliato|Registrazione di SharedListenerProxy avviata per l'URI '%1'.|ActivationServices|  
|[3365 \- SharedListenerProxyRegisterStop](../../../../../docs/framework/wcf/diagnostics/etw/3365-sharedlistenerproxyregisterstop.md)|Dettagliato|Arresto del registro SharedListenerProxy.|ActivationServices|  
|[3366 \- SharedListenerProxyRegisterFailed](../../../../../docs/framework/wcf/diagnostics/etw/3366-sharedlistenerproxyregisterfailed.md)|Errore|Registro SharedListenerProxy non riuscito con stato '%1'.|ActivationServices|  
|[3367 \- ConnectionPoolPreambleFailed](../../../../../docs/framework/wcf/diagnostics/etw/3367-connectionpoolpreamblefailed.md)|Errore|ConnectionPoolPreambleFailed.|Canale|  
|[3368 \- SslOnInitiateUpgrade](../../../../../docs/framework/wcf/diagnostics/etw/3368-ssloninitiateupgrade.md)|Dettagliato|SslOnAcceptUpgradeStart|Sicurezza|  
|[3369 \- SslOnAcceptUpgrade](../../../../../docs/framework/wcf/diagnostics/etw/3369-sslonacceptupgrade.md)|Dettagliato|SslOnAcceptUpgradeStop|Sicurezza|  
|[3370 \- BinaryMessageEncodingStart](../../../../../docs/framework/wcf/diagnostics/etw/3370-binarymessageencodingstart.md)|Dettagliato|BinaryMessageEncoder ha avviato la codifica del messaggio.|Canale|  
|[3371 \- MtomMessageEncodingStart](../../../../../docs/framework/wcf/diagnostics/etw/3371-mtommessageencodingstart.md)|Dettagliato|MtomMessageEncoder ha avviato la codifica del messaggio.|Canale|  
|[3372 \- TextMessageEncodingStart](../../../../../docs/framework/wcf/diagnostics/etw/3372-textmessageencodingstart.md)|Dettagliato|TextMessageEncoder ha avviato la codifica del messaggio.|Canale|  
|[3373 \- BinaryMessageDecodingStart](../../../../../docs/framework/wcf/diagnostics/etw/3373-binarymessagedecodingstart.md)|Dettagliato|BinaryMessageEncoder ha avviato la decodifica del messaggio.|Canale|  
|[3374 \- MtomMessageDecodingStart](../../../../../docs/framework/wcf/diagnostics/etw/3374-mtommessagedecodingstart.md)|Dettagliato|MtomMessageEncoder ha avviato la decodifica del messaggio.|Canale|  
|[3375 \- TextMessageDecodingStart](../../../../../docs/framework/wcf/diagnostics/etw/3375-textmessagedecodingstart.md)|Dettagliato|TextMessageEncoder ha avviato la decodifica del messaggio.|Canale|  
|[3376 \- HttpResponseReceiveStart](../../../../../docs/framework/wcf/diagnostics/etw/3376-httpresponsereceivestart.md)|Informazioni|Il trasporto HTTP ha avviato la ricezione di un messaggio.|HTTP|  
|[3377 \- SocketReadStop](../../../../../docs/framework/wcf/diagnostics/etw/3377-socketreadstop.md)|Dettagliato|SocketId:%1 letti '%2' byte da '%3'.|TCP|  
|[3378 \- SocketAsyncReadStop](../../../../../docs/framework/wcf/diagnostics/etw/3378-socketasyncreadstop.md)|Dettagliato|SocketId:%1 letti '%2' byte da '%3'.|TCP|  
|[3379 \- SocketWriteStart](../../../../../docs/framework/wcf/diagnostics/etw/3379-socketwritestart.md)|Dettagliato|SocketId:%1 scrittura di '%2' byte in '%3' in corso.|TCP|  
|[3380 \- SocketAsyncWriteStart](../../../../../docs/framework/wcf/diagnostics/etw/3380-socketasyncwritestart.md)|Dettagliato|SocketId:%1 scrittura di '%2' byte in '%3' in corso.|TCP|  
|[3381 \- SequenceAcknowledgementSent](../../../../../docs/framework/wcf/diagnostics/etw/3381-sequenceacknowledgementsent.md)|Dettagliato|Acknowledgement SessionId:%1 inviato.|Canale|  
|[3382 \- ClientReliableSessionReconnect](../../../../../docs/framework/wcf/diagnostics/etw/3382-clientreliablesessionreconnect.md)|Informazioni|Riconnessione SessionId:%1.|Canale|  
|[3383 \- ReliableSessionChannelFaulted](../../../../../docs/framework/wcf/diagnostics/etw/3383-reliablesessionchannelfaulted.md)|Informazioni|Errore SessionId:%1.|Canale|  
|[3384 \- WindowsStreamSecurityOnInitiateUpgrade](../../../../../docs/framework/wcf/diagnostics/etw/3384-windowsstreamsecurityoninitiateupgrade.md)|Dettagliato|Avvio dell'aggiornamento di sicurezza da parte di WindowsStreamSecurity.|Sicurezza|  
|[3385 \- WindowsStreamSecurityOnAcceptUpgrade](../../../../../docs/framework/wcf/diagnostics/etw/3385-windowsstreamsecurityonacceptupgrade.md)|Dettagliato|Sicurezza flusso Windows all'accettazione dell'aggiornamento.|Sicurezza|  
|[3386 \- SocketConnectionAbort](../../../../../docs/framework/wcf/diagnostics/etw/3386-socketconnectionabort.md)|Avviso|Interruzione SocketId:%1 in corso.|TCP|  
|[3388 \- HttpGetContextStart](../../../../../docs/framework/wcf/diagnostics/etw/3388-httpgetcontextstart.md)|Dettagliato|Avvio di HttpGetContex.|HTTP|  
|[3389 \- ClientSendPreambleStart](../../../../../docs/framework/wcf/diagnostics/etw/3389-clientsendpreamblestart.md)|Dettagliato|Avvio dell'invio del preambolo da parte del client.|Canale|  
|[3390 \- ClientSendPreambleStop](../../../../../docs/framework/wcf/diagnostics/etw/3390-clientsendpreamblestop.md)|Dettagliato|Arresto dell'invio del preambolo da parte del client.|Canale|  
|[3391 \- HttpMessageReceiveFailed](../../../../../docs/framework/wcf/diagnostics/etw/3391-httpmessagereceivefailed.md)|Avviso|Ricezione messaggio HTTP non riuscita.|HTTP|  
|[3392 \- TransactionScopeCreate](../../../../../docs/framework/wcf/diagnostics/etw/3392-transactionscopecreate.md)|Informazioni|TransactionScope creato con LocalIdentifier:'%1' e DistributedIdentifier:'%2'.|ServiceModel|  
|[3393 \- StreamedMessageReadByEncoder](../../../../../docs/framework/wcf/diagnostics/etw/3393-streamedmessagereadbyencoder.md)|Informazioni|Un messaggio trasmesso è stato letto dal codificatore.|Canale|  
|[3394 \- StreamedMessageWrittenByEncoder](../../../../../docs/framework/wcf/diagnostics/etw/3394-streamedmessagewrittenbyencoder.md)|Informazioni|Un messaggio trasmesso è stato scritto dal codificatore.|Canale|  
|[3395 \- MessageWrittenAsynchronouslyByEncoder](../../../../../docs/framework/wcf/diagnostics/etw/3395-messagewrittenasynchronouslybyencoder.md)|Informazioni|Un messaggio è stato scritto in modo asincrono dal codificatore.|Canale|  
|[3396 \- BufferedAsyncWriteStart](../../../../../docs/framework/wcf/diagnostics/etw/3396-bufferedasyncwritestart.md)|Informazioni|BufferId:%1 ha completato la scrittura di '%2' byte per il flusso sottostante.|Canale|  
|[3397 \- BufferedAsyncWriteStop](../../../../../docs/framework/wcf/diagnostics/etw/3397-bufferedasyncwritestop.md)|Informazioni|Un messaggio è stato scritto in modo asincrono dal codificatore.|Canale|  
|[3398 \- PipeSharedMemoryCreated](../../../../../docs/framework/wcf/diagnostics/etw/3398-pipesharedmemorycreated.md)|Dettagliato|Memoria condivisa della pipe creata in '%1'.|Canale|  
|[3399 \- NamedPipeCreated](../../../../../docs/framework/wcf/diagnostics/etw/3399-namedpipecreated.md)|Dettagliato|NamedPipe '%1' creato.|Canale|  
|[3401 \- SignatureVerificationStart](../../../../../docs/framework/wcf/diagnostics/etw/3401-signatureverificationstart.md)|Dettagliato|Avviata verifica della firma.|Sicurezza|  
|[3402 \- SignatureVerificationSuccess](../../../../../docs/framework/wcf/diagnostics/etw/3402-signatureverificationsuccess.md)|Dettagliato|Verifica della firma completata|Sicurezza|  
|[3403 \- WrappedKeyDecryptionStart](../../../../../docs/framework/wcf/diagnostics/etw/3403-wrappedkeydecryptionstart.md)|Dettagliato|Decrittografia della chiave di cui è stato eseguito il wrapping completata.|Sicurezza|  
|[3404 \- WrappedKeyDecryptionSuccess](../../../../../docs/framework/wcf/diagnostics/etw/3404-wrappedkeydecryptionsuccess.md)|Dettagliato|Decrittografia chiave di cui è stato eseguito il wrapping completata.|Sicurezza|  
|[3405 \- EncryptedDataProcessingStart](../../../../../docs/framework/wcf/diagnostics/etw/3405-encrypteddataprocessingstart.md)|Dettagliato|Elaborazione dati crittografati avviata.|Sicurezza|  
|[3406 \- EncryptedDataProcessingSuccess](../../../../../docs/framework/wcf/diagnostics/etw/3406-encrypteddataprocessingsuccess.md)|Dettagliato|Elaborazione dati crittografati completata.|Sicurezza|  
|[3407 \- HttpPipelineProcessInboundRequestStart](../../../../../docs/framework/wcf/diagnostics/etw/3407-httppipelineprocessinboundrequeststart.md)|Dettagliato|Elaborazione della richiesta in ingresso avviata dal gestore di messaggi HTTP.|HTTP|  
|[3408 \- HttpPipelineBeginProcessInboundRequestStart](../../../../../docs/framework/wcf/diagnostics/etw/3408-httppipelinebeginprocessinboundrequeststart.md)|Dettagliato|Elaborazione asincrona della richiesta in ingresso avviata dal gestore di messaggi HTTP.|HTTP|  
|[3409 \- HttpPipelineProcessInboundRequestStop](../../../../../docs/framework/wcf/diagnostics/etw/3409-httppipelineprocessinboundrequeststop.md)|Dettagliato|Elaborazione della richiesta in ingresso completata dal gestore di messaggi HTTP.|HTTP|  
|[3410 \- HttpPipelineFaulted](../../../../../docs/framework/wcf/diagnostics/etw/3410-httppipelinefaulted.md)|Avviso|Errore del gestore di messaggi HTTP.|HTTP|  
|[3411 \- HttpPipelineTimeoutException](../../../../../docs/framework/wcf/diagnostics/etw/3411-httppipelinetimeoutexception.md)|Errore|Timeout della connessione WebSocket.|HTTP|  
|[3412 \- HttpPipelineProcessResponseStart](../../../../../docs/framework/wcf/diagnostics/etw/3412-httppipelineprocessresponsestart.md)|Dettagliato|Elaborazione della risposta avviata dal gestore di messaggi HTTP.|HTTP|  
|[3413 \- HttpPipelineBeginProcessResponseStart](../../../../../docs/framework/wcf/diagnostics/etw/3413-httppipelinebeginprocessresponsestart.md)|Dettagliato|Elaborazione asincrona della risposta avviata dal gestore di messaggi HTTP.|HTTP|  
|[3414 \- HttpPipelineProcessResponseStop](../../../../../docs/framework/wcf/diagnostics/etw/3414-httppipelineprocessresponsestop.md)|Dettagliato|Elaborazione della risposta completata dal gestore di messaggi HTTP.|HTTP|  
|[3415 \- WebSocketConnectionRequestSendStart](../../../../../docs/framework/wcf/diagnostics/etw/3415-websocketconnectionrequestsendstart.md)|Dettagliato|Avvio dell'invio della richiesta di connessione WebSocket a '%1'.|HTTP|  
|[3416 \- WebSocketConnectionRequestSendStop](../../../../../docs/framework/wcf/diagnostics/etw/3416-websocketconnectionrequestsendstop.md)|Dettagliato|WebSocketId:%1 richiesta di connessione inviata.|HTTP|  
|[3417 \- WebSocketConnectionAcceptStart](../../../../../docs/framework/wcf/diagnostics/etw/3417-websocketconnectionacceptstart.md)|Dettagliato|Avvio accettazione connessione WebSocket.|HTTP|  
|[3418 \- WebSocketConnectionAccepted](../../../../../docs/framework/wcf/diagnostics/etw/3418-websocketconnectionaccepted.md)|Dettagliato|WebSocketId: %1 connessione accettata.|HTTP|  
|[3419 \- WebSocketConnectionDeclined](../../../../../docs/framework/wcf/diagnostics/etw/3419-websocketconnectiondeclined.md)|Errore|Connessione WebSocket rifiutata con codice di stato '%1'|HTTP|  
|[3420 \- WebSocketConnectionFailed](../../../../../docs/framework/wcf/diagnostics/etw/3420-websocketconnectionfailed.md)|Errore|Richiesta di connessione WebSocket non riuscita: '%1'|HTTP|  
|[3421 \- WebSocketConnectionAborted](../../../../../docs/framework/wcf/diagnostics/etw/3421-websocketconnectionaborted.md)|Errore|WebSocketId: %1 connessione interrotta.|HTTP|  
|[3422 \- WebSocketAsyncWriteStart](../../../../../docs/framework/wcf/diagnostics/etw/3422-websocketasyncwritestart.md)|Dettagliato|WebSocketId: %1 scrittura di '%2' byte a '%3'.|HTTP|  
|[3423 \- WebSocketAsyncWriteStop](../../../../../docs/framework/wcf/diagnostics/etw/3423-websocketasyncwritestop.md)|Dettagliato|WebSocketId: %1 arresto scrittura asincrona.|HTTP|  
|[3424 \- WebSocketAsyncReadStart](../../../../../docs/framework/wcf/diagnostics/etw/3424-websocketasyncreadstart.md)|Dettagliato|WebSocketId: %1 avvio lettura.|HTTP|  
|[3425 \- WebSocketAsyncReadStop](../../../../../docs/framework/wcf/diagnostics/etw/3425-websocketasyncreadstop.md)|Dettagliato|WebSocketId: %1 letti '%2' byte da '%3'.|HTTP|  
|[3426 \- WebSocketCloseSent](../../../../../docs/framework/wcf/diagnostics/etw/3426-websocketclosesent.md)|Dettagliato|WebSocketId: %1 invio messaggio di chiusura a '%2' con stato di chiusura '%3'.|HTTP|  
|[3427 \- WebSocketCloseOutputSent](../../../../../docs/framework/wcf/diagnostics/etw/3427-websocketcloseoutputsent.md)|Dettagliato|WebSocketId: %1 invio messaggio di output di chiusura a '%2' con stato di chiusura '%3'.|HTTP|  
|[3428 \- WebSocketConnectionClosed](../../../../../docs/framework/wcf/diagnostics/etw/3428-websocketconnectionclosed.md)|Dettagliato|WebSocketId:%1 connessione chiusa.|HTTP|  
|[3429 \- WebSocketCloseStatusReceived](../../../../../docs/framework/wcf/diagnostics/etw/3429-websocketclosestatusreceived.md)|Dettagliato|WebSocketId: %1 messaggio di chiusura connessione ricevuto con stato '%2'.|HTTP|  
|[3430 \- WebSocketUseVersionFromClientWebSocketFactory](../../../../../docs/framework/wcf/diagnostics/etw/3430-websocketuseversionfromclientwebsocketfactory.md)|Dettagliato|Uso di WebSocketVersion da una factory WebSocket client di tipo '%1'.|HTTP|  
|[3431 \- WebSocketCreateClientWebSocketWithFactory](../../../../../docs/framework/wcf/diagnostics/etw/3431-websocketcreateclientwebsocketwithfactory.md)|Dettagliato|Creazione del client WebSocket con una factory di tipo '%1'.|HTTP|  
|[3553 \- XamlServicesLoadStart](../../../../../docs/framework/wcf/diagnostics/etw/3553-xamlservicesloadstart.md)|Informazioni|Avvio di XamlServicesLoad|WebHost|  
|[3554 \- XamlServicesLoadStop](../../../../../docs/framework/wcf/diagnostics/etw/3554-xamlservicesloadstop.md)|Informazioni|Arresto di XamlServicesLoad|WebHost|  
|[3555 \- CreateWorkflowServiceHostStart](../../../../../docs/framework/wcf/diagnostics/etw/3555-createworkflowservicehoststart.md)|Informazioni|Avvio di CreateWorkflowServiceHost|WebHost|  
|[3556 \- CreateWorkflowServiceHostStop](../../../../../docs/framework/wcf/diagnostics/etw/3556-createworkflowservicehoststop.md)|Informazioni|Arresto di CreateWorkflowServiceHost|WebHost|  
|[3558 \- ServiceActivationStart](../../../../../docs/framework/wcf/diagnostics/etw/3558-serviceactivationstart.md)|Informazioni|Avvio attivazione del servizio|WebHost|  
|[3559 \- ServiceActivationStop](../../../../../docs/framework/wcf/diagnostics/etw/3559-serviceactivationstop.md)|Informazioni|Arresto attivazione del servizio|WebHost|  
|[3560 \- ServiceActivationAvailableMemory](../../../../../docs/framework/wcf/diagnostics/etw/3560-serviceactivationavailablememory.md)|Dettagliato|Memoria disponibile \(byte\): %1|Quota|  
|[3800 \- RoutingServiceClosingClient](../../../../../docs/framework/wcf/diagnostics/etw/3800-routingserviceclosingclient.md)|Informazioni|Servizio di routing: è in corso la chiusura del client '%1'.|RoutingServices|  
|[3800 \- RoutingServiceClosingClient](../../../../../docs/framework/wcf/diagnostics/etw/3800-routingserviceclosingclient.md)|Avviso|Errore del client '%1' del servizio di routing.|RoutingServices|  
|[3802 \- RoutingServiceCompletingOneWay](../../../../../docs/framework/wcf/diagnostics/etw/3802-routingservicecompletingoneway.md)|Informazioni|Completamento in corso di un messaggio unidirezionale del servizio di routing.|RoutingServices|  
|[3803 \- RoutingServiceProcessingFailure](../../../../../docs/framework/wcf/diagnostics/etw/3803-routingserviceprocessingfailure.md)|Errore|Errore del servizio di routing durante l'elaborazione di un messaggio nell'endpoint con indirizzo '%1'.|RoutingServices|  
|[3804 \- RoutingServiceCreatingClientForEndpoint](../../../../../docs/framework/wcf/diagnostics/etw/3804-routingservicecreatingclientforendpoint.md)|Informazioni|Servizio di routing: è in corso la creazione di un client per l'endpoint: '%1'.|RoutingServices|  
|[3805 \- RoutingServiceDisplayConfig](../../../../../docs/framework/wcf/diagnostics/etw/3805-routingservicedisplayconfig.md)|Dettagliato|Servizio di routing configurato con RouteOnHeadersOnly: %1, SoapProcessingEnabled: %2, EnsureOrderedDispatch: %3.|RoutingServices|  
|[3807 \- RoutingServiceCompletingTwoWay](../../../../../docs/framework/wcf/diagnostics/etw/3807-routingservicecompletingtwoway.md)|Informazioni|Completamento in corso di un messaggio di risposta a una richiesta del servizio di routing.|RoutingServices|  
|[3809 \- RoutingServiceMessageRoutedToEndpoints](../../../../../docs/framework/wcf/diagnostics/etw/3809-routingservicemessageroutedtoendpoints.md)|Dettagliato|Il servizio di routing ha indirizzato il messaggio con ID '%1' a %2 elenchi di endpoint.|RoutingServices|  
|[3810 \- RoutingServiceConfigurationApplied](../../../../../docs/framework/wcf/diagnostics/etw/3810-routingserviceconfigurationapplied.md)|Informazioni|Nuova RoutingConfiguration applicata al servizio di routing.|RoutingServices|  
|[3815 \- RoutingServiceProcessingMessage](../../../../../docs/framework/wcf/diagnostics/etw/3815-routingserviceprocessingmessage.md)|Informazioni|Servizio di routing: è in corso l'elaborazione di un messaggio con ID '%1', azione '%2', URL in ingresso '%3' ricevuto nella transazione %4.|RoutingServices|  
|[3816 \- RoutingServiceTransmittingMessage](../../../../../docs/framework/wcf/diagnostics/etw/3816-routingservicetransmittingmessage.md)|Informazioni|Servizio di routing: è in corso la trasmissione del messaggio con ID '%1' \[operazione %2\] a '%3'.|RoutingServices|  
|[3817 \- RoutingServiceCommittingTransaction](../../../../../docs/framework/wcf/diagnostics/etw/3817-routingservicecommittingtransaction.md)|Informazioni|Servizio di routing: è in corso il commit di una transazione con ID '%1'.|RoutingServices|  
|[3818 \- RoutingServiceDuplexCallbackException](../../../../../docs/framework/wcf/diagnostics/etw/3818-routingserviceduplexcallbackexception.md)|Errore|Eccezione di callback duplex rilevata dal componente %1 del servizio di routing.|RoutingServices|  
|[3819 \- RoutingServiceMovedToBackup](../../../../../docs/framework/wcf/diagnostics/etw/3819-routingservicemovedtobackup.md)|Informazioni|Messaggio del servizio di routing con ID '%1' \[operazione %2\] spostato nell'endpoint di backup '%3'.|RoutingServices|  
|[3820 \- RoutingServiceCreatingTransaction](../../../../../docs/framework/wcf/diagnostics/etw/3820-routingservicecreatingtransaction.md)|Informazioni|Il servizio di routing ha creato una nuova transazione con ID '%1' per l'elaborazione di messaggi.|RoutingServices|  
|[3821 \- RoutingServiceCloseFailed](../../../../../docs/framework/wcf/diagnostics/etw/3821-routingserviceclosefailed.md)|Avviso|Errore del servizio di routing durante la chiusura del client in uscita '%1'.|RoutingServices|  
|[3822 \- RoutingServiceSendingResponse](../../../../../docs/framework/wcf/diagnostics/etw/3822-routingservicesendingresponse.md)|Informazioni|Servizio di routing: è in corso il reinvio di un messaggio di risposta con azione '%1'.|RoutingServices|  
|[3823 \- RoutingServiceSendingFaultResponse](../../../../../docs/framework/wcf/diagnostics/etw/3823-routingservicesendingfaultresponse.md)|Avviso|Servizio di routing: è in corso il reinvio di un messaggio di risposta di errore con azione '%1'.|RoutingServices|  
|[3824 \- RoutingServiceCompletingReceiveContext](../../../../../docs/framework/wcf/diagnostics/etw/3824-routingservicecompletingreceivecontext.md)|Dettagliato|Servizio di routing: è in corso la chiamata a ReceiveContext.Complete per il messaggio con ID '%1'.|RoutingServices|  
|[3825 \- RoutingServiceAbandoningReceiveContext](../../../../../docs/framework/wcf/diagnostics/etw/3825-routingserviceabandoningreceivecontext.md)|Avviso|Servizio di routing: è in corso la chiamata a ReceiveContext.Abandon per il messaggio con ID '%1'.|RoutingServices|  
|[3826 \- RoutingServiceUsingExistingTransaction](../../../../../docs/framework/wcf/diagnostics/etw/3826-routingserviceusingexistingtransaction.md)|Dettagliato|Il servizio di routing invierà messaggi tramite la transazione esistente '%1'.|RoutingServices|  
|[3827 \- RoutingServiceTransmitFailed](../../../../../docs/framework/wcf/diagnostics/etw/3827-routingservicetransmitfailed.md)|Avviso|Errore del servizio di routing durante l'invio a '%1'.|RoutingServices|  
|[3828 \- RoutingServiceFilterTableMatchStart](../../../../../docs/framework/wcf/diagnostics/etw/3828-routingservicefiltertablematchstart.md)|Informazioni|Inizio corrispondenza MessageFilterTable servizio di routing.|RoutingServices|  
|[3829 \- RoutingServiceFilterTableMatchStop](../../../../../docs/framework/wcf/diagnostics/etw/3829-routingservicefiltertablematchstop.md)|Informazioni|Arresto corrispondenza MessageFilterTable servizio di routing.|RoutingServices|  
|[3830 \- RoutingServiceAbortingChannel](../../../../../docs/framework/wcf/diagnostics/etw/3830-routingserviceabortingchannel.md)|Dettagliato|Il servizio di routing richiede l'interruzione sul canale: '%1'.|RoutingServices|  
|[3831 \- RoutingServiceHandledException](../../../../../docs/framework/wcf/diagnostics/etw/3831-routingservicehandledexception.md)|Dettagliato|Eccezione gestita dal servizio di routing.|RoutingServices|  
|[3832 \- RoutingServiceTransmitSucceeded](../../../../../docs/framework/wcf/diagnostics/etw/3832-routingservicetransmitsucceeded.md)|Informazioni|Il servizio di routing ha trasmesso correttamente il messaggio con ID: '%1 \[operazione %2\] di '%3'.|RoutingServices|  
|[4001 \- TransportListenerSessionsReceived](../../../../../docs/framework/wcf/diagnostics/etw/4001-transportlistenersessionsreceived.md)|Dettagliato|Sessione listener di trasporto ricevuta tramite '%1'|ActivationServices|  
|[4002 \- FailFastException](../../../../../docs/framework/wcf/diagnostics/etw/4002-failfastexception.md)|Critical|FailFastException.|ActivationServices|  
|[4003 \- ServiceStartPipeError](../../../../../docs/framework/wcf/diagnostics/etw/4003-servicestartpipeerror.md)|Errore|Errore della pipe di avvio del servizio.|ActivationServices|  
|[4008 \- DispatchSessionStart](../../../../../docs/framework/wcf/diagnostics/etw/4008-dispatchsessionstart.md)|Dettagliato|Invio sessione avviato.|ActivationServices|  
|[4008 \- DispatchSessionStart](../../../../../docs/framework/wcf/diagnostics/etw/4008-dispatchsessionstart.md)|Avviso|Invio di sessione per '%1' non riuscito. La coda delle sessioni in sospeso è piena con '%2' elementi in sospeso.|ActivationServices|  
|[4011 \- MessageQueueRegisterStart](../../../../../docs/framework/wcf/diagnostics/etw/4011-messagequeueregisterstart.md)|Dettagliato|Avvio registrazione della coda di messaggi.|ActivationServices|  
|[4012 \- MessageQueueRegisterAbort](../../../../../docs/framework/wcf/diagnostics/etw/4012-messagequeueregisterabort.md)|Errore|Registrazione della coda di messaggi interrotta con lo stato: '%1' per l'URI: '%2'.|ActivationServices|  
|[4013 \- MessageQueueUnregisterSucceeded](../../../../../docs/framework/wcf/diagnostics/etw/4013-messagequeueunregistersucceeded.md)|Dettagliato|Annullamento della registrazione della coda di messaggi completato per l'URI:'%1'.|ActivationServices|  
|[4014 \- MessageQueueRegisterFailed](../../../../../docs/framework/wcf/diagnostics/etw/4014-messagequeueregisterfailed.md)|Errore|Registrazione della coda di messaggi per l'URI:" %1" non riuscita con lo stato:'%2'.|ActivationServices|  
|[4015 \- MessageQueueRegisterCompleted](../../../../../docs/framework/wcf/diagnostics/etw/4015-messagequeueregistercompleted.md)|Informazioni|Registrazione della coda di messaggi completata per l'URI '%1'.|ActivationServices|  
|[4016 \- MessageQueueDuplicatedSocketError](../../../../../docs/framework/wcf/diagnostics/etw/4016-messagequeueduplicatedsocketerror.md)|Errore|Duplicazione socket da parte della coda di messaggi non riuscita.|ActivationServices|  
|[4019 \- MessageQueueDuplicatedSocketComplete](../../../../../docs/framework/wcf/diagnostics/etw/4019-messagequeueduplicatedsocketcomplete.md)|Dettagliato|MessageQueueDuplicatedSocketComplete|ActivationServices|  
|[4020 \- TcpTransportListenerListeningStart](../../../../../docs/framework/wcf/diagnostics/etw/4020-tcptransportlistenerlisteningstart.md)|Dettagliato|Inizio ascolto del Listener di trasporto TCP sull'URI:'%1'.|ActivationServices|  
|[4021 \- TcpTransportListenerListeningStop](../../../../../docs/framework/wcf/diagnostics/etw/4021-tcptransportlistenerlisteningstop.md)|Dettagliato|Listener di trasporto TCP in ascolto.|ActivationServices|  
|[4022 \- WebhostUnregisterProtocolFailed](../../../../../docs/framework/wcf/diagnostics/etw/4022-webhostunregisterprotocolfailed.md)|Errore|Codice di errore:%1|ActivationServices|  
|[4023 \- WasCloseAllListenerChannelInstancesCompleted](../../../../../docs/framework/wcf/diagnostics/etw/4023-wasclosealllistenerchannelinstancescompleted.md)|Informazioni|Chiusura da parte di WAS di tutte le istanze di canali del listener completata.|ActivationServices|  
|[4024 \- WasCloseAllListenerChannelInstancesFailed](../../../../../docs/framework/wcf/diagnostics/etw/4024-wasclosealllistenerchannelinstancesfailed.md)|Errore|Codice di errore:%1|ActivationServices|  
|[4025 \- OpenListenerChannelInstanceFailed](../../../../../docs/framework/wcf/diagnostics/etw/4025-openlistenerchannelinstancefailed.md)|Errore|Codice di errore:%1|ActivationServices|  
|[4026 \- WasConnected](../../../../../docs/framework/wcf/diagnostics/etw/4026-wasconnected.md)|Dettagliato|WAS connesso.|ActivationServices|  
|[4027 \- WasDisconnected](../../../../../docs/framework/wcf/diagnostics/etw/4027-wasdisconnected.md)|Dettagliato|WAS disconnesso.|ActivationServices|  
|[4028 \- PipeTransportListenerListeningStart](../../../../../docs/framework/wcf/diagnostics/etw/4028-pipetransportlistenerlisteningstart.md)|Dettagliato|Avvio dell'ascolto del listener di trasporto della pipe sull'URI:%1.|ActivationServices|  
|[4029 \- PipeTransportListenerListeningStop](../../../../../docs/framework/wcf/diagnostics/etw/4029-pipetransportlistenerlisteningstop.md)|Dettagliato|Arresto dell'ascolto del listener di trasporto della pipe.|ActivationServices|  
|[4030 \- DispatchSessionSuccess](../../../../../docs/framework/wcf/diagnostics/etw/4030-dispatchsessionsuccess.md)|Informazioni|Invio sessione completato.|ActivationServices|  
|[4031 \- DispatchSessionFailed](../../../../../docs/framework/wcf/diagnostics/etw/4031-dispatchsessionfailed.md)|Errore|Invio sessione non riuscito.|ActivationServices|  
|[4032 \- WasConnectionTimedout](../../../../../docs/framework/wcf/diagnostics/etw/4032-wasconnectiontimedout.md)|Critical|Connessione WAS scaduta.|ActivationServices|  
|[4033 \- RoutingTableLookupStart](../../../../../docs/framework/wcf/diagnostics/etw/4033-routingtablelookupstart.md)|Dettagliato|Ricerca tabella di routing avviata.|ActivationServices|  
|[4034 \- RoutingTableLookupStop](../../../../../docs/framework/wcf/diagnostics/etw/4034-routingtablelookupstop.md)|Dettagliato|Ricerca tabella di routing completata.|ActivationServices|  
|[4035 \- PendingSessionQueueRatio](../../../../../docs/framework/wcf/diagnostics/etw/4035-pendingsessionqueueratio.md)|Dettagliato|Percentuale coda di sessione in sospeso: %1\/%2|Quota|  
|[4600 \- MessageLogEventSizeExceeded](../../../../../docs/framework/wcf/diagnostics/etw/4600-messagelogeventsizeexceeded.md)|Avviso|Impossibile registrare il messaggio in quanto supera la dimensione degli eventi ETW|WCFMessageLogging|  
|[4801 \- DiscoveryClientInClientChannelFailedToClose](../../../../../docs/framework/wcf/diagnostics/etw/4801-discoveryclientinclientchannelfailedtoclose.md)|Avviso|Impossibile chiudere DiscoveryClient creato all'interno di DiscoveryClientChannel e pertanto è stato interrotto.|Individuazione|  
|[4802 \- DiscoveryClientProtocolExceptionSuppressed](../../../../../docs/framework/wcf/diagnostics/etw/4802-discoveryclientprotocolexceptionsuppressed.md)|Informazioni|ProtocolException eliminato durante la chiusura di DiscoveryClient.  È possibile che DiscoveryService stia ancora provando a inviare una risposta a DiscoveryClient.|Individuazione|  
|[4803 \- DiscoveryClientReceivedMulticastSuppression](../../../../../docs/framework/wcf/diagnostics/etw/4803-discoveryclientreceivedmulticastsuppression.md)|Informazioni|DiscoveryClient ha ricevuto un messaggio di eliminazione multicast da DiscoveryProxy.|Individuazione|  
|[4804 \- DiscoveryMessageReceivedAfterOperationCompleted](../../../../../docs/framework/wcf/diagnostics/etw/4804-discoverymessagereceivedafteroperationcompleted.md)|Informazioni|Un messaggio %1 con messageId\='%2' è stato eliminato da DiscoveryClient poiché è stata completata l'operazione %3 corrispondente.|Individuazione|  
|[4805 \- DiscoveryMessageWithInvalidContent](../../../../../docs/framework/wcf/diagnostics/etw/4805-discoverymessagewithinvalidcontent.md)|Avviso|Un messaggio %1 con messageId\='%2' è stato eliminato poiché conteneva contenuto non valido.|Individuazione|  
|[4806 \- DiscoveryMessageWithInvalidRelatesToOrOperationCompleted](../../../../../docs/framework/wcf/diagnostics/etw/4806-discoverymessagewithinvalidrelatestooroperationcompleted.md)|Avviso|Un messaggio %1 con messageId\='%2' e relatesTo\='%3' è stato eliminato da DiscoveryClient poiché è stata completata l'operazione %4 corrispondente o il valore relatesTo non è valido.|Individuazione|  
|[4807 \- DiscoveryMessageWithInvalidReplyTo](../../../../../docs/framework/wcf/diagnostics/etw/4807-discoverymessagewithinvalidreplyto.md)|Avviso|Un messaggio di richiesta di individuazione con messageId\='%1' è stato eliminato poiché conteneva un indirizzo ReplyTo non valido.|Individuazione|  
|[4808 \- DiscoveryMessageWithNoContent](../../../../../docs/framework/wcf/diagnostics/etw/4808-discoverymessagewithnocontent.md)|Avviso|Un messaggio %1 è stato eliminato poiché non conteneva alcun contenuto.|Individuazione|  
|[4809 \- DiscoveryMessageWithNullMessageId](../../../../../docs/framework/wcf/diagnostics/etw/4809-discoverymessagewithnullmessageid.md)|Avviso|Un messaggio %1 è stato eliminato poiché l'intestazione del messaggio non conteneva la proprietà MessageId richiesta.|Individuazione|  
|[4810 \- DiscoveryMessageWithNullMessageSequence](../../../../../docs/framework/wcf/diagnostics/etw/4810-discoverymessagewithnullmessagesequence.md)|Avviso|Un messaggio %1 con messageId\='%2' è stato eliminato da DiscoveryClient poiché non conteneva la proprietà DiscoveryMessageSequence.|Individuazione|  
|[4811 \- DiscoveryMessageWithNullRelatesTo](../../../../../docs/framework/wcf/diagnostics/etw/4811-discoverymessagewithnullrelatesto.md)|Avviso|Un messaggio %1 con messageId\='%2' è stato eliminato da DiscoveryClient poiché l'intestazione del messaggio non conteneva la proprietà RelatesTo richiesta.|Individuazione|  
|[4812 \- DiscoveryMessageWithNullReplyTo](../../../../../docs/framework/wcf/diagnostics/etw/4812-discoverymessagewithnullreplyto.md)|Avviso|Un messaggio di richiesta di individuazione con messageId\='%1' è stato eliminato poiché non conteneva un indirizzo ReplyTo.|Individuazione|  
|[4813 \- DuplicateDiscoveryMessage](../../../../../docs/framework/wcf/diagnostics/etw/4813-duplicatediscoverymessage.md)|Avviso|Un messaggio %1 con messageId\='%2' è stato eliminato poiché era un duplicato.|Individuazione|  
|[4814 \- EndpointDiscoverabilityDisabled](../../../../../docs/framework/wcf/diagnostics/etw/4814-endpointdiscoverabilitydisabled.md)|Informazioni|L'individuabilità dell'endpoint con EndpointAddress\='%1' e ListenUri\='%2' è stata disabilitata.|Individuazione|  
|[4814 \- EndpointDiscoverabilityDisabled](../../../../../docs/framework/wcf/diagnostics/etw/4814-endpointdiscoverabilitydisabled.md)|Informazioni|L'individuabilità dell'endpoint con EndpointAddress\='%1' e ListenUri\='%2' è stata abilitata.|Individuazione|  
|[4816 \- FindInitiatedInDiscoveryClientChannel](../../../../../docs/framework/wcf/diagnostics/etw/4816-findinitiatedindiscoveryclientchannel.md)|Dettagliato|Operazione di ricerca avviata in DiscoveryClientChannel per individuare gli endpoint.|Individuazione|  
|[4817 \- InnerChannelCreationFailed](../../../../../docs/framework/wcf/diagnostics/etw/4817-innerchannelcreationfailed.md)|Avviso|DiscoveryClientChannel non è riuscito a creare il canale con un endpoint individuato con EndpointAddress\='%1' e Via\='%2'.  DiscoveryClientChannel tenterà ora di usare l'endpoint individuato disponibile successivo.|Individuazione|  
|[4818 \- InnerChannelOpenFailed](../../../../../docs/framework/wcf/diagnostics/etw/4818-innerchannelopenfailed.md)|Avviso|DiscoveryClientChannel non è riuscito ad aprire il canale con un endpoint individuato con EndpointAddress\='%1' e Via\='%2'.  DiscoveryClientChannel tenterà ora di usare l'endpoint individuato disponibile successivo.|Individuazione|  
|[4819 \- InnerChannelOpenSucceeded](../../../../../docs/framework/wcf/diagnostics/etw/4819-innerchannelopensucceeded.md)|Informazioni|DiscoveryClientChannel ha individuato correttamente un endpoint con il quale ha aperto il canale.  Il client viene connesso a un servizio mediante EndpointAddress\='%1' e Via\='%2'.|Individuazione|  
|[4820 \- SynchronizationContextReset](../../../../../docs/framework/wcf/diagnostics/etw/4820-synchronizationcontextreset.md)|Informazioni|È stato ripristinato il valore originale %1 di SynchronizationContext da DiscoveryClientChannel.|Individuazione|  
|[4821 \- SynchronizationContextSetToNull](../../../../../docs/framework/wcf/diagnostics/etw/4821-synchronizationcontextsettonull.md)|Informazioni|SynchronizationContext è stato impostato su null da DiscoveryClientChannel prima dell'avvio dell'operazione di ricerca.|Individuazione|  
|[5001 \- DCSerializeWithSurrogateStart](../../../../../docs/framework/wcf/diagnostics/etw/5001-dcserializewithsurrogatestart.md)|Dettagliato|Avvio serializzazione di %1 da parte di DataContract con surrogati.|Serializzazione|  
|[5002 \- DCSerializeWithSurrogateStop](../../../../../docs/framework/wcf/diagnostics/etw/5002-dcserializewithsurrogatestop.md)|Dettagliato|Arresto serializzazione di DataContract con surrogati.|Serializzazione|  
|[5003 \- DCDeserializeWithSurrogateStart](../../../../../docs/framework/wcf/diagnostics/etw/5003-dcdeserializewithsurrogatestart.md)|Dettagliato|Avvio deserializzazione di %1 da parte di DataContract con surrogati.|Serializzazione|  
|[5004 \- DCDeserializeWithSurrogateStop](../../../../../docs/framework/wcf/diagnostics/etw/5004-dcdeserializewithsurrogatestop.md)|Dettagliato|Arresto deserializzazione di DataContract con surrogati.|Serializzazione|  
|[5005 \- ImportKnownTypesStart](../../../../../docs/framework/wcf/diagnostics/etw/5005-importknowntypesstart.md)|Dettagliato|Avvio di ImportKnownTypes.|Serializzazione|  
|[5006 \- ImportKnownTypesStop](../../../../../docs/framework/wcf/diagnostics/etw/5006-importknowntypesstop.md)|Dettagliato|Arresto di ImportKnownTypes.|Serializzazione|  
|[5007 \- DCResolverResolve](../../../../../docs/framework/wcf/diagnostics/etw/5007-dcresolverresolve.md)|Dettagliato|Avvio risoluzione di %1 del resolver di DataContract.|Serializzazione|  
|[5008 \- DCGenWriterStart](../../../../../docs/framework/wcf/diagnostics/etw/5008-dcgenwriterstart.md)|Dettagliato|Avvio del writer %1 di generazione di DataContract per %2.|Serializzazione|  
|[5009 \- DCGenWriterStop](../../../../../docs/framework/wcf/diagnostics/etw/5009-dcgenwriterstop.md)|Dettagliato|Arresto del writer di generazione di DataContract.|Serializzazione|  
|[5010 \- DCGenReaderStart](../../../../../docs/framework/wcf/diagnostics/etw/5010-dcgenreaderstart.md)|Dettagliato|Avvio del reader %1 di generazione di DataContract per %2.|Serializzazione|  
|[5011 \- DCGenReaderStop](../../../../../docs/framework/wcf/diagnostics/etw/5011-dcgenreaderstop.md)|Dettagliato|Arresto generazione di DataContract.|Serializzazione|  
|[5012 \- DCJsonGenReaderStart](../../../../../docs/framework/wcf/diagnostics/etw/5012-dcjsongenreaderstart.md)|Dettagliato|Avvio reader %1 di generazione di JSON per %2.|Serializzazione|  
|[5013 \- DCJsonGenReaderStop](../../../../../docs/framework/wcf/diagnostics/etw/5013-dcjsongenreaderstop.md)|Dettagliato|Arresto generazione reader di JSON.|Serializzazione|  
|[5014 \- DCJsonGenWriterStart](../../../../../docs/framework/wcf/diagnostics/etw/5014-dcjsongenwriterstart.md)|Dettagliato|Avvio writer %1 di generazione di JSON per %2.|Serializzazione|  
|[5015 \- DCJsonGenWriterStop](../../../../../docs/framework/wcf/diagnostics/etw/5015-dcjsongenwriterstop.md)|Dettagliato|Arresto writer di generazione di JSON.|Serializzazione|  
|[5016 \- GenXmlSerializableStart](../../../../../docs/framework/wcf/diagnostics/etw/5016-genxmlserializablestart.md)|Dettagliato|Avvio generazione di XML serializzabile per '%1'.|Serializzazione|  
|[5017 \- GenXmlSerializableStop](../../../../../docs/framework/wcf/diagnostics/etw/5017-genxmlserializablestop.md)|Dettagliato|Arresto generazione di XML serializzabile.|Serializzazione|  
|[5203 \- JsonMessageDecodingStart](../../../../../docs/framework/wcf/diagnostics/etw/5203-jsonmessagedecodingstart.md)|Dettagliato|JsonMessageEncoder ha avviato la decodifica del messaggio.|Canale|  
|[5204 \- JsonMessageEncodingStart](../../../../../docs/framework/wcf/diagnostics/etw/5204-jsonmessageencodingstart.md)|Dettagliato|JsonMessageEncoder ha avviato la codifica del messaggio.|Canale|  
|[5402 \- TokenValidationStarted](../../../../../docs/framework/wcf/diagnostics/etw/5402-tokenvalidationstarted.md)|Dettagliato|Convalida di SecurityToken \(tipo '%1' e ID '%2'\) avviata.|Sicurezza|  
|[5403 \- TokenValidationSuccess](../../../../../docs/framework/wcf/diagnostics/etw/5403-tokenvalidationsuccess.md)|Dettagliato|Convalida di SecurityToken \(tipo '%1' e ID '%2'\) completata.|Sicurezza|  
|[5404 \- TokenValidationFailure](../../../../../docs/framework/wcf/diagnostics/etw/5404-tokenvalidationfailure.md)|Errore|Convalida di SecurityToken \(tipo '%1' e ID '%2'\) non riuscita.  %3|Sicurezza|  
|[5405 \- GetIssuerNameSuccess](../../../../../docs/framework/wcf/diagnostics/etw/5405-getissuernamesuccess.md)|Dettagliato|Recupero nome autorità emittente %1 da tokenId %2 completato.|Sicurezza|  
|[5406 \- GetIssuerNameFailure](../../../../../docs/framework/wcf/diagnostics/etw/5406-getissuernamefailure.md)|Errore|Recupero nome autorità emittente da tokenId %1 non riuscito.|Sicurezza|  
|[5600 \- FederationMessageProcessingStarted](../../../../../docs/framework/wcf/diagnostics/etw/5600-federationmessageprocessingstarted.md)|Dettagliato|Elaborazione messaggio della federazione avviata.|Sicurezza|  
|[5601 \- FederationMessageProcessingSuccess](../../../../../docs/framework/wcf/diagnostics/etw/5601-federationmessageprocessingsuccess.md)|Dettagliato|Elaborazione messaggio della federazione completata.|Sicurezza|  
|[5602 \- FederationMessageCreationStarted](../../../../../docs/framework/wcf/diagnostics/etw/5602-federationmessagecreationstarted.md)|Dettagliato|Creazione messaggio della federazione dal Post del form avviata.|Sicurezza|  
|[5603 \- FederationMessageCreationSuccess](../../../../../docs/framework/wcf/diagnostics/etw/5603-federationmessagecreationsuccess.md)|Dettagliato|Creazione messaggio della federazione dal Post del form completata.|Sicurezza|  
|[5604 \- SessionCookieReadingStarted](../../../../../docs/framework/wcf/diagnostics/etw/5604-sessioncookiereadingstarted.md)|Dettagliato|Lettura del token di sessione dal cookie di sessione avviata.|Sicurezza|  
|[5605 \- SessionCookieReadingSuccess](../../../../../docs/framework/wcf/diagnostics/etw/5605-sessioncookiereadingsuccess.md)|Dettagliato|Lettura del token di sessione dal cookie di sessione completata.|Sicurezza|  
|[5606 \- PrincipalSettingFromSessionTokenStarted](../../../../../docs/framework/wcf/diagnostics/etw/5606-principalsettingfromsessiontokenstarted.md)|Dettagliato|Impostazione principale dal token di sessione avviata.|Sicurezza|  
|[5607 \- PrincipalSettingFromSessionTokenSuccess](../../../../../docs/framework/wcf/diagnostics/etw/5607-principalsettingfromsessiontokensuccess.md)|Dettagliato|Impostazione principale dal token di sessione completata.|Sicurezza|  
|[57393 \- AppDomainUnload](../../../../../docs/framework/wcf/diagnostics/etw/57393-appdomainunload.md)|Informazioni|Scaricamento di AppDomain.  AppDomain.FriendlyName %1, ProcessName %2, ProcessId %3.|Infrastruttura|  
|[57394 \- HandledException](../../../../../docs/framework/wcf/diagnostics/etw/57394-handledexception.md)|Informazioni|Gestione di un'eccezione.|Infrastruttura|  
|[57395 \- ShipAssertExceptionMessage](../../../../../docs/framework/wcf/diagnostics/etw/57395-shipassertexceptionmessage.md)|Errore|Errore imprevisto.  Le applicazioni non devono tentare di gestire questo errore.  Per motivi di diagnostica, all'errore è associato questo messaggio in inglese: %1.|Infrastruttura|  
|[57396 \- ThrowingException](../../../../../docs/framework/wcf/diagnostics/etw/57396-throwingexception.md)|Avviso|Generazione di un'eccezione.  Origine %1.|Infrastruttura|  
|[57397 \- UnhandledException](../../../../../docs/framework/wcf/diagnostics/etw/57397-unhandledexception.md)|Critical|Eccezione non gestita.|Infrastruttura|  
|[57399 \- TraceCodeEventLogCritical](../../../../../docs/framework/wcf/diagnostics/etw/57399-tracecodeeventlogcritical.md)|Critical|Scrittura in EventLog completata.|Infrastruttura|  
|[57400 \- TraceCodeEventLogError](../../../../../docs/framework/wcf/diagnostics/etw/57400-tracecodeeventlogerror.md)|Errore|Scrittura in EventLog completata.|Infrastruttura|  
|[57401 \- TraceCodeEventLogInfo](../../../../../docs/framework/wcf/diagnostics/etw/57401-tracecodeeventloginfo.md)|Informazioni|Scrittura in EventLog completata.|Infrastruttura|  
|[57402 \- TraceCodeEventLogVerbose](../../../../../docs/framework/wcf/diagnostics/etw/57402-tracecodeeventlogverbose.md)|Dettagliato|Scrittura in EventLog completata.|Infrastruttura|  
|[57403 \- TraceCodeEventLogWarning](../../../../../docs/framework/wcf/diagnostics/etw/57403-tracecodeeventlogwarning.md)|Avviso|Scrittura in EventLog completata.|Infrastruttura|  
|[57404 \- HandledExceptionWarning](../../../../../docs/framework/wcf/diagnostics/etw/57404-handledexceptionwarning.md)|Avviso|Gestione di un'eccezione.|Infrastruttura|  
|[62326 \- HttpHandlerPickedForUrl](../../../../../docs/framework/wcf/diagnostics/etw/62326-httphandlerpickedforurl.md)|Informazioni|L'URL '%1' ospita il documento XAML con tipo di elemento radice '%2'.  Il gestore HTTP di tipo '%3' è selezionato per gestire tutte le richieste effettuate a questo URL.|WebHost|