---
title: "Procedura: creare credenziali client e del servizio personalizzate | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2b5ba5c3-0c6c-48e9-9e46-54acaec443ba
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Procedura: creare credenziali client e del servizio personalizzate
In questo argomento viene illustrato come implementare credenziali client e del servizio personalizzate e come utilizzare credenziali personalizzate dal codice dell'applicazione.  
  
## Classi di estensibilità delle credenziali  
 Le classi <xref:System.ServiceModel.Description.ClientCredentials> e <xref:System.ServiceModel.Description.ServiceCredentials> sono i punti di ingresso principali all'estensibilità della sicurezza [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Queste classi delle credenziali forniscono le API che consentono al codice dell'applicazione di impostare le informazioni sulle credenziali e convertire i tipi di credenziali in token di sicurezza.\(*token di sicurezza* sono la forma utilizzata per trasmettere le informazioni sulle credenziali all'interno di messaggi SOAP\). Le responsabilità di queste classi di credenziali possono essere divise in due aree:  
  
-   Fornire le API affinché le applicazioni impostino le informazioni sulle credenziali.  
  
-   Fungere da factory per le implementazioni <xref:System.IdentityModel.Selectors.SecurityTokenManager>.  
  
 Entrambe le classi <xref:System.ServiceModel.Description.ClientCredentials> e <xref:System.ServiceModel.Description.ServiceCredentials> ereditano dalla classe astratta <xref:System.ServiceModel.Security.SecurityCredentialsManager> che definisce il contratto per la restituzione di <xref:System.IdentityModel.Selectors.SecurityTokenManager>.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] classi di credenziali e relativo ruolo sull'architettura della sicurezza in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Security Architecture](http://msdn.microsoft.com/it-it/16593476-d36a-408d-808c-ae6fd483e28f).  
  
 Le implementazioni predefinite fornite in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supportano i tipi di credenziali forniti dal sistema e creano un gestore del token di sicurezza in grado di gestire quei tipi di credenziali.  
  
## Motivi di personalizzazione  
 Esistono più motivi per personalizzare classi di credenziali client o del servizio.È necessario innanzitutto modificare il comportamento della sicurezza predefinito di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in merito alla gestione dei tipi di credenziali forniti dal sistema, in particolare per le ragioni seguenti:  
  
-   Necessità di modifiche che non sono possibili utilizzando altri punti di estensibilità.  
  
-   Aggiunta di nuovi tipi di credenziali.  
  
-   Aggiunta di nuovi tipi di token di sicurezza personalizzati.  
  
 In questo argomento viene illustrato come implementare credenziali client e del servizio personalizzate e come utilizzarle dal codice dell'applicazione.  
  
## Primo passaggio  
 La creazione di una classe di credenziali personalizzate è solo il primo passaggio, perché la ragione della personalizzazione è modificare il comportamento di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in merito al provisioning delle credenziali, alla serializzazione del token di sicurezza o all'autenticazione.Negli altri argomenti di questa sezione viene descritto come creare serializzatori e autenticatori personalizzati.In questo caso, la creazione di una classe di credenziali personalizzate è il primo tema dei passaggi.Le azioni successive \(creazione di serializzatori e autenticatori personalizzati\) possono essere eseguite solo dopo avere creato credenziali personalizzate.Gli argomenti aggiuntivi basati su questo argomento includono:  
  
-   [Procedura: creare un provider di token di sicurezza personalizzati](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-provider.md)  
  
-   [Procedura: creare un autenticatore del token di sicurezza personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-authenticator.md)  
  
-   [Procedura: creare un token personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-custom-token.md).  
  
## Procedure  
  
#### Per implementare le credenziali client personalizzate  
  
1.  Definire una nuova classe derivata dalla classe <xref:System.ServiceModel.Description.ClientCredentials>.  
  
2.  Facoltativo.Aggiungere nuovi metodi o proprietà per nuovi tipi di credenziali.Se non vengono aggiunti nuovi tipi di credenziali, ignorare questo passaggio.Nell'esempio seguente viene aggiunta una proprietà `CreditCardNumber`.  
  
