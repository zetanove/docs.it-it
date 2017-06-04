---
title: "Combinazione di protocolli trust in scenari federati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d7b5fee9-2246-4b09-b8d7-9e63cb817279
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# Combinazione di protocolli trust in scenari federati
In alcuni scenari i client federati comunicano con un servizio e con un servizio token di sicurezza che non hanno la stessa versione Trust.  Il WSDL del servizio può contenere un'asserzione `RequestSecurityTokenTemplate` con elementi WS\-Trust di versioni diverse rispetto al servizio token di sicurezza.  In tali casi, un client [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] converte gli elementi WS\-Trust ricevuti da `RequestSecurityTokenTemplate` affinché corrispondano alla versione Trust del servizio token di sicurezza.  In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] le versioni Trust non corrispondenti vengono gestite solo per le associazioni standard.  Tutti i parametri dell'algoritmo standard riconosciuti da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fanno parte del binding standard.  In questo argomento viene descritto il comportamento di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] con le varie impostazioni di trust tra il servizio e il servizio token di sicurezza.  
  
## Componente febbraio 2005 e servizio token di sicurezza febbraio 2005  
 Il WSDL per il componente contiene gli elementi seguenti all'interno della sezione `RequestSecurityTokenTemplate`:  
  
-   `CanonicalizationAlgorithm`  
  
-   `EncryptionAlgorithm`  
  
-   `EncryptWith`  
  
-   `SignWith`  
  
-   `KeySize`  
  
-   `KeyType`  
  
 Il file di configurazione client contiene un elenco di parametri.  
  
 Poiché [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non è in grado di distinguere i parametri del client da quelli del servizio e viceversa, li aggiunge tutti e li invia in `RequestSecurityTokenTemplate` \(RST\).  
  
## Componente Trust 1.3 e servizio token di sicurezza Trust 1.3  
 Il WSDL per il componente contiene gli elementi seguenti all'interno della sezione `RequestSecurityTokenTemplate`:  
  
-   `CanonicalizationAlgorithm`  
  
-   `EncryptionAlgorithm`  
  
-   `EncryptWith`  
  
-   `SignWith`  
  
-   `KeySize`  
  
-   `KeyType`  
  
-   `KeyWrapAlgorithm`  
  
 Il file di configurazione client contiene un elemento `secondaryParameters` che esegue il wrapping dei parametri specificati dal componente.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] rimuove gli elementi `EncryptionAlgorithm`, `CanonicalizationAlgorithm` e `KeyWrapAlgorithm` dall'elemento di primo livello sotto RST se sono presenti nell'elemento `SecondaryParameters`.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] aggiunge l'elemento `SecondaryParameters` al token RST non modificato in uscita.  
  
## Componente Trust febbraio 2005 e servizio token di sicurezza Trust 1.3  
 Il WSDL per il componente contiene i seguenti elementi nella sezione `RequestSecurityTokenTemplate`:  
  
-   `CanonicalizationAlgorithm`  
  
-   `EncryptionAlgorithm`  
  
-   `EncryptWith`  
  
-   `SignWith`  
  
-   `KeySize`  
  
-   `KeyType`  
  
 Il file di configurazione client contiene un elenco di parametri.  
  
 Dal file di configurazione client, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non è in grado di distinguere i parametri del servizio da quelli del client.  Di conseguenza [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] converte tutti i parametri in uno spazio dei nomi della versione Trust 1.3.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] gestisce gli elementi `KeyType`, `KeySize` e `TokenType` nel modo seguente:  
  
-   Scaricare il WSDL, creare il binding e assegnare `KeyType`, `KeySize` e `TokenType` dai parametri del componente.  Viene quindi generato il file di configurazione client.  
  
-   Il client è ora in grado di modificare qualsiasi parametro nel file di configurazione.  
  
-   In fase di esecuzione, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] copia tutti i parametri specificati nella sezione `AdditionalTokenParameters` del file di configurazione client eccetto `KeyType`, `KeySize` e `TokenType`, poiché tali parametri vengono gestiti durante la generazione del file di configurazione.  
  
## Componente Trust 1.3 e servizio token di sicurezza Trust febbraio 2005  
 Il WSDL per il componente contiene i seguenti elementi nella sezione `RequestSecurityTokenTemplate`:  
  
-   `CanonicalizationAlgorithm`  
  
-   `EncryptionAlgorithm`  
  
-   `EncryptWith`  
  
-   `SignWith`  
  
-   `KeySize`  
  
-   `KeyType`  
  
-   `KeyWrapAlgorithm`  
  
 Il file di configurazione client contiene un elemento `secondaryParamters` che esegue il wrapping dei parametri specificati dal componente.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] copia tutti i parametri specificati all'interno della sezione `SecondaryParameters` nell'elemento RST di primo livello, ma non li converte nello spazio dei nomi WS\-Trust 2005.