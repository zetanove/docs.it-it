---
title: "Rilevamento automatico proxy | Microsoft Docs"
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
  - "rilevamento automatico di proxy"
  - "Rilevamento automatico proxy Web"
  - "proxy Web"
  - "automatico, rilevamento di proxy"
  - "WebProxy (classe), rilevamento automatico di proxy"
  - "proxy, rilevamento automatico"
  - "rete"
  - "WPAD (Rilevamento automatico proxy Web)"
ms.assetid: fcd9c3bd-93de-4c92-8ff3-837327ad18de
caps.latest.revision: 18
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 18
---
# Rilevamento automatico proxy
Il rilevamento automatico del proxy è un processo con cui un server proxy Web viene identificato dal sistema e viene utilizzato per inviare richieste per conto del client.  Tale funzionalità è anche nota come WPAD \(Web Proxy Auto\-Discovery\).  Quando il rilevamento automatico del proxy è abilitato, il sistema tenta di trovare uno script di configurazione del proxy responsabile della restituzione del set di proxy che possono essere utilizzati per la richiesta.  Se lo script di configurazione del proxy viene trovato, lo script viene scaricato, compilato ed eseguito nel computer locale quando le informazioni del proxy, il flusso di richieste o, la risposta vengono ottenuti per una richiesta che utilizza un'istanza <xref:System.Net.WebProxy>.  
  
 Il rilevamento automatico del proxy vengono eseguiti dalla classe <xref:System.Net.WebProxy> e può utilizzare le impostazioni a livello di richiesta, le impostazioni nel file di configurazione e le impostazioni specificate utilizzando la finestra di dialogo di Internet Explorer **locale Area Network \(LAN\)**.  
  
> [!NOTE]
>  È possibile visualizzare la finestra di dialogo di Internet Explorer **Impostazioni di Area Network \(LAN\) locali** selezionando **Strumenti** dal menu principale di Internet Explorer e selezionando **Opzioni Internet**.  Seguente, selezionare la scheda **connessioni** e fare clic **impostazioni di LAN**.  
  
 Quando il rilevamento automatico del proxy è abilitato, la classe <xref:System.Net.WebProxy> tenta di individuare lo script di configurazione del proxy come segue:  
  
1.  La funzione di WinInet `InternetQueryOption` viene utilizzata per individuare lo script di configurazione del proxy di recente rilevato da Internet Explorer.  
  
2.  Se lo script non viene individuato, la classe <xref:System.Net.WebProxy> utilizza il DHCP \(DHCP\) per individuare lo script.  Il server DHCP può rispondere alla posizione \(nome host di script o con l'url completo per lo script.  
  
3.  Se il DHCP non identifica l'host di WPAD, il DNS viene eseguita una query per un host con WPAD il nome o l'alias.  
  
4.  Se l'host non viene identificato e la posizione di uno script di configurazione del proxy è determinata dalle impostazioni di LAN Internet Explorer o da un file di configurazione, questa posizione viene utilizzata.  
  
> [!NOTE]
>  Le applicazioni in esecuzione come servizi NT o come parte di ASP.NET utilizzano le impostazioni del server proxy di Internet Explorer \(se disponibile\) dell'utente di chiamata.  Queste impostazioni non possono essere disponibili per tutte le applicazioni di servizio.  
  
 I proxy vengono configurati in un oggetto per la connectoid base.  Un connectoid è un elemento nella finestra di dialogo di connessione di rete e può essere un dispositivo di rete fisica \(un modem o una scheda di Ethernet\) o un'interfaccia virtuale \(ad esempio una connessione VPN che investe un dispositivo di rete\).  Quando le modifiche di un connectoid, ad esempio una connessione wireless modifica un punto di accesso, o un VPN è attivato, l'algoritmo di rilevamento del proxy viene nuovamente eseguita.  
  
 Per impostazione predefinita, le impostazioni proxy di Internet Explorer vengono utilizzate per rilevare il proxy.  Se l'applicazione è in esecuzione con un account non interattivo \(senza un modo pratico per configurare le impostazioni proxy di e, oppure se si desidera utilizzare le impostazioni proxy diverse dalle impostazioni di e, è possibile configurare il proxy crea un file di configurazione con gli elementi [Elemento \<proxy\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/proxy-element-network-settings.md) e [Elemento \<defaultProxy\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md) definiti.  
  
 Per le richieste creati, è possibile disabilitare il rilevamento automatico del proxy a livello di richiesta utilizzando <xref:System.Net.WebRequest.Proxy%2A> null con la richiesta, come illustrato nell'esempio di codice.  
  
```csharp  
public static void DisableForMyRequest (Uri resource)  
{  
    WebRequest request = WebRequest.Create (resource);  
    request.Proxy = null;  
    WebResponse response = request.GetResponse ();  
}  
```  
  
```vb  
Public Shared Sub DisableForMyRequest(ByVal resource As Uri)  
    Dim request As WebRequest = WebRequest.Create(resource)  
    request.Proxy = Nothing  
    Dim response As WebResponse = request.GetResponse()  
    End Sub   
```  
  
 Pretese che non dispongono del proxy predefinito dominio applicazione del proxy utilizzo del, disponibile nella proprietà <xref:System.Net.WebRequest.DefaultWebProxy%2A>.  
  
## Vedere anche  
 <xref:System.Net.WebProxy>   
 <xref:System.Net.WebRequest>   
 [Elemento \<system.Net\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)