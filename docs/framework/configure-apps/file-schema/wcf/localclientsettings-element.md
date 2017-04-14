---
title: "Elemento &lt;localClientSettings&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4680ace5-f4e1-4fcb-b9d8-a4a4af5cd7ae
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Elemento &lt;localClientSettings&gt;
Specifica le impostazioni di sicurezza di un client locale per questa associazione.  
  
## Sintassi  
  
```  
  
<security>  
   <localClientSettings cacheCookies="Boolean"  
      cookieRenewalThresholdPercentage="Integer"  
      detectReplays="Boolean"  
      maxClockSkew="TimeSpan"  
      maxCookieCachingTime="TimeSpan"  
      reconnectTransportOnFailure="Boolean"  
      replayCacheSize="Integer"  
      replayWindow="TimeSpan"  
      sessionKeyRenewalInterval="TimeSpan"  
      sessionKeyRolloverInterval="TimeSpan"  
      timestampValidityDuration="TimeSpan" />  
</security>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`cacheCookies`|Valore booleano che specifica se è attivata la memorizzazione dei cookie nella cache.  Il valore predefinito è `false`.|  
|`cookieRenewalThresholdPercentage`|Un numero intero che specifica la percentuale massima di cookie che possono essere rinnovati.  Questo valore deve essere compreso tra 0 e 100 inclusi.  Il valore predefinito è 90.|  
|`detectReplays`|Valore booleano che specifica se gli attacchi di tipo replay contro il canale vengono rilevati e gestiti automaticamente.  Il valore predefinito è `false`.|  
|`maxClockSkew`|<xref:System.TimeSpan> specifica la differenza massima di tempo tra gli orologi di sistema delle due parti che stanno comunicando.  Il valore predefinito è "00:05:00".<br /><br /> Quando l'impostazione di questo valore è quella predefinita, il destinatario accetta i messaggi con timestamp relativi all'ora di invio precedenti o successivi all'ora in cui il messaggio è stato ricevuto.  I messaggi che non passano i test dell'ora di invio vengono rifiutati.  Questa impostazione viene usata in combinazione con l'attributo `replayWindow`.|  
|`maxCookieCachingTime`|<xref:System.TimeSpan> specifica la durata massima dei cookie.  Il valore predefinito è "10675199.02:48:05.4775807".|  
|`reconnectTransportOnFailure`|Valore booleano che specifica se le connessioni che usano WS\-Reliable Messaging tenteranno la riconnessione in caso di errori del trasporto.  L'impostazione predefinita è `true`, la quale significa un numero infinito di tentativi di riconnessione.  Il ciclo viene interrotto dal timeout di inattività che fa sì che il canale generi un'eccezione quando la riconnessione non è possibile.|  
|`replayCacheSize`|Un numero intero positivo che specifica il numero di parametri nonce da usare per il rilevamento di attacchi di tipo replay.  Se questo limite viene superato, il nonce meno recente viene rimosso e viene creato un nuovo nonce per il messaggio nuovo.  Il valore predefinito è 500000.|  
|`replayWindow`|<xref:System.TimeSpan> specifica la durata di validità dei singoli nonce dei messaggi.<br /><br /> Dopo questa durata, un messaggio inviato con lo stesso nonce di quello inviato precedentemente non verrà accettato.  Questo attributo viene usato in combinazione con l'attributo `maxClockSkew` per impedire attacchi di tipo replay.  L'autore di un attacco può replicare un messaggio dopo che la finestra di replay è scaduta.  Questo messaggio, tuttavia, non supererebbe il test `maxClockSkew` che rifiuta i messaggi con timestamp relativi all'ora di invio che differiscono di un tempo specificato in più o in meno rispetto all'ora in cui il messaggio è stato ricevuto.|  
|`sessionKeyRenewalInterval`|<xref:System.TimeSpan> specifica l'intervallo di tempo dopo il quale l'iniziatore rinnoverà la chiave per la sessione di sicurezza.  L'impostazione predefinita è "10:00:00".|  
|`sessionKeyRolloverInterval`|<xref:System.TimeSpan> specifica l'intervallo di tempo per il quale la chiave della sessione precedente è valida nei messaggi in arrivo durante un rinnovo della chiave.  L'impostazione predefinita è "00:05:00".<br /><br /> Durante il rinnovo della chiave, client e server devono inviare i messaggi usando sempre la chiave disponibile più recente.  Entrambe le parti accetteranno i messaggi in arrivo protetti con la chiave della sessione precedente fino alla scadenza del tempo di sostituzione.|  
|`timestampValidityDuration`|<xref:System.TimeSpan> positivo che specifica il periodo di validità di un timestamp.  L'impostazione predefinita è "00:15:00".|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)|Specifica le opzioni di sicurezza di un'associazione personalizzata.|  
|[\<bootstrapConversazioneProtetta\>](../../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md)|Specifica i valori predefiniti usati per iniziare un servizio di conversazione protetta.|  
  
## Note  
 Le impostazioni sono locali nel senso che non sono derivate dai criteri di sicurezza del servizio.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.LocalClientSecuritySettingsElement>   
 <xref:System.ServiceModel.Configuration.SecurityElementBase.LocalClientSettings%2A>   
 <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalClientSettings%2A>   
 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [Procedura: creare un'associazione personalizzata utilizzando SecurityBindingElement](../../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)   
 [Sicurezza delle associazioni personalizzate](../../../../../docs/framework/wcf/samples/custom-binding-security.md)