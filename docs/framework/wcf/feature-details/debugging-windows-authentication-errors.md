---
title: "Debug degli errori di autenticazione di Windows | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF, autenticazione"
  - "WCF, Autenticazione di Windows"
ms.assetid: 181be4bd-79b1-4a66-aee2-931887a6d7cc
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Debug degli errori di autenticazione di Windows
Quando si utilizza l'autenticazione di Windows come meccanismo di sicurezza, i processi di sicurezza vengono gestiti dall'interfaccia SSPI \(Security Support Provider Interface\).Se si verificano errori di sicurezza a livello SSPI, questi vengono riportati da [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].In questo argomento viene fornito un framework e un insieme di domande per facilitare la diagnosi degli errori.  
  
 Per una panoramica sul protocollo Kerberos, vedere [Kerberos Explained](http://go.microsoft.com/fwlink/?LinkID=86946) \(la pagina potrebbe essere in inglese\), per una panoramica su SSPI, vedere [SSPI](http://go.microsoft.com/fwlink/?LinkId=88941).  
  
 Per l'autenticazione di Windows, in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene in genere utilizzato Security Support Provider \(SSP\) *negoziato*, che esegue l'autenticazione reciproca Kerberos tra il client e il servizio.Se il protocollo Kerberos non è disponibile, per impostazione predefinita [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] esegue il fallback al protocollo NTLM \(NT LAN Manager\).È tuttavia possibile configurare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per utilizzare solo il protocollo Kerberos e viene generata un'eccezione se Kerberos non è disponibile.È inoltre possibile configurare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per utilizzare formati con restrizioni del protocollo Kerberos.  
  
## Metodologia di debug  
 Il metodo di base è il seguente:  
  
1.  Determinare se si sta utilizzando l'autenticazione di Windows.Se si sta utilizzando qualsiasi altro schema, questo argomento non è applicabile.  
  
2.  Se si sta utilizzando con certezza l'autenticazione di Windows, determinare se la configurazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza Kerberos direttamente o Negotiate.  
  
3.  Una volta determinato se la configurazione utilizza il protocollo Kerberos o NTLM, è possibile comprendere i messaggi di errore nel contesto giusto.  
  
### Disponibilità del protocollo Kerberos e NTLM  
 Per l'SSP Kerberos è necessario un controller di dominio che agisca da Centro di distribuzione chiave Kerberos \(KDC, Kerberos Key Distribution Center\).Il protocollo Kerberos è disponibile solo quando sia il client che il servizio utilizzano identità di dominio.In altre combinazioni di account, viene utilizzato il protocollo NTLM, come riepilogato nella tabella seguente.  
  
 Nelle intestazioni della tabella vengono riportati i possibili tipi di account utilizzati dal server,mentre nella colonna sinistra vengono indicati i possibili tipi di account utilizzati dal client.  
  
||Utente locale|Sistema locale|Utente del dominio|Computer del dominio|  
|-|-------------------|--------------------|------------------------|--------------------------|  
|Utente locale|NTLM|NTLM|NTLM|NTLM|  
|Sistema locale|NTLM anonimo|NTLM anonimo|NTLM anonimo|NTLM anonimo|  
|Utente del dominio|NTLM|NTLM|Kerberos|Kerberos|  
|Computer del dominio|NTLM|NTLM|Kerberos|Kerberos|  
  
 In particolare, i quattro tipi di account includono:  
  
-   Utente locale: profilo utente del computer.ad esempio: `MachineName\Administrator` o `MachineName\ProfileName`.  
  
-   Sistema locale: account predefinito SYSTEM in un computer non associato a un dominio.  
  
-   Utente del dominio: account utente in un dominio Windows.Ad esempio: `DomainName\ProfileName`.  
  
-   Computer del dominio: processo con identità di computer in esecuzione in un computer associato a un dominio Windows.Ad esempio: `MachineName\Network Service`.  
  
> [!NOTE]
>  La credenziale del servizio viene acquisita quando viene chiamato il metodo <xref:System.ServiceModel.ICommunicationObject.Open%2A> della classe <xref:System.ServiceModel.ServiceHost>.La credenziale del client viene letta ogni volta che il client invia un messaggio.  
  
## Problemi di autenticazione di Windows comuni  
 In questa sezione vengono illustrati alcuni problemi di autenticazione di Windows comuni e le possibili soluzioni.  
  
### Protocollo Kerberos  
  
#### Problemi SPN\/UPN con il protocollo Kerberos  
 Quando si utilizza l'autenticazione di Windows unitamente al protocollo Kerberos diretto o negoziato mediante SSPI, l'URL utilizzato dall'endpoint client deve includere il nome di dominio completo dell'host del servizio presente nell'URL del servizio.Questo presuppone che l'account utilizzato per l'esecuzione del servizio abbia accesso alla chiave del nome dell'entità servizio \(SPN\) del computer \(impostazione predefinita\) creata quando il computer viene aggiunto al dominio di Active Directory, generalmente eseguendo il servizio con l'account Servizio di rete.Se il servizio non ha accesso alla chiave dell'SPN del computer, è necessario fornire l'SPN corretto o il nome dell'entità utente \(UPN\) dell'account utilizzato per l'esecuzione del servizio nell'identità dell'endpoint del client.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] funzionamento di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] con SPN e UPN, vedere [Identità del servizio e autenticazione](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md).  
  
 In scenari di bilanciamento del carico, ad esempio Web farm o Web garden, viene comunemente definito un account univoco per ogni applicazione, viene assegnato un SPN a tale account e viene verificato che tutti i servizi dell'applicazione siano eseguiti in tale account.  
  
 Per ottenere un SPN per l'account del servizio, è necessario essere amministratore di dominio di Active Directory.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Supplemento tecnico Kerberos per Windows](http://go.microsoft.com/fwlink/?LinkID=88330).  
  
