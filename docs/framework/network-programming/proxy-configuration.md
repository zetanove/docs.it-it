---
title: "Configurazione del proxy | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "proxy adattivi"
  - "Internet, configurazione del proxy"
  - "Risorse di rete"
  - "rete, configurazione del proxy"
  - "Rete"
  - "proxy"
  - "proxy, configurazione"
  - "proxy statici"
ms.assetid: 353c0a8b-4cee-44f6-8e65-60e286743df9
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Configurazione del proxy
Un server proxy gestisce le richieste di risorse del client.  Un proxy può restituire una risorsa richiesta dalla cache o inoltrare la richiesta al server in cui risiede la risorsa.  I proxy possono migliorare le prestazioni della rete riducendo il numero di richieste inviate ai server remoti.  I proxy possono essere usati anche per limitare l'accesso alle risorse.  
  
## Proxy adattivi  
 In .NET Framework i proxy possono essere di due tipi: adattivi e statici.  I proxy adattivi regolano le impostazioni quando viene modificata la configurazione di rete.  Ad esempio, se un utente avvia una connessione di rete remota sul laptop, un proxy adattivo riconosce questa modifica, individua ed esegue il nuovo script di configurazione e regola le impostazioni in modo appropriato.  
  
 I proxy adattivi vengono configurati con uno script di configurazione \(vedere [Rilevamento automatico proxy](../../../docs/framework/network-programming/automatic-proxy-detection.md)\).  Lo script genera un set di protocolli di applicazioni e un proxy per ogni protocollo.  
  
 Diverse opzioni controllano come viene eseguito lo script di configurazione.  È possibile specificare:  
  
-   Frequenza di download e di esecuzione dello script di configurazione.  
  
-   Tempo di attesa del download dello script.  
  
-   Credenziali usate dal sistema per accedere al proxy.  
  
-   Credenziali usate dal sistema per il download dello script di configurazione.  
  
 Le modifiche nell'ambiente di rete possono richiedere che il sistema usi un nuovo set di proxy.  Se una connessione di rete non funziona o viene inizializzata una nuova connessione di rete, il sistema deve individuare l'origine appropriata dello script di configurazione nel nuovo ambiente ed eseguire il nuovo script.  
  
 La tabella seguente mostra le opzioni di configurazione per un proxy adattivo.  
  
|Impostazione di attributo, proprietà o file di configurazione|Descrizione|  
|-------------------------------------------------------------------|-----------------|  
|`scriptDownloadInterval`|Tempo trascorso in secondi tra i download dello script.|  
|`scriptDownloadTimeout`|Tempo di attesa \(in secondi\) per il download dello script.|  
|`useDefaultCredentials` oppure <xref:System.Net.WebProxy.UseDefaultCredentials>|Controlla se il sistema usa le credenziali di rete predefinite per l'accesso a un proxy.|  
|`useDefaultCredentialForScriptDownload`|Controlla se il sistema usa le credenziali di rete predefinite per il download dello script di configurazione.|  
|`usesystemdefaults`|Controlla se le impostazioni del proxy statico \(indirizzo proxy, elenco di esclusione e opzione che specifica se ignorare il proxy per indirizzi locali\) devono essere lette dalle impostazioni del proxy di Internet Explorer per l'utente.  Se questo valore è impostato su "true", verranno usate le impostazioni del proxy statico di Internet Explorer.<br /><br /> Se questo valore è "false" o non impostato, le impostazioni del proxy statico possono essere specificate nella configurazione e sostituiranno le impostazioni del proxy di Internet Explorer.  Questo valore deve essere impostato su "false" o non deve essere impostato anche per abilitare i proxy adattivi.|  
  
 L'esempio seguente mostra una configurazione tipica di un proxy adattivo.  
  
```  
<system.net>  
    <defaultProxy>  
      <proxy  scriptDownloadInterval="600"  
              scriptDownloadTimeout="30"  
              useDefaultCredentials="true"  
              usesystemdefaults="true"  
      />  
    </defaultProxy>  
</system.net>  
```  
  
## Proxy statici  
 I proxy statici in genere vengono configurati in modo esplicito da un'applicazione o quando un file di configurazione viene richiamato da un'applicazione o dal sistema.  I proxy statici sono utili nelle reti in cui la topologia cambia raramente, ad esempio un computer desktop connesso a una rete aziendale.  
  
 Diverse opzioni controllano il funzionamento di un proxy statico.  È possibile specificare:  
  
-   Indirizzo del proxy.  
  
-   Valore che controlla se il proxy deve essere ignorato per gli indirizzi locali.  
  
-   Valore che controlla se il proxy deve essere ignorato per un set di indirizzi.  
  
 La tabella seguente mostra le opzioni di configurazione di un proxy statico.  
  
|Impostazione di attributo, proprietà o file di configurazione|Descrizione|  
|-------------------------------------------------------------------|-----------------|  
|`proxyaddress` oppure <xref:System.Net.WebProxy.Address>|Indirizzo del proxy da usare.|  
|`bypassonlocal` oppure <xref:System.Net.WebProxy.BypassProxyOnLocal>|Valore che controlla se il proxy viene ignorato per gli indirizzi locali.|  
|`bypasslist` oppure <xref:System.Net.WebProxy.BypassArrayList>|Descrive con espressioni regolari un set di indirizzi che ignorano il proxy.|  
|`usesystemdefaults`|Controlla se le impostazioni del proxy statico \(indirizzo proxy, elenco di esclusione e opzione che specifica se ignorare il proxy per indirizzi locali\) devono essere lette dalle impostazioni del proxy di Internet Explorer per l'utente.  Se questo valore è impostato su "true", verranno usate le impostazioni del proxy statico di Internet Explorer.  In .NET Framework 2.0 quando questo valore è impostato su "true", le impostazioni del proxy di Internet Explorer non vengono sostituite dalle altre impostazioni del proxy specificate nel file di configurazione.  In .NET Framework 1.1 le impostazioni del proxy di Internet Explorer possono essere sostituite dalle altre impostazioni del proxy specificate nel file di configurazione.<br /><br /> Se questo valore è "false" o non impostato, le impostazioni del proxy statico possono essere specificate nella configurazione e sostituiranno le impostazioni del proxy di Internet Explorer.  Questo valore deve essere impostato su "false" o non deve essere impostato anche per abilitare i proxy adattivi.|  
  
 L'esempio seguente illustra una configurazione tipica di un proxy statico.  
  
```  
<system.net>  
    <defaultProxy>  
        <proxy  proxyaddress="http://proxy.contoso.com:3128"  
                bypassonlocal="true"  
        />  
        <bypasslist>  
            <add address="[a-z]+.blueyonderairlines.com$" />  
        </bypasslist>  
    </defaultProxy>  
</system.net>  
```  
  
## Vedere anche  
 <xref:System.Net.WebProxy>   
 <xref:System.Net.GlobalProxySelection>   
 [Rilevamento automatico proxy](../../../docs/framework/network-programming/automatic-proxy-detection.md)