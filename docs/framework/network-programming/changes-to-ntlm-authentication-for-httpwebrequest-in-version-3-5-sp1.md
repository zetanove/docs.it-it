---
title: "Modifiche apportate all&#39;autenticazione NTLM per HttpWebRequest nella versione 3.5 SP1 | Microsoft Docs"
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
ms.assetid: 8bf0b428-5a21-4299-8d6e-bf8251fd978a
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# Modifiche apportate all&#39;autenticazione NTLM per HttpWebRequest nella versione 3.5 SP1
Le modifiche di sicurezza apportate in .NET Framework versione 3.5 SP1 e versioni successive che influenzano l'autenticazione integrata di Windows è gestita da <xref:System.Net.HttpWebRequest>, da <xref:System.Net.HttpListener>, da <xref:System.Net.Security.NegotiateStream>e le classi correlate nello spazio dei nomi di System.Net.  Tali modifiche possono influire sulle applicazioni che utilizzano queste classi per effettuare richieste Web e ricevere le risposte in cui l'autenticazione integrata di Windows basata su NTLM.  Questa modifica può influire sui server web e applicazioni client configurati per utilizzare l'autenticazione integrata di Windows.  
  
## Panoramica  
 La progettazione di autenticazione integrata di Windows consente l'invio delle risposte credenziali sia universale, caratteristica può essere riutilizzata o inoltrata.  Se questa caratteristica di progetto specifico non è necessaria, i protocolli di autenticazione devono portare le informazioni specifiche di destinazione e incanalare informazioni specifiche.  I servizi possono quindi garantire la protezione estesa per assicurarsi che le risposte credenziali contengono informazioni specifiche del servizio come un nome principale \(SPN\) di servizio.  Con queste informazioni negli scambi credenziali, i servizi è consigliabile proteggere impieghi dannosi risposte credenziali che potrebbe erroneamente essere ottenute.  
  
 Più componenti in <xref:System.Net> e gli spazi dei nomi <xref:System.Net.Security> eseguono l'autenticazione integrata di Windows per un'applicazione chiamante.  Questa sezione descrive le modifiche ai componenti di System.Net per aggiungere la protezione estesa nel relativo utilizzo di autenticazione integrata di Windows.  
  
