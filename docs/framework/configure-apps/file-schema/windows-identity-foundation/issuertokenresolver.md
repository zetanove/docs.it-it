---
title: "&lt;issuerTokenResolver&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f74392f6-3f5b-4880-bd8a-3a9130d31e65
caps.latest.revision: 9
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# &lt;issuerTokenResolver&gt;
Registra il resolver del token emittente utilizzato dai gestori dell'insieme di gestore del token.  Resolver del token emittente viene utilizzato per risolvere il token di firma di token in arrivo e messaggi.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerTokenResolver type=xs:string>  
        </issuerTokenResolver>  
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
|type|Specifica il tipo di resolver del token dell'emittente.  Deve essere il <xref:System.IdentityModel.Tokens.IssuerTokenResolver> classe o un tipo che deriva dal <xref:System.IdentityModel.Tokens.IssuerTokenResolver> classe.  Per ulteriori informazioni su come specificare il `type` di attributo, vedere [Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferences).  Obbligatorio.|  
  
### Elementi figlio  
 Nessuno  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|Fornisce la configurazione per un insieme di protezione gestori dei token.|  
  
## Note  
 Resolver del token emittente viene utilizzato per risolvere il token di firma di token in arrivo e messaggi.  Esso viene utilizzato per recuperare il materiale di crittografia utilizzato per la verifica della firma.  È necessario specificare il `type` attributo.  Il tipo specificato può essere rappresentato da <xref:System.IdentityModel.Tokens.IssuerTokenResolver> o un tipo personalizzato che deriva dal <xref:System.IdentityModel.Tokens.IssuerTokenResolver> classe.  
  
 Alcuni gestori token consentono di specificare le impostazioni del resolver del token emittente nella configurazione.  Le impostazioni sui singoli gestori token sostituiscono quelli specificati per l'insieme del gestore del token di protezione.  
  
> [!NOTE]
>  Specifica il `<issuerTokenResolver>` come un elemento figlio dell'elemento di [\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) elemento è stato dichiarato obsoleto, ma è ancora supportata per compatibilità con le versioni precedenti.  Le impostazioni di `<securityTokenHandlerConfiguration>` elemento eseguire l'override di quelle sul `<identityConfiguration>` elemento.  
  
## Esempio  
 Il file XML riportato di seguito mostra la configurazione per un resolver del token emittente che si basa su una classe personalizzata che deriva da <xref:System.IdentityModel.Tokens.IssuerTokenResolver>.  Resolver del token mantiene un dizionario delle coppie di chiavi pubblico inizializzata da un elemento di configurazione personalizzato \(`<AddAudienceKeyPair>`\) definite per la classe.  L'override della classe di <xref:System.IdentityModel.Selectors.SecurityTokenResolver.LoadCustomConfiguration%2A> metodo per elaborare questo elemento.  L'override è illustrato nell'esempio riportato di seguito; Tuttavia, i metodi di chiamata non vengono visualizzati per ragioni di brevità.  Per un esempio completo, vedere la `CustomToken` campione.  
  
```  
<issuerTokenResolver type="SimpleWebToken.CustomIssuerTokenResolver, SimpleWebToken">  
  <AddAudienceKeyPair  symmetricKey="wAVkldQiFypTQ+kdNdGWCYCHRcee8XmXxOvgmak8vSY=" audience="http://localhost:19851/" />  
</issuerTokenResolver>  
```  
  
## Esempio  
  
```  
public override void LoadCustomConfiguration(System.Xml.XmlNodeList nodelist)  
{  
    foreach (XmlNode node in nodelist)  
    {  
        XmlDictionaryReader rdr = XmlDictionaryReader.CreateDictionaryReader(new XmlTextReader(new StringReader(node.OuterXml)));  
        rdr.MoveToContent();  
  
        string symmetricKey = rdr.GetAttribute("symmetricKey");  
        string audience = rdr.GetAttribute("audience");  
  
        this.AddAudienceKeyPair(audience, symmetricKey);  
    }  
}  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Tokens.IssuerTokenResolver>