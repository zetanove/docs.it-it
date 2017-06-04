---
title: "&lt;issuerNameRegistry&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58b39d12-c953-40c4-88af-d7eb3343ca28
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 12
---
# &lt;issuerNameRegistry&gt;
Consente di configurare il Registro di sistema del nome dell'emittente che viene utilizzato dai gestori dell'insieme di gestore del token.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerNameRegistry type=xs:string>  
          <optionalCustomConfigurationElements />  
        </issuerNameRegistry>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|type|Un tipo che deriva dal <xref:System.IdentityModel.Tokens.IssuerNameRegistry> classe.  Per ulteriori informazioni su come specificare un personalizzato `type`, vedere [Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferences).|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<trustedIssuers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/trustedissuers.md)|Quando il `type` attributo specifica del Registro di sistema di nome basato sulla configurazione dell'emittente \(il <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> classe\), il [\<trustedIssuers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/trustedissuers.md) elemento deve essere specificato.  Il [\<trustedIssuers\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/trustedissuers.md) elemento può richiedere `<add>`, `<clear>`, o `<remove>` gli elementi come elementi figlio.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|Fornisce la configurazione per un insieme di protezione gestori dei token.|  
  
## Note  
 Tutti i token dell'emittente vengono convalidati tramite un registro di sistema di nome dell'emittente.  Si tratta di un oggetto che deriva dal <xref:System.IdentityModel.Tokens.IssuerNameRegistry> classe.  Il Registro di sistema di nome autorità emittente viene utilizzato per associare un nome per il materiale di crittografia è necessaria per verificare le firme di token prodotta dall'emittente corrispondente tasti di scelta rapida.  Il Registro di sistema di nome autorità emittente gestisce un elenco delle certificazioni attendibili dall'applicazione di terze parti \(RP\) componente di applicazione.  Il tipo del Registro di sistema di nome dell'emittente è specificato mediante la `type` attributo.  Il `<issuerNameRegistry>` elemento può avere uno o più elementi figlio che forniscono la configurazione per il tipo specificato.  Si fornisce la logica che elabora gli elementi figlio mediante l'override di <xref:System.IdentityModel.Tokens.IssuerNameRegistry.LoadCustomConfiguration%2A> metodo.  
  
 WIF fornisce un emittente singolo tipo di nome del Registro di sistema non la casella di <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> classe.  Questa classe viene utilizzata una serie di certificati di autorità emittente attendibile specificato nella configurazione.  È necessario disporre di un elemento di configurazione figlio `<trustedIssuers>`, in cui è configurato l'insieme dei certificati di autorità emittente attendibile.  Attendibili i certificati vengono specificati utilizzando l'ASN. 1 codificato in forma di identificazione personale del certificato e viene aggiunti o rimossi dall'insieme utilizzando `<add>`, `<clear>`, o `<remove>` gli elementi.  
  
 Il `<issuerNameRegistry>` elemento è rappresentato dal <xref:System.IdentityModel.Configuration.IssuerNameRegistryElement> classe.  
  
> [!NOTE]
>  Specifica il `<issuerNameRegistry>` come un elemento figlio dell'elemento di [\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) elemento è stato dichiarato obsoleto, ma è ancora supportata per compatibilità con le versioni precedenti.  Le impostazioni di `<securityTokenHandlerConfiguration>` elemento eseguire l'override di quelle sul `<identityConfiguration>` elemento.  
  
## Esempio  
 Il file XML riportato di seguito viene illustrato come specificare l'emittente di configurazione in base del Registro di sistema di nome.  
  
```  
<issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
  <trustedIssuers>  
    <add thumbprint="9B74CB … 1EF40D0" name="LocalSTS" />  
  </trustedIssuers>  
</issuerNameRegistry>  
  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Tokens.IssuerNameRegistry>   
 <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>