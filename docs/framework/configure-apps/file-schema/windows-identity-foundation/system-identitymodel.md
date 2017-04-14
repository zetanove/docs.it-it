---
title: "&lt;system.identityModel&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 210ce7e9-d07b-400c-800f-5f525dcf95e8
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;system.identityModel&gt;
Fornisce la configurazione per l'attivazione delle opzioni di base di identità di Windows \(WIF\) nelle applicazioni.  
  
 \<system.identityModel\>  
  
## Sintassi  
  
```  
<system.identityModel>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|Specifica le impostazioni di identità a livello di servizio.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`<configuration>`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
  
## Note  
 Aggiungere una `<system.identityModel>` sezione del file di configurazione per configurare un servizio o applicazione di utilizzare Windows identità Foundation \(WIF\).  Il `<system.identityModel>` elemento è rappresentato dal <xref:System.IdentityModel.Configuration.SystemIdentityModelSection> classe.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come aggiungere una `<system.identityModel>` sezione in un file di configurazione.  È innanzitutto necessario aggiungere la dichiarazione di spazio dei nomi e la sezione di configurazione sotto il `<configSections>` elemento.  Quindi è possibile aggiungere il `<system.IdentityModel>` elemento nel file di configurazione per specificare una o più configurazioni di identità.  
  
```  
<configuration>  
  <configSections>  
    <!--WIF 4.5 sections -->  
    <section name="system.identityModel" type="System.IdentityModel.Configuration.SystemIdentityModelSection, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089"/>  
    <section name="system.identityModel.services" type="System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089"/>  
  </configSections>  
  
  ...  
  
  <system.identityModel>  
    <identityConfiguration>  
      <audienceUris>  
        <add value="http://localhost/WebApplication1/" />  
      </audienceUris>  
      <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089">  
        <trustedIssuers>  
          <add thumbprint="313D3B … 9106A9EC" name="SelfSTS" />  
        </trustedIssuers>  
      </issuerNameRegistry>  
      <certificateValidation certificateValidationMode="None"/>  
    </identityConfiguration>  
  </system.identityModel>  
  
  ...  
  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Configuration.SystemIdentityModelSection>