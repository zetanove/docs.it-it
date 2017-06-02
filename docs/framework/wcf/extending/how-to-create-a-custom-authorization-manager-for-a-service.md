---
title: "Procedura: creare un gestore autorizzazioni personalizzato per un servizio | Microsoft Docs"
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
  - "Classe OperationRequirement"
  - "Windows Communication Foundation, estensione"
ms.assetid: 6214afde-44c1-4bf5-ba07-5ad6493620ea
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Procedura: creare un gestore autorizzazioni personalizzato per un servizio
L'infrastruttura dei modelli di identità di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] supporta un modello di autorizzazione basato su attestazioni estensibili.Le attestazioni vengono estratte dai token, elaborate facoltativamente da criteri di autorizzazione personalizzati e quindi inserite in una classe <xref:System.IdentityModel.Policy.AuthorizationContext>.Un gestore autorizzazioni esamina le attestazioni contenute nel contesto <xref:System.IdentityModel.Policy.AuthorizationContext> per prendere decisioni di autorizzazione.  
  
 Per impostazione predefinita, le decisioni di autorizzazione sono prese dalla classe <xref:System.ServiceModel.ServiceAuthorizationManager>. È tuttavia possibile creare un gestore autorizzazioni personalizzato per eseguire l'override di queste decisioni.Per creare un gestore autorizzazioni personalizzato, creare una classe che deriva da <xref:System.ServiceModel.ServiceAuthorizationManager> e che implementa il metodo <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A>.Le decisioni di autorizzazione sono prese tramite il metodo <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> che restituisce `true` quando l'accesso è concesso e `false` quando l'accesso è negato.  
  
 Se la decisione di autorizzazione dipende dal contenuto del corpo del messaggio, utilizzare il metodo <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccess%2A>.  
  
 A causa di problemi riguardanti le prestazioni, è consigliabile ridisegnare l'applicazione, se possibile, in modo tale che per la decisione di autorizzazione non sia necessario l'accesso al corpo del messaggio.  
  
 La registrazione del gestore autorizzazioni personalizzato per un servizio può essere eseguita in codice o in configurazione.  
  
### Per creare un gestore autorizzazioni personalizzato  
  
