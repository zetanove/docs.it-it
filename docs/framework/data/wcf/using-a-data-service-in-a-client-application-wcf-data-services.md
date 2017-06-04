---
title: "Utilizzo di un servizio dati in un&#39;applicazione client (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, libreria client"
  - "WCF Data Services, guida introduttiva"
ms.assetid: 90872d0c-e989-4490-b3e9-54afb10d33d4
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Utilizzo di un servizio dati in un&#39;applicazione client (WCF Data Services)
È possibile accedere a un servizio che espone un feed [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] specificando un URI per un browser.  L'URI fornisce l'indirizzo di una risorsa e i messaggi di richiesta vengono inviati a questi indirizzi per accedere ai dati sottostanti rappresentati dalla risorsa o per modificarli.  Il browser invia un comando GET HTTP e restituisce la risorsa richiesta come feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  Per altre informazioni, vedere [Accesso al servizio da un browser](../../../../docs/framework/data/wcf/accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md).  
  
 Sebbene l'uso di un browser possa risultare utile per verificare che un servizio [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] restituisca i dati previsti, l'accesso ai servizi [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] di produzione che consentono inoltre di creare, aggiornare ed eliminare dati viene in genere eseguito tramite linguaggi di codice delle applicazioni o di script in una pagina Web.  In questo argomento vengono forniti cenni preliminari sull'accesso ai feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] da un'applicazione client.  
  
## Accesso ai dati e relativa modifica tramite la semantica REST  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] garantisce l'interoperabilità tra i servizi che espongono feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] e le applicazioni che usano feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]. Le applicazioni accedono ai dati in un servizio basato su [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] e li modificano inviando messaggi di richiesta di un'azione HTTP specifica e usando un URI che indirizza una risorsa di entità sulla quale deve essere eseguita l'azione.  I dati di entità necessari vengono forniti come payload codificato in modo appropriato nel corpo del messaggio.  
  
### Azioni HTTP  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] supporta le azioni HTTP riportate di seguito per l'esecuzione di operazioni di creazione, lettura, aggiornamento ed eliminazione sui dati di entità rappresentati dalla risorsa indirizzata.  
  
-   **GET HTTP**: rappresenta l'azione predefinita quando l'accesso a una risorsa viene eseguito da un browser.  Nel messaggio di richiesta non viene fornito alcun payload e viene restituito un metodo di risposta con un payload contenente i dati richiesti.  
  
-   **POST HTTP**: inserisce nuovi dati di entità nella risorsa fornita.  I dati da inserire vengono forniti nel payload del messaggio di richiesta.  Il payload del messaggio di risposta contiene i dati per l'entità appena creata,  inclusi i valori della chiave generati automaticamente.  L'intestazione contiene inoltre l'URI che indirizza la nuova risorsa di entità.  
  
-   **DELETE HTTP**: elimina i dati di entità rappresentati dalla risorsa specificata.  Nei messaggi di richiesta o di risposta non è presente un payload.  
  
-   **PUT HTTP**: sostituisce i dati di entità esistenti in corrispondenza della risorsa richiesta con i nuovi dati forniti nel payload del messaggio di richiesta.  
  
-   **MERGE HTTP**: a causa delle inefficienze esistenti a livello di esecuzione di un'eliminazione seguita da un inserimento nell'origine dati allo scopo di modificare i dati di entità, in [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] è stata introdotta una nuova azione MERGE HTTP.  Il payload del messaggio di richiesta contiene le proprietà che devono essere modificate nella risorsa di entità indirizzata.  Poiché l'azione MERGE HTTP non è definita nella specifica HTTP, è possibile che sia necessaria elaborazione aggiuntiva per indirizzare una richiesta MERGE HTTP tramite server non dotati di supporto per [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  
  
 Per altre informazioni, vedere la pagina relativa alle [operazioni in OData](http://go.microsoft.com/fwlink/?LinkID=185792).  
  
### Formati payload  
 Per una richiesta PUT HTTP, POST HTTP o MERGE HTTP, il payload di un messaggio di richiesta contiene i dati di entità da inviare al servizio dati.  Il contenuto del payload dipende dal formato dei dati del messaggio.  Tale payload è inoltre incluso nelle risposte HTTP a tutte le azioni, tranne DELETE.  [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] supporta i formati del payload seguenti per l'accesso ai dati e la relativa modifica con il servizio:  
  
-   **Atom**: codifica di messaggi basati su XML definita da [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] come estensione del protocollo di pubblicazione Atom \(AtomPub\) per lo scambio di dati su HTTP per feed Web, podcast, Wiki e funzionalità Internet basate su XML.  Per altre informazioni, vedere la pagina relativa al [formato Atom in OData](http://go.microsoft.com/fwlink/?LinkId=185794).  
  
-   **JSON**: acronimo di JavaScript Object Notation. Si tratta di un formato di interscambio dei dati leggero basato su un subset del linguaggio di programmazione JavaScript.  Per altre informazioni, vedere la pagina relativa alle [convenzioni JSON in OData](http://go.microsoft.com/fwlink/?LinkId=185795).  
  
 Il formato del messaggio per il payload deve essere incluso nell'intestazione del messaggio di richiesta HTTP.  Per altre informazioni, vedere la pagina relativa alle [operazioni in OData](http://go.microsoft.com/fwlink/?LinkID=185792).  
  
## Accesso ai dati e relativa modifica tramite le librerie client  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] include librerie client che consentono di usare con più facilità un feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] dalle applicazioni client basate su .NET Framework e Silverlight.  Queste librerie semplificano l'invio e la ricezione di messaggi HTTP,  oltre a convertire il payload del messaggio in oggetti CLR che rappresentano dati di entità.  Le librerie client rendono disponibili le due classi principali <xref:System.Data.Services.Client.DataServiceContext> e <xref:System.Data.Services.Client.DataServiceQuery%601> che consentono di eseguire una query su un servizio dati e di usare quindi i dati di entità restituiti come oggetti CLR.  Per altre informazioni, vedere [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md) e [WCF Data Services \(Silverlight\)](http://msdn.microsoft.com/it-it/c0cd9f4b-1372-48e4-9935-c8421239da30).  
  
 È possibile usare la finestra di dialogo **Aggiungi riferimento al servizio** in Visual Studio per aggiungere un riferimento a un servizio dati.  Questo strumento richiede i metadati del servizio a un servizio dati a cui viene fatto riferimento e genera l'oggetto <xref:System.Data.Services.Client.DataServiceContext> che rappresenta un servizio dati, oltre a generare le classi del servizio dati client che rappresentano entità.  Per altre informazioni, vedere [Generazione della libreria client del servizio dati](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md).  
  
 Sono disponibili altre librerie di programmazione per consentire l'uso di un feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] in altri tipi di applicazioni client.  Per altre informazioni, vedere la pagina relativa a [OData SDK](http://go.microsoft.com/fwlink/?LinkId=185796).  
  
## Vedere anche  
 [Accesso alle risorse del servizio dati](../../../../docs/framework/data/wcf/accessing-data-service-resources-wcf-data-services.md)   
 [Guida rapida](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)