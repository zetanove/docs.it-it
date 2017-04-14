---
title: "Ridenominazione di un servizio WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 14235a65-b1c5-409d-b6cc-a979acd54bbd
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Ridenominazione di un servizio WCF
In questo argomento viene illustrato come ridenominare un servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)].  
  
## Ridenominazione di un servizio WCF  
 Per ridenominare un servizio di un modello di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)], eseguire i passaggi seguenti.  
  
-   Modificare il nome della classe che implementa il servizio.  
  
-   Nel file di configurazione del servizio, impostare il nome del servizio sul nuovo nome scelto, come indicato nell'esempio seguente.A seconda del modello di hosting utilizzato, il file di configurazione può essere app.config oppure web.config.  
  
```  
<system.servicemodel>  
   <services>  
      <service name=”WcfService.NewName”>  
      </service>  
   </services>  
</system.servicemodel>  
```  
  
-   Se il servizio è WebHosted, utilizza un file \*.svc.Aprire questo file e modificare il nome del servizio, come indicato nell'esempio seguente.Questo passaggio non è necessario per le applicazioni indipendenti, in quanto questo tipo di applicazione non prevede alcun file con estensione svc.  
  
```  
<%@ ServiceHost Service=”WcfService.NewName”>  
```  
  
## Ridenominazione del contratto di un servizio WCF  
  
-   Per ridenominare il contratto di servizio, attenersi ai passaggi seguenti:  
  
-   Modificare il nome del contratto di servizio.  
  
-   Nel file di configurazione del servizio, impostare il nome del contratto di servizio sul nuovo nome scelto, come indicato nell'esempio seguente.A seconda del modello di hosting utilizzato, il file di configurazione può essere app.config oppure web.config.  
  
```  
<system.servicemodel>  
   <services>  
      <service>  
         <endpoint contract=”WcfService.NewContractName” />  
      </service>  
   </services>  
</system.servicemodel>  
```