1.  Derivare una classe dalla classe <xref:System.ServiceModel.ServiceAuthorizationManager>.  
  
     [!code-csharp[c_CustomAuthMgr#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthmgr/cs/c_customauthmgr.cs#5)]
     [!code-vb[c_CustomAuthMgr#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthmgr/vb/c_customauthmgr.vb#5)]  
  
2.  Eseguire l'override del metodo <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%28System.ServiceModel.OperationContext%29>.  
  
     Utilizzare il contesto <xref:System.ServiceModel.OperationContext> passato al metodo <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%28System.ServiceModel.OperationContext%29> per prendere decisioni di autorizzazione.  
  
     Nell'esempio di codice seguente il metodo <xref:System.IdentityModel.Claims.ClaimSet.FindClaims%28System.String%2CSystem.String%29> viene utilizzato per individuare l'attestazione personalizzata `http://www.contoso.com/claims/allowedoperation` allo scopo di prendere una decisione di autorizzazione.  
  
     [!code-csharp[c_CustomAuthMgr#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthmgr/cs/c_customauthmgr.cs#6)]
     [!code-vb[c_CustomAuthMgr#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthmgr/vb/c_customauthmgr.vb#6)]  
  
### Per registrare un gestore autorizzazioni personalizzato in codice  
  
1.  Creare un'istanza del gestore autorizzazioni personalizzato e assegnarla alla proprietà <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ServiceAuthorizationManager%2A>.  
  
     Per accedere al comportamento <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> è possibile utilizzare la proprietà <xref:System.ServiceModel.ServiceHostBase.Authorization%2A>.  
  
     Nell'esempio di codice seguente viene illustrato come registrare il gestore autorizzazioni personalizzato `MyServiceAuthorizationManager`.  
  
     [!code-csharp[c_CustomAuthMgr#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthmgr/cs/c_customauthmgr.cs#4)]
     [!code-vb[c_CustomAuthMgr#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthmgr/vb/c_customauthmgr.vb#4)]  
  
### Per registrare un gestore autorizzazioni personalizzato in configurazione  
  
1.  Aprire il file di configurazione del servizio.  
  
2.  Aggiungere un [\<autorizzazioneServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md) all'[\<comportamenti\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md).  
  
     Aggiungere un attributo `serviceAuthorizationManagerType` all'[\<autorizzazioneServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md) e quindi impostare il valore di tale attributo sul tipo che rappresenta il gestore autorizzazioni personalizzato.  
  
3.  Aggiungere un'associazione in grado di proteggere la comunicazione tra client e servizio.  
  
     L'associazione scelta per questa comunicazione determina le attestazioni aggiunte al contesto <xref:System.IdentityModel.Policy.AuthorizationContext> utilizzate dal gestore autorizzazioni personalizzato per prendere le decisioni di autorizzazione.Per ulteriori dettagli sulle associazioni fornite dal sistema, vedere [Associazioni fornite dal sistema](../../../../docs/framework/wcf/system-provided-bindings.md).  
  
4.  Associare il comportamento a un endpoint di servizio aggiungendo un elemento [\<service\>](../../../../docs/framework/configure-apps/file-schema/wcf/service.md)`behaviorConfiguration e quindi impostare il valore dell'attributo` [\<comportamento\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md).  
  
     Per ulteriori informazioni sulla configurazione di un endpoint di servizio, vedere [Procedura: creare un endpoint di servizio nella configurazione](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md).  
  
     Nell'esempio di codice seguente viene illustrato come registrare il gestore autorizzazioni personalizzato `Samples.MyServiceAuthorizationManager`.  
  
    ```  
    <configuration>  
      <system.serviceModel>  
        <services>  
          <service   
              name="Microsoft.ServiceModel.Samples.CalculatorService"  
              behaviorConfiguration="CalculatorServiceBehavior">  
            <host>  
              <baseAddresses>  
                <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
              </baseAddresses>  
            </host>  
            <endpoint address=""  
                      binding="wsHttpBinding_Calculator"  
                      contract="Microsoft.ServiceModel.Samples.ICalculator" />  
          </service>  
        </services>  
        <bindings>  
          <WSHttpBinding>  
           <binding name = "wsHttpBinding_Calculator">  
             <security mode="Message">  
               <message clientCredentialType="Windows"/>  
             </security>  
            </binding>  
          </WSHttpBinding>  
    </bindings>  
        <behaviors>  
          <serviceBehaviors>  
            <behavior name="CalculatorServiceBehavior">  
              <serviceAuthorization serviceAuthorizationManagerType="Samples.MyServiceAuthorizationManager,MyAssembly" />  
             </behavior>  
         </serviceBehaviors>  
       </behaviors>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
    > [!WARNING]
    >  Si noti che quando si specifica l'oggetto serviceAuthorizationManagerType, la stringa deve contenere il nome di tipo completo,una virgola e il nome dell'assembly in cui il tipo è definito.Se si omette il nome dell'assembly, WCF tenterà di caricare il tipo da System.ServiceModel.dll.  
  
## Esempio  
 Nell'esempio di codice seguente viene descritta un'implementazione di base di una classe <xref:System.ServiceModel.ServiceAuthorizationManager> che prevede l'override del metodo <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A>.Nell'esempio di codice viene eseguita una ricerca all'interno del contesto <xref:System.IdentityModel.Policy.AuthorizationContext> allo scopo di individuare un'attestazione personalizzata e quindi viene restituito `true` quando la risorsa relativa a tale attestazione personalizzata corrisponde al valore di azione indicato nel contesto <xref:System.ServiceModel.OperationContext>.Per un'implementazione più completa di una classe <xref:System.ServiceModel.ServiceAuthorizationManager>, vedere [Criteri di autorizzazione](../../../../docs/framework/wcf/samples/authorization-policy.md).  
  
 [!code-csharp[c_CustomAuthMgr#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthmgr/cs/c_customauthmgr.cs#2)]
 [!code-vb[c_CustomAuthMgr#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthmgr/vb/c_customauthmgr.vb#2)]  
  
## Vedere anche  
 <xref:System.ServiceModel.ServiceAuthorizationManager>   
 [Criteri di autorizzazione](../../../../docs/framework/wcf/samples/authorization-policy.md)   
 [Criteri di autorizzazione](../../../../docs/framework/wcf/samples/authorization-policy.md)