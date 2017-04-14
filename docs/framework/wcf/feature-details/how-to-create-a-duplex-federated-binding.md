---
title: "Procedura: creare un&#39;associazione federata duplex | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4331d2bc-5455-492a-9189-634a82597726
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Procedura: creare un&#39;associazione federata duplex
<xref:System.ServiceModel.WSFederationHttpBinding> supporta solo contratti di scambio di datagrammi e messaggi request\/reply.Per utilizzare il contratto di scambio di messaggi duplex, è necessario creare un'associazione personalizzata.Nelle procedure seguenti viene illustrato come effettuare questa operazione nella configurazione, utilizzando la sicurezza in modalità messaggio per i trasporti HTTP e TCP e la sicurezza in modalità mista per il trasporto TCP.Alla fine di questo argomento viene riportato il codice di esempio che illustra tutte e 3 le associazioni.  
  
 È inoltre possibile creare l'associazione nel codice.Per una descrizione dello stack degli elementi di associazione da creare, vedere [Procedura: creare un'associazione personalizzata utilizzando SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).  
  
### Per creare un'associazione personalizzata federata duplex con HTTP  
  
1.  Nel nodo [\<associazioni\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)[\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md).  
  
2.  Nell'elemento [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)[\<associazione\>](../../../../docs/framework/misc/binding.md)`name` `con l'attributo FederationDuplexHttpMessageSecurityBinding` impostato su .  
  
3.  Nell'elemento [\<associazione\>](../../../../docs/framework/misc/binding.md)[\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)`authenticationMode` `con l'attributo SecureConversation` impostato su .  
  
4.  Nell'elemento [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)[\<bootstrapConversazioneProtetta\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md)`authenticationMode` `con l'attributo IssuedTokenForCertificate` `impostato su IssuedTokenForSslNegotiated` o .  
  
5.  Dopo l'elemento [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)[\< compositeDuplex \>](../../../../docs/framework/configure-apps/file-schema/wcf/compositeduplex.md) vuoto.  
  
6.  Dopo l'elemento [\< compositeDuplex \>](../../../../docs/framework/configure-apps/file-schema/wcf/compositeduplex.md)[\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md) vuoto.  
  
7.  Dopo l'elemento [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)[\<trasportoHttp\>](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md) vuoto.  
  
### Per creare un'associazione personalizzata federata duplex con la modalità di sicurezza dei messaggi TCP  
  
1.  Nel nodo [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)[\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md).  
  
2.  Nell'elemento [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)[\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)`name` `con l'attributo FederationDuplexTcpMessageSecurityBinding` impostato su .  
  
3.  Nell'elemento [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)[\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)`authenticationMode` `con l'attributo SecureConversation` impostato su .  
  
4.  Nell'elemento [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)[\<bootstrapConversazioneProtetta\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md)`authenticationMode` `con l'attributo IssuedTokenForCertificate` `impostato su IssuedTokenForSslNegotiated` o .  
  
5.  Dopo l'elemento [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)[\<trasportoTcp\>](../../../../docs/framework/configure-apps/file-schema/wcf/tcptransport.md) vuoto.  
  
### Per creare un'associazione personalizzata federata duplex con la modalità di sicurezza mista TCP  
  
1.  Nel nodo [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)[\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md).  
  
2.  Nell'elemento [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)[\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)`name` `con l'attributo FederationDuplexTcpTransportSecurityWithMessageCredentialBinding` impostato su .  
  
3.  Nell'elemento [\<oneWay\>](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)[\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)`authenticationMode` `con l'attributo SecureConversation` impostato su .  
  
4.  Nell'elemento [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)[\<bootstrapConversazioneProtetta\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md)`authenticationMode` `con l'attributo IssuedTokenForCertificate` `impostato su IssuedTokenForSslNegotiated` o .  
  
5.  Dopo l'elemento [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)[\<sslStreamSecurity\>](../../../../docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md) vuoto.  
  
6.  Dopo l'elemento [\<sslStreamSecurity\>](../../../../docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md)[\<trasportoTcp\>](../../../../docs/framework/configure-apps/file-schema/wcf/tcptransport.md) vuoto.  
  
## Esempio di codice  
  
#### Esempio con 3 associazioni  
  
1.  Inserire il codice seguente nel file di configurazione.  
  
## Esempio  
  
```  
  
<bindings>  
   <customBinding>  
      <binding name="FederationDuplexHttpMessageSecurityBinding">  
<!-- duplex contract requires secure conversation with require cancellation = true -->  
          <security authenticationMode="SecureConversation">  
              <secureConversationBootstrap authenticationMode="IssuedTokenForSslNegotiated" />  
          </security>  
          <compositeDuplex />  
          <oneWay />  
          <httpTransport />  
       </binding>  
<!-- duplex over https is not supported -->  
       <binding name="FederationDuplexTcpMessageSecurityBinding">  
<!-- duplex contract requires secure conversation with require cancellation = true -->  
          <security authenticationMode="SecureConversation">  
              <secureConversationBootstrap authenticationMode="IssuedTokenForSslNegotiated" />  
          </security>  
          <tcpTransport />  
       </binding>              
       <binding name="FederationDuplexTcpTransportSecurityWithMessageCredentialsBinding">  
<!-- duplex contract requires secure conversation with require cancellation = true -->  
          <security authenticationMode="SecureConversation">  
              <secureConversationBootstrap authenticationMode="IssuedTokenOverTransport" />  
          </security>  
<!-- requireClientCertificate = true or <windowsStreamSecurity /> can be used, but does not make sense for most scenarios -->  
          <sslStreamSecurity />  
          <tcpTransport />  
       </binding>              
    </customBinding>  
</bindings>  
  
```