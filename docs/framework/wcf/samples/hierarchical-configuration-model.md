---
title: "Modello di configurazione gerarchica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 28dcc698-226c-4b77-9e51-8bf45a36216c
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Modello di configurazione gerarchica
In questo esempio viene descritto come implementare una gerarchia di file di configurazione per i servizi.Viene inoltre descritto come associazioni, comportamenti del servizio e comportamenti dell'endpoint vengono ereditati dai livelli superiori nella gerarchia.  
  
## Dettagli dell'esempio  
 Una delle funzionalità sviluppate per [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] è il miglioramento nel modello di configurazione gerarchico.Un esempio di un modello di configurazione gerarchico può essere quello definito da Machine.config \-\> Rootweb.config \-\> Web.config.In [!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)], le associazioni e i comportamenti definiti nei livelli superiori della gerarchia di configurazione vengono aggiunti ai servizi senza configurazione esplicita.In questo esempio viene illustrato come è possibile semplificare la configurazione del servizio basandosi sugli elementi di configurazione definiti a livello di applicazione o computer.  
  
 Questo esempio è costituito da nove servizi, definiti in tre livelli di gerarchia.`Service1` è alla radice.`Service2` e `Service3` ereditano gli elementi predefiniti da `Service1`.`Service4`, `Service5`, `Service6` e `Service7` sono definiti a un terzo livello della gerarchia, ereditando gli elementi predefiniti da `Service3`.Infine, `Service10` e `Service11` sono a un quarto livello della gerarchia.  
  
 Tutti i servizi implementano il contratto `IDesc`.Gli elementi seguenti sono la definizione dell'interfaccia `IDesc`, che mostra i metodi esposti in questa interfaccia.L'interfaccia `IDesc` è definita in Service1.cs.  
  
```  
// Define a service contract  
[ServiceContract(Namespace="http://Microsoft.Samples.ConfigHierarchicalModel")]  
public interface IDesc  
{  
    [OperationContract]  
    List<string> ListEndpoints();  
    [OperationContract]  
    List<string> ListServiceBehaviors();  
    [OperationContract]  
    List<string> ListEndpointBehaviors();  
}  
  
```  
  
 L'implementazione di tali metodi da parte dei servizi risulta semplificata.`ListEndpoints` scorre tutti gli endpoint del servizio e restituisce un elenco di tutti gli endpoint in possesso del servizio.`ListServiceBehaviors` scorre tutti i comportamenti aggiunti al servizio e restituisce l'elenco di tutti i comportamenti del servizio ad esso associati.`ListEndpointBehaviors` si comporta in modo analogo a `ListServiceBehaviors`, ma restituisce l'elenco dei comportamenti dell'endpoint.  
  
 L'implementazione consente al client di conoscere quanti endpoint il servizio sta esponendo e quali comportamenti del servizio e comportamenti dell'endpoint sono stati aggiunti al servizio.Il client implementato come parte dell'esempio aggiunge un riferimento al servizio a tutti i servizi nella soluzione e mostra tali elementi per ognuno dei servizi.  
  
## Per utilizzare questo esempio  
  
#### Per eseguire il client.  
  
1.  Utilizzando [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)], aprire il file ConfigHierarchicalModel.sln.  
  
2.  Se il progetto client non è già stato configurato come progetto di avvio, attenersi alla seguente procedura.  
  
    1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla soluzione, quindi selezionare **Proprietà**.  
  
    2.  In **Proprietà comuni** selezionare **Progetto di avvio**, quindi fare clic su **Progetto di avvio singolo**.  
  
    3.  Nell'elenco a discesa **Progetto di avvio singolo** selezionare **Client**.  
  
    4.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
3.  Per compilare l'esempio, premere CTRL\+MAIUSC\+B.  
  
4.  Premere CTRL\+F5 per eseguire il client.  
  
> [!NOTE]
>  Se questi passaggi non funzionano, verificare che l'ambiente sia stato configurato correttamente, utilizzando i passaggi seguenti.  
>   
>  1.  Verificare di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
> 2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
> 3.  Per eseguire l'esempio in una configurazione con singolo computer o più computer, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\ConfigHierarchicalModel`  
  
## Vedere anche  
 [Gestione](http://go.microsoft.com/fwlink/?LinkId=193960)