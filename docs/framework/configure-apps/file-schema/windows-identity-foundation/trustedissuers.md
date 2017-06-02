---
title: "&lt;trustedIssuers&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d818c917-07b4-40db-9801-8676561859fd
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;trustedIssuers&gt;
Consente di configurare l'elenco dei certificati di autorità emittente attendibile utilizzato dal Registro di sistema di nome basato sulla configurazione dell'emittente \(<xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>\).  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerNameRegistry>  
          <trustedIssuers>  
            <add thumbprint=xs:string name=xs:string>  
            <clear>  
            <remove thumbprint=xs:string>  
          </trustedIssuers>  
        </issuerNameRegistry>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`<add thumbprint=xs:string name=xs:string>`|Aggiunge un certificato per l'insieme delle certificazioni attendibili.  Il certificato è specificato con il `thumbprint` attributo.  Questo attributo è obbligatorio e deve contenere il modulo ASN. 1 codificato di identificazione personale del certificato.  Il `name` attributo è facoltativo e può essere utilizzato per specificare un nome descrittivo per il certificato.|  
|`<clear>`|Cancella tutti i certificati dall'insieme delle certificazioni attendibili.|  
|`<remove thumbprint=xs:string>`|Rimuove un certificato dall'insieme delle certificazioni attendibili.  Il certificato è specificato con il `thumbprint` attributo.  Questo attributo è obbligatorio.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<issuerNameRegistry\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/issuernameregistry.md)|Consente di configurare il Registro di sistema di nome dell'emittente. **Important:**  Il `type` attributo del `<issuerNameRegistry>` deve fare riferimento a elemento di <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> di classe per il `<trustedIssuers>` elemento sia valido.|  
  
## Note  
 Foundation identità Windows \(WIF\) fornisce una singola implementazione del <xref:System.IdentityModel.Tokens.IssuerNameRegistry> classe fuori della finestra, il <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> classe.  Il Registro di sistema di configurazione dell'emittente nome mantiene un elenco delle certificazioni attendibili che viene caricato dalla configurazione.  Nell'elenco associa ciascun nome dell'emittente del certificato x. 509 è necessaria per verificare la firma di token prodotta dall'emittente.  L'elenco dei certificati di autorità emittente attendibile viene specificato sotto il `<trustedIssuers>` elemento.  Ogni elemento nell'elenco associa un nome mnemonico emittente del certificato x. 509 è necessaria per verificare la firma di token prodotte da tale emittente.  Attendibili i certificati vengono specificati utilizzando l'ASN. 1 codificato in forma di identificazione personale del certificato e vengono aggiunti all'insieme utilizzando `<add>` elemento.  È possibile eliminare o rimuovere gli emittenti \(certificati\) dall'elenco utilizzando il `<clear>` e `<remove>` gli elementi.  
  
 Il `type` attributo del `<issuerNameRegistry>` deve fare riferimento a elemento di <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> di classe per il `<trustedIssuers>` elemento sia valido.  
  
## Esempio  
 Il file XML riportato di seguito viene illustrato come specificare l'emittente di configurazione in base del Registro di sistema di nome.  
  
```  
<issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
  <trustedIssuers>  
    <add thumbprint="9B74CB2F32 … B1DC01EF40D0" name="LocalSTS" />  
  </trustedIssuers>  
</issuerNameRegistry>  
  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>   
 <xref:System.IdentityModel.Tokens.IssuerNameRegistry>