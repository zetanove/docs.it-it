---
title: "Procedura: implementare l&#39;accesso utente con i servizi dell&#39;applicazione client | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "servizi delle applicazioni client, autenticare gli utenti"
  - "convalida degli utenti [servizi delle applicazioni client]"
  - "convalida [.NET Framework], servizi delle applicazioni client"
ms.assetid: 5431a671-eb02-4e18-a651-24764fccec9a
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: implementare l&#39;accesso utente con i servizi dell&#39;applicazione client
È possibile usare i servizi delle applicazioni client per convalidare gli utenti tramite un servizio profili [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] esistente.  Per informazioni su come configurare il servizio di profili [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)], vedere l'argomento relativo all'[Using Forms Authentication with Microsoft Ajax](../Topic/Using%20Forms%20Authentication%20with%20Microsoft%20Ajax.md).  
  
 Le procedure seguenti descrivono come convalidare gli utenti tramite il servizio di autenticazione quando l'applicazione è configurata per usare uno dei provider di servizi di autenticazione client.  Per altre informazioni, vedere [Procedura: configurare i servizi delle applicazioni client](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md).  
  
 Tutte le convalide verranno in genere eseguite tramite il metodo `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName>.  Questo metodo gestisce l'interazione con il servizio di autenticazione tramite il provider di autenticazione configurato.  Per altre informazioni, vedere [Cenni preliminari sui servizi delle applicazioni client](../../../docs/framework/common-client-technologies/client-application-services-overview.md).  
  
 Le procedure di autenticazione basata su form richiedono l'accesso a un servizio di autenticazione [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] in esecuzione.  Per istruzioni sul test end\-to\-end delle funzionalità dei servizi dell'applicazione client, vedere [Procedura dettagliata: utilizzo di servizi delle applicazioni client](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md).  
  
### Per autenticare un utente con autenticazione basata su form usando un provider di credenziali di appartenenza  
  
1.  Implementare l'interfaccia <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider>.  L’esempio di codice seguente mostra un’implementazione <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A?displayProperty=fullName> per una classe di una finestra di dialogo di accesso derivata da <xref:System.Windows.Forms.Form?displayProperty=fullName>.  In questa finestra di dialogo vi sono caselle di testo per il nome utente e la password e una casella di controllo di memorizzazione dei dati.  Quando il provider di autenticazione client chiama il metodo <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A>, il form viene visualizzato.  Quando l'utente inserisce le informazioni nella finestra di dialogo di accesso e fa clic su OK, vengono restituiti i valori specificati in un nuovo oggetto <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationCredentials>.  
  
     [!code-csharp[ClientApplicationServices#210](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Login.cs#210)]
     [!code-vb[ClientApplicationServices#210](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Login.vb#210)]  
  
2.  Chiamare il metodo `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> e passare stringhe vuote come valori del parametro.  Quando si specificano stringhe vuote, questo metodo chiama internamente il metodo <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> per il provider di credenziali configurato per l'applicazione.  Il codice di esempio seguente chiama questo metodo per limitare l’accesso a un’intera applicazione Windows Form.  È possibile aggiungere questo codice per un gestore <xref:System.Windows.Forms.Form.Load?displayProperty=fullName>.  
  
     [!code-csharp[ClientApplicationServices#317](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Class1.cs#317)]
     [!code-vb[ClientApplicationServices#317](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Class1.vb#317)]  
  
### Per autenticare un utente con autenticazione basata su form senza usare un provider di credenziali di appartenenza  
  
-   Chiamare il metodo `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> e passare i valori del nome utente e password recuperati dall'utente.  
  
     [!code-csharp[ClientApplicationServices#318](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Class1.cs#318)]
     [!code-vb[ClientApplicationServices#318](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Class1.vb#318)]  
  
### Per autenticare un utente con l’autenticazione di Windows  
  
-   Chiamare il metodo `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> e passare stringhe vuote per i parametri.  Questa chiamata al metodo restituirà sempre `true` e aggiungerà un cookie alla cache dei cookie dell'utente che contiene l'identità di Windows.  
  
     [!code-csharp[ClientApplicationServices#319](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Class1.cs#319)]
     [!code-vb[ClientApplicationServices#319](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Class1.vb#319)]  
  
## Programmazione efficiente  
 Il codice di esempio in questo argomento illustra gli usi di autenticazione più semplici in un’applicazione client Windows.  Quando si chiama il metodo `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> con i servizi delle applicazioni client e l’autenticazione basata su form, il codice può tuttavia generare un <xref:System.Net.WebException>.  Ciò indica che il servizio di autenticazione non è disponibile.  Per un esempio di come gestire questa eccezione, vedere [Procedura dettagliata: utilizzo di servizi delle applicazioni client](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md).  
  
## Vedere anche  
 [Servizi applicazioni client](../../../docs/framework/common-client-technologies/client-application-services.md)   
 [Cenni preliminari sui servizi delle applicazioni client](../../../docs/framework/common-client-technologies/client-application-services-overview.md)   
 [Procedura: configurare i servizi delle applicazioni client](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)   
 [Procedura dettagliata: utilizzo di servizi delle applicazioni client](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md)   
 [Using Forms Authentication with Microsoft Ajax](../Topic/Using%20Forms%20Authentication%20with%20Microsoft%20Ajax.md)