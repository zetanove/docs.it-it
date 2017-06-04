---
title: "Procedura: utilizzare un validator di nome utente e password personalizzato | Microsoft Docs"
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
  - "WCF, nome utente e password"
ms.assetid: 8e08b74b-fa44-4018-b63d-0d0805f85e3f
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Procedura: utilizzare un validator di nome utente e password personalizzato
Per impostazione predefinita, quando per l'autenticazione vengono utilizzati un nome utente e una password, in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene utilizzato Windows per convalidarli.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], tuttavia, consente l'utilizzo di schemi personalizzati di autenticazione di nome utente e password, noti come *validator*.Per incorporare un validator personalizzato di nome utente e password, creare una classe che deriva da <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> e configurarla.  
  
 Per un'applicazione di esempio, vedere [Validator del nome utente e password](../../../../docs/framework/wcf/samples/user-name-password-validator.md).  
  
### Per creare un validator di nome utente e password personalizzato  
  
1.  Creare una classe che deriva da <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>.  
  
     [!code-csharp[C_CustomUsernameAndPasswordValidator#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#3)]
     [!code-vb[C_CustomUsernameAndPasswordValidator#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#3)]  
  
2.  Implementare lo schema di autenticazione personalizzato eseguendo l'override del metodo <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A>.  
  
     Non utilizzare il codice contenuto nell'esempio seguente, che esegue l'override del metodo <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A>, in un ambiente di produzione.Sostituire il codice con lo schema di convalida di nome utente e password personalizzato, operazione che potrebbe comportare il recupero di coppie di nome utente e password da un database.  
  
     Affinché gli errori di autenticazione vengano restituiti al client, generare una classe <xref:System.ServiceModel.FaultException> nel metodo <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A>.  
  
     [!code-csharp[C_CustomUsernameAndPasswordValidator#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#4)]
     [!code-vb[C_CustomUsernameAndPasswordValidator#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#4)]  
  
### Per configurare un servizio per l'utilizzo di un validator di nome utente e password personalizzato  
  
1.  Configurare un'associazione che utilizza meccanismi di sicurezza a livello di messaggio su qualsiasi trasporto o meccanismi di sicurezza a livello di trasporto su HTTP\(S\).  
  
     Quando si utilizza la modalità di sicurezza dei messaggi, aggiungere uno dei binding forniti dal sistema, ad esempio un elemento [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) o [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) che supporta la modalità di sicurezza dei messaggi e il tipo di credenziale `UserName`.  
  
     Quando si utilizza la modalità di sicurezza a livello di trasporto su HTTP\(S\), aggiungere l'elemento [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md), [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md), [\<netTcpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md) o [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) in cui vengono utilizzati il protocollo HTTP\(S\) e lo schema di autenticazione `Basic`.  
  
    > [!NOTE]
    >  Quando si utilizza [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] o versioni successive, è possibile utilizzare un validator di nome utente e password personalizzato con modalità di sicurezza dei messaggi e del trasporto.Quando si utilizza [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)], un validator di nome utente e password personalizzato può essere utilizzato solo con la modalità di sicurezza dei messaggi.  
  
    > [!TIP]
    >  Per ulteriori informazioni sull'utilizzo di \<netTcpBinding\> in questo contesto, vedere [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md)  
  
    1.  Aggiungere un elemento [\<associazioni\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) al file di configurazione, sotto l'elemento [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md).  
  
    2.  Aggiungere un elemento [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) o [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md) alla sezione delle associazioni.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sulla creazione di un elemento di associazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Procedura: specificare un'associazione al servizio in configurazione](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md).  
  
    3.  Impostare l'attributo `mode` dell'elemento [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md) o [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md) su `Message`, `Transport` o `TransportWithMessageCredential`.  
  
    4.  Impostare l'attributo `clientCredentialType` dell'elemento [\<messaggio\>](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md) o [\<transport\>](../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-wshttpbinding.md).  
  
         Quando si utilizza la modalità di sicurezza dei messaggi, impostare l'attributo `clientCredentialType` dell'elemento [\<messaggio\>](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md) su `UserName`.  
  
         Quando si utilizza la modalità di sicurezza a livello di trasporto su HTTP\(S\), impostare l'attributo `clientCredentialType` dell'elemento [\<transport\>](../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-wshttpbinding.md) o [\<transport\>](../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-basichttpbinding.md) su `Basic`.  
  
        > [!NOTE]
        >  Quando un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è ospitato in Internet Information Services \(IIS\) utilizzando la protezione a livello di trasporto e la proprietà <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.UserNamePasswordValidationMode%2A> è impostata su <xref:System.ServiceModel.Security.UserNamePasswordValidationMode>, lo schema di autenticazione personalizzato utilizza un sottoinsieme dell'autenticazione di Windows.Questo avviene perché in tale scenario, IIS esegue l'autenticazione di Windows prima di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiamando l'autenticatore personalizzato.  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sulla creazione di un elemento di associazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Procedura: specificare un'associazione al servizio in configurazione](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md).  
  
     Nell'esempio seguente viene illustrato il codice di configurazione per l'associazione.  
  
    ```  
    <system.serviceModel>   
      <bindings>  
      <wsHttpBinding>  
          <binding name="Binding1">  
            <security mode="Message">  
              <message clientCredentialType="UserName" />  
            </security>  
          </binding>          
        </wsHttpBinding>  
      </bindings>  
    </system.serviceModel>  
    ```  
  
2.  Configurare un comportamento che specifica che un validator personalizzato di nome utente e password viene utilizzato per convalidare coppie di nome utente e password per i token di sicurezza <xref:System.IdentityModel.Tokens.UserNameSecurityToken> in arrivo.  
  
    1.  Aggiungere un elemento [\<comportamenti\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) come figlio dell'elemento [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md).  
  
    2.  Aggiungere una sezione [\<comportamentiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md) all'elemento [\<comportamenti\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md).  
  
    3.  Aggiungere un elemento [\<comportamento\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md)`name e impostare l'attributo`  su un valore appropriato.  
  
    4.  Aggiungere una sezione [\<credenzialiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)[\<comportamento\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) all'elemento .  
  
    5.  Aggiungere un [\<autenticazioneNomeUtente\>](../../../../docs/framework/configure-apps/file-schema/wcf/usernameauthentication.md) all'[\<credenzialiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md).  
  
    6.  Impostare `userNamePasswordValidationMode` su `Custom`.  
  
        > [!IMPORTANT]
        >  Se il valore `userNamePasswordValidationMode` non è impostato, in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene utilizzata l'autenticazione Windows anziché il validator personalizzato di nome utente e password.  
  
    7.  Impostare `customUserNamePasswordValidatorType` sul tipo che rappresenta il validator personalizzato di nome utente e password.  
  
     Nell'esempio seguente viene illustrato il frammento `<serviceCredentials>` fino a questo punto.  
  
    ```  
    <serviceCredentials>  
      <userNameAuthentication userNamePasswordValidationMode="Custom" customUserNamePasswordValidatorType="Microsoft.ServiceModel.Samples.CalculatorService.CustomUserNameValidator, service" />  
    </serviceCredentials>  
    ```  
  
## Esempio  
 Nel codice di esempio seguente viene dimostrato come creare un validator personalizzato di nome utente e password.Non utilizzare il codice che esegue l'override del metodo <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> in un ambiente di produzione.Sostituire il codice con lo schema di convalida di nome utente e password personalizzato, operazione che potrebbe comportare il recupero di coppie di nome utente e password da un database.  
  
 [!code-csharp[C_CustomUsernameAndPasswordValidator#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#1)]
 [!code-vb[C_CustomUsernameAndPasswordValidator#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#1)]  
[!code-csharp[C_CustomUsernameAndPasswordValidator#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#2)]
[!code-vb[C_CustomUsernameAndPasswordValidator#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#2)]  
  
## Vedere anche  
 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>   
 [Procedura: utilizzare provider di appartenenza ASP.NET](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md)   
 [Autenticazione](../../../../docs/framework/wcf/feature-details/authentication-in-wcf.md)