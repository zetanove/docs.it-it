---
title: "Configurazione di una channel factory | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3b749493-bd8a-4ccb-893e-5948901a1486
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Configurazione di una channel factory
In questo esempio viene descritto l'utilizzo di <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>.<xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> consente la gestione centrale della configurazione client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Può essere anche utile in scenari nei quali la configurazione viene selezionata o modificata dopo la fase di caricamento del dominio dell'applicazione.  
  
## Dimostrazione  
 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>  
  
## Discussione  
 In questo esempio viene descritto come utilizzare <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> per aggiungere uno specifico file di configurazione a un'applicazione client, senza che sia necessario utilizzare il file di configurazione dell'applicazione predefinito.  
  
 L'esempio è costituito da due progetti.Il primo progetto è un servizio semplice in esecuzione per rispondere a messaggi provenienti dai client.Il secondo progetto è un'applicazione client che compila due oggetti <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> utilizzando un <xref:System.Configuration.ExeConfigurationFileMap> per il file di configurazione Test.config e li utilizza per comunicare con il servizio.Entrambi i client comunicano con il servizio utilizzando la configurazione specificata in Test.config.  
  
 Il codice seguente aggiunge un file di configurazione personalizzato a un'applicazione client.  
  
```  
ExeConfigurationFileMap fileMap = new ExeConfigurationFileMap();  
fileMap.ExeConfigFilename = "Test.config";  
Configuration newConfiguration = ConfigurationManager.OpenMappedExeConfiguration(fileMap, ConfigurationUserLevel.None);  
  
ConfigurationChannelFactory<ICalculatorChannel> factory1 = new ConfigurationChannelFactory<ICalculatorChannel>("endpoint1", newConfiguration, new EndpointAddress("http://localhost:8000/servicemodelsamples/service"));  
ICalculatorChannel client1 = factory1.CreateChannel();  
  
```  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] con privilegi di amministratore.  
  
2.  Fare clic con il pulsante destro del mouse sulla soluzione ConfigurationChannelFactory \(2 progetti\), quindi selezionare **Proprietà**.  
  
3.  In **Proprietà comuni** selezionare **Progetto di avvio**, quindi fare clic su **Progetti di avvio multipli**.  
  
4.  Spostare il progetto **Service** all'inizio dell'elenco, con **Azione 'Avvia'**, quindi spostare il progetto **Client** dopo il progetto **Servizio**, anche in questo caso con **Azione 'Avvia'**, affinché il progetto **Client** venga eseguito dopo il progetto **Servizio**.  
  
5.  Fare clic su **OK**, quindi premere F5 \(o CTRL\+F5\) per eseguire l'esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\ConfigurationChannelFactory`