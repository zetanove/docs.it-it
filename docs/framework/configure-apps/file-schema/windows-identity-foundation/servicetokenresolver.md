---
title: "&lt;serviceTokenResolver&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6e9001e1-e064-4f47-84b2-46225c177746
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;serviceTokenResolver&gt;
Registra il resolver del token servizio utilizzato dai gestori dell'insieme di gestore del token.  Resolver del token di servizio viene utilizzato per risolvere il token di crittografia in token in arrivo e messaggi.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <serviceTokenResolver type=xs:string>  
        </serviceTokenResolver>  
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
|type|Specifica il tipo di resolver del token di servizio.  Entrambi i <xref:System.IdentityModel.Selectors.SecurityTokenResolver> tipo o un tipo che deriva dal <xref:System.IdentityModel.Selectors.SecurityTokenResolver> classe.  Per ulteriori informazioni su come specificare il `type` di attributo, vedere [Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferences).  Obbligatorio.|  
  
### Elementi figlio  
 Nessuno  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|Fornisce la configurazione per un insieme di protezione gestori dei token.|  
  
## Note  
 Resolver del token di servizio consente di risolvere il token di crittografia in token in arrivo e messaggi.  Viene utilizzata per recuperare la chiave che deve essere utilizzata per decrittografare i token in ingresso.  È necessario specificare il `type` attributo.  Il tipo specificato può essere rappresentato da <xref:System.IdentityModel.Selectors.SecurityTokenResolver> o un tipo personalizzato che deriva dal <xref:System.IdentityModel.Selectors.SecurityTokenResolver> classe.  
  
 Alcuni gestori token consentono di specificare le impostazioni del resolver del token di servizio nella configurazione.  Le impostazioni sui singoli gestori token sostituiscono quelli specificati per l'insieme del gestore del token di protezione.  
  
> [!NOTE]
>  Specifica il `<serviceTokenResolver>` come un elemento figlio dell'elemento di [\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) elemento è stato dichiarato obsoleto, ma è ancora supportata per compatibilità con le versioni precedenti.  Le impostazioni di `<securityTokenHandlerConfiguration>` elemento eseguire l'override di quelle sul `<identityConfiguration>` elemento.  
  
## Esempio  
  
```  
<serviceTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
```