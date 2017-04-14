---
title: "Procedura: configurare i servizi WCF per interagire con i client WSE 3.0 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0f38c4a0-49a6-437c-bdde-ad1d138d3c4a
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Procedura: configurare i servizi WCF per interagire con i client WSE 3.0
I servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] sono compatibili a livello di rete con i client Web Services Enhancements 3.0 for Microsoft .NET \(WSE\) se tali servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono configurati per utilizzare la versione dell'agosto 2004 della specifica WS\-Addressing.  
  
### Per consentire a un servizio WCF di interagire con i client WSE 3.0  
  
1.  Definire un'associazione personalizzata per il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
     Per specificare l'utilizzo della versione dell'agosto 2004 della specifica WS\-Addressing per la codifica dei messaggi, è necessario creare un'associazione personalizzata.  
  
    1.  Aggiungere un [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) figlio ad [\<associazioni\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) del file di configurazione del servizio.  
  
    2.  Specificare un nome per l'associazione aggiungendo un [\<associazione\>](../../../../docs/framework/misc/binding.md) all'[\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) e impostando l'attributo `name`.  
  
    3.  Specificare una modalità di autenticazione e la versione delle specifiche WS\-Security utilizzate per proteggere i messaggi compatibili con WSE 3.0, aggiungendo un [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) figlio all'[\<associazione\>](../../../../docs/framework/misc/binding.md).  
  
         Per impostare la modalità di autenticazione, impostare l'attributo `authenicationMode` dell'[\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md).Una modalità di autenticazione è più o meno equivalente a un'asserzione di sicurezza turnkey in WSE 3.0.Nella tabella che segue viene illustrato il mapping delle modalità di autenticazione in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] alle asserzioni di sicurezza turnkey in WSE 3.0.  
  
        |Modalità di autenticazione WCF|Asserzione di sicurezza turnkey WSE 3.0|  
        |------------------------------------|---------------------------------------------|  
        |<xref:System.ServiceModel.Configuration.AuthenticationMode>|`anonymousForCertificateSecurity`|  
        |<xref:System.ServiceModel.Configuration.AuthenticationMode>|`kerberosSecurity`|  
        |<xref:System.ServiceModel.Configuration.AuthenticationMode>|`mutualCertificate10Security`\*|  
        |<xref:System.ServiceModel.Configuration.AuthenticationMode>|`mutualCertificate11Security`\*|  
        |<xref:System.ServiceModel.Configuration.AuthenticationMode>|`usernameOverTransportSecurity`|  
        |<xref:System.ServiceModel.Configuration.AuthenticationMode>|`usernameForCertificateSecurity`|  
  
         \* Una delle differenze principali tra le asserzioni di sicurezza turnkey `mutualCertificate10Security` e `mutualCertificate11Security` è la versione della specifica WS\-Security utilizzata da WSE per proteggere i messaggi SOAP.Per `mutualCertificate10Security` viene utilizzata la versione WS\-Security 1.0, mentre per `mutualCertificate11Security` viene utilizzata la versione WS\-Security 1.1.Per [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], la versione della specifica WS\-Security viene definita nell'attributo `messageSecurityVersion` dell'[\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md).  
  
         Per impostare la versione della specifica WS\-Security utilizzata per proteggere i messaggi SOAP, impostare l'attributo `messageSecurityVersion` dell'[\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md).Per interagire con WSE 3.0, impostare il valore dell'attributo `messageSecurityVersion` su <xref:System.ServiceModel.MessageSecurityVersion.WSSecurity11WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11BasicSecurityProfile10%2A>.  
  
    4.  Specificare l'utilizzo della versione dell'agosto 2004 della specifica WS\-Addressing da parte di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] aggiungendo un [\<codificaMessaggiTesto\>](../../../../docs/framework/configure-apps/file-schema/wcf/textmessageencoding.md) e impostare `messageVersion` sul relativo valore nella classe <xref:System.ServiceModel.Channels.MessageVersion.Soap11WSAddressingAugust2004%2A>.  
  
        > [!NOTE]
        >  Quando si utilizza SOAP 1.2, impostare l'attributo `messageVersion` su <xref:System.ServiceModel.Channels.MessageVersion.Soap12WSAddressingAugust2004%2A>.  
  
2.  Specificare l'utilizzo dell'associazione personalizzata da parte del servizio.  
  
    1.  Impostare l'attributo `binding` dell'elemento [\<endpoint\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md) su `customBinding`.  
  
    2.  Impostare l'attributo `bindingConfiguration` dell'elemento [\<endpoint\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md) sul valore specificato nell'attributo `name` dell'[\<associazione\>](../../../../docs/framework/misc/binding.md) per l'associazione personalizzata.  
  
## Esempio  
 Nell'esempio di codice seguente viene specificato che `Service.HelloWorldService` utilizza un'associazione personalizzata per interagire con i client WSE 3.0.L'associazione personalizzata specifica che per la codifica dei messaggi scambiati viene utilizzata la versione dell'agosto 2004 del set di specifiche WS\-Addressing e WS\-Security 1.1.I messaggi vengono protetti utilizzando la modalità di autenticazione <xref:System.ServiceModel.Configuration.AuthenticationMode>.  
  
```  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service   
        behaviorConfiguration="ServiceBehavior"   
        name="Service.HelloWorldService">  
        <endpoint binding="customBinding" address=""  
          bindingConfiguration="ServiceBinding"  
          contract="Service.IHelloWorld"></endpoint>  
      </service>  
    </services>  
  
    <bindings>  
      <customBinding>  
        <binding name="ServiceBinding">  
          <security authenticationMode="AnonymousForCertificate"  
                  messageProtectionOrder="SignBeforeEncrypt"  
                  messageSecurityVersion="WSSecurity11WSTrustFebruary2005WSSecureConversationFebruary2005WSSecurityPolicy11BasicSecurityProfile10"  
                  requireDerivedKeys="false">  
          </security>  
          <textMessageEncoding messageVersion ="Soap11WSAddressingAugust2004"></textMessageEncoding>  
          <httpTransport/>  
        </binding>  
      </customBinding>  
    </bindings>  
    <behaviors>  
      <behavior name="ServiceBehavior" returnUnknownExceptionsAsFaults="true">  
        <serviceCredentials>  
          <serviceCertificate findValue="CN=WCFQuickstartServer" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectDistinguishedName"/>  
        </serviceCredentials>  
      </behavior>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
## Vedere anche  
 [Procedura: personalizzare un'associazione fornita dal sistema](../../../../docs/framework/wcf/extending/how-to-customize-a-system-provided-binding.md)