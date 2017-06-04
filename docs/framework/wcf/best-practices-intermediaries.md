---
title: "Procedure consigliate: Intermediari | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2d41b337-8132-4ac2-bea2-6e9ae2f00f8d
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Procedure consigliate: Intermediari
Per assicurarsi della corretta chiusura dei canali lato servizio nell'intermediario, è necessario prestare attenzione affinché gli errori vengano gestiti correttamente quando si chiamano gli intermediari.  
  
 Si consideri lo scenario seguente.Tramite un client viene effettuata una chiamata a un intermediario mediante il quale, successivamente, viene chiamato un servizio back\-end.Tramite il servizio back\-end non viene definito alcun contratto di errori, pertanto qualsiasi errore generato da questo servizio sarà trattato come un errore non tipizzato.Tramite il servizio back\-end viene generato un oggetto <xref:System.ApplicationException> e tramite WCF viene interrotto correttamente il canale lato servizio.L'oggetto <xref:System.ApplicationException> viene quindi esposto come oggetto <xref:System.ServiceModel.FaultException> generato per l'intermediario.Tramite l'intermediario viene generato di nuovo l'oggetto <xref:System.ApplicationException>.In WCF questo oggetto viene interpretato come errore non tipizzato dall'intermediario e viene inoltrato al client.Al momento della ricezione dell'errore, i canali lato client sia dell'intermediario sia del client presentano un errore.Il canale lato servizio dell'intermediario, tuttavia, rimane aperto dal momento che in WCF questo errore non viene riconosciuto come irreversibile.  
  
 La procedura consigliata in questo scenario consiste nel rilevare se l'errore proveniente dal servizio è irreversibile e, in tal caso, il canale lato client dell'intermediario deve presentare un errore, come mostrato nel frammento di codice riportato di seguito.  
  
```csharp  
catch (Exception e)  
{  
    bool faulted = service.State == CommunicationState.Faulted;  
    service.Abort();  
    if (faulted)  
    {  
        throw new ApplicationException(e.Message);  
    }  
    Else  
    {  
        throw;  
    }  
}  
  
```  
  
## Vedere anche  
 [Gestione errori WCF](../../../docs/framework/wcf/wcf-error-handling.md)   
 [Specifica e gestione di errori in contratti e servizi](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)