---
title: "Procedura: controllare gli eventi di sicurezza di Windows Communication Foundation | Microsoft Docs"
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
  - "sicurezza [WCF], controllo eventi"
ms.assetid: e71e9587-3336-46a2-9a9e-d72a1743ecec
caps.latest.revision: 19
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 19
---
# Procedura: controllare gli eventi di sicurezza di Windows Communication Foundation
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] consente di registrarsi eventi di sicurezza nel registro eventi di Windows, che può essere visualizzato usando il Visualizzatore eventi di Windows.  In questo argomento viene illustrato come configurare un'applicazione in modo che registri eventi di sicurezza.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]l controllo, vedere [Controllo](../../../../docs/framework/wcf/feature-details/auditing-security-events.md).  
  
### Per controllare gli eventi di sicurezza nel codice  
  
1.  Specificare il percorso del registro di controllo.  A questo scopo, impostare la proprietà <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.AuditLogLocation%2A> della classe <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> su uno dei valori dell'enumerazione <xref:System.ServiceModel.AuditLogLocation>, come illustrato nel codice seguente.  
  
     [!code-csharp[AuditingSecurityEvents#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#2)]
     [!code-vb[AuditingSecurityEvents#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#2)]  
  
     L'enumerazione <xref:System.ServiceModel.AuditLogLocation> ha tre valori: `Application`, `Security` o `Default`.  Il valore specifica uno dei log visibili nel Visualizzatore eventi, il registro protezione o il registro applicazioni.  Se si usa il valore `Default`, il log effettivo dipenderà dal sistema operativo su cui è in esecuzione l'applicazione.  Se il controllo è attivato e il percorso del log non viene specificato, verrà usato, per impostazione predefinita, il registro `Security`, per le piattaforme che supportano la scrittura nel registro protezione, altrimenti verrà usato il registro `Application`.  Solo [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] e [!INCLUDE[wv](../../../../includes/wv-md.md)] supportano la scrittura nel registro protezione per impostazione predefinita.  
  
2.  Impostare i tipi di eventi da controllare.  È possibile controllare simultaneamente eventi a livello di servizio o eventi di autorizzazione a livello di messaggio.  A questo scopo, impostare la proprietà <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.ServiceAuthorizationAuditLevel%2A> o <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.MessageAuthenticationAuditLevel%2A> su uno dei valori dell'enumerazione <xref:System.ServiceModel.AuditLevel>, come illustrato nel codice seguente.  
  
     [!code-csharp[AuditingSecurityEvents#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#3)]
     [!code-vb[AuditingSecurityEvents#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#3)]  
  
3.  Specificare se esporre o meno gli errori all'applicazione relativamente agli eventi di controllo del log.  Impostare la proprietà <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> su `true` o `false`, come illustrato nel codice seguente.  
  
     [!code-csharp[AuditingSecurityEvents#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#4)]
     [!code-vb[AuditingSecurityEvents#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#4)]  
  
     La proprietà `SuppressAuditFailure` predefinita è `true`, in modo che l'errore da controllare non influenzi l'applicazione.  In caso contrario, viene generata un'eccezione.  Per ogni controllo riuscito viene scritta una traccia dettagliata.  Per ogni errore da controllare, la traccia viene scritta a livello errore.  
  
4.  Eliminare la classe <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> esistente dalla raccolta dei comportamenti trovati nella descrizione di una classe <xref:System.ServiceModel.ServiceHost>.  La raccolta dei comportamenti è accessibile tramite la proprietà <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A>, che a sua volta è accessibile dalla proprietà <xref:System.ServiceModel.ServiceHostBase.Description%2A>.  Aggiungere quindi la nuova classe <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> alla stessa raccolta, come illustrato nel codice seguente.  
  
     [!code-csharp[AuditingSecurityEvents#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#5)]
     [!code-vb[AuditingSecurityEvents#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#5)]  
  
### Per impostare il controllo nella configurazione  
  
1.  Per configurare il controllo nella configurazione, aggiungere l'elemento [\<comportamento\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)[\<comportamenti\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) del file web.config.  Aggiungere quindi un elemento [\<controlloSicurezzaServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md) e impostare i vari attributi, come illustrato nell'esempio seguente.  
  
    ```  
    <behaviors>  
       <behavior name="myAuditBehavior">  
          <serviceSecurityAudit auditLogLocation="Application"  
                suppressAuditFailure="false"   
                serviceAuthorizationAuditLevel="None"   
                messageAuthenticationAuditLevel="SuccessOrFailure" />  
          </behavior>  
    </behaviors>  
    ```  
  
2.  È necessario specificare il comportamento del servizio, come illustrato nell'esempio seguente.  
  
    ```  
    <services>  
        <service type="WCS.Samples.Service.Echo"   
        behaviorConfiguration=" myAuditBehavior">  
           <endpoint address=""  
                    binding="wsHttpBinding"  
                    bindingConfiguration="CertificateDefault"   
                    contract="WCS.Samples.Service.IEcho" />  
        </service>  
    </services>  
  
    ```  
  
## Esempio  
 Nel codice seguente viene creata un'istanza della classe <xref:System.ServiceModel.ServiceHost> e viene aggiunta una nuova classe <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> alla raccolta dei comportamenti.  
  
 [!code-csharp[AuditingSecurityEvents#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/auditingsecurityevents/cs/auditingsecurityevents.cs#1)]
 [!code-vb[AuditingSecurityEvents#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/auditingsecurityevents/vb/auditingsecurityevents.vb#1)]  
  
## Sicurezza di .NET Framework  
 Se si imposta la proprietà <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> su `true`, viene evitata la visualizzazione di qualsiasi errore per generare controlli di sicurezza \(se la proprietà viene impostata su `false`, viene generata un'eccezione\).  Tuttavia, se si abilita la proprietà **Impostazioni di sicurezza locali** di Windows seguente, un errore per generare eventi di controllo causerà l'arresto immediato di Windows:  
  
 **Controllo: arresto del sistema immediato se non è possibile registrare i controlli di sicurezza**  
  
 Per impostare la proprietà, aprire la finestra di dialogo **Impostazioni protezione locale**.  In **Impostazioni di sicurezza** fare clic su **Criteri locali**.  Quindi fare clic su **Opzioni di sicurezza**.  
  
 Se la proprietà <xref:System.ServiceModel.AuditLogLocation> è impostata su <xref:System.ServiceModel.AuditLogLocation> e se nei **Criteri di sicurezza locali** non è stata impostata l'opzione **Controlla accesso agli oggetti**, gli eventi di controllo non vengono scritti nel registro protezione.  Si noti che non viene restituito alcun errore, ma non vengono scritte voci di controllo nel registro protezione.  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.AuditLogLocation%2A>   
 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>   
 <xref:System.ServiceModel.AuditLogLocation>   
 [Controllo](../../../../docs/framework/wcf/feature-details/auditing-security-events.md)