## Modifiche  
 Il processo di autenticazione NTLM utilizzato con l'autenticazione integrata di Windows include una sfida pubblicata dal computer di destinazione e rinviata al computer client.  Quando un computer riceve una richiesta che ha generato, l'autenticazione non funzionerà a meno che la connessione sia una connessione a " loopback " \(IPv4 indirizzo 127.0.0.1, ad esempio\).  
  
 Quando si accede a un servizio in un server Web interno, è normale accedere al servizio utilizzando un URL simile a http:\/\/contoso\/service o https:\/\/contoso\/service.  Il nome “contoso„ non è spesso il nome computer del computer sul quale il servizio viene distribuito.  <xref:System.Net> e il supporto correlato di spazi dei nomi mediante Active Directory, il DNS, di Netbios, il file visitatori del computer locale \(in genere WINDOWS\\system32\\drivers\\etc\\hosts, ad esempio\), o del file di lmhosts del computer locale \(in genere WINDOWS\\system32\\drivers\\etc\\lmhosts, ad esempio\) per risolvere i nomi indirizzi.  Il nome “contoso„ viene risolto in modo da inviare richieste inviate a “contoso„ sul computer server appropriato.  
  
 Una volta configurato per le distribuzioni grandi dimensioni, è comune per un singolo nome del Server virtuale viene fornito alla distribuzione con i nomi di computer e non utilizzare mai da applicazioni client e degli utenti finali.  Ad esempio, è possibile chiamare semplicemente www.contoso.com server, ma in un utilizzo “contoso di rete interna.  Questo nome viene chiamato l'intestazione host nella richiesta Web client.  Come specificato dal protocollo HTTP, il campo di intestazione di richiesta host specifica l'host Internet e il numero di porta della risorsa richiesta.  Queste informazioni vengono ottenute dall'URI di originale fornito dall'utente o che fa riferimento alla risorsa \(in genere un URL HTTP\).  In .NET Framework versione 4, queste informazioni possono essere impostate dal client mediante la nuova proprietà <xref:System.Net.HttpWebRequest.Host%2A>.  
  
 La classe <xref:System.Net.AuthenticationManager> controlla i componenti serviti di autenticazione \(“modulo„\) utilizzate dalle classi derivate <xref:System.Net.WebRequest> e la classe <xref:System.Net.WebClient>.  La classe <xref:System.Net.AuthenticationManager> fornisce una proprietà che espone un oggetto <xref:System.Net.AuthenticationManager.CustomTargetNameDictionary%2A?displayProperty=fullName>, indicizzata dalla stringa dell'URI, per le applicazioni fornire una stringa di SPN personalizzato da utilizzare durante l'autenticazione.  
  
 Le impostazioni predefinite della versione 3.5 SP1 consentono di specificare il nome host utilizzato nell'URL della richiesta in SPN nello scambio di autenticazione NTLM \(Windows NT LAN Manager\) quando non è impostata la proprietà <xref:System.Net.AuthenticationManager.CustomTargetNameDictionary%2A>.  È possibile che il nome host utilizzato nell'URL della richiesta sia diverso dall'intestazione host specificata nell'oggetto <xref:System.Net.HttpRequestHeader?displayProperty=fullName> nella richiesta del client.  È possibile che il nome host utilizzato nell'URL della richiesta sia diverso dal nome host effettivo del server, dal nome del computer del server, dall'indirizzo IP del computer o dall'indirizzo di loopback.  In questi casi, Windows non completerà la richiesta di autenticazione.  Per risolvere il problema, è necessario informare Windows che il nome host utilizzato nell'URL della richiesta nella richiesta del client \(“contoso„, ad esempio\) è effettivamente un nome alternativo per il computer locale.  
  
 Esistono diversi metodi possibili di un'applicazione server possa risolvere questa modifica.  È consigliabile eseguire il mapping del nome host utilizzato nell'URL della richiesta a `BackConnectionHostNames` chiavi del Registro di sistema nel server.  La chiave del Registro di sistema `BackConnectionHostNames` viene generalmente utilizzata per associare il nome host a un indirizzo di loopback.  I passaggi sono elencati in.  
  
 Per specificare i nomi host mappati all'indirizzo di loopback e possono connettersi ai siti Web in un computer locale, seguire questi passaggi:  
  
 1.  Fare clic sul pulsante Start, scegliere Esegui, digitare regedit, quindi scegliere OK.  
  
 2.  Nell'editor del Registro di sistema, individuare e fare clic sulla seguente chiave del Registro di sistema:  
  
 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\MSV1_0`  
  
 3.  Fare clic con il pulsante destro del mouse MSV1\_0, scegliere nuovo quindi fare clic sul valore di più Stringhe.  
  
 4.  Digitare `BackConnectionHostNames`, quindi premere INVIO.  
  
 5.  Fare clic con il pulsante destro del mouse `BackConnectionHostNames`quindi scegliere modifica.  
  
 6.  Nella casella Dati valore, digitare il nome host o nomi host per i siti \(il nome host utilizzato nell'URL della richiesta\) che si trova sul computer locale e fare clic su OK.  
  
 7.  Termini l'editor del Registro di sistema e quindi riavviare il servizio di IISAdmin e IISReset eseguito.  
  
 Minore lavoro sicuro che è possibile disabilitare il controllo di " loopback ", come descritto [http:\/\/support.microsoft.com\/kb\/896861](http://go.microsoft.com/fwlink/?LinkID=179657)in.  Si disabilita la protezione contro gli attacchi di reflection.  Pertanto è preferibile limitare il set di nomi alternativi solo a quelli che si prevede che il computer effettivamente da utilizzare.  
  
## Vedere anche  
 <xref:System.Net.AuthenticationManager.CustomTargetNameDictionary%2A?displayProperty=fullName>   
 <xref:System.Net.HttpRequestHeader?displayProperty=fullName>   
 <xref:System.Net.HttpWebRequest.Host%2A?displayProperty=fullName>