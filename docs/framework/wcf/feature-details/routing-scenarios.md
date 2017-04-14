---
title: "Scenari di routing | Microsoft Docs"
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
  - "rounting [WCF], scenari"
ms.assetid: ec22f308-665a-413e-9f94-7267cb665dab
caps.latest.revision: 7
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 7
---
# Scenari di routing
Sebbene il servizio di routing sia notevolmente personalizzabile, può risultare difficile progettare una logica di routing efficiente quando si crea una nuova configurazione da zero.  Esistono tuttavia diversi scenari comuni seguiti dalla maggior parte delle configurazioni dei servizi di routing.  Tali scenari possono non essere direttamente applicabili a una configurazione specifica, tuttavia comprendere le modalità di configurazione del servizio di routing per tali scenari consente di acquisire familiarità con le potenzialità del servizio stesso.  
  
## Scenari comuni  
 L'utilizzo più comune del servizio di routing consiste nell'aggregazione di più endpoint di destinazione allo scopo di ridurre il numero degli endpoint esposti alle applicazioni client e quindi nell'utilizzo di filtri messaggi per indirizzare ogni messaggio alla destinazione corretta.  I messaggi possono essere indirizzati in base a requisiti di elaborazione fisica o logica, ad esempio a seconda che un messaggio debba essere elaborato da un servizio specifico o in base a esigenze aziendali arbitrarie quali l'elaborazione prioritaria a seconda dell'origine del messaggio.  Nella tabella seguente vengono elencati alcuni scenari comuni e le circostanze in cui si verificano:  
  
|Scenario|Casi di utilizzo|  
|--------------|----------------------|  
|Controllo delle versioni dei servizi|È necessario supportare più versioni di un servizio o prevedere la distribuzione futura di una versione aggiornata del servizio|  
|Partizionamento dei dati del servizio|È necessario partizionare un servizio tra più host|  
|Aggiornamento dinamico|È necessario riconfigurare dinamicamente la logica di routing al runtime per gestire distribuzioni del servizio mutevoli|  
|Multicast|È necessario inviare un messaggio a più endpoint|  
|Bridging del protocollo|Si ricevono messaggi su un protocollo di trasporto ma l'endpoint di destinazione usa un protocollo diverso|  
|Gestione degli errori|È necessario assicurare la continuità dei servizi in caso di limitazioni di rete ed errori di comunicazione|  
  
> [!NOTE]
>  Sebbene molti degli scenari indicati siano specifici di precise esigenze aziendali o di particolari requisiti di elaborazione, prevedere il supporto per gli aggiornamenti dinamici e l'uso della gestione degli errori è spesso consigliabile in quanto in questo modo è possibile modificare la logica di routing al runtime e ripristinare i servizi in caso di errori di rete e di comunicazione temporanei.  
  
### Controllo delle versioni dei servizi  
 Quando si introduce una nuova versione di un servizio è spesso necessario mantenere la versione precedente finché tutti i client non sono passati al nuovo servizio.  Ciò è di particolare importanza se il servizio è un processo a esecuzione prolungata il cui completamento richiede giorni, settimane o perfino mesi.  In questi casi, è in genere necessario implementare un nuovo indirizzo per l'endpoint del nuovo servizio e mantenere l'endpoint originale della versione precedente.  
  
 Con il servizio di routing è possibile esporre un endpoint affinché riceva i messaggi dalle applicazioni client e quindi indirizzare ogni messaggio alla versione corretta del servizio in base al contenuto del messaggio.  L'implementazione più semplice prevede l'aggiunta di un'intestazione personalizzata al messaggio, la quale indichi la versione del servizio da cui deve essere elaborato il messaggio.  Il servizio di routing può usare XPathMessageFilter per verificare in ogni messaggio la presenza dell'intestazione personalizzata e indirizzare il messaggio all'endpoint di destinazione appropriato.  
  
 Per le procedure da usare per creare una configurazione di controllo delle versioni dei servizi, vedere [Procedura: controllo delle versioni dei servizi](../../../../docs/framework/wcf/feature-details/how-to-service-versioning.md).  Per un esempio dell'utilizzo di XPathMessageFilter per indirizzare messaggi in base a un'intestazione personalizzata, vedere [Filtri avanzati](../../../../docs/framework/wcf/samples/advanced-filters.md).  
  
### Partizionamento dei dati del servizio  
 Quando si progetta un ambiente distribuito, è spesso consigliabile suddividere il carico di elaborazione tra più computer in modo da offrire disponibilità elevata, ridurre il carico sui singoli computer o fornire risorse dedicate per uno specifico subset di messaggi.  Sebbene il servizio di routing non sostituisca una soluzione di bilanciamento del carico dedicata, la possibilità di eseguire il routing basato sul contenuto consente di indirizzare messaggi simili a specifiche destinazioni.  Potrebbe essere ad esempio necessario elaborare i messaggi di un determinato cliente separatamente da quelli ricevuti da altri client.  
  
 Per le procedure da usare per creare una configurazione di partizionamento dei dati del servizio, vedere [Procedura: partizionamento dei dati del servizio](../../../../docs/framework/wcf/feature-details/how-to-service-data-partitioning.md).  Per un esempio dell'utilizzo di filtri per partizionare i dati in base a URL e intestazioni personalizzate, vedere [Filtri avanzati](../../../../docs/framework/wcf/samples/advanced-filters.md).  
  
