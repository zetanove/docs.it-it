---
title: "Guida di interoperabilit&#224; dei protocolli di servizi Web | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f2981678-ebdb-433d-899b-467f7df95fb2
caps.latest.revision: 20
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 20
---
# Guida di interoperabilit&#224; dei protocolli di servizi Web
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] implementa una serie di protocolli di servizi Web.  Molti di questi protocolli includono diverse opzioni e punti estendibilità lasciati alla discrezione dell'implementatore.  In questo argomento viene fornito un elenco di protocolli di servizi Web implementati da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Altri argomenti di questa sezione forniscono dettagli di implementazione per ogni protocollo supportato.  
  
## Protocolli di servizi Web implementati da WCF  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce il supporto per protocolli dell'infrastruttura di servizi Web \(WS\) attraverso canali e protocolli di applicazioni di servizi Web tramite la funzionalità dei contratti.  L'interoperabilità per i protocolli di applicazioni è ottenuta tramite il linguaggio XSD \(XML Description Language\) 1.0 e il linguaggio WSDL \(Web Services Description Language\) 1.1.  
  
 L'interoperabilità dei protocolli dell'infrastruttura è garantita dalle specifiche WS\-\*.  I canali [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] forniscono il supporto per numerosi protocolli dell'infrastruttura WS\-\*.  I canali [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono configurati mediante elementi di associazione.  Nelle tabelle seguenti è riportato l'elenco completo dei protocolli dell'infrastruttura WS\-\* implementati da vari elementi di associazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> supporta le specifiche indicate nella tabella seguente.  
  
