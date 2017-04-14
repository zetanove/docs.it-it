---
title: "Procedura: creare un autenticatore del token di sicurezza personalizzato | Microsoft Docs"
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
  - "WCF, autenticazione"
ms.assetid: 10e245f7-d31e-42e7-82a2-d5780325d372
caps.latest.revision: 12
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 12
---
# Procedura: creare un autenticatore del token di sicurezza personalizzato
In questo argomento viene illustrato come creare un autenticatore del token di sicurezza personalizzato e come integrarlo con un gestore del token di sicurezza personalizzato.Un autenticatore del token di sicurezza codi sicurezzantenuto di un token di sicurezza fornito con un messaggio in ingresso.Se la convalida ha esito positivo, l'autenticatore restituisce una raccolta di istanze <xref:System.IdentityModel.Policy.IAuthorizationPolicy> che, quando valutata, restituisce un set di attestazioni.  
  
 Per utilizzare un autenticatore del token di sicurezza personalizzato in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], è necessario creare prima credenziali personalizzate e implementazioni del gestore del token di sicurezza.Per ulteriori informazioni sulla creazione di credenziali personalizzate e di un gestore del token di sicurezza, vedere [Procedura: creare credenziali client e del servizio personalizzate](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md).Per ulteriori informazioni sulle credenziali, sul gestore del token di sicurezza e sulle classi del provider e dell'autenticatore, vedere [Security Architecture](http://msdn.microsoft.com/it-it/16593476-d36a-408d-808c-ae6fd483e28f).  
  
## Procedure  
  
#### Per creare un autenticatore del token di sicurezza personalizzato  
  
1.  Definire una nuova classe derivata dalla classe <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator>.  
  
2.  Eseguire l'override del metodo <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator.CanValidateTokenCore%2A>.Il metodo restituisce `true` o `false` a seconda che l'autenticatore personalizzato possa convalidare o meno il tipo di token in ingresso.  
  
3.  Eseguire l'override del metodo <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator.ValidateTokenCore%2A>.Questo metodo deve convalidare in modo appropriato il contenuto del token.Se il token supera la fase di convalida, restituisce una raccolta di istanze <xref:System.IdentityModel.Policy.IAuthorizationPolicy>.Nell'esempio seguente viene utilizzata un'implementazione di criteri di autorizzazione personalizzata che verrà creata nella procedura successiva.  
  
     [!code-csharp[C_CustomTokenAuthenticator#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenauthenticator/cs/source.cs#1)]
     [!code-vb[C_CustomTokenAuthenticator#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenauthenticator/vb/source.vb#1)]  
  
 Il codice precedente restituisce una raccolta di criteri di autorizzazione nel metodo <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator.CanValidateToken%28System.IdentityModel.Tokens.SecurityToken%29>.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non fornisce un'implementazione pubblica di questa interfaccia.Nella procedura seguente viene illustrato come eseguire l'operazione in base ai propri requisiti.  
  
#### Per creare un criterio di autorizzazione personalizzato  
  
1.  Definire una nuova classe che implementa l'interfaccia <xref:System.IdentityModel.Policy.IAuthorizationPolicy>.  
  
2.  Implementare la proprietà di sola lettura <xref:System.IdentityModel.Policy.IAuthorizationComponent.Id%2A>.Un sistema per implementare questa proprietà consiste nel generare un identificatore univoco globale \(GUID, Globally Unique Identifier\) nel costruttore della classe e restituirlo ogni volta che viene richiesto il valore per questa proprietà.  
  
3.  Implementare la proprietà di sola lettura <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Issuer%2A>.Questa proprietà deve restituire un emittente dei set di attestazioni ottenuti dal token.Tale emittente deve corrispondere all'emittente del token o a un'autorità responsabile della convalida del contenuto del token.Nell'esempio seguente viene utilizzata l'attestazione dell'emittente passata alla classe dall'autenticatore del token di sicurezza personalizzato creato nella procedura precedente.L'autenticatore del token di sicurezza personalizzato utilizza il set di attestazioni fornito dal sistema \(restituito dalla proprietà <xref:System.IdentityModel.Claims.ClaimSet.System%2A>\) per rappresentare l'emittente del token nome utente.  
  
4.  Implementare il metodo <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A>.Questo metodo compila un'istanza della classe <xref:System.IdentityModel.Policy.EvaluationContext> \(passata come argomento\) con attestazioni basate sul contenuto del token di sicurezza in ingresso.Il metodo restituisce `true` al termine della valutazione.Nei casi in cui l'implementazione si basa sulla presenza di altri criteri di autorizzazione che forniscono informazioni aggiuntive al contesto di valutazione, questo metodo può restituire `false` se le informazioni necessarie non sono ancora presenti nel contesto di valutazione.In tal caso, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] chiamerà nuovamente il metodo dopo la valutazione di tutti gli altri criteri di autorizzazione generati per il messaggio in ingresso se almeno uno di tali criteri di autorizzazione ha modificato il contesto di valutazione.  
  
     [!code-csharp[c_CustomTokenAuthenticator#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenauthenticator/cs/source.cs#2)]
     [!code-vb[c_CustomTokenAuthenticator#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenauthenticator/vb/source.vb#2)]  
  
 In [Procedura: creare credenziali client e del servizio personalizzate](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md) viene illustrato come creare credenziali personalizzate e un gestore del token di sicurezza personalizzato.Per utilizzare l'autenticatore del token di sicurezza personalizzato qui creato, viene modificata un'implementazione del gestore del token di sicurezza per restituire l'autenticatore personalizzato dal metodo <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenAuthenticator%2A>.Il metodo restituisce un autenticatore quando viene passato un requisito di token di sicurezza appropriato.  
  
#### Per integrare un autenticatore del token di sicurezza personalizzato con un gestore del token di sicurezza personalizzato  
  
1.  Eseguire l'override del metodo <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenAuthenticator%2A> nell'implementazione del gestore del token di sicurezza personalizzato.  
  
2.  Aggiungere logica al metodo per consentire la restituzione dell'autenticatore del token di sicurezza personalizzato in base al parametro <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>.Nell'esempio seguente viene restituito un autenticatore del token di sicurezza personalizzato se il tipo di token dei requisiti di token è un nome utente \(rappresentato dalla proprietà <xref:System.IdentityModel.Tokens.SecurityTokenTypes.UserName%2A>\) e la direzione del messaggio per cui viene richiesto l'autenticatore del token di sicurezza è di input \(rappresentata dal campo <xref:System.ServiceModel.Description.MessageDirection>\).  
  
     [!code-csharp[c_CustomTokenAuthenticator#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenauthenticator/cs/source.cs#3)]
     [!code-vb[c_CustomTokenAuthenticator#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenauthenticator/vb/source.vb#3)]  
  
## Vedere anche  
 <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator>   
 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>   
 <xref:System.IdentityModel.Selectors.SecurityTokenManager>   
 <xref:System.IdentityModel.Tokens.UserNameSecurityToken>   
 [Procedura: creare credenziali client e del servizio personalizzate](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md)   
 [Procedura: creare un provider di token di sicurezza personalizzati](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-provider.md)   
 [Security Architecture](http://msdn.microsoft.com/it-it/16593476-d36a-408d-808c-ae6fd483e28f)