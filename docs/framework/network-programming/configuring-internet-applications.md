---
title: "configurazione di applicazioni Internet | Microsoft Docs"
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
  - "download delle risorse Internet, proxy predefinito"
  - "invio di dati, proxy predefinito"
  - "ricezione di dati, proxy predefinito"
  - "download delle risorse Internet, configurazione delle applicazioni Internet"
  - "moduli specifici del protocollo"
  - "moduli di autenticazione personalizzata"
  - "ricezione di dati, configurazione di applicazioni Internet"
  - "impostazioni di configurazione [.NET Framework], applicazioni Internet"
  - "richiesta di dati da Internet, configurazione di applicazioni Internet"
  - "richiesta di dati da Internet, proxy predefinito"
  - "risposta a richiesta Internet, proxy predefinito"
  - "Internet, configurazione di applicazioni Internet"
  - "richiesta a richiesta Internet, configurazione di applicazioni Internet"
  - "proxy predefinito"
  - "risorse di rete, proxy predefinito"
  - "invio di dati, configurazione di applicazioni Internet"
  - "risorse di rete, configurazione di applicazioni Internet"
  - "Internet, proxy predefinito"
ms.assetid: bb707c72-eed2-4a82-8800-c9e68df2fd4f
caps.latest.revision: 15
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 15
---
# configurazione di applicazioni Internet
L'elemento di configurazione [Elemento \<system.Net\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md) contiene le informazioni di configurazione di rete per le applicazioni.  Utilizzando l'elemento [Elemento \<system.Net\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md), è possibile impostare i server proxy, impostare i parametri di gestione della connessione e include i moduli personalizzati di richiesta e di autenticazione nell'applicazione.  
  
 L'elemento [Elemento \<defaultProxy\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md) definisce il server proxy restituito dalla classe `GlobalProxySelection`.  Qualsiasi <xref:System.Net.HttpWebRequest> che non dispone del proprio set di proprietà <xref:System.Net.HttpWebRequest.Proxy%2A> a un valore specifico utilizzato il proxy predefinito.  Oltre a impostare l'indirizzo proxy, è possibile creare un elenco degli indirizzi del server che non utilizzeranno il proxy di e è possibile indicare che il proxy non deve essere utilizzato per gli indirizzi locali.  
  
 È importante notare che le impostazioni di Microsoft Internet Explorer vengono combinate con le impostazioni di configurazione, con la precedenza del caso.  
  
 L'esempio seguente consente di impostare l'indirizzo predefinito del server proxy a http:\/\/proxyserver, indica che il proxy non deve essere utilizzato per gli indirizzi locali e specifica che tutte le richieste ai server presenti nel dominio di contoso.com devono ignorare il server proxy.  
  
```  
<configuration>  
    <system.net>  
        <defaultProxy>  
            <proxy  
                usesystemdefault = "false"  
                proxyaddress = "http://proxyserver:80"  
                bypassonlocal = "true"  
            />  
            <bypasslist>  
                <add address="http://[a-z]+\.contoso\.com/" />  
            </bypasslist>  
        </defaultProxy>  
    </system.net>  
</configuration>  
```  
  
 Utilizzare l'elemento [Elemento \<connectionManagement\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/connectionmanagement-element-network-settings.md) per configurare il numero di connessioni permanenti che possono essere effettuate a uno specifico server o a tutti gli altri server.  Nell'esempio configura l'applicazione per l'utilizzo di due connessioni permanenti a www.contoso.com server, quattro permanenti connessioni al server con l'indirizzo IP 192.168.1.2 e una connessione permanente a tutti gli altri server.  
  
```  
<configuration>  
    <system.net>  
        <connectionManagement>  
            <add address="http://www.contoso.com" maxconnection="2" />  
            <add address="192.168.1.2" maxconnection="4" />  
            <add address="*" maxconnection="1" />  
        </connectionManagement>  
    </system.net>  
</configuration>  
```  
  
 i moduli di autenticazione personalizzati sono configurati con l'elemento [Elemento \<authenticationModules\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/authenticationmodules-element-network-settings.md).  i moduli di autenticazione personalizzati devono implementare l'interfaccia <xref:System.Net.IAuthenticationModule>.  
  
 Nell'esempio seguente viene configurato un modulo di autenticazione personalizzato.  
  
```  
<configuration>  
    <system.net>  
        <authenticationModules>  
            <add type="MyAuthModule, MyAuthModule.dll" />  
        </authenticationModules>  
    </system.net>  
</configuration>  
```  
  
 È possibile utilizzare l'elemento [Elemento \<webRequestModules\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md) per configurare l'applicazione per utilizzare i moduli specifici protocollo personalizzati per richiedere le informazioni nelle risorse Internet.  i moduli specificati devono implementare l'interfaccia <xref:System.Net.IWebRequestCreate>.  È possibile ignorare l'impostazione predefinita HTTP, HTTPS e di richiesta del file specificando il modulo personalizzata nel file di configurazione, come nell'esempio seguente.  
  
```  
<configuration>  
    <system.net>  
        <webRequestModules>  
            <add  
                prefix="HTTP"  
                type = "MyHttpRequest.dll, MyHttpRequestCreator"  
            />  
        </webRequestModules>  
    </system.net>  
</configuration>  
```  
  
## Vedere anche  
 [Programmazione di rete in .NET Framework](../../../docs/framework/network-programming/index.md)   
 [Schema delle impostazioni di rete](../../../docs/framework/configure-apps/file-schema/network/index.md)   
 [Elemento \<system.Net\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)