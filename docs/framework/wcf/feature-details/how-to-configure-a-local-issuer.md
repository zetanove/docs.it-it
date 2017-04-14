---
title: "Procedura: configurare un emittente locale | Microsoft Docs"
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
ms.assetid: 15263371-514e-4ea6-90fb-14b4939154cd
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Procedura: configurare un emittente locale
In questo argomento viene illustrato come configurare un client per utilizzare un emittente locale per i token emessi.  
  
 Spesso, quando un client comunica con un servizio federato, il servizio specifica l'indirizzo del servizio token di sicurezza previsto per l'emissione del token che il client utilizzerà per autenticarsi presso il servizio federato.In alcune situazioni, è possibile configurare il client per utilizzare un *emittente locale*.  
  
 In [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene utilizzato un emittente locale quando l'indirizzo dell'emittente di un'associazione federata è http:\/\/schemas.microsoft.com\/2005\/12\/ServiceModel\/Addressing\/Anonymous o `null`.In tali casi, è necessario configurare la classe <xref:System.ServiceModel.Description.ClientCredentials> con l'indirizzo dell'emittente locale e con l'associazione da utilizzare per comunicare con tale emittente.  
  
> [!NOTE]
>  Se la proprietà <xref:System.ServiceModel.Description.ClientCredentials.SupportInteractive%2A> della classe `ClientCredentials` è impostata su `true`, l'indirizzo dell'emittente locale non viene specificato e l'indirizzo dell'emittente specificato dall'[\<wsFederationHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md) o da un'altra associazione federata è http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/issuer\/self, http:\/\/schemas.microsoft.com\/2005\/12\/ServiceModel\/Addressing\/Anonymous o è `null`, viene utilizzato l'emittente [!INCLUDE[infocard](../../../../includes/infocard-md.md)] di Windows.  
  
### Per configurare l'emittente locale nel codice  
  
1.  Creare una variabile di tipo <xref:System.ServiceModel.Security.IssuedTokenClientCredential>.  
  
2.  Impostare la variabile sull'istanza restituita dalla proprietà <xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A> della classe `ClientCredentials`.L'istanza viene restituita dalla proprietà <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> del client \(ereditata da <xref:System.ServiceModel.ClientBase%601>\) o dalla proprietà <xref:System.ServiceModel.ChannelFactory.Credentials%2A> della classe <xref:System.ServiceModel.ChannelFactory>:  
  
     [!code-csharp[c_CreateSTS#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#9)]
     [!code-vb[c_CreateSTS#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#9)]  
  
3.  Impostare la proprietà <xref:System.ServiceModel.Security.IssuedTokenClientCredential.LocalIssuerAddress%2A> su una nuova istanza di <xref:System.ServiceModel.EndpointAddress>, con l'indirizzo dell'emittente locale come argomento per il costruttore.  
  
     [!code-csharp[c_CreateSTS#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#10)]
     [!code-vb[c_CreateSTS#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#10)]  
  
     In alternativa, creare una nuova istanza <xref:System.Uri> come argomento per il costruttore.  
  
     [!code-csharp[c_CreateSTS#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#11)]
     [!code-vb[c_CreateSTS#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#11)]  
  
     Il parametro `addressHeaders` è una matrice di istanze di <xref:System.ServiceModel.Channels.AddressHeader>, come illustrato.  
  
     [!code-csharp[c_CreateSTS#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#12)]
     [!code-vb[c_CreateSTS#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#12)]  
  
4.  Impostare l'associazione per l'emittente locale utilizzando la proprietà <xref:System.ServiceModel.Security.IssuedTokenClientCredential.LocalIssuerBinding%2A>.  
  
     [!code-csharp[c_CreateSTS#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#13)]
     [!code-vb[c_CreateSTS#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#13)]  
  
5.  Facoltativo.Aggiungere i comportamenti dell'endpoint configurati per l'emittente locale aggiungendo tali comportamenti alla raccolta restituita dalla proprietà <xref:System.ServiceModel.Security.IssuedTokenClientCredential.LocalIssuerChannelBehaviors%2A>.  
  
     [!code-csharp[c_CreateSTS#14](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#14)]
     [!code-vb[c_CreateSTS#14](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#14)]  
  
### Per configurare l'emittente locale nella configurazione  
  
1.  Creare un elemento [\<emittenteLocale\>](../../../../docs/framework/configure-apps/file-schema/wcf/localissuer.md)[\<tokenEmesso\>](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtoken.md)[\<credenzialiClient\>](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md), che è a sua volta figlio dell'elemento  in un comportamento dell'endpoint.  
  
2.  Impostare l'attributo `address` sull'indirizzo dell'emittente locale che accetterà richieste del token.  
  
3.  Impostare gli attributi `binding` e `bindingConfiguration` su valori che fanno riferimento all'associazione appropriata da utilizzare durante la comunicazione con l'endpoint dell'emittente locale.  
  
4.  Facoltativo.Impostare l'elemento [\<identità\>](../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)\< `come figlio dell'elemento localIssuer`\> e specificare le informazioni di identità per l'emittente locale.  
  
5.  Facoltativo.Impostare l'elemento [\<intestazioni\>](../../../../docs/framework/configure-apps/file-schema/wcf/headers.md)\< `come figlio dell'elemento localIssuer`\> e specificare le intestazioni aggiuntive necessarie per indirizzare correttamente l'emittente locale.  
  
## Sicurezza di .NET Framework  
 Si noti che, se per una determinata associazione vengono specificati l'indirizzo dell'emittente e l'associazione, l'emittente locale non verrà utilizzato per gli endpoint che utilizzano tale associazione.Per i client che prevedono di utilizzare sempre l'emittente locale, è necessario accertarsi di non utilizzare tale associazione o di modificare l'associazione in modo che l'indirizzo dell'emittente sia `null`.  
  
## Vedere anche  
 [Procedura: configurare le credenziali in un servizio federativo](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)   
 [Procedura: creare un client federato](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)   
 [Procedura: creare una classe WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)