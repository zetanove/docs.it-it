---
title: "Procedura: utilizzare certificati X.509 separati per la firma e la crittografia | Microsoft Docs"
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
  - "classe ClientCredentials"
  - "Classe ClientCredentialsSecurityTokenManager"
  - "WCF, extensibility"
ms.assetid: 0b06ce4e-7835-4d82-8baf-d525c71a0e49
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Procedura: utilizzare certificati X.509 separati per la firma e la crittografia
In questo argomento viene illustrato come configurare [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per utilizzare certificati diversi per la firma e la crittografia dei messaggi sul client e nel servizio.  
  
 Per consentire l'utilizzo di certificati separati per la firma e la crittografia, è necessario creare credenziali personalizzate del client o del servizio \(o di entrambi\) poiché in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non viene fornita alcuna API per impostare più certificati client o del servizio.È inoltre necessario specificare un gestore del token di sicurezza per utilizzare le informazioni di più certificati e creare un provider di token di sicurezza appropriato per l'utilizzo della chiave specificata e la direzione del messaggio.  
  
 Nel diagramma seguente vengono illustrate le principali classi utilizzate, le classi da cui ereditano \(contrassegnate da una freccia rivolta verso l'alto\) e i tipi restituiti di alcuni metodi e proprietà.  
  
-   `MyClientCredentials` è un'implementazione personalizzata di <xref:System.ServiceModel.Description.ClientCredentials>.  
  
    -   Tutte le relative proprietà illustrate nel diagramma restituiscono istanze di <xref:System.Security.Cryptography.X509Certificates.X509Certificate2>.  
  
    -   Il metodo <xref:System.ServiceModel.Description.ClientCredentials.CreateSecurityTokenManager%2A> restituisce un'istanza di `MyClientCredentialsSecurityTokenManager`.  
  
-   `MyClientCredentialsSecurityTokenManager` è un'implementazione personalizzata di <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager>.  
  
    -   Il relativo metodo <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager.CreateSecurityTokenProvider%2A> restituisce un'istanza di <xref:System.IdentityModel.Selectors.X509SecurityTokenProvider>.  
  
 ![Grafico indicante l'uso delle credenziali client](../../../../docs/framework/wcf/extending/media/e4971edd-a59f-4571-b36f-7e6b2f0d610f.gif "e4971edd\-a59f\-4571\-b36f\-7e6b2f0d610f")  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sulle credenziali personalizzate, vedere [Procedura: creare credenziali client e del servizio personalizzate](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md).  
  
 Inoltre, è necessario creare un sistema di verifica dell'identità personalizzato e collegarlo a un elemento di associazione di sicurezza in un'associazione personalizzata.È inoltre necessario utilizzare le credenziali personalizzate anziché quelle predefinite.  
  
 Nel diagramma seguente vengono illustrate le classi coinvolte nell'associazione personalizzata e il modo in cui viene collegato il sistema di verifica dell'identità personalizzato.I diversi elementi di associazione coinvolti ereditano tutti da <xref:System.ServiceModel.Channels.BindingElement>.<xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> dispone della proprietà <xref:System.ServiceModel.Channels.LocalClientSecuritySettings> che restituisce un'istanza di <xref:System.ServiceModel.Security.IdentityVerifier>, da cui viene personalizzato `MyIdentityVerifier`.  
  
 ![Grafico con un elemento di associazione personalizzato](../../../../docs/framework/wcf/extending/media/dddea4a2-0bb4-4921-9bf4-20d4d82c3da5.gif "dddea4a2\-0bb4\-4921\-9bf4\-20d4d82c3da5")  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sulla creazione di un sistema di verifica dell'identità personalizzato, vedere [Procedura: creare un verificatore di identità client personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-custom-client-identity-verifier.md).  
  
### Per utilizzare certificati separati per la firma e la crittografia  
  
1.  Definire una nuova classe di credenziali client che eredita dalla classe <xref:System.ServiceModel.Description.ClientCredentials>.Implementare quattro nuove proprietà per consentire di specificare più certificati: `ClientSigningCertificate`, `ClientEncryptingCertificate`, `ServiceSigningCertificate` e `ServiceEncryptingCertificate`.Eseguire inoltre l'override del metodo <xref:System.ServiceModel.Description.ClientCredentials.CreateSecurityTokenManager%2A> per restituire un'istanza della classe <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> personalizzata definita nel passaggio successivo.  
  
     [!code-csharp[c_FourCerts#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#1)]
     [!code-vb[c_FourCerts#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#1)]  
  
2.  Definire un nuovo gestore del token di sicurezza che eredita dalla classe <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager>.Eseguire l'override del metodo <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager.CreateSecurityTokenProvider%2A> per creare un provider di token di sicurezza appropriato.Il parametro `requirement` \(<xref:System.IdentityModel.Selectors.SecurityTokenRequirement>\) specifica la direzione del messaggio e l'utilizzo della chiave.  
  
     [!code-csharp[c_FourCerts#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#2)]
     [!code-vb[c_FourCerts#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#2)]  
  
3.  Definire una nuova classe di credenziali del servizio che eredita dalla classe <xref:System.ServiceModel.Description.ServiceCredentials>.Implementare quattro nuove proprietà per consentire di specificare più certificati: `ClientSigningCertificate`, `ClientEncryptingCertificate`, `ServiceSigningCertificate` e `ServiceEncryptingCertificate`.Eseguire inoltre l'override del metodo <xref:System.ServiceModel.Description.ServiceCredentials.CreateSecurityTokenManager%2A> per restituire un'istanza della classe <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager> personalizzata definita nel passaggio successivo.  
  
     [!code-csharp[c_FourCerts#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#3)]
     [!code-vb[c_FourCerts#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#3)]  
  
4.  Definire un nuovo gestore del token di sicurezza del servizio che eredita dalla classe <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager>.Eseguire l'override del metodo <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager.CreateSecurityTokenProvider%2A> per creare un provider di token di sicurezza appropriato per la direzione del messaggio passato e l'utilizzo della chiave.  
  
     [!code-csharp[c_FourCerts#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#4)]
     [!code-vb[c_FourCerts#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#4)]  
  
### Per utilizzare più certificati sul client  
  
1.  Creare un'associazione personalizzata.È necessario che l'elemento di associazione di sicurezza operi in modalità duplex per consentire ai provider di token di sicurezza diversi di essere presenti per le richieste e le risposte.A questo scopo, è possibile aggiungere un trasporto con funzionalità duplex o utilizzare la classe <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement> come illustrato nel codice seguente.Collegare l'oggetto <xref:System.ServiceModel.Security.IdentityVerifier> personalizzato definito nel passaggio successivo all'elemento di associazione di sicurezza.Sostituire le credenziali client predefinite con le credenziali client personalizzate create precedentemente.  
  
     [!code-csharp[c_FourCerts#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#5)]
     [!code-vb[c_FourCerts#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#5)]  
  
2.  Definire un oggetto <xref:System.ServiceModel.Security.IdentityVerifier> personalizzato.Il servizio possiede più identità poiché vengono utilizzati certificati diversi per crittografare la richiesta e firmare la risposta.  
  
    > [!NOTE]
    >  Nell'esempio seguente, il verificatore di identità personalizzato non esegue alcun controllo di identità dell'endpoint a scopo dimostrativo.Non è tuttavia una pratica consigliabile per il codice di produzione.  
  
     [!code-csharp[c_FourCerts#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#6)]
     [!code-vb[c_FourCerts#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#6)]  
  
### Per utilizzare più certificati nel servizio  
  
1.  Creare un'associazione personalizzata.È necessario che l'elemento di associazione di sicurezza operi in modalità duplex per consentire ai provider di token di sicurezza diversi di essere presenti per le richieste e le risposte.Come per il lato client, utilizzare un trasporto con funzionalità duplex o la classe <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement> come illustrato nel codice seguente.Sostituire le credenziali del servizio predefinite con quelle personalizzate create precedentemente.  
  
     [!code-csharp[c_FourCerts#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#7)]
     [!code-vb[c_FourCerts#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#7)]  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Description.ServiceCredentials>   
 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager>   
 <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager>   
 <xref:System.ServiceModel.Security.IdentityVerifier>   
 [Procedura: creare credenziali client e del servizio personalizzate](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md)