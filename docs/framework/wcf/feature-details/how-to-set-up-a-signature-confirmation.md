---
title: "Procedura: impostare una conferma della firma | Microsoft Docs"
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
  - "conferma della firma"
  - "WCF, sicurezza"
ms.assetid: 2424c137-c7c2-4aa9-8d5d-a066e12fefda
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Procedura: impostare una conferma della firma
*La conferma della firma* è un meccanismo che permette all'iniziatore del messaggio di assicurare che la risposta ricevuta sia stata generata in risposta al messaggio originale del mittente.La conferma della firma è definita nella specifica WS\-Security 1.1.Se un endpoint supporta WS\-Security 1.0, non è possibile utilizzare la conferma della firma.  
  
 Nelle procedure seguenti viene illustrato come consentire la conferma della firma utilizzando un <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>.È possibile utilizzare la stessa procedura con un <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>.La procedura è basata sui passaggi di base illustrati in [Procedura: creare un'associazione personalizzata utilizzando SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).  
  
### Per consentire la conferma della firma nel codice  
  
1.  Creare un'istanza della classe <xref:System.ServiceModel.Channels.BindingElementCollection>.  
  
2.  Creare un'istanza della classe <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>.  
  
3.  Impostare <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.RequireSignatureConfirmation%2A> su `true`.  
  
4.  Aggiungere l'elemento di sicurezza alla raccolta di associazioni.  
  
5.  Creare un'associazione personalizzata, come specificato in [Procedura: creare un'associazione personalizzata utilizzando SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).  
  
### Per consentire la conferma della firma nella configurazione  
  
1.  Aggiungere un elemento `<customBinding>``<bindings> alla sezione`  del file di configurazione.  
  
2.  Aggiungere un elemento `<binding>` e impostare l'attributo del nome su un valore appropriato.  
  
3.  Aggiungere un elemento di codifica appropriato.Nell'esempio seguente viene aggiunto un elemento `<TextMessageEncoding>`.  
  
4.  Aggiungere un elemento figlio `<security>``requireSignatureConfirmation e impostare l'attributo` `true su` .  
  
5.  Facoltativo.Per consentire la conferma della firma durante il bootstrap, aggiungere un elemento figlio [\<bootstrapConversazioneProtetta\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) e impostare l'attributo `equireSignatureConfirmation` su `true`.  
  
6.  Aggiungere un elemento di trasporto appropriato.Nell'esempio seguente viene aggiunto un [\<trasportoHttp\>](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md):  
  
    ```  
    <bindings>  
      <customBinding>  
        <binding name="SignatureConfirmationBinding">  
          <security requireSignatureConfirmation="true">  
            <secureConversationBootstrap requireSignatureConfirmation="true" />  
              </security>  
           <textMessageEncoding />  
             <httpTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
## Esempio  
 Nel codice seguente viene creata un'istanza di <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> e viene impostata la proprietà <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.RequireSignatureConfirmation%2A> su `true`.Si noti che in questo esempio non viene utilizzato l'elemento `<secureConversationBootstrap>` illustrato nell'esempio precedente.In questo esempio viene illustrata la conferma della firma quando si utilizza un token di Windows \(protocollo Kerberos\).In questo caso, la firma del client viene restituita in tutte le risposte dal servizio e viene confermata dal client.  
  
 [!code-csharp[c_SignatureConfirmation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_signatureconfirmation/cs/source.cs#1)]
 [!code-vb[c_SignatureConfirmation#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_signatureconfirmation/vb/source.vb#1)]  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateMutualCertificateBindingElement%2A>   
 [Procedura: creare un'associazione personalizzata utilizzando SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)   
 [Procedura: creare un elemento SecurityBindingElement per una modalità di autenticazione specificata](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)