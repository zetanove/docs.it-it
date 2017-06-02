---
title: "Attraversamento NAT con IPv6 e Teredo | Microsoft Docs"
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
ms.assetid: 568cd245-3300-49ef-a995-d81bf845d961
caps.latest.revision: 6
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# Attraversamento NAT con IPv6 e Teredo
I miglioramenti sono stati fatti che forniscono il supporto per l'attraversamento di \(NAT\) di conversione indirizzo di rete.  Queste modifiche sono progettate per l'utilizzo con la IPv6 e Teredo, ma sono applicabili anche ad altre tecnologie di tunneling IP.  Questi miglioramenti influiscono sulle classi in <xref:System.Net> e gli spazi dei nomi correlati.  
  
 Tali modifiche possono influire sulle applicazioni client e server che decidere di utilizzare tecnologie di tunneling IP.  
  
 Le modifiche all'attraversamento NAT di supporto sono disponibili solo per le applicazioni con.NET Framework versione 4.  Queste funzionalità non disponibili nelle versioni precedenti di .NET Framework.  
  
## Panoramica  
 La versione 4 \(IPv4\) del protocollo internet ha definito da un indirizzo IPv4 come 32 bit.  Pertanto, in l IPv4 supporta su 4 miliardi di indirizzi IP univoci \(2^32\).  Come numero di computer e dispositivi di rete su Internet espanso negli anni 90, i limiti dello spazio degli indirizzi IPv4 sono divengono evidenti.  
  
 Una delle numerose tecniche utilizzate per estendere la durata dell'IPv4 è stata di implementare il NAT per consentire a un singolo indirizzo IP pubblico univoco rappresenti un numero elevato di indirizzi IP privati \(Intranet privato\).  Gli indirizzi IP privati del dispositivo di NAT condividono il singolo indirizzo pubbliche IPv4.  Il dispositivo di NAT può essere un dispositivo hardware dedicato \(un punto di accesso wireless e un router economici, ad esempio\) o un computer che esegue un servizio per fornire il NAT.  Un dispositivo o un servizio per questo indirizzo IP pubblico converte i pacchetti di rete IP tra l'area Intranet pubbliche e private.  
  
 Questo schema è appropriato per le applicazioni client in esecuzione su una rete Intranet privato che invia richieste agli indirizzi IP \(in genere server\) in Internet.  Il dispositivo o il server di NAT può mantenere un mapping delle richieste del client quando una risposta le viene restituita conosce dove inviare la risposta.  Ma questa combinazione pone problemi per le applicazioni eseguite in Internet privato del dispositivo di NAT che desiderano fornire servizi, attendono pacchetti e rispondono.  Ciò è particolarmente l'argomento per le applicazioni peer\-to\-peer.  
  
 Il protocollo IPv6 definita lungo un indirizzo IPv4 come 128 bit.  Pertanto, il IPv6 supporta molto grande spazio degli indirizzi IP di indirizzi univoci 3,2 x 10^38 \(2^128\).  Con lo spazio degli indirizzi di questa dimensione, è possibile per ogni dispositivo connesso a Internet da fornire un indirizzo univoco.  Esistono problemi.  Gran parte del mondo continua a utilizzare solo il IPv4.  In particolare, molti router esistenti e i punti di accesso wireless utilizzati dalle piccole imprese, le organizzazioni e da quelli non supportano in IPv6.  Anche alcuni provider di servizi Internet che eseguono i clienti non supportano o non hanno configurato il supporto per IPv6.  
  
 Diverse tecnologie di transizione IPv6 compilate eventi di tunneling gli indirizzi IPv6 in un pacchetto IPv4.  Queste tecnologie sono 6to4, ISATAP e di tunneling di Teredo che forniscono l'assegnazione e host \(host di indirizzo tunneling automatico per il traffico unicast IPv6 quando gli host IPv6 devono superare le reti IP4 per ottenere altre reti IPv6.  I pacchetti IPv6 vengono inviati con scavato il tunneling come pacchetti IPv4.  Diverse tecniche di tunneling vengono utilizzati che consentono all'attraversamento NAT per gli indirizzi IPv6 da un dispositivo di NAT.  
  
 Il Teredo è una delle tecnologie di transizione IPv6 che porta la connettività IPv6 reti IPv4.  Il Teredo è documentato nello standard RFC 4380 pubblicato da Internet Engineering Task Force \(IETF\).  In Windows XP SP2 e versioni successive forniscono il supporto per un adattatore virtuale di Teredo che può fornire un indirizzo IPv6 pubblico nell'intervallo 2001:0::\/32.  Questo indirizzo IPv6 può essere utilizzato per ascoltare le connessioni in ingresso da Internet e può essere fornito ai client abilitati IPv6 che devono connettersi al servizio in ascolto.  Si libera un'applicazione da considerare eventuali come destinazione un computer protetto da un dispositivo di NAT, poiché l'applicazione può connettersi a tramite il relativo indirizzo di tipo Teredo IPv6.  
  
