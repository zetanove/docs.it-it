---
title: "&lt;audienceUris&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7a3d8515-d756-4afe-a22d-07cbe2217ee3
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# &lt;audienceUris&gt;
Specifica l'insieme di URI sono identificatori accettabili della controparte \(RP\).  Token non verranno accettati a meno che non vengono inclusi nell'ambito di uno degli utenti consentiti gli URI.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <audienceUris mode=xs:string>  
          <add value=xs:string />  
          <clear />  
          <remove value=xs:string />  
        </audienceUris>  
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
|mode|Un <xref:System.IdentityModel.Selectors.AudienceUriMode> valore che specifica se la restrizione pubblico deve essere applicata a un token in ingresso.  I valori possibili sono "Always", "Mai" e "BearerKeyOnly".  Il valore predefinito è "Sempre".  Parametro facoltativo.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`<add value=xs:string>`|Aggiunge l'URI specificato per il `value` di attributo all'insieme audienceUris.  L'attributo `value` è obbligatorio.  L'URI è tra maiuscole e minuscole.|  
|`<clear>`|Cancella l'insieme audienceUris.  Tutti gli identificatori vengono rimossi dall'insieme.|  
|`<remove value=xs:string>`|Rimuove l'URI specificato per il `value` attributo dall'insieme audienceUris.  L'attributo `value` è obbligatorio.  L'URI è tra maiuscole e minuscole.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|Fornisce la configurazione per un insieme di protezione gestori dei token.|  
  
## Note  
 Per impostazione predefinita, l'insieme è vuoto; Utilizzare `<add>`, `<clear>`, e `<remove>` gli elementi per modificare l'insieme.  <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>e <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> utilizzano i valori nell'insieme di URI pubblico per configurare una consentito pubblico restrizioni URI in <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> oggetti.  
  
 Il `<audienceUris>` elemento è rappresentato dal <xref:System.IdentityModel.Configuration.AudienceUriElementCollection> classe.  Un URI singolo aggiunto all'insieme è rappresentato dal <xref:System.IdentityModel.Configuration.AudienceUriElement> classe.  
  
> [!NOTE]
>  L'utilizzo del `<audienceUris>` come un elemento figlio dell'elemento di [\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) elemento è stato dichiarato obsoleto, ma è ancora supportata per compatibilità con le versioni precedenti.  Le impostazioni di `<securityTokenHandlerConfiguration>` elemento eseguire l'override di quelle sul `<identityConfiguration>` elemento.  
  
## Esempio  
 Il file XML riportato di seguito viene illustrato come configurare il pubblico accettabile gli URI per un'applicazione.  In questo esempio consente di configurare un singolo URI.  Token con ambito di questo URI verrà accettato, tutti gli altri verranno rifiutati.  
  
```  
<audienceUris>  
  <add value="http://localhost:19851/"/>  
</audienceUris>  
```