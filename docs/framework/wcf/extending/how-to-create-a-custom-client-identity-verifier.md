---
title: "Procedura: creare un verificatore di identit&#224; client personalizzato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f2d34e43-fa8b-46d2-91cf-d2960e13e16b
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Procedura: creare un verificatore di identit&#224; client personalizzato
La funzionalità *identità* di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] consente a un client di specificare in anticipo l'identità prevista del servizio.  Ogni volta che un server esegue l'autenticazione al client, l'identità viene confrontata con l'identità prevista.  Per una descrizione dell'identità e del relativo funzionamento, vedere [Identità del servizio e autenticazione](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md).  
  
 Se necessario, la verifica può essere personalizzata usando un verificatore di identità personalizzato.  È possibile, ad esempio, eseguire ulteriori controlli di verifica dell'identità del servizio.  In questo esempio il verificatore di identità personalizzato verifica le attestazioni aggiuntive nel certificato X.509 restituito dal server.  Per un'applicazione di esempio, vedere [Esempio identità del servizio](../../../../docs/framework/wcf/samples/service-identity-sample.md).  
  
### Per estendere la classe EndpointIdentity  
  
1.  Definire una nuova classe che deriva dalla classe <xref:System.ServiceModel.EndpointIdentity>.  Questo esempio attribuisce un nome all'estensione `OrgEndpointIdentity`.  
  
2.  Aggiungere membri privati insieme a proprietà che verranno usate dalla classe <xref:System.ServiceModel.Security.IdentityVerifier> estesa per eseguire il controllo dell'identità rispetto alle attestazioni incluse nel token di sicurezza restituito dal servizio.  Questo esempio definisce una proprietà, ovvero `OrganizationClaim`.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#6)]
     [!code-vb[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#6)]  
  
### Per estendere la classe IdentityVerifier  
  
1.  Definire una nuova classe che deriva dall'interfaccia <xref:System.ServiceModel.Security.IdentityVerifier>.  Questo esempio attribuisce un nome all'estensione `CustomIdentityVerifier`.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#7)]
     [!code-vb[c_HowToSetCustomClientIdentity#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#7)]  
  
2.  Eseguire l'override del metodo <xref:System.ServiceModel.Security.IdentityVerifier.CheckAccess%2A>.  Il metodo determina se il controllo dell'identità ha esito positivo o negativo.  
  
3.  Il metodo `CheckAccess` ha due parametri.  Il primo è un'istanza della classe <xref:System.ServiceModel.EndpointIdentity>.  Il secondo è un'istanza della classe <xref:System.IdentityModel.Policy.AuthorizationContext>.  
  
     Nell'implementazione del metodo, esaminare la raccolta di attestazioni restituita dalla proprietà <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> della classe <xref:System.IdentityModel.Policy.AuthorizationContext> ed eseguire i controlli di autenticazione necessari.  Questo esempio inizia cercando qualsiasi attestazione di tipo "Nome distinto" e confronta quindi il nome all'estensione della classe <xref:System.ServiceModel.EndpointIdentity> \(`OrgEndpointIdentity`\).  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#1)]
     [!code-vb[c_HowToSetCustomClientIdentity#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#1)]  
  
### Per implementare il metodo TryGetIdentity  
  
1.  Implementare il metodo <xref:System.ServiceModel.Security.IdentityVerifier.TryGetIdentity%2A> che determina se un'istanza della classe <xref:System.ServiceModel.EndpointIdentity> può essere restituita dal client.  L'infrastruttura di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] chiama prima l'implementazione del metodo `TryGetIdentity` per recuperare l'identità del servizio dal messaggio.  L'infrastruttura chiama quindi l'implementazione `CheckAccess` con le classi `EndpointIdentity` e <xref:System.IdentityModel.Policy.AuthorizationContext> restituite.  
  
2.  Nel metodo `TryGetIdentity` inserire il seguente codice:  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#2)]
     [!code-vb[c_HowToSetCustomClientIdentity#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#2)]  
  
### Per implementare un'associazione personalizzata e impostare il verificatore di identità personalizzato  
  
1.  Creare un metodo che restituisca un oggetto <xref:System.ServiceModel.Channels.Binding>.  Questo esempio inizia con la creazione di un'istanza della classe <xref:System.ServiceModel.WSHttpBinding> e imposta la propria modalità di sicurezza su <xref:System.ServiceModel.SecurityMode>e la propria proprietà <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> su <xref:System.ServiceModel.MessageCredentialType>.  
  
2.  Creare una classe <xref:System.ServiceModel.Channels.BindingElementCollection> usando il metodo <xref:System.ServiceModel.WSHttpBinding.CreateBindingElements%2A>.  
  
3.  Restituire la classe <xref:System.ServiceModel.Channels.SecurityBindingElement> dalla raccolta ed eseguirne il cast su una variabile <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>.  
  
4.  Imposta la proprietà <xref:System.ServiceModel.Channels.LocalClientSecuritySettings.IdentityVerifier%2A> della classe <xref:System.ServiceModel.Channels.LocalClientSecuritySettings> su una nuova istanza della classe `CustomIdentityVerifier` creata precedentemente.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#3)]
     [!code-vb[c_HowToSetCustomClientIdentity#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#3)]  
  
5.  L'associazione personalizzata restituita viene usata per creare un'istanza del client e della classe.  Il client può eseguire quindi un controllo di verifica dell'identità del servizio personalizzato, come illustrato nel codice seguente.  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#4)]
     [!code-vb[c_HowToSetCustomClientIdentity#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#4)]  
  
## Esempio  
 Nell'esempio seguente viene illustrata un'implementazione completa della classe <xref:System.ServiceModel.Security.IdentityVerifier>.  
  
 [!code-csharp[c_HowToSetCustomClientIdentity#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#5)]
 [!code-vb[c_HowToSetCustomClientIdentity#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#5)]  
  
## Esempio  
 Nell'esempio seguente viene illustrata un'implementazione completa della classe <xref:System.ServiceModel.EndpointIdentity>.  
  
 [!code-csharp[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#6)]
 [!code-vb[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#6)]  
  
## Vedere anche  
 <xref:System.ServiceModel.ServiceAuthorizationManager>   
 <xref:System.ServiceModel.EndpointIdentity>   
 <xref:System.ServiceModel.Security.IdentityVerifier>   
 [Esempio identità del servizio](../../../../docs/framework/wcf/samples/service-identity-sample.md)   
 [Criteri di autorizzazione](../../../../docs/framework/wcf/samples/authorization-policy.md)   
 [Criteri di autorizzazione](../../../../docs/framework/wcf/samples/authorization-policy.md)