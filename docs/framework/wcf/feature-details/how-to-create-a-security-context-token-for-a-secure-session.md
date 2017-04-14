---
title: "Procedura: creare un token di contesto di sicurezza per una sessione sicura | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 640676b6-c75a-4ff7-aea4-b1a1524d71b2
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# Procedura: creare un token di contesto di sicurezza per una sessione sicura
Per evitare la perdita di una determinata sessione protetta quando il servizio viene riciclato, è possibile utilizzare in tale sessione un token di contesto di sicurezza \(SCT, Security Context Token\) con stato.Ad esempio, quando in una sessione protetta si utilizza un token SCT senza stato e si reimposta Internet Information Services \(IIS\), i dati di sessione associati al servizio vengono persi.Questi dati di sessione comprendono una cache del token SCT.Pertanto, quando un client invia al servizio un token SCT senza stato, viene restituito un errore, in quanto risulta impossibile recuperare la chiave associata al token SCT.Se tuttavia si utilizza un token SCT con stato, la relativa chiave associata è contenuta nel token SCTe quindi nel messaggio. Ne consegue che in questo caso il riciclo del servizio non influisce sulla sessione protetta.Per impostazione predefinita, [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] utilizza token SCT senza stato nelle sessioni protette.In questo argomento viene descritto in modo dettagliato come utilizzare token SCT con stato in una sessione protetta.  
  
> [!NOTE]
>  I token SCT con stato non possono essere utilizzati in una sessione protetta che prevede un contratto derivato dall'interfaccia <xref:System.ServiceModel.Channels.IDuplexChannel>.  
  
> [!NOTE]
>  Nelle applicazioni che utilizzano token SCT con stato in una sessione protetta, l'ID del thread del servizio deve essere un account utente a cui è stato associato un profilo utente.Quando il servizio viene eseguito nel contesto di un account privo di profilo utente, ad esempio `Local Service`, è possibile che venga generata un'eccezione.  
  
> [!NOTE]
>  Quando la rappresentazione è obbligatoria in Windows XP, utilizzare una sessione protetta priva di token SCT con stato.Infatti, quando i token SCT con stato vengono utilizzati con la rappresentazione, il sistema genera un'eccezione <xref:System.InvalidOperationException>.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Scenari non supportati](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md).  
  
### Per utilizzare token SCT con stato in una sessione protetta  
  
-   Creare un'associazione personalizzata che prevede la protezione dei messaggi SOAP mediante una sessione protetta che utilizza un token SCT con stato.  
  
    1.  Definire un'associazione personalizzata, aggiungendo un [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) al file di configurazione del servizio.  
  
        ```  
        <customBinding>  
        ```  
  
    2.  Aggiungere un elemento figlio [\<associazione\>](../../../../docs/framework/misc/binding.md)[\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md).  
  
         Specificare il nome dell'associazione impostando l'attributo `name` su un nome univoco all'interno del file di configurazione.  
  
        ```  
        <binding name="StatefulSCTSecureSession">  
        ```  
  
    3.  Specificare la modalità di autenticazione dei messaggi scambiati con il servizio aggiungendo un elemento figlio dell'[\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) all'[\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md).  
  
         Specificare l'utilizzo di una sessione protetta impostando l'attributo `authenticationMode` su `SecureConversation`.Specificare l'utilizzo di token SCT con stato impostando l'attributo `requireSecurityContextCancellation` su `false`.  
  
        ```  
        <security authenticationMode="SecureConversation"  
                  requireSecurityContextCancellation="false">  
        ```  
  
    4.  Specificare la modalità di autenticazione del client durante la creazione della sessione protetta aggiungendo un elemento figlio dell'[\<bootstrapConversazioneProtetta\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) all'[\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md).  
  
         Specificare la modalità di autenticazione del client impostando l'attributo `authenticationMode`.  
  
        ```  
        <secureConversationBootstrap authenticationMode="UserNameForCertificate" />  
        ```  
  
    5.  Specificare la codifica dei messaggi aggiungendo un elemento di codifica, ad esempio l'[\<codificaMessaggiTesto\>](../../../../docs/framework/configure-apps/file-schema/wcf/textmessageencoding.md).  
  
        ```  
        <textMessageEncoding />  
        ```  
  
    6.  Specificare il trasporto aggiungendo un elemento di trasporto, ad esempio l'[\<trasportoHttp\>](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md).  
  
        ```  
        <httpTransport />  
        ```  
  
     Nell'esempio di codice seguente si utilizza la configurazione per specificare un'associazione personalizzata in cui i messaggi possono utilizzare token SCT con stato in una sessione protetta.  
  
    ```  
    <customBinding>  
      <binding name="StatefulSCTSecureSession">  
        <security authenticationMode="SecureConversation"  
                  requireSecurityContextCancellation="false">  
          <secureConversationBootstrap authenticationMode="UserNameForCertificate" />  
        </security>  
        <textMessageEncoding />  
        <httpTransport />  
      </binding>  
    </customBinding>  
    ```  
  
## Esempio  
 Nell'esempio di codice seguente viene creata un'associazione personalizzata che utilizza la modalità di autenticazione <xref:System.ServiceModel.Configuration.AuthenticationMode> per il bootstrap di una sessione protetta.  
  
 [!code-csharp[c_CreateStatefulSCT#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createstatefulsct/cs/secureservice.cs#2)]
 [!code-vb[c_CreateStatefulSCT#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createstatefulsct/vb/secureservice.vb#2)]  
  
 Quando si utilizza l'autenticazione di Windows insieme ai token SCT con stato, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] imposta la proprietà <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> su anonimo anziché popolarla con l'ID del chiamante effettivo.Poiché il sistema di sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] deve ricreare il contenuto del contesto di sicurezza del servizio per ogni richiesta contenuta nel token SCT in ingresso, il server non memorizza alcuna traccia relativa alla sessione di sicurezza.Inoltre, poiché è impossibile serializzare l'istanza della classe <xref:System.Security.Principal.WindowsIdentity> nel token SCT, la proprietà <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> restituisce un'identità anonima.  
  
 Questo comportamento viene illustrato nella configurazione seguente.  
  
```  
<customBinding>  
  <binding name="Cancellation">  
       <textMessageEncoding />  
        <security   
            requireSecurityContextCancellation="false">  
              <secureConversationBootstrap />  
      </security>  
    <httpTransport />  
  </binding>  
</customBinding>  
  
```  
  
## Vedere anche  
 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)