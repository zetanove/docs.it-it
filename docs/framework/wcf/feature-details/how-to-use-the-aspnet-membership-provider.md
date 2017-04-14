---
title: "Procedura: utilizzare provider di appartenenza ASP.NET | Microsoft Docs"
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
  - "WCF e ASP.NET"
  - "WCF, autorizzazione"
  - "WCF, sicurezza"
ms.assetid: 322c56e0-938f-4f19-a981-7b6530045b90
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Procedura: utilizzare provider di appartenenza ASP.NET
Il provider di appartenenza [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] è una funzionalità che consente agli sviluppatori di [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] di creare siti Web che consentono agli utenti di creare combinazioni di nome utente e password univoche.Con questa funzionalità qualsiasi utente può stabilire un account nel sito e accedere in modo esclusivo al sito e ai relativi servizi.Si tratta di una funzionalità in contrasto con la sicurezza di Windows, in base alla quale è necessario che gli utenti dispongano di un account in un dominio Windows.Qualsiasi utente che fornisca le credenziali \(ovvero nome utente e password\) può utilizzare il sito e i relativi servizi.  
  
 Per un'applicazione di esempio, vedere [Provider di appartenenza e di ruoli](../../../../docs/framework/wcf/samples/membership-and-role-provider.md).Per ulteriori informazioni sull'utilizzo della funzionalità provider di ruoli [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], vedere [Procedura: utilizzare il provider di ruoli ASP.NET con un servizio](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md).  
  
 La funzionalità di appartenenza richiede l'utilizzo di un database SQL Server per archiviare le informazioni utente.La funzionalità include anche metodi per presentare una domanda agli utenti che hanno dimenticato la password.  
  
 Gli sviluppatori [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] possono sfruttare queste funzionalità a fini di sicurezza.In caso di integrazione in un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], gli utenti devono fornire una combinazione di nome utente e password all'applicazione client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Per trasferire i dati al servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], utilizzare un'associazione che supporta credenziali di nome utente\/password, ad esempio <xref:System.ServiceModel.WSHttpBinding> \(nella configurazione, [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)\) e impostare il tipo di credenziale client su `UserName`.Nel servizio, la sicurezza [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] autentica l'utente sulla base del nome utente e della password, inoltre assegna il ruolo specificato dal ruolo [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  
  
> [!NOTE]
>  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non fornisce metodi per popolare il database con combinazioni di nome utente\/password o altre informazioni utente.  
  
### Per configurare il provider di appartenenza  
  
1.  Nel file Web.config, sotto l'elemento \<`system.web`\> creare un elemento \<`membership`\>.  
  
2.  Sotto l'elemento `<membership>`, creare un elemento `<providers>`.  
  
3.  Come figlio dell'elemento \<`providers`\>, aggiungere un elemento `<clear />` per scaricare la raccolta di provider.  
  
4.  Sotto l'elemento `<clear />`\<`, creare un elemento add`\>`name con gli attributi seguenti impostati sui valori appropriati:` `type,` `connectionStringName,` `applicationName,` `enablePasswordRetrieval,` `enablePasswordReset,` `requiresQuestionAndAnswer,` `requiresUniqueEmail,` `passwordFormat e` .L'attributo `name` viene utilizzato in seguito come valore nel file di configurazione.Nell'esempio seguente viene impostato su `SqlMembershipProvider`.  
  
     Nell'esempio che segue viene illustrata la sezione di configurazione.  
  
    ```xml  
    <!-- Configure the Sql Membership Provider -->  
    <membership defaultProvider="SqlMembershipProvider" userIsOnlineTimeWindow="15">  
      <providers>  
        <clear />  
          <add   
            name="SqlMembershipProvider"   
            type="System.Web.Security.SqlMembershipProvider"   
            connectionStringName="SqlConn"  
            applicationName="MembershipAndRoleProviderSample"  
            enablePasswordRetrieval="false"  
            enablePasswordReset="false"  
            requiresQuestionAndAnswer="false"  
            requiresUniqueEmail="true"  
            passwordFormat="Hashed" />  
      </providers>  
    </membership>  
    ```  
  
