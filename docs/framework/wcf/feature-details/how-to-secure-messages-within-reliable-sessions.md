---
title: "Procedura: proteggere i messaggi in sessioni affidabili | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: aee33e50-936f-4486-9ca8-c1520c19a62d
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# Procedura: proteggere i messaggi in sessioni affidabili
In questo argomento vengono delineati i passaggi necessari per attivare la protezione a livello di messaggio per i messaggi scambiati all'interno di una sessione affidabile utilizzando una delle associazioni fornite dal sistema che supportano tale sessione, ma non per impostazione predefinita.È possibile attivare una sessione affidabile protetta in modo imperativo, mediante codice, o in modo dichiarativo, nel file di configurazione.In questa procedura vengono utilizzati i file di configurazione del client e del servizio per attivare la sessione affidabile protetta.  
  
 Questa procedura è costituita dalle tre attività chiave seguenti:  
  
1.  Specificare che il client e il servizio si scambiano messaggi in una sessione affidabile.  
  
2.  Richiedere la protezione a livello di messaggio all'interno della sessione affidabile.  
  
3.  Specificare il tipo di credenziale client che il client deve utilizzare per essere autenticato con il servizio.  
  
 Nella prima attività, è importante che l'elemento di configurazione endpoint contenga un attributo `bindingConfiguration` che faccia riferimento a una configurazione di associazione denominata, in questo esempio, "MessageSecurity". L'elemento di configurazione [\<associazione\>](../../../../docs/framework/misc/binding.md)`enabled può quindi fare riferimento a questo nome per attivare sessioni affidabili impostando l'attributo` [reliableSession dell'elemento](http://msdn.microsoft.com/it-it/9c93818a-7dfa-43d5-b3a1-1aafccf3a00b)`true su` .È possibile richiedere che le garanzie di recapito ordinato siano disponibili all'interno di una sessione affidabile impostando l'attributo `ordered` su `true`.  
  
 Per l'originale dell'esempio su cui si basa questa procedura di configurazione, vedere [Sessioni affidabili WS](../../../../docs/framework/wcf/samples/ws-reliable-session.md).  
  
 Gli elementi essenziali della seconda attività vengono eseguiti impostando l'attributo `mode` dell'elemento \<`security`\> contenuto nell'elemento \<`binding`\> del client e del servizio su `Message`.  
  
 Gli elementi essenziali della terza attività vengono eseguiti impostando l'attributo `clientCredentialType` dell'elemento \<`message`\> contenuto nell'elemento \<`security`\> del client e del servizio su `Certificate`.  
  
> [!NOTE]
>  Quando si utilizza la protezione dei messaggi con sessioni affidabili, se il client non viene autenticato, la messaggistica affidabile tenta di autenticarlo fino al verificarsi di un timeout, invece di generare un'eccezione al primo errore.  
  
### Per configurare il servizio con una classe WSHttpBinding per utilizzare una sessione affidabile  
  
1.  Questa procedura viene descritta in [Procedura: scambiare messaggi in una sessione affidabile](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-within-a-reliable-session.md).  
  
### Per configurare il client con una classe WSHttpBinding per utilizzare una sessione affidabile  
  
1.  Questa procedura viene descritta in [Procedura: scambiare messaggi in una sessione affidabile](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-within-a-reliable-session.md).  
  
### Per impostare la modalità e la proprietà ClientCredentialType nella configurazione  
  
1.  Aggiungere un elemento di associazione appropriato all'elemento [\<associazioni\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) del file di configurazione.Nell'esempio seguente viene aggiunto un elemento [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).  
  
2.  Aggiungere un elemento \<`binding`\> e impostare il relativo attributo `name` su un valore appropriato.  
  
3.  Aggiungere un elemento `<security>``mode e impostare l'attributo` `Message su` .  
  
     Nell'esempio seguente, la modalità viene impostata su `Message` e quindi l'attributo `clientCredentialType` dell'elemento \<`message`\> viene impostato su `Certificate`.  
  
    ```  
    <wsHttpBinding>  
    <binding name="MessageSecurity">  
        <security mode="Message" />  
           <message clientCredentialType = " Certificate" />  
        </security>  
    </binding>  
    </wsHttpBinding >  
    ```