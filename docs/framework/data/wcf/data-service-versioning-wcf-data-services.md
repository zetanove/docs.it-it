---
title: "Controllo delle versioni del servizio dati (WCF Data Services) | Microsoft Docs"
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
  - "controllo delle versioni [WCF Data Services]"
  - "controllo delle versioni, WCF Data Services"
  - "WCF Data Services, controllo delle versioni"
ms.assetid: e3e899cc-7f25-4f67-958f-063f01f79766
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Controllo delle versioni del servizio dati (WCF Data Services)
[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] consente di creare servizi dati in modo che i client possono accedere ai dati come risorse usando URI basati su un modello di dati.  [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] supporta inoltre la definizione di operazioni del servizio.  Dopo la distribuzione iniziale e, potenzialmente, più volte durante il loro ciclo di vita, potrebbe essere necessario cambiare questi servizi dati per molteplici ragioni, ad esempio perché cambiano le esigenze aziendali, i requisiti IT o per risolvere altri problemi.  Quando si apportano modifiche a un servizio dati esistente, è necessario valutare se definire una nuova versione del servizio dati e il modo migliore per ridurre l'impatto sulle applicazioni client esistenti.  In questo argomento vengono fornite informazioni su quando e come creare una nuova versione di un servizio dati.  Viene inoltre descritto il modo in cui in [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] viene gestito uno scambio tra client e servizi dati che supportano versioni diverse del protocollo [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  
  
## Controllo delle versioni di un'istanza di WCF Data Services  
 Una volta che un servizio dati viene distribuito e i dati vengono usati, le modifiche apportate al servizio dati potrebbero provocare problemi di compatibilità con le applicazioni client esistenti.  Tuttavia, perché le modifiche spesso sono richieste dalle esigenze aziendali complessive relative al servizio, è necessario considerare quando e come creare una nuova versione del servizio dati con il minimo impatto sulle applicazioni client.  
  
### Modifiche al modello di dati per cui è consigliabile usare una nuova versione del servizio dati  
 Quando si valuta se pubblicare una nuova versione di un servizio dati, è importante capire come i tipi diversi di modifiche possano influire sulle applicazioni client.  Le modifiche a un servizio dati che potrebbero richiedere la creazione di una nuova versione di un servizio dati possono essere divise nelle due categorie seguenti:  
  
-   Modifiche al contratto del servizio, ossia aggiornamenti alle operazioni del servizio e all'accessibilità di set di entità \(feed\), modifiche alle versioni e altre modifiche ai comportamenti del servizio.  
  
-   Modifiche al contratto dati, ossia modifiche al modello di dati o ai formati o alle personalizzazioni di feed.  
  
 Nella tabella seguente sono contenute informazioni dettagliate sui tipi di modifiche che è necessario valutare per pubblicare una nuova versione del servizio dati:  
  
|Tipo di modifica|Nuova versione richiesta|Nuova versione non necessaria|  
|----------------------|------------------------------|-----------------------------------|  
|Operazioni di servizio|-   Aggiungi nuovo parametro<br />-   Modificare il tipo restituito<br />-   Rimuovere l'operazione del servizio|-   Eliminare un parametro esistente<br />-   Aggiungere una nuova operazione del servizio|  
|Comportamenti del servizio|-   Disabilitare le richieste di conteggio<br />-   Disabilitare il supporto della proiezione<br />-   Aumentare la versione del servizio dati richiesta|-   Abilitare le richieste di conteggio<br />-   Abilitare il supporto della proiezione<br />-   Diminuire la versione del servizio dati richiesta|  
|Autorizzazioni del set di entità|-   Limitare le autorizzazioni del set di entità<br />-   Modificare il codice di risposta \(nuovo valore della prima cifra\) <sup>1</sup>|-   Concedere liberamente le autorizzazioni del set di entità<br />-   Modificare il codice di risposta \(stesso valore della prima cifra\)|  
|Proprietà delle entità|-   Rimuovere una proprietà o una relazione esistente<br />-   Aggiungere una proprietà che non ammette i valori Null<br />-   Modificare una proprietà esistente|-   Aggiungere una proprietà che ammette i valori Null<sup>2</sup>|  
|Set di entità|-   Rimuovere un set di entità|-   Aggiungere un tipo derivato<br />-   Modificare il tipo di base<br />-   Aggiungere un set di entità|  
|Personalizzazione di feed|-   Modificare il mapping di proprietà di entità||  
  
 <sup>1</sup> Può dipendere da quanto un'applicazione client si basa sul ricevimento di un codice di errore specifico.  
  
 <sup>2</sup> È possibile impostare la proprietà <xref:System.Data.Services.Client.DataServiceContext.IgnoreMissingProperties%2A> su `true` in modo che il client ignori qualsiasi nuova proprietà inviata dal servizio dati non definita sul client.  Tuttavia, quando vengono eseguiti inserimenti, le proprietà non incluse dal client nella richiesta POST vengono impostate sui valori predefiniti.  Per gli aggiornamenti, qualsiasi dato esistente in una proprietà sconosciuto al client potrebbe essere sovrascritto da valori predefiniti.  In questo caso, è necessario inviare l'aggiornamento come una richiesta MERGE \(impostazione predefinita\).  Per altre informazioni, vedere [Gestione del contesto del servizio dati](../../../../docs/framework/data/wcf/managing-the-data-service-context-wcf-data-services.md).  
  
