---
title: "&lt;soapProcessing&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e8707027-e6b8-4539-893d-3cd7c13fbc18
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;soapProcessing&gt;
Definisce il comportamento dell'endpoint client usato per effettuare il marshalling dei messaggi tra versioni del messaggio e tipi di associazione diversi.  
  
## Sintassi  
  
```  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|processMessages|Valore booleano che specifica se è necessario effettuare il marshalling dei messaggi tra le versioni di messaggi SOAP.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un comportamento dell'endpoint.|  
  
## Note  
 L'elaborazione SOAP è il processo in cui i messaggi vengono convertiti tra le versioni dei messaggi.  
  
 Il servizio di routing [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] è in grado di convertire messaggi da un protocollo a un altro.  Se le versioni del messaggio in ingresso e in uscita sono diverse, viene creato un nuovo messaggio della versione corretta.  L'elaborazione di messaggi da un oggetto <xref:System.ServiceModel.Channel.MessageVersion> a un altro viene eseguita mediante la costruzione di un nuovo messaggio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] contenente la parte del corpo e le intestazioni pertinenti del messaggio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] in ingresso.  Le intestazioni specifiche dell'indirizzamento o quelle riconosciute al livello del router non vengono usate durante la costruzione del nuovo messaggio WCF, poiché queste intestazioni presentano una versione diversa \(nel caso delle intestazioni di indirizzamento\) o sono state elaborate come parte della comunicazione tra il client e il router.  
  
 Il posizionamento di un'intestazione nel messaggio in uscita viene determinato dal fatto che essa venga contrassegnata o meno come riconosciuta quando è passata attraverso il livello del canale in ingresso.  Le intestazioni non riconosciute \(ad esempio le intestazioni personalizzate\) non vengono rimosse e passano pertanto attraverso il servizio di routing mediante copia nel messaggio in uscita.  Il corpo del messaggio viene copiato nel messaggio in uscita.  Il messaggio viene quindi inviato al canale di uscita al quale puntano tutte le intestazioni e verranno creati e aggiunti gli altri dati di envelope specifici di tale protocollo\/trasporto di comunicazione.  
  
 Questi passaggi di elaborazione vengono eseguiti quando il comportamento di elaborazione SOAP è specificato.  Questo comportamento [\<soapProcessingExtension\>](../../../../../docs/framework/configure-apps/file-schema/wcf/soapprocessing.md) è il comportamento di un endpoint applicato a tutti gli endpoint client \(in uscita\) all'avvio del servizio di routing.  Per impostazione predefinita, il comportamento [\<routing\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing-of-servicebehavior.md) determina la creazione e il collegamento di un nuovo comportamento [\<soapProcessingExtension\>](../../../../../docs/framework/configure-apps/file-schema/wcf/soapprocessing.md) con `processMessages` impostato su `true` per ogni endpoint client.  Se si dispone di un protocollo che il servizio di routing non interpreta o si desidera eseguire l'override del comportamento di elaborazione predefinito, è possibile disabilitare l'elaborazione SOAP per l'intero servizio di routing o solo per determinati endpoint. Per disabilitare l'elaborazione SOAP per l'intero servizio di routing su tutti gli endpoint, impostare l'attributo `soapProcessing` del comportamento [\<routing\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing-of-servicebehavior.md) su `false`.  Per disattivare l'elaborazione SOAP per un determinato endpoint, usare questo comportamento e impostare l'attributo `processMessages` su `false`, quindi collegare questo comportamento all'endpoint che non si desidera venga eseguito con il codice di elaborazione predefinito. Quando il comportamento [\<routing\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing-of-servicebehavior.md) determina l'impostazione del servizio di routing, la riapplicazione del comportamento dell'endpoint verrà ignorata fino a quando non ne esiste già un altro.  
  
## Vedere anche  
 <xref:System.ServiceModel.Routing.Configuration.> SoapProcessingExtensionElement?qualifyHint=False&autoUpgrade=True   
 <xref:System.ServiceModel.Routing.SoapProcessingBehavior>