---
title: "Procedura: impostare la modalit&#224; di sicurezza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Proprietà Mode"
  - "WCF, protezione"
  - "WCF, modalità di sicurezza"
ms.assetid: 6e01dd9f-b5dd-4474-b24c-06e124de4ff7
caps.latest.revision: 22
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 22
---
# Procedura: impostare la modalit&#224; di sicurezza
Il sistema di sicurezza di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] presenta tre modalità di sicurezza in genere disponibili nella maggior parte delle associazioni predefinite: a livello di trasporto \("Transport"\), a livello di messaggio \("Message"\) e "Trasporto con credenziale a livello di messaggio" \("TransportWithMessageCredential"\). Esistono inoltre due modalità aggiuntive disponibili soltanto in due associazioni specifiche: la modalità "Solo credenziale a livello di trasporto" \("TransportCredentialOnly"\) dell'associazione <xref:System.ServiceModel.BasicHttpBinding> e la modalità "Entrambi" \("Both"\) dell'associazione <xref:System.ServiceModel.NetMsmqBinding>.Tuttavia, questo argomento descrive solo le tre modalità di sicurezza generali, ovvero: <xref:System.ServiceModel.SecurityMode>, <xref:System.ServiceModel.SecurityMode> e <xref:System.ServiceModel.SecurityMode>.  
  
 Si noti che non tutte le associazioni predefinite supportano queste modalità.Questo argomento descrive come utilizzare le classi <xref:System.ServiceModel.WSHttpBinding> e <xref:System.ServiceModel.NetTcpBinding> per impostare la modalità, sia a livello di programmazione sia in configurazione.  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)] sicurezza di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], vedere [Cenni preliminari sulla sicurezza](../../../docs/framework/wcf/feature-details/security-overview.md), [Protezione dei servizi](../../../docs/framework/wcf/securing-services.md) e [Protezione di servizi e client](../../../docs/framework/wcf/feature-details/securing-services-and-clients.md).[!INCLUDE[crabout](../../../includes/crabout-md.md)] sicurezza di trasporti e messaggi, vedere [Protezione del trasporto](../../../docs/framework/wcf/feature-details/transport-security.md) e [Protezione dei messaggi](../../../docs/framework/wcf/feature-details/message-security-in-wcf.md).  
  
### Per impostare la modalità di sicurezza in codice  
  
1.  Creare un'istanza della classe di associazione in uso.Per un elenco di associazioni predefinite, vedere [Associazioni fornite dal sistema](../../../docs/framework/wcf/system-provided-bindings.md).In questo esempio viene creata un'istanza della classe <xref:System.ServiceModel.WSHttpBinding>  
  
