---
title: "Procedura: rappresentare un client in un servizio | Microsoft Docs"
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
  - "WCF, rappresentazione"
  - "rappresentazione"
  - "WCF, sicurezza"
ms.assetid: 431db851-a75b-4009-9fe2-247243d810d3
caps.latest.revision: 33
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 33
---
# Procedura: rappresentare un client in un servizio
La rappresentazione di un client in un servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] consente a quest'ultimo di eseguire azioni per conto del client. Per le azioni soggette ai controlli dell'elenco di controllo di accesso \(ACL\), ad esempio l'accesso a directory e file in un computer o l'accesso a un database SQL Server, il controllo ACL si basa sull'account utente del client. In questo argomento vengono illustrati i passaggi di base necessari che consentono a un client in un dominio Windows di impostare un livello di rappresentazione di client. Per un esempio pratico, vedere [Rappresentazione di client](../../../docs/framework/wcf/samples/impersonating-the-client.md).[!INCLUDE[crabout](../../../includes/crabout-md.md)]lla rappresentazione di client, vedere [Delega e rappresentazione](../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md).  
  
> [!NOTE]
>  Quando il client e il servizio sono in esecuzione nello stesso computer e il client è in esecuzione con un account del sistema \(ad esempio `Local System` o `Network Service`\), il client non può essere rappresentato quando viene stabilita una sessione protetta con token del contesto di sicurezza con stato. Un'applicazione Windows Form o console viene in genere eseguita con l'account attualmente connesso che quindi può essere rappresentato per impostazione predefinita. Tuttavia, quando il client è una pagina [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] ospitata in [!INCLUDE[iis601](../../../includes/iis601-md.md)] o IIS 7.0, il client viene eseguito con l'account `Network Service` per impostazione predefinita. Tutte le associazioni fornite dal sistema che supportano le sessioni protette utilizzano un token del contesto di sicurezza senza stato per impostazione predefinita. Tuttavia, se il client è una pagina [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] e si utilizzano sessioni protette con token del contesto di sicurezza con stato, non è possibile eseguire la rappresentazione del client.[!INCLUDE[crabout](../../../includes/crabout-md.md)]ll'uso di token del contesto di sicurezza con stato in una sessione di sicurezza, vedere [Procedura: creare un token di contesto di sicurezza per una sessione sicura](../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md).  
  
### Per consentire la rappresentazione di un client da un token di Windows memorizzato nella cache in un servizio  
  
1.  Creare il servizio. Per un'esercitazione su questa procedura di base, vedere [Esercitazione introduttiva](../../../docs/framework/wcf/getting-started-tutorial.md).  
  
2.  Utilizzare un'associazione che utilizza l'autenticazione di Windows e che crea una sessione, ad esempio <xref:System.ServiceModel.NetTcpBinding> o <xref:System.ServiceModel.WSHttpBinding>.  
  
3.  Quando si crea l'implementazione dell'interfaccia del servizio, applicare la classe <xref:System.ServiceModel.OperationBehaviorAttribute> al metodo che richiede la rappresentazione del client. Impostare la proprietà <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> su <xref:System.ServiceModel.ImpersonationOption>.  
  
     [!code-csharp[c_SimpleImpersonation#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_simpleimpersonation/cs/source.cs#2)]
     [!code-vb[c_SimpleImpersonation#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_simpleimpersonation/vb/source.vb#2)]  
  
### Per impostare il livello di rappresentazione consentito nel client  
  
1.  Creare un codice client del servizio tramite [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Accesso ai servizi tramite client WCF](../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md).  
  
2.  Dopo la creazione del client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], impostare la proprietà <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> della classe <xref:System.ServiceModel.Security.WindowsClientCredential> su uno dei valori di enumerazione di <xref:System.Security.Principal.TokenImpersonationLevel>.  
  
    > [!NOTE]
    >  Per usare <xref:System.Security.Principal.TokenImpersonationLevel>, deve essere usata l'autenticazione Kerberos negoziata, a volte denominata *multifase* o *in più passaggi*. Per una descrizione dell'implementazione, vedere [Procedure consigliate per la protezione](../../../docs/framework/wcf/feature-details/best-practices-for-security-in-wcf.md).  
  
     [!code-csharp[c_SimpleImpersonation#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_simpleimpersonation/cs/source.cs#1)]
     [!code-vb[c_SimpleImpersonation#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_simpleimpersonation/vb/source.vb#1)]  
  
## Vedere anche  
 <xref:System.ServiceModel.OperationBehaviorAttribute>   
 <xref:System.Security.Principal.TokenImpersonationLevel>   
 [Rappresentazione di client](../../../docs/framework/wcf/samples/impersonating-the-client.md)   
 [Delega e rappresentazione](../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)