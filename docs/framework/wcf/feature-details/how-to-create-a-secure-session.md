---
title: "Procedura: creare una sessione protetta | Microsoft Docs"
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
  - "sicurezza [WCF], creazione di una sessione"
ms.assetid: b6f42b5a-bbf7-45cf-b917-7ec9fa7ae110
caps.latest.revision: 10
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 10
---
# Procedura: creare una sessione protetta
Ad eccezione dell'associazione [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md), le associazioni fornite dal sistema in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] usano automaticamente sessioni protette quando è abilitata la protezione dei messaggi.  
  
 Per impostazione predefinita, le sessioni protette non restano attive quando un server Web viene riciclato.  Quando si stabilisce una sessione protetta, il client e il servizio memorizzano nella cache la chiave associata alla sessione protetta.  Durante lo scambio dei messaggi, viene scambiato solo un identificatore della chiave memorizzata nella cache.  Se il server Web viene riciclato, anche la cache viene riciclata, pertanto il server Web non può recuperare la chiave memorizzata nella cache per l'identificatore.  In questo caso, al client viene restituita un'eccezione.  Le sessioni protette che usano un token del contesto di sicurezza \(SCT\) con stato possono restare attive quando un server Web viene riciclato.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'utilizzo di un token del contesto di sicurezza con stato in una sessione protetta, vedere [Procedura: creare un token di contesto di sicurezza per una sessione sicura](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md).  
  
### Per specificare che un servizio usa sessioni protette mediante una delle associazioni fornite dal sistema  
  
-   Configurare un servizio per l'uso di un'associazione fornita dal sistema che supporta la protezione dei messaggi.  
  
     Ad eccezione dell'associazione [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md), se le associazioni fornite dal sistema sono configurate per l'uso della protezione dei messaggi, in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono usate automaticamente le sessioni protette.  Nella tabella seguente vengono elencate le associazioni fornite dal sistema che supportano la protezione dei messaggi e viene indicato se la protezione del messaggio è il meccanismo di sicurezza predefinito.  
  
    |Binding fornito dal sistema|Elemento Configuration|Sicurezza dei messaggi attivata per impostazione predefinita|  
    |---------------------------------|----------------------------|------------------------------------------------------------------|  
    |<xref:System.ServiceModel.BasicHttpBinding>|[\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)|No|  
    |<xref:System.ServiceModel.WSHttpBinding>|[\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)|Sì|  
    |<xref:System.ServiceModel.WSDualHttpBinding>|[\<wsDualHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)|Sì|  
    |<xref:System.ServiceModel.WSFederationHttpBinding>|[\<wsFederationHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md)|Sì|  
    |<xref:System.ServiceModel.NetTcpBinding>|[\<netTcpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)|No|  
    |<xref:System.ServiceModel.NetMsmqBinding>|[\<netMsmqBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md)|No|  
  
     Nell'esempio di codice seguente viene usata la configurazione per specificare un'associazione denominata `wsHttpBinding_Calculator` che usa la sicurezza dei messaggi [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) e le sessioni protette.  
  
    ```  
    <bindings>  
      <WSHttpBinding>  
       <binding name = "wsHttpBinding_Calculator">  
         <security mode="Message">  
           <message clientCredentialType="Windows"/>  
         </security>  
        </binding>  
      </WSHttpBinding>  
    </bindings>  
    ```  
  
     Nell'esempio di codice seguente viene specificato che [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md), la protezione dei messaggi e le sessioni protette vengono usati per proteggere il servizio `secureCalculator`.  
  
     [!code-csharp[c_CreateSecureSession#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createsecuresession/cs/secureservice.cs#1)]
     [!code-vb[c_CreateSecureSession#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createsecuresession/vb/secureservice.vb#1)]  
  
    > [!NOTE]
    >  Le sessioni protette possono essere disattivate per [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) impostando l'attributo `establishSecurityContext` su `false`.  Per le altre associazioni fornite dal sistema, è possibile disattivare le sessioni protette solo creando un'associazione personalizzata.  
  
### Per specificare che un servizio usa sessioni protette mediante un'associazione personalizzata  
  
-   Creare un'associazione personalizzata che specifica che i messaggi SOAP sono protetti mediante una sessione protetta.  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sulla creazione di un'associazione personalizzata, vedere [Procedura: personalizzare un'associazione fornita dal sistema](../../../../docs/framework/wcf/extending/how-to-customize-a-system-provided-binding.md).  
  
     Nell'esempio di codice seguente viene usata la configurazione per specificare un'associazione personalizzata che protegge i messaggi mediante una sessione protetta.  
  
    ```  
    <bindings>  
      <!-- configure a custom binding -->  
      <customBinding>  
        <binding name="customBinding_Calculator">  
          <security authenticationMode="SecureConversation" />  
          <secureConversationBootstrap authenticationMode="SspiNegotiated" />  
          <textMessageEncoding messageVersion="Soap12WSAddressing10" writeEncoding="utf-8"/>  
          <httpTransport/>  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
     Nell'esempio di codice seguente viene creata un'associazione personalizzata che usa la modalità di autenticazione <xref:System.ServiceModel.Configuration.AuthenticationMode> per l'avvio automatico di una sessione protetta.  
  
     [!code-csharp[c_CreateSecureSession#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createsecuresession/cs/secureservice.cs#2)]
     [!code-vb[c_CreateSecureSession#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createsecuresession/vb/secureservice.vb#2)]  
  
## Vedere anche  
 [Panoramica delle associazioni WCF](../../../../docs/framework/wcf/bindings-overview.md)