### Per configurare la protezione del servizio per accettare la combinazione di nome utente\/password  
  
1.  Aggiungere un elemento [\<associazioni\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) al file di configurazione, sotto l'elemento [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md).  
  
2.  Aggiungere un [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) alla sezione delle associazioni.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sulla creazione di un elemento di associazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Procedura: specificare un'associazione al servizio in configurazione](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md).  
  
3.  Impostare l'attributo `mode` dell'elemento `<security>``Message su` .  
  
4.  Impostare l'attributo `clientCredentialType` dell'elemento \<`message`\> su `UserName`.Viene in questo modo specificato che un nome utente e una password saranno utilizzati come credenziale del client.  
  
     Nell'esempio seguente viene illustrato il codice di configurazione per l'associazione.  
  
    ```xml  
    <system.serviceModel>  
    <bindings>  
      <wsHttpBinding>  
      <!-- Set up a binding that uses UserName as the client credential type -->  
        <binding name="MembershipBinding">  
          <security mode ="Message">  
            <message clientCredentialType ="UserName"/>  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    </system.serviceModel>  
    ```  
  
### Per configurare un servizio affinché utilizzi il provider di appartenenza  
  
1.  Aggiungere un elemento [\<comportamenti\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) come figlio dell'elemento `<system.serviceModel>`  
  
2.  Aggiungere una sezione [\<comportamentiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md) all'elemento \<`behaviors`\>.  
  
3.  Aggiungere un elemento [\<comportamento\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) e impostare l'attributo `name` su un valore appropriato.  
  
4.  Aggiungere [\<credenzialiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)\<`behavior all'elemento` \>.  
  
5.  Aggiungere [\<autenticazioneNomeUtente\>](../../../../docs/framework/configure-apps/file-schema/wcf/usernameauthentication.md) all'elemento `<serviceCredentials>`.  
  
6.  Impostare l'attributo `userNamePasswordValidationMode` su `MembershipProvider`.  
  
    > [!IMPORTANT]
    >  Se il valore `userNamePasswordValidationMode` non è impostato, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza l'autenticazione di Windows invece del provider di appartenenza [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  
  
7.  Impostare l'attributo `membershipProviderName` sul nome del provider \(specificato al momento di aggiungere il provider nella prima procedura in questo argomento\).Nell'esempio seguente viene illustrato il frammento `<serviceCredentials>` fino a questo punto.  
  
    ```xml  
    <behaviors>  
       <serviceBehaviors>  
          <behavior name="MyServiceBehavior">  
             <serviceCredentials>  
                <userNameAuthentication   
                userNamePasswordValidationMode="MembershipProvider"  
                membershipProviderName="SqlMembershipProvider" />  
             </serviceCredentials>  
          </behavior>  
       </serviceBehaviors>  
    </behaviors>  
  
    ```  
  
## Esempio  
 Nel codice seguente viene mostrata la configurazione per un servizio che utilizza la funzionalità di appartenenza ASP.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service behaviorConfiguration="MyServiceBehavior" name="Microsoft.Samples.GettingStarted.CalculatorService">  
        <endpoint address="http://microsoft.com/WCFservices/Calculator"  
          binding="wsHttpBinding" bindingConfiguration="MembershipBinding"  
          name="ASPmemberUserName" contract="Microsoft.Samples.GettingStarted.ICalculator" />  
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="MyServiceBehavior">  
          <serviceCredentials>  
            <userNameAuthentication   
              userNamePasswordValidationMode="MembershipProvider"  
              membershipProviderName="SqlMembershipProvider" />  
          </serviceCredentials>  
        </behavior>  
          </serviceBehaviors>  
    </behaviors>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="MembershipBinding">  
          <security mode="Message">  
            <message clientCredentialType="UserName" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
  </system.serviceModel>  
</configuration>  
  
```  
  
## Vedere anche  
 [Procedura: utilizzare il provider di ruoli ASP.NET con un servizio](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)   
 [Provider di appartenenza e di ruoli](../../../../docs/framework/wcf/samples/membership-and-role-provider.md)