3.  Eseguire l'override del metodo <xref:System.ServiceModel.Security.SecurityCredentialsManager.CreateSecurityTokenManager%2A>.Questo metodo viene chiamato automaticamente dall'infrastruttura di sicurezza [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] quando viene utilizzata la credenziale client personalizzata.Questo metodo è responsabile della creazione e della restituzione di un'istanza di un'implementazione della classe <xref:System.IdentityModel.Selectors.SecurityTokenManager>.  
  
    > [!IMPORTANT]
    >  È importante da notare che l'override del metodo <xref:System.ServiceModel.Security.SecurityCredentialsManager.CreateSecurityTokenManager%2A> viene eseguito per creare un gestore del token di sicurezza personalizzato.Il gestore del token di sicurezza, derivato da <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> deve restituire un provider del token di sicurezza personalizzato, derivato da <xref:System.IdentityModel.Selectors.SecurityTokenProvider>, per creare il token di sicurezza effettivo.Se non si segue questo modello per creare token di sicurezza, l'applicazione potrebbe funzionare in modo non corretto quando gli oggetti <xref:System.ServiceModel.ChannelFactory> vengono memorizzati nella cache \(comportamento predefinito dei proxy client WCF\), provocando un potenziale attacco di tipo elevazione dei privilegi.L'oggetto credenziale personalizzata viene memorizzato nella cache come parte dell'oggetto <xref:System.ServiceModel.ChannelFactory>.L'oggetto <xref:System.IdentityModel.Selectors.SecurityTokenManager> personalizzato viene creato tuttavia a ogni chiamata in modo da limitare la minaccia alla sicurezza se la logica di creazione del token è presente nell'oggetto <xref:System.IdentityModel.Selectors.SecurityTokenManager>.  
  
