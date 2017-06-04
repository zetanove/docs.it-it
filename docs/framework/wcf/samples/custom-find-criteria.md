---
title: "Criteri di ricerca personalizzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b2723929-8829-424d-8015-a37ba2ab4f68
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Criteri di ricerca personalizzati
In questo esempio viene illustrato come creare una corrispondenza degli ambiti personalizzata utilizzando la logica e come implementare un servizio di individuazione personalizzato.I client utilizzano la funzionalità di corrispondenza degli ambiti personalizzata per rifinire ed eseguire l'ulteriore compilazione sulla funzionalità di individuazione fornita dal sistema di WCF Discovery.Lo scenario analizzato in questo esempio è il seguente:  
  
1.  Un client esegue la ricerca di un servizio calcolatrice.  
  
2.  Per rifinirne la ricerca, il client deve utilizzare una regola per la corrispondenza degli ambiti personalizzata.  
  
3.  In base a questa regola, un servizio risponde al client se il relativo endpoint corrisponde a uno qualsiasi degli ambiti specificati dal client.  
  
## Dimostrazione  
  
-   Creazione di un servizio di individuazione personalizzato.  
  
-   Implementazione di una corrispondenza degli ambiti personalizzata mediante un algoritmo.  
  
## Discussione  
 Il client esegue la ricerca del criterio di corrispondenza di tipo "OR".Un servizio risponde se gli ambiti sui relativi endpoint corrispondono a uno qualsiasi degli ambiti forniti dal client.In questo caso, il client esegue la ricerca di un servizio calcolatrice che dispone di uno qualsiasi degli ambiti riportati nell'elenco seguente:  
  
1.  `net.tcp://Microsoft.Samples.Discovery/RedmondLocation`  
  
2.  `net.tcp://Microsoft.Samples.Discovery/SeattleLocation`  
  
3.  `net.tcp://Microsoft.Samples.Discovery/PortlandLocation`  
  
 A tale scopo, il client indica ai servizi di utilizzare una regola per la corrispondenza degli ambiti personalizzata passando una corrispondenza degli ambiti personalizzata tramite URI.Per facilitare la corrispondenza degli ambiti personalizzata, il servizio deve utilizzare un servizio di individuazione personalizzato in grado di comprendere la regola per la corrispondenza degli ambiti personalizzata e di implementare la logica corrispondente associata.  
  
 Nel progetto client aprire il file Program.cs.Si noti che il campo `ScopeMatchBy` dell'oggetto `FindCriteria` è impostato su un URI specifico.Questo identificatore viene inviato al servizio.Se il servizio non è in grado di comprendere questa regola, la richiesta di ricerca del client verrà ignorata.  
  
 Aprire il progetto del servizio.Per implementare il servizio di individuazione personalizzato vengono utilizzati i tre file seguenti:  
  
1.  **AsyncResult.cs**: si tratta dell'implementazione di `AsyncResult` richiesta dai metodi di individuazione.  
  
2.  **CustomDiscoveryService.cs**: questo file implementa il servizio di individuazione personalizzato.L'implementazione estende la classe <xref:System.ServiceModel.Discovery.DiscoveryService> ed esegue l'override dei metodi necessari.Si noti l'implementazione del metodo <xref:System.ServiceModel.Discovery.DiscoveryService.OnBeginFind%2A>.Il metodo esegue un controllo per determinare se la corrispondenza degli ambiti personalizzata definita da una regola è stata specificata dal client.Si tratta dello stesso URI personalizzato specificato dal client in precedenza.Se la regola personalizzata viene specificata, verrà seguito il percorso del codice che implementa la logica di corrispondenza "OR."  
  
     Questa logica personalizzata passa attraverso tutti gli ambiti in ognuno degli endpoint di cui dispone il servizio.Se uno degli ambiti dell'endpoint corrisponde a uno qualsiasi degli ambiti forniti dal client, il servizio di individuazione aggiungerà tale endpoint alla risposta restituita al client.  
  
3.  **CustomDiscoveryExtension.cs**: l'ultimo passaggio nell'implementazione del servizio di individuazione consiste nel connettere questa implementazione del servizio di individuazione personalizzato all'host del servizio.La classe di supporto utilizzata in questo caso è `CustomDiscoveryExtension`.Questa classe estende la classe <xref:System.ServiceModel.Discovery.DiscoveryServiceExtension>.È necessario che l'utente esegua l'override del metodo <xref:System.ServiceModel.Discovery.DiscoveryServiceExtension.GetDiscoveryService%2A>.In questo caso, il metodo restituisce un'istanza del servizio personalizzato di individuazione creato in precedenza.`PublishedEndpoints` è un oggetto <xref:System.Collections.ObjectModel.ReadOnlyCollection> che contiene tutti gli endpoint delle applicazioni che vengono aggiunti all'oggetto <xref:System.ServiceModel.ServiceHost>.Il servizio di individuazione personalizzato utilizza questo oggetto per popolare l'elenco interno.Un utente ha la possibilità di aggiungere altri metadati dell'endpoint.  
  
 Aprire infine Program.cs.Si noti che <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> e `CustomDiscoveryExtension` vengono entrambi aggiunti all'host.Dopo avere eseguito questa operazione e aver fatto in modo che l'host disponga di un endpoint sul quale ricevere messaggi di individuazione, l'applicazione potrà utilizzare il servizio di individuazione personalizzato.  
  
 Si osservi che il client è in grado di trovare il servizio senza conoscerne l'indirizzo.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione contenente il progetto.  
  
2.  Compilare il progetto.  
  
3.  Eseguire l'applicazione del servizio.  
  
4.  Eseguire l'applicazione client.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Discovery\CustomFindCriteria`