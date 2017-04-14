---
title: "Selezione e convalida dei certificati | Microsoft Docs"
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
ms.assetid: c933aca2-4cd0-4ff1-9df9-267143f25a6f
caps.latest.revision: 15
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 15
---
# Selezione e convalida dei certificati
Le classi <xref:System.Net> supportano diversi modi per selezionare e convalidare <xref:System.Security.Cryptography.X509Certificates> per le connessioni di Secure Socket Layer \(SSL\).  Un client può selezionare una o più certificati per autenticarsi a un server.  Un server può richiedere che un certificato client presenti uno o più attributi specifici di autenticazione.  
  
## Definizione  
 Un certificato è un flusso di byte ASCII che contiene una chiave pubblica, gli attributi ad esempio il numero di versione, il numero di serie e data di scadenza\) e una firma digitale da un'autorità di certificazione.  I certificati utilizzati per stabilire una connessione crittografata o per autenticare un client a un server.  
  
## Selezione e la convalida del certificato client  
 Un client può selezionare una o più certificati per una connessione SSL specifica.  I certificati client possono essere associati alla connessione SSL a un server web o in un server di posta elettronica SMTP.  Un client aggiunge i certificati a una raccolta <xref:System.Security.Cryptography.X509Certificates.X509Certificate> o di oggetti di classe <xref:System.Security.Cryptography.X509Certificates.X509Certificate2>.  Utilizzo di posta elettronica ad esempio, la raccolta del certificato è un'istanza <xref:System.Security.Cryptography.X509Certificates.X509CertificateCollection>\) associato alla proprietà <xref:System.Net.Mail.SmtpClient.ClientCertificates%2A> della classe <xref:System.Net.Mail.SmtpClient>.  La classe <xref:System.Net.HttpWebRequest> è simile proprietà <xref:System.Net.HttpWebRequest.ClientCertificates%2A>.  
  
 La differenza principale tra <xref:System.Security.Cryptography.X509Certificates.X509Certificate> e la classe <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> è che la chiave privata deve trovarsi nell'archivio certificati per la classe <xref:System.Security.Cryptography.X509Certificates.X509Certificate>.  
  
 Anche se i certificati vengono aggiunti a una raccolta e sono associati a una connessione SSL specifica, certificato non verrà inviato al server a meno che il server li richiedono.  Se i certificati client più sono impostati su una connessione, la migliore verrà utilizzata in base a un algoritmo che prende in considerazione la corrispondenza tra l'elenco di emittenti del certificato forniti dal server e il nome dell'autorità di certificazione client.  
  
 La classe <xref:System.Net.Security.SslStream> fornisce ulteriormente il handshake SSL.  Un client può specificare un delegato per selezionare con certificati client da utilizzare.  
  
 Un server remoto può accadere che un certificato client sia valido, corrente e firmato da un'autorità di certificazione appropriata.  Un delegato può essere aggiunto a <xref:System.Net.ServicePointManager.ServerCertificateValidationCallback%2A> per applicare la convalida del certificato.  
  
## Selezione del certificato client  
 .NET Framework consente di selezionare il certificato client per presentare al server nel modo seguente:  
  
1.  Se un certificato client è stata verificata in precedenza al server, il certificato viene memorizzato nella cache quando viene innanzitutto verificato e viene riutilizzato per le richieste successive del certificato client.  
  
2.  Se un delegato è presente, utilizzare sempre il risultato del delegato come il certificato client per selezionare.  Provare a utilizzare un certificato memorizzato nella cache quando possibile, ma non utilizzare credenziali anonime memorizzate nella cache se il delegato ha restituito null e la raccolta del certificato non è vuota.  
  
3.  Se è la prima richiesta a un certificato client, Framework enumera i certificati in <xref:System.Security.Cryptography.X509Certificates.X509Certificate> o oggetti della classe <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> associati alla connessione, individuare una corrispondenza tra l'elenco di emittenti del certificato forniti dal server e il nome dell'autorità di certificazione client.  Il primo certificato che corrisponde viene inviato al server.  Se non esiste alcuna corrispondenza del certificato o del certificato vuote, pertanto una delle credenziali anonime al server.  
  
## Strumenti per configurare il certificato  
 Una serie di strumenti disponibili per la configurazione di certificati client e server.  
  
 Lo strumento *Winhttpcertcfg.exe* può essere utilizzato per configurare certificati client.  Lo strumento *Winhttpcertcfg.exe* viene fornito come uno degli strumenti Windows Server 2003 Resource Kit.  Questo strumento è disponibile anche download come parte degli strumenti Windows Server 2003 Resource Kit a www.microsoft.com.  
  
 Lo strumento di*Il HttpCfg.exe* può essere utilizzato per configurare certificati server per la classe <xref:System.Net.HttpListener>.  Lo strumento *HttpCfg.exe* viene fornito come uno degli strumenti di supporto per Windows Server 2003 e Windows XP Service Pack 2.  *HttpCfg.exe* e gli altri strumenti di supporto non sono installati per impostazione predefinita in Windows Server 2003 o Windows XP.  Windows Server 2003.  gli strumenti di supporto sono installati separatamente dalle cartelle e file nel CD\- ROM Windows Server 2003:  
  
 \\Support\\Tools\\Suptools.msi  
  
 Per l'utilizzo con Windows XP Service Pack 2, Windows XP gli strumenti è disponibile come download da www.microsoft.com.  
  
 Il codice sorgente a una versione dello strumento *HttpCfg.exe* viene fornito come esempio di Windows Server SDK.  Il codice sorgente dell'esempio *HttpCfg.exe* è installato per impostazione predefinita con esempi di rete come componente di Windows SDK nella cartella seguente:  
  
 *C:\\Program Files\\Microsoft SDKs\\Windows\\v1.0\\Samples\\NetDS\\http\\serviceconfig*  
  
 Oltre a questi strumenti, le classi <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> e <xref:System.Security.Cryptography.X509Certificates.X509Certificate> fornisce metodi per caricare il certificato dal file system.  
  
## Vedere anche  
 [Sicurezza in programmazione di rete](../../../docs/framework/network-programming/security-in-network-programming.md)   
 [Programmazione di rete in .NET Framework](../../../docs/framework/network-programming/index.md)