### Routing dinamico  
 È spesso necessario modificare la configurazione di routing per soddisfare nuove esigenze aziendali, ad esempio con l'aggiunta di una route a una versione più recente di un servizio, la modifica dei criteri di routing oppure la modifica dell'endpoint di destinazione di uno specifico messaggio.  Queste modifiche sono possibile tramite <xref:System.ServiceModel.Routing.RoutingExtension> grazie al quale è possibile specificare una nuova configurazione di routing in fase di esecuzione.  La nuova configurazione viene applicata immediatamente, ma influisce solo sulle nuove sessioni elaborate dal servizio di routing.  
  
 Per le procedure da usare per implementare il routing dinamico, vedere [Procedura: aggiornamento dinamico](../../../../docs/framework/wcf/feature-details/how-to-dynamic-update.md).  Per un esempio di utilizzo del routing dinamico, vedere [Riconfigurazione dinamica](../../../../docs/framework/wcf/samples/dynamic-reconfiguration.md).  
  
### Multicast  
 Il routing dei messaggi avviene in genere a uno specifico endpoint di destinazione.  Può tuttavia risultare talvolta necessario indirizzare una copia del messaggio a più endpoint di destinazione.  Per il routing multicast, è necessario che siano soddisfatte le condizioni seguenti:  
  
-   La forma del canale non deve essere di tipo request\/reply \(tuttavia può essere unidirezionale o duplex\), poiché tale forma impone che l'applicazione client debba ricevere una sola risposta alla richiesta.  
  
-   Più filtri devono restituire **true** in seguito alla valutazione del messaggio.  
  
 Se vengono soddisfatte queste condizioni, ogni endpoint di destinazione associato a un filtro che restituisce true riceverà una copia del messaggio.  
  
### Bridging del protocollo  
 Per il routing dei messaggi tra protocolli SOAP diversi, il servizio di routing usa le API WCF per convertire il messaggio da un protocollo all'altro.  Il bridging viene eseguito automaticamente se l'endpoint servizio esposto dal servizio di routing usa un protocollo diverso rispetto agli endpoint client ai quali vengono indirizzati i messaggi.  È possibile disabilitare questo comportamento se i protocolli usati non sono standard; tuttavia, è necessario fornire codice di bridging specifico.  
  
 .  Per un esempio dell'utilizzo del servizio di routing per convertire messaggi tra diversi protocolli, vedere [Bridging e gestione degli errori](../../../../docs/framework/wcf/samples/bridging-and-error-handling.md).  
  
### Gestione degli errori  
 In un ambiente distribuito non è insolito che si verifichino errori di rete o di comunicazione temporanei.  In assenza di un servizio intermediario quale quello di routing, la gestione di tali errori dipende dall'applicazione client.  Se l'applicazione client non include logica specifica per eseguire un nuovo tentativo in caso di errori di rete o di comunicazione e non sono noti indirizzi alternativi, è possibile che un messaggio debba essere inviato più volte affinché possa essere elaborato correttamente dal servizio di destinazione.  Ciò può determinare disservizi per i clienti che potrebbero considerare l'applicazione inaffidabile.  
  
 Il servizio di routing offre affidabili funzionalità di gestione degli errori di rete e di comunicazione allo scopo di rimediare a tali scenari.  Creando un elenco di possibili endpoint di destinazione da associare a ogni filtro messaggi, è possibile evitare il singolo punto di errore determinato dalla presenza di un'unica possibile destinazione.  In caso di errore, il servizio di routing tenta di recapitare il messaggio all'endpoint successivo nell'elenco finché l'operazione non ha esito positivo, si verifica un errore non di comunicazione o si esauriscono tutti gli endpoint.  
  
 Per le procedure da usare per configurare la gestione degli errori, vedere [Procedura: gestione degli errori](../../../../docs/framework/wcf/feature-details/how-to-error-handling.md).  Per un esempio di implementazione della gestione degli errori, vedere [Bridging e gestione degli errori](../../../../docs/framework/wcf/samples/bridging-and-error-handling.md) e [Gestione avanzata degli errori](../../../../docs/framework/wcf/samples/advanced-error-handling.md).  
  
### Contenuto della sezione  
 [Procedura: controllo delle versioni dei servizi](../../../../docs/framework/wcf/feature-details/how-to-service-versioning.md)  
  
 [Procedura: partizionamento dei dati del servizio](../../../../docs/framework/wcf/feature-details/how-to-service-data-partitioning.md)  
  
 [Procedura: aggiornamento dinamico](../../../../docs/framework/wcf/feature-details/how-to-dynamic-update.md)  
  
 [Procedura: gestione degli errori](../../../../docs/framework/wcf/feature-details/how-to-error-handling.md)  
  
## Vedere anche  
 [Introduzione al routing](../../../../docs/framework/wcf/feature-details/routing-introduction.md)