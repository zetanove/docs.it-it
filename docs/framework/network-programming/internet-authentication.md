---
title: "Autenticazione Internet | Microsoft Docs"
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
  - "autenticazione [.NET Framework], classi"
  - "IAuthenticationModule (interfaccia)"
  - "ICredentialLookup (interfaccia)"
  - "CredentialCache (classe), informazioni"
  - "ricezione di dati, autenticazione"
  - "AuthenticationManager (classe), informazioni"
  - "Internet, autenticazione"
  - "invio di dati, autenticazione"
  - "risorse di rete, autenticazione"
  - "autenticazione utente, classi per l'autenticazione"
  - "NetworkCredential (classe), informazioni"
  - "autenticazione client, classi per l'autenticazione"
ms.assetid: d342e87c-f672-4660-a513-41a2f2b80c4a
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Autenticazione Internet
Le classi <xref:System.Net> supportano diversi meccanismi di autenticazione del client, inclusi la base standard di metodi di autenticazione Internet, digeriscono, negoziano, NTLM e Kerberos e metodi personalizzati creati.  
  
 Le credenziali di autenticazione viene archiviato nelle classi <xref:System.Net.CredentialCache> e <xref:System.Net.NetworkCredential>, che implementano l'interfaccia <xref:System.Net.ICredentials>.  Quando una di queste classi è possibile eseguire una query per le credenziali, restituisce un'istanza della classe **NetworkCredential**.  Il processo di autenticazione è gestito dalla classe <xref:System.Net.AuthenticationManager> e il processo di autenticazione viene eseguito da una classe del modulo di autenticazione che implementa l'interfaccia <xref:System.Net.IAuthenticationModule>.  È necessario registrare un modulo di autenticazione personalizzato con **AuthenticationManager** poter utilizzare; i moduli per la base, digest, negoziano, NTLM e i metodi di autenticazione Kerberos sono registrati per impostazione predefinita.  
  
 **NetworkCredential** archivia un set di credenziali associate a una singola risorsa Internet identificata da un URI e vengono restituiti in risposta a qualsiasi chiamata al metodo <xref:System.Net.NetworkCredential.GetCredential%2A>.  La classe **NetworkCredential** in genere utilizzata dalle applicazioni che accedono a un numero limitato delle risorse Internet o da applicazioni che utilizzano lo stesso set di credenziali in tutti i casi.  
  
 La classe **CredentialCache** contiene una raccolta di credenziali per varie risorse Web.  Quando il metodo <xref:System.Net.CredentialCache.GetCredential%2A> viene chiamato, **CredentialCache** restituisce l'insieme corretto di credenziali, come determinato dall'URI della risorsa Web e dello schema di autenticazione richiesto.  Le applicazioni che utilizzano diverse risorse Internet con diversi schemi di autenticazione traggono vantaggio di utilizzare la classe **CredentialCache**, poiché archivia tutte le credenziali e offre come richiesto.  
  
 Quando una risorsa Internet richiede l'autenticazione, il metodo <xref:System.Net.WebRequest.GetResponse%2A?displayProperty=fullName> invia <xref:System.Net.WebRequest> a **AuthenticationManager** con la richiesta per le credenziali.  La richiesta viene autenticata come il seguente processo:  
  
1.  **AuthenticationManager** chiama il metodo <xref:System.Net.IAuthenticationModule.Authenticate%2A> su ciascun form di autenticazione registrati nell'ordine in cui sono stati registrati.  **AuthenticationManager** utilizza il primo modulo che non restituisce **null** per effettuare il processo di autenticazione.  I dettagli del processo variano a seconda del tipo di form di autenticazione utilizzati.  
  
2.  Quando il processo di autenticazione è completo, il modulo di autenticazione restituisce <xref:System.Net.Authorization> a **WebRequest** che contiene le informazioni necessarie per accedere alla risorsa Internet.  
  
 Alcuni schemi di autenticazione è possibile autenticare un utente senza prima eseguire una richiesta per una risorsa.  Un'applicazione può risparmiare tempo preauthenticating l'utente con la risorsa, eliminando così almeno un round trip al server.  In alternativa, può eseguire successivamente l'autenticazione durante l'avvio del programma sia più rispondente all'utente.  Gli schemi di autenticazione che possono utilizzare il preauthentication impostare la proprietà [CanPreAuthenticate](frlrfsystemnetiauthenticationmoduleclasspreauthenticatetopic) a **true**.  
  
## Vedere anche  
 [Autenticazione di base e del digest](../../../docs/framework/network-programming/basic-and-digest-authentication.md)   
 [Autenticazione NTLM e Kerberos](../../../docs/framework/network-programming/ntlm-and-kerberos-authentication.md)   
 [Sicurezza in programmazione di rete](../../../docs/framework/network-programming/security-in-network-programming.md)