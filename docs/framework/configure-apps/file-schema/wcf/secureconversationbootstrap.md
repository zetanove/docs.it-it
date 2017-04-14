---
title: "&lt;bootstrapConversazioneProtetta&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 66b46f95-fa2d-4b5b-b6ce-0572ab0cdd50
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 13
---
# &lt;bootstrapConversazioneProtetta&gt;
Specifica i valori predefiniti usati per iniziare un servizio di conversazione protetta.  
  
## Sintassi  
  
```  
  
<secureConversationBootstrap  
   allowSerializedSigningTokenOnReply="Boolean"  
   authenticationMode="AuthenticationMode"  
   defaultAlgorithmSuite="SecurityAlgorithmSuite"  
   includeTimestamp="Boolean"  
   requireDerivedKeys="Boolean"  
   keyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy"   
messageProtectionOrder="SignBeforeEncrypt/SignBeforeEncryptAndEncryptSignature/EncryptBeforeSign"  
   messageSecurityVersion="WSSecurityJan2004/WSSecurityXXX2005"  
   requireDerivedKeys="Boolean"  
   requireSecurityContextCancellation="Boolean"  
   requireSignatureConfirmation="Boolean" >  
   securityHeaderLayout="Strict/Lax/LaxTimestampFirst/LaxTimestampLast"  
   includeTimestamp="Boolean" />  
```  
  
## Tipo  
 `Type`  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`allowSerializedSigningTokenOnReply`|Parametro facoltativo.  Valore booleano che specifica se è possibile usare un token serializzato nella risposta.  Il valore predefinito è `false`.  Se si usa un'associazione duplice, l'impostazione assume `true` come valore predefinito e qualsiasi impostazione effettuata sarà ignorata.|  
