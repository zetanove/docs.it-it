---
title: "How to: Add Installers to Your Service Application | Microsoft Docs"
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
  - "Windows Service applications, deploying"
  - "installation components, adding to services"
  - "installers, adding to services"
  - "Windows Service applications, adding installers"
  - "services, adding installers"
  - "ServiceInstaller class, adding installers to services"
  - "ServiceProcessInstaller class, adding installers to services"
ms.assetid: 8b698e9a-b88e-4f44-ae45-e0c5ea0ae5a8
caps.latest.revision: 14
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 14
---
# How to: Add Installers to Your Service Application
Visual Studio fornisce componenti di installazione in grado di installare risorse associate alle applicazioni di servizio.  I componenti di installazione registrano un singolo servizio sul sistema su cui viene installato e comunicano a Gestione controllo servizi l'esistenza del servizio.  Quando si utilizza un'applicazione di servizio, è possibile selezionare un collegamento nella finestra Proprietà per aggiungere automaticamente i programmi di installazione appropriati per il progetto.  
  
> [!NOTE]
>  I valori delle proprietà per il servizio vengono copiati dalla classe di servizio nella classe del programma di installazione.  Se si aggiornano nella classe di servizio, i valori delle proprietà non vengono aggiornati automaticamente nel programma di installazione.  
  
 Quando in un progetto viene aggiunto un programma di installazione, nel progetto vengono create una nuova classe, denominata `ProjectInstaller` per impostazione predefinita, e le istanze dei componenti di installazione appropriati.  Questa classe agisce da punto centrale per tutti i componenti di installazione richiesti dal progetto.  Se ad esempio si aggiunge un secondo servizio all'applicazione e si fa clic sul collegamento Aggiungi programma di installazione, non verrà creata una seconda classe per il programma di installazione, ma il componente di installazione aggiuntivo necessario per il secondo servizio verrà aggiunto alla classe esistente.  
  
 Non occorre scrivere codice specifico nei programmi di installazione per installare correttamente i servizi.  Può essere talvolta necessario modificare il contenuto dei programmi di installazione per aggiungere una determinata funzionalità al processo di installazione.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per aggiungere programmi di installazione all'applicazione di servizio  
  
1.  In **Esplora soluzioni** accedere alla visualizzazione **Progettazione** per il servizio a cui si desidera aggiungere un componente di installazione.  
  
2.  Fare clic sullo sfondo della finestra di progettazione per selezionare il servizio anziché parte del suo contenuto.  
  
3.  Nella finestra di progettazione fare clic con il pulsante destro del mouse e scegliere **Aggiungi programma di installazione**.  
  
     Al progetto verranno aggiunti una nuova classe, denominata `ProjectInstaller`, e due componenti di installazione, <xref:System.ServiceProcess.ServiceProcessInstaller> e <xref:System.ServiceProcess.ServiceInstaller>. I valori delle proprietà del servizio verranno copiati nei componenti.  
  
4.  Fare clic sul componente <xref:System.ServiceProcess.ServiceInstaller>, quindi verificare che il valore della proprietà <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> sia impostato sullo stesso valore della proprietà <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> del servizio stesso.  
  
5.  Per stabilire la modalità del servizio, fare clic sul componente <xref:System.ServiceProcess.ServiceInstaller> , quindi impostare la proprietà <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> sul valore appropriato.  
  
    |Valore|Risultato|  
    |------------|---------------|  
    |<xref:System.ServiceProcess.ServiceStartMode>|Il servizio deve essere avviato manualmente dopo l'installazione.  Per ulteriori informazioni, vedere [How to: Start Services](../../../docs/framework/windows-services/how-to-start-services.md).|  
    |<xref:System.ServiceProcess.ServiceStartMode>|Il servizio si avvia automaticamente ad ogni riavvio del computer.|  
    |<xref:System.ServiceProcess.ServiceStartMode>|Il servizio non può essere avviato.|  
  
6.  Per determinare il contesto di sicurezza in cui verrà eseguito il servizio, fare clic sul componente <xref:System.ServiceProcess.ServiceProcessInstaller>, quindi impostare i valori delle proprietà appropriati.  Per ulteriori informazioni, vedere [How to: Specify the Security Context for Services](../../../docs/framework/windows-services/how-to-specify-the-security-context-for-services.md).  
  
7.  Eseguire l'override dei metodi per i quali si desidera definire un funzionamento personalizzato.  
  
8.  Ripetere i passaggi da 1 a 7 per ogni ulteriore servizio del progetto.  
  
    > [!NOTE]
    >  Per ogni altro servizio del progetto, è necessario aggiungere un ulteriore componente <xref:System.ServiceProcess.ServiceInstaller> alla classe `ProjectInstaller` del progetto.  Il componente <xref:System.ServiceProcess.ServiceProcessInstaller> aggiunto al passaggio 3 può essere utilizzato con tutti i singoli programmi di installazione di servizi del progetto.  
  
## Vedere anche  
 [Introduction to Windows Service Applications](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)   
 [How to: Install and Uninstall Services](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)   
 [How to: Start Services](../../../docs/framework/windows-services/how-to-start-services.md)   
 [How to: Specify the Security Context for Services](../../../docs/framework/windows-services/how-to-specify-the-security-context-for-services.md)