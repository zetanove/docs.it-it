---
title: "Informazioni su problemi ed eccezioni di WebRequest | Microsoft Docs"
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
ms.assetid: 74a361a5-e912-42d3-8f2e-8e9a96880a2b
caps.latest.revision: 6
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# Informazioni su problemi ed eccezioni di WebRequest
<xref:System.Net.WebRequest> e le relative classi derivate \(<xref:System.Net.HttpWebRequest>, <xref:System.Net.FtpWebRequest>e <xref:System.Net.FileWebRequest>\) generano eccezioni per segnalare lo stato anomala.  Talvolta la risoluzione di questi problemi non è ovvio.  
  
## Soluzioni  
 Esaminare la proprietà <xref:System.Net.WebException.Status%2A><xref:System.Net.WebException> per determinare il problema.  Nella tabella seguente vengono illustrati diversi valori dello stato e alcune possibili soluzioni.  
  
|Stato|Dettagli|Soluzione|  
|-----------|--------------|---------------|  
|<xref:System.Net.WebExceptionStatus><br /><br /> In alternativa<br /><br /> <xref:System.Net.WebExceptionStatus>|Esiste un problema con il socket sottostante.  La connessione venga reimpostata.|Riconnettere e inviare la richiesta.<br /><br /> Assicurarsi dell'ultimo Service Pack sia installato.<br /><br /> Aumentare il valore della proprietà <xref:System.Net.ServicePointManager.MaxServicePointIdleTime%2A?displayProperty=fullName>.<br /><br /> Impostare la proprietà <xref:System.Net.HttpWebRequest.KeepAlive%2A?displayProperty=fullName> su `false`.<br /><br /> Aumentare il numero massimo di connessioni dalla proprietà <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A>.<br /><br /> Verificare la configurazione del proxy.<br /><br /> Se tramite SSL, assicurarsi che il processo server disponga di autorizzazioni per accedere all'archivio certificati.<br /><br /> Se inviando grandi quantità di dati, impostare <xref:System.Net.HttpWebRequest.AllowWriteStreamBuffering%2A> a `false`.|  
|<xref:System.Net.WebExceptionStatus>|Il certificato server potrebbe non essere convalidati.|Si tenta di aprire l'uri che utilizza Internet Explorer.  Risolvere eventuali avvisi di sicurezza visualizzato da e.  Se non è possibile risolvere il problema di sicurezza, è possibile creare una classe di certificato che implementa <xref:System.Net.ICertificatePolicy> che restituisce `true`e lo passa a <xref:System.Net.ServicePointManager.CertificatePolicy%2A>.<br /><br /> Vedere. [http:\/\/support.microsoft.com\/?id\=823177](http://go.microsoft.com/fwlink/?LinkID=179653)<br /><br /> Assicurarsi che il certificato dell'Autorità di certificazione che ha firmato il certificato server venga aggiunto all'elenco attendibile da un'autorità di certificazione in Internet Explorer.<br /><br /> Assicurarsi che il nome host in URL corrisponda al nome comune al certificato server.|  
|<xref:System.Net.WebExceptionStatus>|Si è verificato un errore nella transazione di SSL, o esiste un problema del certificato.|La versione 3,0 di supporta SSL .NET Framework versione 1.1 solo.  Se il server utilizza solo la versione 1,0 di TLS o la versione 2,0 di SSL, viene generata l'eccezione.  Aggiornamento a.NET Framework 2.0 e set <xref:System.Net.ServicePointManager.SecurityProtocol%2A> in base al server.<br /><br /> Il certificato del client è stato firmato da un'autorità di certificazione \(CA\) del server non è attendibile.  Installare il certificato CA sul server.  Vedere [http:\/\/support.microsoft.com\/?id\=332077](http://go.microsoft.com/fwlink/?LinkID=179654).<br /><br /> Assicurarsi di disporre dell'ultimo Service Pack che sia installato.|  
|<xref:System.Net.WebExceptionStatus>|Connessione non riuscita.|Un firewall o un proxy blocca la connessione.  Modificare il firewall o il proxy per consentire la connessione.<br /><br /> Definire in modo esplicito <xref:System.Net.WebProxy> nell'applicazione client chiamando il costruttore <xref:System.Net.WebProxy> \(\= WebServiceProxyClass.Proxy nuovi WebProxy true \([http:\/\/server:80](http://server/),\).<br /><br /> Eseguire Filemon o Regmon per verificare che l'identità del processo di lavoro dispone delle autorizzazioni necessarie per accedere a WSPWSP.dll, HKLM\\System\\CurrentControlSet\\Services\\DnsCache o HKLM\\System\\CurrentControlSet\\Services\\WinSock2.|  
|<xref:System.Net.WebExceptionStatus>|Il servizio del nome di dominio non può risolvere il nome host.|Configurare il proxy correttamente.  Vedere [http:\/\/support.microsoft.com\/?id\=318140](http://go.microsoft.com/fwlink/?LinkID=179655).<br /><br /> Assicurarsi che nessun software antivirus o firewall installato non blocca la connessione.|  
|<xref:System.Net.WebExceptionStatus>|<xref:System.Net.WebRequest.Abort%2A> è stato chiamato, oppure si è verificato un errore.|Questo problema potrebbe essere causata da un carico pesante nel client o sul server.  Ridurre il carico.<br /><br /> Aumentare l'impostazione <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A>.<br /><br /> Per modificare [http:\/\/support.microsoft.com\/?id\=821268](http://go.microsoft.com/fwlink/?LinkID=179656) le impostazioni di prestazioni del servizio Web.|  
|<xref:System.Net.WebExceptionStatus>|L'applicazione ha tentato di scrivere in un socket che è già stato chiuso.|Il client o nel server è sottoposto a overload.  Ridurre il carico.<br /><br /> Aumentare l'impostazione <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A>.<br /><br /> Per modificare [http:\/\/support.microsoft.com\/?id\=821268](http://go.microsoft.com/fwlink/?LinkID=179656) le impostazioni di prestazioni del servizio Web.|  
|<xref:System.Net.WebExceptionStatus>|Il limite impostato su \(<xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A>\) sulla lunghezza di messaggio è stato superato.|Aumentare il valore della proprietà <xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A>.|  
|<xref:System.Net.WebExceptionStatus>|Il servizio del nome di dominio non può risolvere il nome host del proxy.|Configurare il proxy correttamente.  Vedere [http:\/\/support.microsoft.com\/?id\=318140](http://go.microsoft.com/fwlink/?LinkID=179655).<br /><br /> Per forzare chiamate ripetute <xref:System.Net.HttpWebRequest> non utilizzare proxy impostando la proprietà <xref:System.Net.HttpWebRequest.Proxy%2A> a `null`.|  
|<xref:System.Net.WebExceptionStatus>|La risposta dal server non è una risposta HTTP valida.  Questo problema si verifica quando .NET Framework viene rilevato che la risposta server non conforme allo standard RFC HTTP 1.1.  Questo problema può verificarsi quando la risposta contiene corrette intestazioni o l'errata intestazione delimiters.RFC 2616 definisce HTTP 1.1 e il formato valido per la risposta dal server.  Per ulteriori informazioni, vedere [http:\/\/www.ietf.org](http://go.microsoft.com/fwlink/?LinkID=147388).|Ottenere un'analisi di rete della transazione ed esaminare le intestazioni della risposta.<br /><br /> Se l'applicazione richiede la risposta server senza analisi \(si potrebbe costituire un problema di sicurezza\), impostare `useUnsafeHeaderParsing` a `true` nel file di configurazione.  Vedere [Elemento \<httpWebRequest\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/httpwebrequest-element-network-settings.md).|  
  
## Vedere anche  
 <xref:System.Net.HttpWebRequest>   
 <xref:System.Net.HttpWebResponse>   
 <xref:System.Net.Dns>