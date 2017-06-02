---
title: "Procedura: Configurare la tracciatura della rete | Microsoft Docs"
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
  - "app.config (file), tracciatura della rete"
  - "file di configurazione dell'applicazione, tracciatura della rete"
  - "file di configurazione [.NET Framework], tracciatura della rete"
  - "formattazione [.NET Framework], tracciatura della rete"
  - "attributo livello"
  - "tracciatura della rete, configurazione"
  - "di output di tracciatura a livello di protocollo"
  - "socket, l'output di traccia"
ms.assetid: 5ef9fe4b-8d3d-490e-9259-1d014b2181af
caps.latest.revision: 23
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 23
---
# Procedura: Configurare la tracciatura della rete
Nel file di configurazione del computer o dell'applicazione sono contenute le impostazioni che determinano il formato e il contenuto delle tracce di rete. Prima di eseguire questa procedura, assicurarsi che la funzionalità di traccia sia abilitata. Per informazioni su come abilitare la traccia, vedere [Abilitazione della traccia di rete](../../../docs/framework/network-programming/enabling-network-tracing.md).  
  
 Il file di configurazione del computer, machine.config, è memorizzato nella cartella %Windir%\\Microsoft.NET\\Framework nella directory in cui è installato Windows. Esiste un file machine.config separato nelle cartelle %Windir%\\Microsoft.NET\\Framework per ogni versione di .NET Framework installata nel computer, ad esempio C:\\WINDOWS\\Microsoft.NET\\Framework\\v2.0.50727\\machine.config.  
  
 Queste impostazioni possono essere effettuate anche nel file di configurazione dell'applicazione, che ha la precedenza sul file di configurazione del computer.  
  
### Per configurare la traccia di rete  
  
-   Aggiungere le seguenti righe al file di configurazione appropriato. I valori e le opzioni per queste impostazioni sono descritti nelle tabelle riportate di seguito.  
  
    ```  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <source name="System.Net" tracemode="includehex" maxdatasize="1024">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
          <source name="System.Net.Cache">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
          <source name="System.Net.Http">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
          <source name="System.Net.Sockets">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
          <source name="System.Net.WebSockets">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="System.Net" value="Verbose"/>  
          <add name="System.Net.Cache" value="Verbose"/>  
          <add name="System.Net.Http" value="Verbose"/>  
          <add name="System.Net.Sockets" value="Verbose"/>  
          <add name="System.Net.WebSockets" value="Verbose"/>  
        </switches>  
        <sharedListeners>  
          <add name="System.Net"  
            type="System.Diagnostics.TextWriterTraceListener"  
            initializeData="network.log"  
          />  
        </sharedListeners>  
        <trace autoflush="true"/>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
 Quando si aggiunge un nome al blocco `<switches>`, l'output di traccia include informazioni da alcuni metodi correlati al nome. Nella tabella riportata di seguito viene descritto l'output.  
  
|Nome|Output da|  
|----------|---------------|  
|`System.Net.Sockets`|Alcuni metodi pubblici delle classi <xref:System.Net.Sockets.Socket>, <xref:System.Net.Sockets.TcpListener>, <xref:System.Net.Sockets.TcpClient> e <xref:System.Net.Dns>|  
|`System.Net`|Alcuni metodi pubblici delle classi <xref:System.Net.HttpWebRequest>, <xref:System.Net.HttpWebResponse>, <xref:System.Net.FtpWebRequest> e <xref:System.Net.FtpWebResponse> e informazioni sul debug SSL \(certificati non validi, elenco di autorità emittenti mancante ed errori di certificato del client\).|  
|`System.Net.HttpListener`|Alcuni metodi pubblici delle classi <xref:System.Net.HttpListener>, <xref:System.Net.HttpListenerRequest> e <xref:System.Net.HttpListenerResponse>.|  
|`System.Net.Cache`|Alcuni metodi interni e privati in `System.Net.Cache`.|  
|`System.Net.Http`|Alcuni metodi pubblici delle classi <xref:System.Net.Http.HttpClient>, <xref:System.Net.Http.DelegatingHandler>, <xref:System.Net.Http.HttpClientHandler>, <xref:System.Net.Http.HttpMessageHandler>, <xref:System.Net.Http.MessageProcessingHandler> e <xref:System.Net.Http.WebRequestHandler>.|  
|`System.Net.WebSockets.WebSocket`|Alcuni metodi pubblici delle classi <xref:System.Net.WebSockets.ClientWebSocket> e <xref:System.Net.WebSockets.WebSocket>.|  
  
 Gli attributi elencati nella tabella seguente sono utilizzati per configurare l'output di traccia.  
  
|Nome attributo|Valore attributo|  
|--------------------|----------------------|  
|`Value`|Attributo <xref:System.String> obbligatorio. Imposta il livello di dettaglio dell'output. I valori consentiti sono `Critical`, `Error`, `Verbose`, `Warning` e `Information`.<br /><br /> Questo attributo deve essere impostato sull'elemento \<add name\> dell'elemento \<switches\> come mostrato nell'esempio. Viene generata un'eccezione se l'attributo è impostato sull'elemento \<source\>.|  
|`maxdatasize`|Attributo <xref:System.Int32> facoltativo. Imposta il numero massimo di byte di dati di rete inclusi in ogni traccia di riga. Il valore predefinito è 1024.<br /><br /> Questo attributo deve essere impostato sull'elemento \<source\> come mostrato nell'esempio. Viene generata un'eccezione se questo attributo è impostato su un elemento sotto l'elemento \<switches\>.|  
|`Tracemode`|Attributo <xref:System.String> facoltativo. Impostare su `includehex` per visualizzare le tracce del protocollo nel formato esadecimale e di testo. Impostare su `protocolonly` per mostrare solo testo. Il valore predefinito è `includehex`.<br /><br /> Questo attributo deve essere impostato sull'elemento \<switches\> come mostrato nell'esempio. Viene generata un'eccezione se questo attributo è impostato su un elemento sotto l'elemento \<source\>.|  
  
## Vedere anche  
 [Interpretazione della traccia di rete](../../../docs/framework/network-programming/interpreting-network-tracing.md)   
 [Tracciatura di rete in .NET Framework](../../../docs/framework/network-programming/network-tracing.md)   
 [Abilitazione della traccia di rete](../../../docs/framework/network-programming/enabling-network-tracing.md)   
 [Introduzione alla strumentazione e alla traccia](http://msdn.microsoft.com/it-it/e924e57c-33cf-4b0e-9e7f-a45d13e38f2c)