## Miglioramenti per supportare attraversamento NAT e Teredo  
 Miglioramenti vengono aggiunti a <xref:System.Net>, a <xref:System.Net.NetworkInformation>agli spazi dei nomi <xref:System.Net.Sockets> dell'attraversamento NAT supporto mediante IPv6 e Teredo.  
  
 Diversi metodi vengono aggiunti alla classe <xref:System.Net.NetworkInformation.IPGlobalProperties?displayProperty=fullName> per ottenere l'elenco di indirizzi IP unicasthost.  Inizia al metodo <xref:System.Net.NetworkInformation.IPGlobalProperties.BeginGetUnicastAddresses%2A> una richiesta asincrona di recuperare la tabella di indirizzi IP unicast stabili nel computer locale.  Fine del metodo <xref:System.Net.NetworkInformation.IPGlobalProperties.EndGetUnicastAddresses%2A> di una richiesta asincrona in attesa di recuperare la tabella di indirizzi IP unicast stabili nel computer locale.  Il metodo <xref:System.Net.NetworkInformation.IPGlobalProperties.GetUnicastAddresses%2A> è una richiesta sincrona di recuperare la tabella di indirizzi IP unicast stabili nel computer locale, in attesa finché la tabella address non si stabilizzare se necessario.  
  
 La proprietà <xref:System.Net.IPAddress.IsIPv6Teredo%2A?displayProperty=fullName> può essere utilizzata per determinare se <xref:System.Net.IPAddress> è un indirizzo di tipo Teredo IPv6.  
  
 Utilizzando questi nuovi metodi della classe <xref:System.Net.NetworkInformation.IPGlobalProperties> combinate alla proprietà <xref:System.Net.IPAddress.IsIPv6Teredo%2A> consente a un'applicazione trovare facilmente l'indirizzo di tipo Teredo.  Un'applicazione è in genere sufficiente conoscere l'indirizzo di tipo Teredo locale se vengono passate queste informazioni alle applicazioni remote.  Ad esempio, un'applicazione peer\-to\-peer può inviare tutti gli indirizzi IPv6 in un server di schema che può quindi inoltrarli ad altri scruta per consentire la comunicazione diretta.  
  
 Un'applicazione deve in genere impostarne il servizio in ascolto di ascolto su <xref:System.Net.IPAddress.IPv6Any?displayProperty=fullName> anziché l'indirizzo di tipo Teredo locale.  Se pertanto un client remoto o un peer ha una route mediante IPv6 all'host del servizio in ascolto, il client o il peer può connettersi direttamente mediante IPv6 e non devono utilizzare il Teredo eventi di tunneling pacchetti.  
  
 Per le applicazioni TCP, la classe <xref:System.Net.Sockets.TcpListener?displayProperty=fullName> dispone di un metodo <xref:System.Net.Sockets.TcpListener.AllowNatTraversal%2A> per consentire all'attraversamento NAT.  Per le applicazioni di UDP, la classe <xref:System.Net.Sockets.UdpClient?displayProperty=fullName> dispone di un metodo <xref:System.Net.Sockets.UdpClient.AllowNatTraversal%2A> per consentire all'attraversamento NAT.  
  
 Per le applicazioni che utilizzano <xref:System.Net.Sockets.Socket?displayProperty=fullName> e le classi correlate, è <xref:System.Net.Sockets.Socket.GetSocketOption%2A> e i metodi <xref:System.Net.Sockets.Socket.SetSocketOption%2A> possono essere utilizzati con l'opzione di socket <xref:System.Net.Sockets.SocketOptionName?displayProperty=fullName> eseguire una query, abilitare, disabilitare o attraversamento NAT.  
  
## Vedere anche  
 <xref:System.Net.IPAddress.IsIPv6Teredo%2A?displayProperty=fullName>   
 <xref:System.Net.NetworkInformation.IPGlobalProperties.BeginGetUnicastAddresses%2A?displayProperty=fullName>   
 <xref:System.Net.NetworkInformation.IPGlobalProperties.EndGetUnicastAddresses%2A?displayProperty=fullName>   
 <xref:System.Net.NetworkInformation.IPGlobalProperties.GetUnicastAddresses%2A?displayProperty=fullName>   
 <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=fullName>   
 <xref:System.Net.Sockets.Socket.SetIPProtectionLevel%2A?displayProperty=fullName>   
 <xref:System.Net.Sockets.TcpListener.AllowNatTraversal%2A?displayProperty=fullName>   
 <xref:System.Net.Sockets.UdpClient.AllowNatTraversal%2A?displayProperty=fullName>