4.  Eseguire l'override del metodo <xref:System.ServiceModel.Description.ClientCredentials.CloneCore%2A>.  
  
     [!code-csharp[c_CustomCredentials#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#1)]
     [!code-vb[c_CustomCredentials#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/client/client.vb#1)]  
  
#### Per implementare un gestore del token di sicurezza client personalizzato  
  
1.  Definire una nuova classe derivata da <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager>.  
  
2.  Facoltativo.Eseguire l'override del metodo <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenProvider%28System.IdentityModel.Selectors.SecurityTokenRequirement%29>, se è necessario creare un'implementazione <xref:System.IdentityModel.Selectors.SecurityTokenProvider> personalizzata.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sui provider di token di sicurezza personalizzati, vedere [Procedura: creare un provider di token di sicurezza personalizzati](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-provider.md).  
  
3.  Facoltativo.Eseguire l'override del metodo <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenAuthenticator%28System.IdentityModel.Selectors.SecurityTokenRequirement%2CSystem.IdentityModel.Selectors.SecurityTokenResolver%40%29>, se è necessario creare un'implementazione <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator> personalizzata.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] autenticatori di token di sicurezza personalizzati, vedere [Procedura: creare un autenticatore del token di sicurezza personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-authenticator.md).  
  
4.  Facoltativo.Eseguire l'override del metodo <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenSerializer%2A>, se è necessario creare un oggetto <xref:System.IdentityModel.Selectors.SecurityTokenSerializer> personalizzato.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] token di sicurezza personalizzati e serializzatori del token di sicurezza personalizzati, vedere [Procedura: creare un token personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-custom-token.md).  
  
     [!code-csharp[c_CustomCredentials#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#2)]
     [!code-vb[c_CustomCredentials#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/client/client.vb#2)]  
  
#### Per utilizzare credenziali client personalizzate dal codice dell'applicazione  
  
1.  Creare un'istanza del client generato che rappresenta l'interfaccia del servizio oppure creare un'istanza di <xref:System.ServiceModel.ChannelFactory> che punta a un servizio con il quale si desidera comunicare.  
  
2.  Rimuovere il comportamento delle credenziali client fornite dal sistema dalla raccolta <xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A>, alla quale è possibile accedere tramite la proprietà <xref:System.ServiceModel.ChannelFactory.Endpoint%2A>.  
  
3.  Creare una nuova istanza di una classe di credenziali client personalizzate e aggiungerla alla raccolta <xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A>, alla quale è possibile accedere tramite la proprietà <xref:System.ServiceModel.ChannelFactory.Endpoint%2A>.  
  
     [!code-csharp[c_CustomCredentials#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#3)]
     [!code-vb[c_CustomCredentials#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/client/client.vb#3)]  
  
 Nella procedura precedente viene illustrato come utilizzare credenziali client dal codice dell'applicazione.Le credenziali [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] possono essere configurate anche utilizzando il file di configurazione dell'applicazione.Spesso è preferibile utilizzare la configurazione dell'applicazione anziché la specifica a livello di codice, perché consente di modificare i parametri dell'applicazione senza dovere modificare l'origine, ricompilare e ridistribuire.  
  
 Nella prossima procedura viene illustrato come fornire supporto per la configurazione di credenziali personalizzate.  
  
#### Creazione di un gestore di configurazione per credenziali client personalizzate  
  
1.  Definire una nuova classe derivata da <xref:System.ServiceModel.Configuration.ClientCredentialsElement>.  
  
2.  Facoltativo.Aggiungere proprietà per tutti i parametri di configurazione aggiuntivi che si desidera esporre tramite la configurazione dell'applicazione.Nell'esempio seguente viene aggiunta una proprietà denominata `CreditCardNumber`.  
  
3.  Eseguire l'override della proprietà <xref:System.ServiceModel.Configuration.BehaviorExtensionElement.BehaviorType%2A> per restituire il tipo di classe di credenziali client personalizzate creata con l'elemento di configurazione.  
  
4.  Eseguire l'override del metodo <xref:System.ServiceModel.Configuration.BehaviorExtensionElement.CreateBehavior%2A>.Il metodo è responsabile della creazione e restituzione di un'istanza della classe di credenziali personalizzati basata sulle impostazioni caricate dal file di configurazione.Chiamare il metodo <xref:System.ServiceModel.Configuration.ClientCredentialsElement.ApplyConfiguration%28System.ServiceModel.Description.ClientCredentials%29> di base da questo metodo per recuperare le impostazioni delle credenziali fornite dal sistema caricate nell'istanza delle credenziali client personalizzate.  
  
5.  Facoltativo.Se nel passaggio 2 sono state aggiunte altre proprietà, è necessario eseguire l'override della proprietà <xref:System.Configuration.ConfigurationElement.Properties%2A> per registrare le impostazioni di configurazione aggiuntive affinché il framework di configurazione le riconosca.Combinare le proprietà con le proprietà della classe di base per consentire la configurazione delle impostazioni fornite dal sistema tramite questo elemento di configurazione delle credenziali client personalizzate.  
  
     [!code-csharp[c_CustomCredentials#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#7)]
     [!code-vb[c_CustomCredentials#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/service/service.vb#7)]  
  
 Quando disponibile, la classe del gestore di configurazione può essere integrata nel framework di configurazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Ciò consente di utilizzare le credenziali client personalizzate negli elementi di comportamento dell'endpoint client, come illustrato nella procedura seguente.  
  
#### Per registrare e utilizzare un gestore di configurazione di credenziali client personalizzate nella configurazione dell'applicazione  
  
1.  Aggiungere un elemento \<`extensions`\> e un elemento \<`behaviorExtensions`\> al file di configurazione.  
  
2.  Aggiungere un elemento \<`add`\> all'elemento \<`behaviorExtensions`\> e impostare l'attributo `name` su un valore appropriato.  
  
3.  Impostare l'attributo `type` sul nome del tipo completo.Includere inoltre il nome e altri attributi dell'assembly.  
  
    ```  
    <system.serviceModel>  
      <extensions>  
        <behaviorExtensions>  
          <add name="myClientCredentials" type="Microsoft.ServiceModel.Samples.MyClientCredentialsConfigHandler, CustomCredentials, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
        </behaviorExtensions>  
      </extensions>  
    <system.serviceModel>  
    ```  
  
4.  Dopo aver registrato il gestore di configurazione, nello stesso file di configurazione è possibile utilizzare l'elemento delle credenziali personalizzate anziché l'elemento \<`clientCredentials`\> fornito dal sistema.È possibile utilizzare sia le proprietà fornite dal sistema che qualsiasi nuova proprietà aggiunta all'implementazione del gestore di configurazione.Nell'esempio seguente viene impostato il valore di una proprietà personalizzata utilizzando l'attributo `creditCardNumber`.  
  
    ```  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="myClientCredentialsBehavior">  
          <myClientCredentials creditCardNumber="123-123-123"/>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    ```  
  
#### Per implementare credenziali del servizio personalizzate  
  
1.  Definire una nuova classe derivata da <xref:System.ServiceModel.Description.ServiceCredentials>.  
  
2.  Facoltativo.Aggiungere nuove proprietà per fornire API per i nuovi valori delle credenziali che vengono aggiunte.Se non vengono aggiunti nuovi valori delle credenziali, ignorare questo passaggio.Nell'esempio seguente viene aggiunta una proprietà `AdditionalCertificate`.  
  
3.  Eseguire l'override del metodo <xref:System.ServiceModel.Security.SecurityCredentialsManager.CreateSecurityTokenManager%2A>.Questo metodo viene chiamato automaticamente dall'infrastruttura [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] quando viene utilizzata la credenziale client personalizzata.Il metodo è responsabile della creazione e della restituzione di un'istanza di un'implementazione della classe <xref:System.IdentityModel.Selectors.SecurityTokenManager>, descritta nella procedura seguente.  
  
4.  Facoltativo.Eseguire l'override del metodo <xref:System.ServiceModel.Description.ServiceCredentials.CloneCore%2A>.È richiesto solo se si aggiungono nuove proprietà o campi interni all'implementazione delle credenziali client personalizzate.  
  
     [!code-csharp[c_CustomCredentials#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#4)]
     [!code-vb[c_CustomCredentials#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/service/service.vb#4)]  
  
#### Per implementare un gestore del token di sicurezza del servizio personalizzato  
  
1.  Definire una nuova classe derivata dalla classe <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager>.  
  
2.  Facoltativo.Eseguire l'override del metodo <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenProvider%2A>, se è necessario creare un'implementazione <xref:System.IdentityModel.Selectors.SecurityTokenProvider> personalizzata.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sui provider di token di sicurezza personalizzati, vedere [Procedura: creare un provider di token di sicurezza personalizzati](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-provider.md).  
  
3.  Facoltativo.Eseguire l'override del metodo <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenAuthenticator%2A>, se è necessario creare un'implementazione <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator> personalizzata.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] autenticatori di token di sicurezza personalizzati, vedere l'argomento [Procedura: creare un autenticatore del token di sicurezza personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-authenticator.md).  
  
4.  Facoltativo.Eseguire l'override del metodo <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenSerializer%28System.IdentityModel.Selectors.SecurityTokenVersion%29>, se è necessario creare un oggetto <xref:System.IdentityModel.Selectors.SecurityTokenSerializer> personalizzato.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] token di sicurezza personalizzati e serializzatori del token di sicurezza personalizzati, vedere [Procedura: creare un token personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-custom-token.md).  
  
     [!code-csharp[c_CustomCredentials#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#5)]
     [!code-vb[c_CustomCredentials#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/service/service.vb#5)]  
  
#### Per utilizzare credenziali del servizio personalizzate dal codice dell'applicazione  
  
1.  Creare un'istanza di <xref:System.ServiceModel.ServiceHost>.  
  
2.  Rimuovere il comportamento delle credenziali del servizio fornite dal sistema dalla raccolta <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A>.  
  
3.  Creare una nuova istanza della classe di credenziali del servizio personalizzate e aggiungerla alla raccolta <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A>.  
  
     [!code-csharp[c_CustomCredentials#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcredentials/cs/source.cs#6)]
     [!code-vb[c_CustomCredentials#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcredentials/vb/service/service.vb#6)]  
  
 Aggiungere il supporto per la configurazione utilizzando i passaggi descritti in precedenza nelle procedure "`To create a configuration handler for custom client credentials`" e "`To register and use a custom client credentials configuration handler in the application configuration`." L'unica differenza è nell'utilizzo della classe <xref:System.ServiceModel.Configuration.ServiceCredentialsElement> invece che della classe <xref:System.ServiceModel.Configuration.ClientCredentialsElement> come classe base per il gestore della configurazione.L'elemento credenziale personalizzata del servizio può quindi essere utilizzato ovunque sia utilizzato l'elemento `<serviceCredentials>` fornito dal sistema.  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Description.ServiceCredentials>   
 <xref:System.ServiceModel.Security.SecurityCredentialsManager>   
 <xref:System.IdentityModel.Selectors.SecurityTokenManager>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement>   
 <xref:System.ServiceModel.Configuration.ServiceCredentialsElement>   
 [Procedura: creare un provider di token di sicurezza personalizzati](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-provider.md)   
 [Procedura: creare un autenticatore del token di sicurezza personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-authenticator.md)   
 [Procedura: creare un token personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-custom-token.md)