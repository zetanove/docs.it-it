---
title: "Comportamento di controllo dei servizi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 59bf0cda-e496-4418-a3a1-2f0f6e85f8ce
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Comportamento di controllo dei servizi
Questo esempio illustra come utilizzare <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> per abilitare il controllo degli eventi di sicurezza durante le operazioni del servizio.L'esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).Il servizio e il client sono stati configurati utilizzando [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).L'attributo `mode` di [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) è stato impostato su `Message` e `clientCredentialType` è stato impostato su `Windows`.In questo esempio, il client è un'applicazione console \(.exe\) e il servizio è ospitato da Internet Information Services \(IIS\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Il file di configurazione del servizio utilizza l'elemento `serviceSecurityAudit` per configurare il controllo.  
  
```  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      ...  
<!-- serviceSecurityAudit allows specification of audit location   
     and whether to audit success, failure or both. This service   
     logs success and failure of messageAuthentication   
     to the default location -->  
     <serviceSecurityAudit auditLogLocation ="Default" messageAuthenticationAuditLevel = "SuccessOrFailure" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Premere INVIO nella finestra della console per arrestare il client.  
  
 I log di controllo risultanti possono essere visualizzati eseguendo il Visualizzatore eventi.Per impostazione predefinita, in Windows XP gli eventi di controllo possono essere visualizzati nel registro applicazioni, mentre in Windows Server 2003 e Windows Vista gli eventi di controllo possono essere visti nel registro sicurezza.In Windows Server 2008 e Windows 7 è possibile visualizzare gli eventi di controllo nei registri applicazioni e sicurezza.Il percorso degli eventi di controllo può essere specificato impostando l'attributo `auditLogLocation` su "Application" o "Security".Per ulteriori informazioni, vedere [Procedura: controllare gli eventi di sicurezza](../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md).Se gli eventi vengono scritti nel registro di sicurezza, il valore di LocalSecurityPolicy\-\> per l'abilitazione dell'accesso all'oggetto deve essere impostato per "Success" e "Failure".  
  
 Nel registro eventi l'origine degli eventi di controllo corrisponde a "ServiceModel Audit 3.0.0.0".Ai record di controllo dell'autenticazione dei messaggi è associata una categoria "MessageAuthentication", mentre ai record di controllo dell'autorizzazione del servizio è associata una categoria "ServiceAuthorization".  
  
 Gli eventi di controllo dell'autenticazione dei messaggi analizzano se il messaggio è stato manomesso, se è scaduto e se il client può essere autenticato presso il servizio.Tali eventi forniscono inoltre informazioni sull'esito positivo o meno dell'autenticazione nonché l'identità del client e dell'endpoint a cui è stato inviato il messaggio insieme all'azione associata a quest'ultimo.  
  
 Gli eventi di controllo dell'autorizzazione del servizio analizzano la decisione di autorizzazione adottata dalla gestione autorizzazioni del servizio.Tali eventi forniscono inoltre informazioni sull'esito positivo o meno dell'autorizzazione nonché l'identità del client, l'endpoint al quale è stato inviato il messaggio, l'azione associata al messaggio, l'identificatore del contesto di autorizzazione generato dal messaggio in arrivo e il tipo di gestione autorizzazioni che ha preso la decisione relativa all'accesso.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Vedere anche  
 [Controllo](../../../../docs/framework/wcf/feature-details/auditing-security-events.md)   
 [Procedura: controllare gli eventi di sicurezza](../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md)