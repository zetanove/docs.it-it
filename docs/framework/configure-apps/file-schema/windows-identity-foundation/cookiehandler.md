---
title: "&lt;cookieHandler&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bfdc127f-8d94-4566-8bef-f583c6ae7398
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;cookieHandler&gt;
Consente di configurare il <xref:System.IdentityModel.Services.CookieHandler> che il <xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\) viene utilizzato per leggere e scrivere i cookie.  
  
## Sintassi  
  
```  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler name=xs:string  
        path=Path  
        mode="Chunked||Custom||Default"  
        persistentSessionLifetime=xs:string  
        hideFromScript=xs:boolean  
        requireSSL=xs:boolean  
        domain=xs:string  
      <chunkedCookieHandler size=xs:int />  
      <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" />  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|name|Specifica il nome di base per tutti i cookie scritti.  Il valore predefinito è "FedAuth".|  
|path|Specifica il valore di percorso per tutti i cookie scritti.  Il valore predefinito è "HttpRuntime.AppDomainAppVirtualPath".|  
|mode|Uno della <xref:System.IdentityModel.Services.CookieHandlerMode> i valori che specifica il tipo di gestore del cookie utilizzato da SAM.  Possono essere utilizzati i seguenti valori:<br /><br /> -   "Default", ovvero lo stesso "Chunked".<br />-   "Chunked", ovvero utilizza un'istanza del <xref:System.IdentityModel.Services.ChunkedCookieHandler> classe.  Questo gestore cookie assicura che singoli cookie non superino la dimensione massima del set.  Ciò avviene mediante potenzialmente "chunking" un cookie logico in un numero di cookie in transito.<br />-   "Custom", viene utilizzata un'istanza di una classe personalizzata derivata da <xref:System.IdentityModel.Services.CookieHandler>.  La classe derivata fa riferimento la `<customCookieHandler>` elemento figlio.<br /><br /> Il valore predefinito è "Default".|  
|persistentSessionLifetime|Specifica la durata delle sessioni permanenti.  Se è zero, le sessioni temporanee vengono sempre utilizzate.  Il valore predefinito è "0:0:0", che specifica una sessione temporanea.  Il valore massimo è "365:0:0", che specifica una sessione di 365 giorni.  Il valore deve essere precisato secondo la seguente limitazione: `<xs:pattern value="([0-9.]+:){0,1}([0-9]+:){0,1}[0-9.]+" />`, in cui il valore all'estrema sinistra specifica giorni, il valore medio \(se presente\) specifica ore e il valore all'estrema destra \(se presente\) minuti.|  
|requireSsl|Specifica se il flag "Secure" e viene creato per tutti i cookie scritti.  Se questo valore è impostato, i cookie di sessione di accesso è disponibili solo tramite HTTPS.  Il valore predefinito è "true".|  
|hideFromScript|Controlla se il flag "HttpOnly" e viene creato per tutti i cookie scritti.  In alcuni browser rispetta questo flag mantenendo uno script lato client di accedere al valore del cookie.  Il valore predefinito è "true".|  
|dominio|Il valore di dominio per tutti i cookie scritti.  Il valore predefinito è "".|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<chunkedCookieHandler\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/chunkedcookiehandler.md)|Consente di configurare il <xref:System.IdentityModel.Services.ChunkedCookieHandler>.  Può essere presente solo questo elemento se il `mode` attributo del `<cookieHandler>` elemento è "Default" o "Chunked".|  
|[\<customCookieHandler\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/customcookiehandler.md)|Imposta il tipo di gestore di cookie personalizzati.  Questo elemento deve essere presente se il `mode` attributo del `<cookieHandler>` elemento è "Custom".  Non può essere presente per tutti gli altri valori della `mode` attributo.  Il tipo personalizzato deve essere derivato dal <xref:System.IdentityModel.Services.CookieHandler> classe.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md)|Contiene le impostazioni che configurano il <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> \(WSFAM\) e il <xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\).|  
  
## Note  
 Il <xref:System.IdentityModel.Services.CookieHandler> è responsabile di livello del protocollo di lettura e scrittura dei cookie non elaborati in HTTP.  È possibile configurare un <xref:System.IdentityModel.Services.ChunkedCookieHandler> o un gestore di cookie personalizzati derivati dal <xref:System.IdentityModel.Services.CookieHandler> classe.  
  
 Per configurare un gestore chunked cookie, impostare l'attributo mode "Chunked" o "Default".  Le dimensioni del blocco predefinito sono 2000 byte, ma si può specificare una dimensione diversa del blocco, includendo un `<chunkedCookieHandler>` elemento figlio.  
  
 Per configurare un gestore personalizzato cookie, impostare l'attributo mode su "Custom".  È inoltre necessario specificare un `<customCookieHandler>` elemento figlio che fa riferimento al tipo di gestore personalizzato.  
  
 Il `<cookieHandler>` elemento è rappresentato dal <xref:System.IdentityModel.Services.CookieHandlerElement> classe.  Il gestore di cookie è stato specificato nella configurazione è disponibile il <xref:System.IdentityModel.Services.Configuration.FederationConfiguration.CookieHandler%2A> proprietà del <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> oggetto impostato sul <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=fullName> proprietà.  
  
## Esempio  
 Nel XML che segue un `<cookieHandler>` elemento.  In questo esempio, poiché il `mode` non è specificato, verrà utilizzato il gestore di cookie predefinito del SAM.  Si tratta di un'istanza del <xref:System.IdentityModel.Services.ChunkedCookieHandler> classe.  Poiché il `<chunkedCookieHandler>` l'elemento figlio non è specificato, verrà utilizzata la dimensione del blocco predefinito.  HTTPS non saranno più necessari perché il `requireSsl` è impostato l'attributo `false`.  
  
> [!WARNING]
>  In questo esempio, non è necessario scrivere i cookie di sessione HTTPS.  Infatti il `requireSsl` di attributo sul `<cookieHandler>` è impostato su `false`.  Come può presentare un rischio di protezione, questa impostazione non è consigliata per la maggior parte degli ambienti di produzione.  
  
```  
<cookieHandler requireSsl="false" />  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Services.CookieHandler>   
 <xref:System.IdentityModel.Services.ChunkedCookieHandler>   
 <xref:System.IdentityModel.Services.SessionAuthenticationModule>