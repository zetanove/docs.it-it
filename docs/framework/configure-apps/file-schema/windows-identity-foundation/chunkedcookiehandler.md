---
title: "&lt;chunkedCookieHandler&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7220de45-1d14-4aec-a29e-4a2ea8ac861f
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;chunkedCookieHandler&gt;
Consente di configurare il <xref:System.IdentityModel.Services.ChunkedCookieHandler>.  Può essere presente solo questo elemento se il `mode` attributo del `<cookieHandler>` elemento è "Default" o "Chunked".  
  
## Sintassi  
  
```  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler mode="Chunked||Default" >  
      <chunkedCookieHandler size=xs:int >  
      </chunkedCookieHandler>  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|chunkSize|Dimensione massima in caratteri, i dati del cookie HTTP per un cookie HTTP.  È necessario prestare attenzione quando si modifica la dimensione del blocco.  I browser Web hanno diversi limiti alle dimensioni del cookie e il numero consentito per ogni dominio.  Ad esempio, le specifiche di Netscape originali precisare tali limiti: totale per i 300 cookie, 4096 byte per intestazione cookie \(inclusi i metadati, non solo il valore del cookie\) e 20 cookie per dominio.  Il valore predefinito è 2000.  Obbligatorio.|  
  
### Elementi figlio  
 Nessuno  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<cookieHandler\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/cookiehandler.md)|Consente di configurare il <xref:System.IdentityModel.Services.CookieHandler> che il <xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\) viene utilizzato per leggere e scrivere i cookie.|  
  
## Note  
 Quando si specifica un <xref:System.IdentityModel.Services.ChunkedCookieHandler> impostando il `mode` attributo del `<cookieHandler>` elemento "Default" o "Chunked", è possibile specificare le dimensioni del blocco che il gestore del cookie utilizzato per leggere e scrivere cookie includendo un `<chunkedCookieHandler>` elemento figlio e l'impostazione relativa `chunkSize` attributo.  Se il `<chunkedCookieHandler>` elemento non è presente, viene utilizzata la dimensione del blocco predefinito di 2000 byte.  Questo elemento non può essere specificato quando il `mode` attributo è impostato su "Custom".  
  
 Il `<chunkedCookieHandler>` elemento è rappresentato dal <xref:System.IdentityModel.Services.ChunkedCookieHandlerElement> classe.  
  
## Esempio  
 Nell'esempio riportato di seguito consente di configurare un gestore di cookie chunked scrive i cookie in blocchi di 3000 byte.  
  
```  
<cookieHandler mode="Chunked">  
    <chunkedCookieHandler chunkSize=3000/>  
</cookieHandler>  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Services.ChunkedCookieHandler>