#### Per il protocollo Kerberos diretto è necessario che il servizio venga eseguito utilizzando un account di tipo computer del dominio  
 Questo si verifica quando la proprietà `ClientCredentialType` è impostata su `Windows` e la proprietà <xref:System.ServiceModel.MessageSecurityOverHttp.NegotiateServiceCredential%2A> è impostata su `false`, come illustrato nel codice seguente.  
  
 [!code-csharp[C_DebuggingWindowsAuth#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#1)]
 [!code-vb[C_DebuggingWindowsAuth#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#1)]  
  
 Per risolvere questo problema, eseguire il servizio utilizzando un account di tipo computer del dominio, ad esempio Servizio di rete, in un computer associato al dominio.  
  
### Requisito di negoziazione della credenziale in caso di delega  
 Per poter essere utilizzato con la funzionalità di delega, il protocollo di autenticazione Kerberos deve essere implementato con la negoziazione della credenziale. Questa versione di Kerberos è nota come Kerberos multifase o multipassaggio.Se si implementa l'autenticazione Kerberos senza negoziazione della credenziale \(ovvero una versione di Kerberos anche nota come "monofase" o "monopassaggio\), verrà generata un'eccezione.  
  
 Per implementare Kerberos con negoziazione della credenziale, eseguire le operazioni seguenti:  
  
1.  Implementare la delega impostando <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> su <xref:System.Security.Principal.TokenImpersonationLevel>.  
  
2.  Richiedere la negoziazione SSPI:  
  
    1.  Se si utilizzano associazioni standard, impostare la proprietà `NegotiateServiceCredential` su `true`.  
  
    2.  Se si utilizzano associazioni personalizzate, impostare l'attributo `AuthenticationMode` dell'elemento `Security` su `SspiNegotiated`.  
  
3.  Richiedere che la negoziazione SSPI utilizzi Kerberos impedendo l'utilizzo di NTLM:  
  
    1.  È possibile eseguire questa operazione nel codice utilizzando l'istruzione seguente: `ChannelFactory.Credentials.Windows.AllowNtlm = false`  
  
    2.  In alternativa, è possibile operare nel file di configurazione impostando l'attributo `allowNtlm` su `false`.Questo attributo è contenuto in [\<finestre\>](../../../../docs/framework/configure-apps/file-schema/wcf/windows-of-clientcredentials-element.md).  
  
### Protocollo NTLM  
  
#### Il provider SSP Negotiate esegue il fallback a NTLM, ma NTLM è disabilitato  
 Poiché la proprietà <xref:System.ServiceModel.Security.WindowsClientCredential.AllowNtlm%2A> è impostata su `false`, [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] tenta di generare un'eccezione se viene utilizzato NTLM.Si noti che l'impostazione di questa proprietà su `false` potrebbe non impedire l'invio di credenziali NTLM nella rete.  
  
 Nel codice seguente viene illustrato come disabilitare il fallback a NTLM.  
  
 [!code-csharp[C_DebuggingWindowsAuth#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#4)]
 [!code-vb[C_DebuggingWindowsAuth#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#4)]  
  
#### Impossibile accedere a NTLM  
 Le credenziali client non sono valide per il servizio.Verificare che il nome utente e la password siano impostati correttamente e che corrispondano a un account noto al computer in cui viene eseguito il servizio.Per accedere al computer del servizio, NTLM utilizza le credenziali specificate.Anche se le credenziali possono essere valide nel computer in cui il client è in esecuzione, l'accesso non riuscirà se le credenziali non sono valide nel computer del servizio.  
  
#### Si verifica un accesso NTLM anonimo, ma gli accessi anonimi sono disabilitati per impostazione predefinita  
 Quando si crea un client, la proprietà <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> viene impostata su <xref:System.Security.Principal.TokenImpersonationLevel>, come illustrato nell'esempio seguente, ma per impostazione predefinita il server impedisce gli accessi anonimi.Tale situazione si verifica perché il valore predefinito della proprietà <xref:System.ServiceModel.Security.WindowsServiceCredential.AllowAnonymousLogons%2A> della classe <xref:System.ServiceModel.Security.WindowsServiceCredential> è `false`.  
  
 Nel codice client seguente viene tentata l'abilitazione degli accessi anonimi \(si noti che la proprietà predefinita è `Identification`\).  
  
 [!code-csharp[C_DebuggingWindowsAuth#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#5)]
 [!code-vb[C_DebuggingWindowsAuth#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#5)]  
  
 Nel codice del servizio seguente viene modificata l'impostazione predefinita per consentire gli accessi anonimi.  
  
 [!code-csharp[C_DebuggingWindowsAuth#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#6)]
 [!code-vb[C_DebuggingWindowsAuth#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#6)]  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] rappresentazione, vedere [Delega e rappresentazione](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md).  
  
 In alternativa, il client viene eseguito come un servizio Windows, utilizzando l'account predefinito System.  
  
### Altri problemi  
  
#### Le credenziali client non sono impostate correttamente  
 L'autenticazione di Windows utilizza l'istanza <xref:System.ServiceModel.Security.WindowsClientCredential> restituita dalla proprietà <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> della classe <xref:System.ServiceModel.ClientBase%601>, non l'istanza <xref:System.ServiceModel.Security.UserNamePasswordClientCredential>.Nel codice seguente viene illustrato un esempio non corretto.  
  
 [!code-csharp[C_DebuggingWindowsAuth#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#2)]
 [!code-vb[C_DebuggingWindowsAuth#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#2)]  
  
 Nel codice seguente viene illustrato l'esempio corretto.  
  
 [!code-csharp[C_DebuggingWindowsAuth#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#3)]
 [!code-vb[C_DebuggingWindowsAuth#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#3)]  
  
#### L'interfaccia SSPI non è disponibile  
 I sistemi operativi seguenti non supportano l'autenticazione di Windows se utilizzati come server: [!INCLUDE[wxp](../../../../includes/wxp-md.md)] Home Edition, [!INCLUDE[wxp](../../../../includes/wxp-md.md)] Media Center Edition e [!INCLUDE[wv](../../../../includes/wv-md.md)] Home edition.  
  
#### Sviluppo e distribuzione con identità diverse  
 Se l'applicazione viene sviluppata in un computer e distribuita in un altro e si utilizzano diversi tipi di account per l'autenticazione in ogni computer, potrebbe verificarsi un comportamento diverso.Si supponga, ad esempio, di sviluppare l'applicazione in un computer Windows XP Pro utilizzando la modalità di autenticazione `SSPI Negotiated`.Se si utilizza un account utente locale per l'autenticazione, verrà utilizzato il protocollo NTLM.Una volta sviluppata l'applicazione, il servizio viene distribuito in un computer Windows Server 2003 in cui è in esecuzione un account di dominio.A questo punto il client non è in grado di autenticare il servizio poiché utilizza Kerberos e un controller di dominio.  
  
## Vedere anche  
 <xref:System.ServiceModel.Security.WindowsClientCredential>   
 <xref:System.ServiceModel.Security.WindowsServiceCredential>   
 <xref:System.ServiceModel.Security.WindowsClientCredential>   
 <xref:System.ServiceModel.ClientBase%601>   
 [Delega e rappresentazione](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)   
 [Scenari non supportati](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)