|Specifica\/documento|Collegamento|  
|--------------------------|------------------|  
|HTTP 1.1|[RFC 2616](http://go.microsoft.com/fwlink/?LinkId=90372)|  
|Associazione SOAP 1,1 HTTP|[Simple Object Access Protocol \(SOAP\) 1.1](http://go.microsoft.com/fwlink/?LinkId=90520), Section 7|  
|Associazione SOAP 1,2 HTTP|[SOAP Version 1.2 Part 2: Adjuncts \(Second Edition\)](http://go.microsoft.com/fwlink/?LinkId=95329), Section 7|  
  
 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> e <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> supportano le specifiche indicate nella tabella seguente.  
  
|Specifica\/documento|Collegamento|  
|--------------------------|------------------|  
|XML|[Extensible Markup Language \(XML\) 1.0 \(Fourth Edition\)](http://go.microsoft.com/fwlink/?LinkId=15139)|  
|SOAP 1,1|[Simple Object Access Protocol \(SOAP\) 1.1](http://go.microsoft.com/fwlink/?LinkId=96687)|  
|SOAP 1.2 Core|[SOAP Version 1.2 Part 1: Messaging Framework \(Second Edition\)](http://go.microsoft.com/fwlink/?LinkId=94664)|  
|WS\-Addressing 2004\/08|[Web Services Addressing \(WS\-Addressing\)](http://go.microsoft.com/fwlink/?LinkId=81239)|  
|W3C Web Services Addressing 1.0 \- Core|[Web Services Addressing 1.0 \- Core](http://go.microsoft.com/fwlink/?LinkId=96688)|  
|W3C Web Services Addressing 1.0 \- SOAP Binding|[Web Services Addressing 1.0 \- SOAP Binding](http://go.microsoft.com/fwlink/?LinkId=96689)|  
|W3C Web Services Addressing 1.0 \- WSDL Binding\*|[Web Services Addressing 1.0 \- WSDL Binding](http://go.microsoft.com/fwlink/?LinkId=96690)|  
|W3C Web Services Addressing 1.0 \- Metadata|[Web Services Addressing 1.0 \- Metadata](http://www.w3.org/TR/ws-addr-metadata/)|  
|WSDL SOAP1.1 Binding|[Web Services Description Language \(WSDL\) 1.1](http://go.microsoft.com/fwlink/?LinkId=96160)|  
|WSDL SOAP1.2 Binding|[WSDL 1.1 Binding Extension for SOAP 1.2](http://go.microsoft.com/fwlink/?LinkId=96691)|  
  
 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> supporta le specifiche indicate nella tabella seguente.  
  
|Specifica\/documento|Collegamento|  
|--------------------------|------------------|  
|XOP|[XML\-binary Optimized Packaging](http://go.microsoft.com/fwlink/?LinkId=96714)|  
|MTOM \+ SOAP1.2 Binding|[SOAP Message Transmission Optimization Mechanism](http://go.microsoft.com/fwlink/?LinkId=96713)|  
|MTOM SOAP 1.1 Binding|[SOAP 1.1 Binding for MTOM 1.0](http://go.microsoft.com/fwlink/?LinkId=96712)|  
|MTOM WS\-PolicyAssertions|Non ancora pubblicato.|  
  
 <xref:System.ServiceModel.Channels.SecurityBindingElement> supporta le specifiche indicate nella tabella seguente.  
  
|Specifica\/documento|Collegamento|  
|--------------------------|------------------|  
|WSS: SOAP Message Security 1,0|[Web Services Security: SOAP Message Security 1.0](http://go.microsoft.com/fwlink/?LinkId=94684)|  
|WSS: Username Token Profile 1.0|[Web Services Security UsernameToken Profile 1.0](http://go.microsoft.com/fwlink/?LinkId=95334)<br /><br /> richiedere Password\/@Type\=PasswordText \(impostazione predefinita\)|  
|WSS: X.509 Token Profile 1.0|[Web Services Security X.509 Certificate Token Profile](http://go.microsoft.com/fwlink/?LinkId=95335)|  
|WSS: SAML 1.1 Token Profile 1.0|[Web Services Security: SAML Token Profile](http://go.microsoft.com/fwlink/?LinkId=96693)|  
|WSS: SOAP Message Security 1.1|[Web Services Security: SOAP Message Security 1.1](http://go.microsoft.com/fwlink/?LinkId=91240)|  
|WSS Username Token Profile 1.1|[Web Services Security UsernameToken Profile 1.1](http://go.microsoft.com/fwlink/?LinkId=95331)<br /><br /> non implementare la funzionalità di derivazione della chiave basata su password;<br /><br /> richiedere Password\/@Type\=PasswordText \(impostazione predefinita\)|  
|WSS: X509 Token Profile 1.1|[Web Services Security X.509 Certificate Token Profile 1.1](http://go.microsoft.com/fwlink/?LinkId=95332)|  
|WSS: Kerberos Token Profile 1.1|[Web Services Security Kerberos Token Profile 1.1](http://go.microsoft.com/fwlink/?LinkId=95333)|  
|WSS: SAML 1.1 Token Profile 1.1|[Web Services Security SAML Token Profile 1.1](http://go.microsoft.com/fwlink/?LinkId=96694)|  
|WS\-Secure Conversation|[Web Services Secure Conversation Language](http://go.microsoft.com/fwlink/?LinkId=95317)|  
|WS\-Trust 1.4|[Web Services Trust Language](http://go.microsoft.com/fwlink/?LinkId=169514)|  
|WS\-SecurityPolicy 2005\/07|[Web Services Secure Conversation Language](http://go.microsoft.com/fwlink/?LinkId=95317)<br /><br /> Rettificato in base all'errata corrige inviato all'OASIS WS\-SX TC.<br /><br /> [ws\-sx message](http://go.microsoft.com/fwlink/?LinkId=96700)|  
|WS\-ReliableMessaging 1.1|[Protocollo Reliable Messaging versione 1.1](../../../../docs/framework/wcf/feature-details/reliable-messaging-protocol-version-1-1.md)|  
  
 <xref:System.ServiceModel.Channels.TransactionFlowBindingElement> supporta le specifiche indicate nella tabella seguente.  
  
|Specifica\/documento|Collegamento|  
|--------------------------|------------------|  
|WS\-Coordination|[Web Services Coordination](http://go.microsoft.com/fwlink/?LinkId=95324)|  
|WS\-AtomicTransaction|[Web Services Atomic Transaction](http://go.microsoft.com/fwlink/?LinkId=95323)|  
  
 Le classi <xref:System.ServiceModel.Description.MetadataExporter>, <xref:System.ServiceModel.Description.MetadataImporter>, <xref:System.ServiceModel.Description.WSDLExporter>, <xref:System.ServiceModel.Description.WSDLImporter> e <xref:System.ServiceModel.Description.MetadataResolver> forniscono il supporto per le specifiche di metadati seguenti:  
  
-   [XML Schema Part 1: Structures Second Edition](http://go.microsoft.com/fwlink/?LinkId=3536)  
  
-   [XML Schema Part 2: Datatypes Second Edition](http://go.microsoft.com/fwlink/?LinkId=40138)  
  
-   [WSDL 1.1](http://go.microsoft.com/fwlink/?LinkId=96160)  
  
-   [WS\-Policy 1.2](http://go.microsoft.com/fwlink/?LinkId=96705)  
  
-   [WS\-Policy 1.5](http://go.microsoft.com/fwlink/?LinkId=96706)  
  
-   [WS\-PolicyAttachment 1.2](http://go.microsoft.com/fwlink/?LinkId=96707)  
  
-   [WS\-MetadataExchange 1.1](http://go.microsoft.com/fwlink/?LinkId=94868)  
  
-   [WS\-Transfer Get for metadata retrieval](http://go.microsoft.com/fwlink/?LinkId=96708)  
  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono inoltre implementati i profili di interoperabilità elencati di seguito:  
  
-   [Basic Profile 1.1](http://go.microsoft.com/fwlink/?LinkId=69313)  
  
-   [Simple SOAP Binding 1.0](http://go.microsoft.com/fwlink/?LinkId=96710)  
  
-   [Basic Security Profile 1.0 Working Draft](http://go.microsoft.com/fwlink/?LinkId=96711)  
  
## Vedere anche  
 [Protocolli di servizi Web supportati da associazioni di interoperabilità fornite dal sistema](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)   
 [Protocolli di messaggistica](../../../../docs/framework/wcf/feature-details/messaging-protocols.md)   
 [Riferimento allo schema del contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)   
 [WSDL e criteri](../../../../docs/framework/wcf/feature-details/wsdl-and-policy.md)   
 [Protocolli di sicurezza](../../../../docs/framework/wcf/feature-details/security-protocols.md)   
 [Protocollo Reliable Messaging versione 1.0](../../../../docs/framework/wcf/feature-details/reliable-messaging-protocol-version-1-0.md)   
 [Protocollo Reliable Messaging versione 1.1](../../../../docs/framework/wcf/feature-details/reliable-messaging-protocol-version-1-1.md)   
 [Protocolli di transazione](../../../../docs/framework/wcf/feature-details/transaction-protocols.md)   
 [Protocollo di scambio del contesto](../../../../docs/framework/wcf/feature-details/context-exchange-protocol.md)