|`authenticationMode`|Specifica la modalità di autenticazione SOAP usata tra l'iniziatore e il risponditore.<br /><br /> L'impostazione predefinita è sspiNegotiated.<br /><br /> L'attributo è di tipo <xref:System.ServiceModel.Configuration.AuthenticationMode>.|  
|`defaultAlgorithmSuite`|La suite di algoritmi di sicurezza definisce vari algoritmi, fra cui gli algoritmi Canonicalization, Digest, KeyWrap, Signature, Encryption e KeyDerivation.  Ciascuna delle suite di algoritmi di sicurezza definisce valori per questi parametri diversi.  La sicurezza basata su messaggi è ottenuta usando questi algoritmi.<br /><br /> Questo attributo viene usato con una piattaforma differente che usa un set di algoritmi diverso da quello predefinito.  Quando si apportano modifiche a questa impostazione, è necessario essere consapevoli dei punti di forza e dei punti di debolezza degli algoritmi pertinenti.  L'attributo è di tipo <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>.  Il valore predefinito è `Basic256`.|  
|`includeTimestamp`|Valore booleano che specifica se in ogni messaggio vengono inclusi gli indicatori di data e ora.  Il valore predefinito è `true`.|  
|`keyEntropyMode`|Specifica la modalità di calcolo delle chiavi per la sicurezza dei messaggi.  Le chiavi possono essere basate solo sul materiale della chiave client, solo sul materiale della chiave del servizio o su una combinazione di entrambi.  I valori validi sono:<br /><br /> -   ClientEntropy: la chiave della sessione è basata sul materiale della chiave fornito dal client.<br />-   ServerEntropy: la chiave della sessione è basata sul materiale della chiave fornito dal servizio.<br />-   CombineEntropy: la chiave della sessione è basata sul materiale della chiave fornito dal client e dal servizio.<br /><br /> L'impostazione predefinita è CombinedEntropy.<br /><br /> L'attributo è di tipo <xref:System.ServiceModel.Security.SecurityKeyEntropyMode>.|  
|`messageProtectionOrder`|Imposta l'ordine nel quale gli algoritmi di sicurezza a livello di messaggio vengono applicati al messaggio.  Di seguito vengono elencati i valori validi:<br /><br /> -   SignBeforeEncrypt: prima firma, quindi crittografia.<br />-   SignBeforeEncryptAndEncryptSignature: firma, crittografia e crittografia della firma.<br />-   EncryptBeforeSign: prima crittografia, quindi firma.<br /><br /> SignBeforeEncryptAndEncryptSignature è il valore predefinito se si usano i certificati reciproci con WS\-Security 1.1.  SignBeforeEncrypt è l'impostazione predefinita con WS\-Security 1.0.<br /><br /> L'attributo è di tipo <xref:System.ServiceModel.Security.MessageProtectionOrder>.|  
|`messageSecurityVersion`|Imposta la versione di WS\-Security da usare.  Di seguito vengono elencati i valori validi:<br /><br /> -   WSSecurityJan2004<br />-   WSSecurityXXX2005<br /><br /> L'impostazione predefinita è WSSecurityXXX2005.  L'attributo è di tipo <xref:System.ServiceModel.MessageSecurityVersion>.|  
|`requireDerivedKeys`|Valore booleano che specifica se le chiavi possono essere derivate dalle chiavi di prova originali.  Il valore predefinito è `true`.|  
|`requireSecurityContextCancellation`|Valore booleano che specifica se il contesto di sicurezza deve essere annullato e terminato nel caso in cui non sia più richiesto.  Il valore predefinito è `true`.|  
|`requireSignatureConfirmation`|Valore booleano che specifica se la conferma della firma WS\-Security è attivata.  Quando è impostato su `true`, le firme del messaggio vengono confermate dal responder.  Il valore predefinito è `false`.<br /><br /> La conferma della firma è usata per confermare che la risposta del servizio sia completamente compatibile con una richiesta.|  
|`securityHeaderLayout`|Specifica l'ordine degli elementi nell'intestazione di sicurezza.  I valori validi sono:<br /><br /> -   Strict.  Gli elementi vengono aggiunti all'intestazione di sicurezza secondo il principio generale di "dichiarazione prima dell'uso".<br />-   Lax.  Gli elementi vengono aggiunti all'intestazione di sicurezza in qualsiasi ordine conforme alla sicurezza WSS: messaggi SOAP.<br />-   LaxWithTimestampFirst.  Gli elementi vengono aggiunti all'intestazione di sicurezza in qualsiasi ordine conforme alla sicurezza WSS: messaggi SOAP, tranne che il primo elemento nell'intestazione di sicurezza deve essere un elemento wsse:Timestamp.<br />-   LaxWithTimestampLast.  Gli elementi vengono aggiunti all'intestazione di sicurezza in qualsiasi ordine conforme alla sicurezza WSS: messaggi SOAP, tranne che l'ultimo elemento nell'intestazione di sicurezza deve essere un elemento wsse:Timestamp.<br /><br /> L'impostazione predefinita è Strict.<br /><br /> L'elemento è di tipo <xref:System.ServiceModel.Channels.SecurityHeaderLayout>.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<parametriTokenEmesso\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenparameters.md)|Specifica un token corrente rilasciato.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement>.|  
|[\<impostazioniClientLocali\>](../../../../../docs/framework/configure-apps/file-schema/wcf/localclientsettings-element.md)|Specifica le impostazioni di sicurezza di un client locale per questa associazione.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.LocalClientSecuritySettingsElement>.|  
|[\<impostazioniServizioLocali\>](../../../../../docs/framework/configure-apps/file-schema/wcf/localservicesettings-element.md)|Specifica le impostazioni di sicurezza di un servizio locale per questa associazione.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.LocalServiceSecuritySettingsElement>.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)|Specifica le opzioni di sicurezza di un'associazione personalizzata.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.LocalServiceSecuritySettingsElement>   
 <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalServiceSettings%2A>   
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [Procedura: creare un'associazione personalizzata utilizzando SecurityBindingElement](../../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)   
 [Sicurezza delle associazioni personalizzate](../../../../../docs/framework/wcf/samples/custom-binding-security.md)