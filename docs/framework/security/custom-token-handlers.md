---
title: "Gestori di token personalizzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5062669f-8bfc-420a-a25d-d8ab992ab10e
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# Gestori di token personalizzati
In questo argomento vengono illustrati i gestori di token in WIF e come vengono utilizzati per elaborare i token.  Vengono inoltre archiviati cosa è necessario creare i gestori di token personalizzati per i tipi di token non supportati per impostazione predefinita in WIF.  
  
## Introduzione ai gestori di token in WIF  
 WIF si basa sui gestori del token di sicurezza per creare, leggere, scrivere e convalidare i token per un'applicazione di \(RP\) del componente o un servizio token di sicurezza \(STS\).  I gestori di token sono punti di estensibilità di aggiungere un gestore di token personalizzato nella pipeline di WIF, o per personalizzare la modalità di un gestore di token esistente gestisce i token.  WIF fornisce a nove gestori incorporati del token di sicurezza che possono essere modificati o completamente essere sottoposti a override per modificare necessaria la funzionalità.  
  
## Gestori incorporati del token di sicurezza in WIF  
 WIF 4,5 include nove classi del gestore del token di sicurezza che derivano dalla classe base astratta <xref:System.IdentityModel.Tokens.SecurityTokenHandler>:  
  
-   <xref:System.IdentityModel.Tokens.EncryptedSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.KerberosSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.RsaSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.UserNameSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.WindowsUserNameSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler>  
  
## Aggiungere un gestore di token personalizzato  
 Alcuni tipi di token, come token Web semplici \(SWT\) e token Web \(JWT\) JSON senza gestori simbolici incorporati forniti da WIF.  Per questi tipi di token e per altri che non dispongano di un gestore incorporato, è necessario eseguire i passaggi seguenti per creare un gestore di token personalizzato.  
  
#### Aggiungere un gestore di token personalizzato  
  
1.  Creare una nuova classe da <xref:System.IdentityModel.Tokens.SecurityTokenHandler>.  
  
2.  Eseguire l'override dei seguenti metodi e fornire un'implementazione personalizzata:  
  
    -   <xref:System.IdentityModel.Tokens.SecurityTokenHandler.CanReadToken%2A>  
  
    -   <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ReadToken%2A>  
  
    -   <xref:System.IdentityModel.Tokens.SecurityTokenHandler.CanWriteToken%2A>  
  
    -   <xref:System.IdentityModel.Tokens.SecurityTokenHandler.WriteToken%2A>  
  
    -   <xref:System.IdentityModel.Tokens.SecurityTokenHandler.CanValidateToken%2A>  
  
    -   <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ValidateToken%2A>  
  
3.  Aggiungere un riferimento al nuovo gestore di token personalizzato *nel file Web.config o* in App.configfile *,* nella sezione **\<system.identityModel\>** che si applica a WIF.  Ad esempio, il seguente markup di configurazione specifica un nuovo gestore denominato token **MyCustomTokenHandler** che risiedono nello spazio dei nomi **CustomToken**.  
  
    ```  
    <system.identityModel>  
        <identityConfiguration saveBootstrapContext="true">  
            <securityTokenHandlers>  
                <add type="CustomToken.MyCustomTokenHandler, CustomToken" />  
            </securityTokenHandlers>  
        </identityConfiguration>  
    </system.identityModel>  
    ```  
  
     Si noti che se si stanno immettendo al gestore di token per gestire un tipo di token che dispone già di un gestore di token incorporato, è necessario aggiungere un elemento **\<remove\>** per rilasciare il gestore predefinito e utilizzare il gestore personalizzato.  Ad esempio, la configurazione seguente sostituisce <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler> predefinito con il gestore di token personalizzato:  
  
    ```  
    <system.identityModel>  
        <identityConfiguration saveBootstrapContext="true">  
            <securityTokenHandlers>  
                <remove type=”System.IdentityModel.Tokens.SamlSecurityTokenHandler, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=abcdefg123456789”>  
                <add type="CustomToken.MyCustomTokenHandler, CustomToken" />  
            </securityTokenHandlers>  
        </identityConfiguration>  
    </system.identityModel>  
    ```