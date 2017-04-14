---
title: "Elemento &lt;add&gt; di &lt;claimTypeRequirements&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3234cd45-1478-468e-8b19-5c50815c4786
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Elemento &lt;add&gt; di &lt;claimTypeRequirements&gt;
Specifica i tipi di attestazione obbligatori e facoltativi previsti in una credenziale federata.  Ad esempio, i servizi definiscono requisiti per le credenziali in entrata affinché dispongano di un determinato set di tipi di attestazione.  
  
## Sintassi  
  
```  
  
<claimTypeRequirements>  
      <add claimType="URI"  
        isOptional="Boolean" />  
</claimTypeRequirements>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|claimType|URI che definisce il tipo di un'attestazione.  Ad esempio, per acquistare un prodotto da un sito Web, l'utente deve presentare una carta di credito valida avente un limite di credito sufficiente.  Il tipo di attestazione in questo caso è l'URI della carta di credito.|  
|isOptional|Valore booleano che specifica se l'attestazione è facoltativa.  Impostare questo attributo su `false` se l'attestazione è obbligatoria.<br /><br /> Questo attributo può essere usato quando il servizio richiede alcune informazioni non obbligatorie.  Ad esempio, è possibile richiedere obbligatoriamente che l'utente immetta nome, cognome e indirizzo, ma stabilire che il numero telefonico sia facoltativo.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<requisitiTipoAttestazione\>](../../../../../docs/framework/configure-apps/file-schema/wcf/claimtyperequirements-for-message.md)|Specifica una raccolta di tipi di attestazione obbligatori.  Ciascun elemento è di tipo <xref:System.ServiceModel.Configuration.ClaimTypeElement>.<br /><br /> In un scenario federato, i servizi attestano i requisiti per le credenziali in ingresso.  Ad esempio, le credenziali in ingresso devono disporre di un certo set di tipi di attestazioni.  Ogni elemento di questa raccolta specifica i tipi di attestazione obbligatori e facoltativi previsti in una credenziale federata.|  
  
## Note  
 In un scenario federato, i servizi attestano i requisiti per le credenziali in ingresso.  Ad esempio, le credenziali in ingresso devono disporre di un certo set di tipi di attestazioni.  Questo requisito si presenta in un criterio di sicurezza.  Quando un client richiede credenziali da un servizio federato \(ad esempio CardSpace\), tale client inserisce i requisiti in una richiesta di token \(RequestSecurityToken\) affinché il servizio federato sia in grado di rilasciare le credenziali che soddisfano opportunamente i requisiti.  
  
## Esempio  
 Nella configurazione seguente vengono aggiunti due requisiti di tipo di attestazione a un'associazione di sicurezza.  
  
```  
<bindings>  
    <wsFederationHttpBinding>  
      <binding name="myFederatedBinding">  
        <security mode="Message">  
          <message issuedTokenType="urn:oasis:names:tc:SAML:1.0:assertion">  
            <claimTypeRequirements>  
              <add claimType=  
"http://schemas.microsoft.com/ws/2005/05/identity/claims/EmailAddress"/>  
              <add claimType=  
"http://schemas.microsoft.com/ws/2005/05/identity/claims/UserName"    
optional="true" />  
            </claims>  
          </message>  
        </security>  
      </binding>  
    </wsFederationHttpBinding>  
</bindings>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.ClaimTypeRequirements%2A>   
 <xref:System.ServiceModel.Security.Tokens.ClaimTypeRequirement>   
 <xref:System.ServiceModel.Configuration.FederatedMessageSecurityOverHttpElement.ClaimTypeRequirements%2A>   
 <xref:System.ServiceModel.Configuration.ClaimTypeElementCollection>   
 <xref:System.ServiceModel.Configuration.ClaimTypeElement>