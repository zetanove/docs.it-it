---
title: "Procedura: creare un servizio token di sicurezza | Microsoft Docs"
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
  - "federazione"
  - "WCF, federazione"
ms.assetid: 98e82101-4cff-4bb8-a220-f7abed3556e5
caps.latest.revision: 12
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 12
---
# Procedura: creare un servizio token di sicurezza
Un servizio token di sicurezza implementa il protocollo definito nella specifica WS\-Trust.Questo protocollo definisce i formati e i modelli di scambio dei messaggi per il rilascio, il rinnovo, l'annullamento e la convalida di token di sicurezza.Un determinato servizio token di sicurezza fornisce una o più di queste funzionalità.In questo argomento viene descritto lo scenario più comune: l'implementazione del rilascio di token.  
  
## Rilascio di token  
 Per l'esecuzione del rilascio del token WS\-Trust definisce i formati dei messaggi in base all'elemento dello schema XSD \(XML Schema Definition Language\) di `RequestSecurityToken` e all'elemento dello schema XSD di `RequestSecurityTokenResponse`.Definisce inoltre gli URI \(Uniform Resource Identifiers\) dell'azione associati.L'URI dell'azione associato al messaggio `RequestSecurityToken` è http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/trust\/RST\/Issue.L'URI dell'azione associato al messaggio `RequestSecurityTokenResponse` è http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/trust\/RSTR\/Issue.  
  
### Struttura del messaggio di richiesta  
 In genere la struttura del messaggio di richiesta consiste negli elementi seguenti:  
  
-   Un URI del tipo di richiesta con valore http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/trust\/Issue.  
  
-   Un URI di tipo token.Per token SAML 1.1 il valore dell'URI è http:\/\/docs.oasis\-open.org\/wss\/oasis\-wss\-saml\-token\-profile\-1.1\#SAMLV1.1.  
  
-   Un valore della dimensione della chiave che indica il numero di bit nella chiave da associare al token rilasciato.  
  
-   Un URI di tipo chiave.Per le chiavi simmetriche, il valore di questo URI è http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/trust\/SymmetricKey.  
  
 Potrebbero inoltre essere presenti altri elementi:  
  
-   Materiale della chiave fornito dal client.  
  
-   Informazioni di ambito che indicano il servizio di destinazione con il quale verrà utilizzato il token rilasciato.  
  
 Il servizio token di sicurezza utilizza le informazioni contenute nel messaggio di richiesta di rilascio quando costruisce il messaggio di risposta del rilascio.  
  
## Struttura del messaggio di risposta  
 In genere la struttura del messaggio di risposta consiste negli elementi seguenti:  
  
-   Token di sicurezza rilasciato, ad esempio un'asserzione SAML 1.1.  
  
-   Token di prova associato al token di sicurezza.Per le chiavi simmetriche spesso si tratta della forma crittografata del materiale della chiave.  
  
-   Riferimenti al token di sicurezza rilasciato.In genere, il servizio token di sicurezza restituisce un riferimento che può essere utilizzato quando il token rilasciato ricorre in un messaggio successivo inviato dal client e un altro riferimento che può essere utilizzato quando il token non è presente nei messaggi successivi.  
  
 Potrebbero inoltre essere presenti altri elementi:  
  
-   Materiale della chiave fornito dal servizio token di sicurezza.  
  
-   Algoritmo necessario per calcolare la chiave condivisa.  
  
-   Informazioni sulla durata per il token rilasciato.  
  
## Elaborazione dei messaggi di richiesta  
 Il servizio token di sicurezza elabora la richiesta di rilascio esaminando i vari elementi del messaggio di richiesta e valutando la possibilità di rilasciare un token che soddisfi la richiesta.Il servizio token di sicurezza deve determinare quanto segue prima di costruire il token da rilasciare:  
  
-   La richiesta riguarda effettivamente il rilascio di un token.  
  
-   Il servizio token di sicurezza supporta il tipo di token richiesto.  
  
-   Il richiedente è autorizzato a eseguire la richiesta.  
  
-   Il servizio token di sicurezza può soddisfare le aspettative del richiedente in merito al materiale della chiave.  
  
 Due punti fondamentali nella costruzione di un token consistono nello stabilire la chiave con la quale firmare il token e la chiave con la quale crittografare la chiave condivisa.È necessario che il token venga firmato affinché, quando il client presenta il token al servizio di destinazione, quest'ultimo sia in grado di appurare che il token è stato rilasciato da un servizio token di sicurezza affidabile.Il materiale della chiave deve essere crittografato in modo tale da consentire al servizio di destinazione di decrittografarlo.  
  
 La firma di un'asserzione SAML implica la creazione di un'istanza <xref:System.IdentityModel.Tokens.SigningCredentials>.Il costruttore di questa classe accetta quanto segue:  
  