2.  Impostare la proprietà `Mode` dell'oggetto restituito dalla proprietà `Security`.  
  
     [!code-csharp[c_SettingSecurityMode#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#1)]
     [!code-vb[c_SettingSecurityMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#1)]  
  
     In alternativa, impostare la modalità su "Message", come mostrato nel codice seguente.  
  
     [!code-csharp[c_SettingSecurityMode#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#2)]
     [!code-vb[c_SettingSecurityMode#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#2)]  
  
     In alternativa, impostare la modalità su "TransportWithMessageCredential", come mostrato nel codice seguente.  
  
     [!code-csharp[c_SettingSecurityMode#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#3)]
     [!code-vb[c_SettingSecurityMode#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#3)]  
  
3.  La modalità può anche essere impostata nel costruttore dell'associazione, come mostrato nel codice seguente.  
  
     [!code-csharp[c_SettingSecurityMode#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#4)]
     [!code-vb[c_SettingSecurityMode#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#4)]  
  
## Impostazione della proprietà ClientCredentialType  
 L'impostazione della modalità su uno dei tre valori determina il valore su cui impostare la proprietà che specifica il tipo di credenziale client, ovvero `ClientCredentialType`.Ad esempio, se si utilizza la classe <xref:System.ServiceModel.WSHttpBinding> e si imposta la modalità su `Transport`, occorre impostare la proprietà <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A> della classe <xref:System.ServiceModel.HttpTransportSecurity> su un valore appropriato.  
  
#### Per impostare la proprietà ClientCredentialType quando si imposta la modalità "Transport"  
  
1.  Creare un'istanza dell'associazione.  
  
2.  Impostare la proprietà `Mode` su `Transport`.  
  
3.  Impostare la proprietà `ClientCredential` su un valore appropriato.Nell'esempio di codice seguente la proprietà viene impostata su `Windows`.  
  
     [!code-csharp[c_SettingSecurityMode#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#5)]
     [!code-vb[c_SettingSecurityMode#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#5)]  
  
#### Per impostare la proprietà ClientCredentialType quando si imposta la modalità "Message"  
  
1.  Creare un'istanza dell'associazione.  
  
2.  Impostare la proprietà `Mode` su `Message`.  
  
3.  Impostare la proprietà `ClientCredential` su un valore appropriato.Nell'esempio di codice seguente la proprietà viene impostata su `Certificate`.  
  
     [!code-csharp[c_SettingSecurityMode#6](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#6)]
     [!code-vb[c_SettingSecurityMode#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#6)]  
  
#### Per impostare la modalità e la proprietà ClientCredentialType in configurazione  
  
1.  Aggiungere un elemento di associazione appropriato all'elemento [\<associazioni\>](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) del file di configurazione.Nell'esempio seguente viene aggiunto un elemento [\<wsHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).  
  
2.  Aggiungere un elemento `<binding>``name e impostare il relativo attributo`  su un valore appropriato.  
  
3.  Aggiungere un elemento `<security>``mode e impostare l'attributo` `Message su` `Transport,` `TransportWithMessageCredential oppure` .  
  
4.  Se si imposta la modalità su `Transport`, aggiungere un elemento `<transport>``clientCredential e impostare l'attributo`  su un valore appropriato.  
  
     Nell'esempio seguente, la modalità viene impostata su "`Transport"`, quindi l'attributo `clientCredentialType` dell'elemento `<transport>` viene impostato su "`Windows"`.  
  
    ```  
    <wsHttpBinding>  
    <binding name="TransportSecurity">  
        <security mode="Transport" />  
           <transport clientCredentialType = "Windows" />  
        </security>  
    </binding>  
    </wsHttpBinding >  
    ```  
  
     In alternativa, impostare la `security mode` su "`Message"` seguita da un elemento `<"message">`.In questo esempio l'attributo `clientCredentialType` viene impostato su "`Certificate"`.  
  
    ```  
    <wsHttpBinding>  
    <binding name="MessageSecurity">  
        <security mode="Message" />  
           <message clientCredentialType = "Certificate" />  
        </security>  
    </binding>  
    </wsHttpBinding >  
    ```  
  
     L'utilizzo del valore <xref:System.ServiceModel.BasicHttpSecurityMode> rappresenta un caso speciale e viene spiegato di seguito.  
  
### Utilizzo della modalità TransportWithMessageCredential  
 Quando si imposta la modalità di sicurezza su `TransportWithMessageCredential`, il trasporto determina il meccanismo di sicurezza a livello di trasporto effettivamente utilizzato.Ad esempio, il protocollo di trasporto HTTP utilizza il meccanismo Secure Sockets Layer \(SSL\) su HTTP \(HTTPS\).Pertanto, l'impostazione della proprietà `ClientCredentialType` di qualsiasi oggetto di sicurezza a livello di trasporto \(ad esempio <xref:System.ServiceModel.HttpTransportSecurity>\) viene ignorata.In altre parole, è possibile impostare solo la proprietà `ClientCredentialType` dell'oggetto di sicurezza a livello di messaggio \(per l'associazione `WSHttpBinding`, tale proprietà può essere impostata solo per l'oggetto <xref:System.ServiceModel.NonDualMessageSecurityOverHttp>\).  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Procedura: utilizzare le funzionalità di sicurezza a livello di trasporto e le credenziali a livello di messaggio](../../../docs/framework/wcf/feature-details/how-to-use-transport-security-and-message-credentials.md).  
  
## Vedere anche  
 [Procedura: configurare una porta con un certificato SSL](../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)   
 [Procedura: utilizzare le funzionalità di sicurezza a livello di trasporto e le credenziali a livello di messaggio](../../../docs/framework/wcf/feature-details/how-to-use-transport-security-and-message-credentials.md)   
 [Protezione del trasporto](../../../docs/framework/wcf/feature-details/transport-security.md)   
 [Protezione dei messaggi](../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)   
 [Cenni preliminari sulla sicurezza](../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Associazioni fornite dal sistema](../../../docs/framework/wcf/system-provided-bindings.md)   
 [\<sicurezza\>](../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md)   
 [\<sicurezza\>](../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md)   
 [\<sicurezza\>](../../../docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md)