### Come controllare le versioni di un servizio dati  
 Se necessario, una nuova versione del servizio dati viene definita creando una nuova istanza del servizio con un contratto di servizio o un modello di dati aggiornato.  Questo nuovo servizio viene quindi esposto tramite un nuovo endpoint dell'URI che lo differenzia dalla versione precedente.  Ad esempio:  
  
-   Versione obsoleta: `http://services.odata.org/Northwind/v1/Northwind.svc/`  
  
-   Nuova versione: `http://services.odata.org/Northwind/v2/Northwind.svc/`  
  
 Quando si aggiorna un servizio dati, sarà necessario inoltre aggiornare i client in base ai nuovi metadati del servizio dati e usare il nuovo URI radice.  Quando possibile, è necessario gestire la versione precedente del servizio dati per supportare i client non ancora aggiornati per usare la nuova versione.  Quando non sono più necessarie, le versioni precedenti di un servizio dati possono essere rimosse.  È opportuno valutare la gestione dell'URI dell'endpoint del servizio dati in file di configurazione esterno.  
  
## Versioni del protocollo OData  
 Al rilascio di nuove versioni di [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] è possibile che la versione del protocollo [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] usata nelle applicazioni client non coincida con quella supportata dal servizio dati.  È possibile che un'applicazione client meno recente acceda a un servizio dati che supporta una versione più recente di [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  Un'applicazione client può inoltre usare una versione più recente della libreria client di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] che supporta una versione più recente di [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] rispetto a quella a cui il servizio dati ha eseguito l'accesso.  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] si avvale del supporto fornito da [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] per gestire tali scenari di controllo delle versioni.  È inoltre disponibile il supporto per la generazione e l'uso di metadati del modello di dati per creare le classi del servizio dati client quando la versione di [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] usata dal client differisce da quella del servizio dati.  Per altre informazioni, vedere [OData: Controllo delle versioni dei protocolli](http://go.microsoft.com/fwlink/?LinkId=186071).  
  
### Negoziazione della versione  
 È possibile configurare il servizio dati per definire la versione massima del protocollo [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] che verrà usata dal servizio, indipendentemente dalla versione richiesta dal client.  A tale scopo è possibile specificare un valore <xref:System.Data.Services.Common.DataServiceProtocolVersion> per la proprietà <xref:System.Data.Services.DataServiceBehavior.MaxProtocolVersion%2A> dell'oggetto <xref:System.Data.Services.DataServiceBehavior> usato dal servizio dati.  Per altre informazioni, vedere [Configurazione del servizio dati](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md).  
  
 Quando un'applicazione usa le librerie client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] per accedere a un servizio dati, le intestazioni delle librerie vengono impostate automaticamente sui valori corretti, a seconda della versione di [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] e delle caratteristiche usate nell'applicazione.  Per impostazione predefinita, [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] usa la versione minima del protocollo che supporta l'operazione richiesta.  
  
 Nella tabella seguente sono contenuti i dettagli delle versioni di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] e [!INCLUDE[silverlight](../../../../includes/silverlight-md.md)] che includono il supporto [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] per versioni specifiche del protocollo [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  
  
|Versione del protocollo [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]|Supporto introdotto in…|  
|------------------------------------------------------------------------------------------|-----------------------------|  
|Versione 1|-   [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] Service Pack 1 \(SP1\)<br />-   [!INCLUDE[silverlight](../../../../includes/silverlight-md.md)] versione 3|  
|Versione 2|-   [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)]<br />-   Aggiornamento a [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] SP1.  Per scaricare e installare l'aggiornamento, visitare l'[Area download Microsoft](http://go.microsoft.com/fwlink/?LinkId=158125).<br />-   [!INCLUDE[silverlight](../../../../includes/silverlight-md.md)] versione 4|  
|Versione 3|-   È possibile scaricare e installare una versione preliminare che supporta [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] versione 3 dall'[Area download Microsoft](http://go.microsoft.com/fwlink/?LinkId=203885).|  
  
### Versioni di metadati  
 Per impostazione predefinita, [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] usa la versione 1.1 di CSDL per rappresentare un modello di dati.  Questo comportamento viene applicato sempre nel caso di modelli di dati basati su un provider di reflection o un provider del servizio dati personalizzato.  Tuttavia, quando il modello di dati è definito tramite [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)], viene restituita la stessa versione di CSDL usata da [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)].  La versione del linguaggio CSDL è determinata dallo spazio dei nomi dell'[elemento Schema](http://msdn.microsoft.com/it-it/396074d8-f99c-4f50-a073-68bce848224f).  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la specifica del [formato di file CSDL \(Conceptual Schema Definition Language\) \[MC\-CSDL\]](http://go.microsoft.com/fwlink/?LinkId=159072).  
  
 L'elemento `DataServices` dei metadati restituiti contiene inoltre un attributo `DataServiceVersion` che corrisponde al valore dell'intestazione `DataServiceVersion` nel messaggio di risposta.  Le applicazioni client, ad esempio la finestra di dialogo **Aggiungi riferimento al servizio** in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)], usano queste informazioni per generare classi del servizio dati client che funzionano correttamente con la versione di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] che funge da host del servizio dati.  Per altre informazioni, vedere [OData: Controllo delle versioni dei protocolli](http://go.microsoft.com/fwlink/?LinkId=186071).  
  
## Vedere anche  
 [Provider di servizi dati](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md)   
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)