-   Un elemento <xref:System.IdentityModel.Tokens.SecurityKey> che la chiave utilizza per firmare l'asserzione SAML.  
  
-   Una stringa che identifica l'algoritmo della firma da utilizzare.  
  
-   Una stringa che identifica l'algoritmo di digest da utilizzare.  
  
-   Facoltativamente un elemento <xref:System.IdentityModel.Tokens.SecurityKeyIdentifier> che identifica la chiave da utilizzare per firmare l'asserzione.  
  
 [!code-csharp[c_CreateSTS#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#1)]
 [!code-vb[c_CreateSTS#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#1)]  
  
 La crittografia della chiave condivisa comporta la crittografia del materiale della chiave con una chiave che il servizio di destinazione può utilizzare per decrittografare la chiave condivisa.In genere viene utilizzata la chiave pubblica del servizio di destinazione.  
  
 [!code-csharp[c_CreateSTS#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#2)]
 [!code-vb[c_CreateSTS#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#2)]  
  
 È inoltre necessario un elemento <xref:System.IdentityModel.Tokens.SecurityKeyIdentifier> per la chiave crittografata.  
  
 [!code-csharp[c_CreateSTS#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#3)]
 [!code-vb[c_CreateSTS#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#3)]  
  
 L'oggetto <xref:System.IdentityModel.Tokens.SecurityKeyIdentifier> viene quindi utilizzato per creare `SamlSubject` come parte di `SamlToken`.  
  
 [!code-csharp[c_CreateSTS#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#4)]
 [!code-vb[c_CreateSTS#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#4)]  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Esempio di federazione](../../../../docs/framework/wcf/samples/federation-sample.md).  
  
## Creazione dei messaggi di risposta  
 Terminata l'elaborazione della richiesta di rilascio da parte del servizio token di sicurezza e conclusa la costruzione del token da rilasciare unitamente alla chiave di prova, è necessario costruire il messaggio di risposta, che deve comprendere almeno il token richiesto, il token di prova e i riferimenti del token rilasciato.Il token rilasciato è in genere un <xref:System.IdentityModel.Tokens.SamlSecurityToken> creato da <xref:System.IdentityModel.Tokens.SamlAssertion>, come illustrato nell'esempio seguente.  
  
 [!code-csharp[c_CreateSTS#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#5)]
 [!code-vb[c_CreateSTS#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#5)]  
  
 Nel caso in cui il servizio token di sicurezza fornisca il materiale della chiave condivisa, il token di prova viene costruito creando un elemento <xref:System.ServiceModel.Security.Tokens.BinarySecretSecurityToken>.  
  
 [!code-csharp[c_CreateSTS#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#6)]
 [!code-vb[c_CreateSTS#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#6)]  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] su come costruire il token di prova quando il client e il servizio token di sicurezza forniscono entrambi materiale per la chiave condivisa, vedere [Esempio di federazione](../../../../docs/framework/wcf/samples/federation-sample.md).  
  
 I riferimenti del token rilasciato sono costruiti creando istanze della classe <xref:System.IdentityModel.Tokens.SecurityKeyIdentifierClause>.  
  
 [!code-csharp[c_CreateSTS#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#7)]
 [!code-vb[c_CreateSTS#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#7)]  
  
 Tutti questi diversi valori vengono quindi serializzati nel messaggio di risposta restituito al client.  
  
## Esempio  
 Per il codice completo di un servizio token di sicurezza, vedere [Esempio di federazione](../../../../docs/framework/wcf/samples/federation-sample.md).  
  
## Vedere anche  
 <xref:System.IdentityModel.Tokens.SigningCredentials>   
 <xref:System.IdentityModel.Tokens.SecurityKey>   
 <xref:System.IdentityModel.Tokens.SecurityKeyIdentifier>   
 <xref:System.IdentityModel.Tokens.SamlSecurityToken>   
 <xref:System.IdentityModel.Tokens.SamlAssertion>   
 <xref:System.ServiceModel.Security.Tokens.BinarySecretSecurityToken>   
 <xref:System.IdentityModel.Tokens.SecurityKeyIdentifierClause>   
 [Esempio di federazione](../../../../docs/framework/wcf/samples/federation-sample.md)