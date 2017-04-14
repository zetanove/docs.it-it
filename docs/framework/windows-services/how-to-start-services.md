---
title: "How to: Start Services | Microsoft Docs"
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
  - "Windows Service applications, starting"
  - "services, starting"
ms.assetid: 9ea77955-2d96-4c3d-913c-14db7604cdad
caps.latest.revision: 16
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 14
---
# How to: Start Services
Una volta installato il servizio, è necessario avviarlo.  All'avvio, viene chiamato il metodo <xref:System.ServiceProcess.ServiceBase.OnStart%2A> sulla classe di servizio.  In genere il metodo <xref:System.ServiceProcess.ServiceBase.OnStart%2A> definisce le operazioni che il servizio dovrà eseguire.  Dopo l'avvio, un servizio rimane attivo finché non viene sospeso o interrotto manualmente.  
  
 I servizi possono essere impostati per l'avvio automatico o manuale.  Un servizio con avvio automatico si avvia quando il computer sul quale è installato viene riavviato o acceso per la prima volta.  Un servizio con avvio manuale deve essere avviato dall'utente.  
  
> [!NOTE]
>  Per impostazione predefinita, i servizi creati con [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] vengono avviati manualmente.  
  
 Il servizio può essere avviato manualmente da **Esplora server**, da **Gestione controllo servizi** oppure dal codice, mediante il componente <xref:System.ServiceProcess.ServiceController>.  
  
 Per stabilire se un servizio deve essere avviato manualmente o automaticamente, impostare la proprietà <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> della classe <xref:System.ServiceProcess.ServiceInstaller>.  
  
### Per definire il metodo di avvio di un servizio  
  
1.  Dopo aver creato il servizio, aggiungere i programmi di installazione necessari.  Per ulteriori informazioni, vedere [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md).  
  
2.  Nella finestra di progettazione fare clic sul programma di installazione del servizio in uso.  
  
3.  Nella finestra **Proprietà** impostare la proprietà <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> su uno dei seguenti valori:  
  
    |Per avviare il servizio|Impostare il valore|  
    |-----------------------------|-------------------------|  
    |Al riavvio del computer|**Automatic**|  
    |Con un'operazione esplicita dell'utente|**Manual**|  
  
    > [!TIP]
    >  Per impedire che il servizio venga avviato, impostare la proprietà <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> su **Disabled**.  Ciò può essere utile se occorre riavviare un server più volte e si desidera risparmiare tempo impedendo il normale avvio dei servizi.  
  
    > [!NOTE]
    >  Questa e altre proprietà possono essere modificate dopo l'installazione del servizio.  
  
     Un servizio per cui la proprietà <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> è impostata su **Manual** può essere avviato da **Esplora server**, da **Gestione controllo servizi di Windows** oppure dal codice.  È importante sottolineare che non tutti questi metodi avviano il servizio nel contesto di **Gestione controllo servizi**, poiché il controller viene effettivamente manipolato da **Esplora server** e dai metodi di avvio a livello di codice.  
  
### Per avviare manualmente un servizio da Esplora server  
  
1.  In **Esplora server** aggiungere il server desiderato, se non è presente nell'elenco.  Per ulteriori informazioni, vedere [How to: Access and Initialize Server Explorer\/Database Explorer](../Topic/How%20to:%20Access%20and%20Initialize%20Server%20Explorer-Database%20Explorer.md).  
  
2.  Espandere il nodo **Servizi**, quindi individuare il servizio che si desidera avviare.  
  
3.  Fare clic con il pulsante destro del mouse sul nome del servizio, quindi scegliere **Avvia**.  
  
### Per avviare manualmente un servizio da Gestione controllo servizi  
  
1.  Per aprire **Gestione controllo servizi**, effettuare una delle seguenti operazioni:  
  
    -   In Windows XP e 2000 Professional fare clic con il pulsante destro del mouse su **Risorse del computer** sul desktop, quindi scegliere **Gestione**.  Nella finestra di dialogo visualizzata espandere il nodo **Servizi e applicazioni**.  
  
         \-oppure\-  
  
    -   In Windows Server 2003 e Windows 2000 Server scegliere **Start**, scegliere **Programmi**, **Strumenti di amministrazione**, quindi **Servizi**.  
  
        > [!NOTE]
        >  In Windows NT versione 4.0 è possibile visualizzare questa finestra di dialogo dal **Pannello di controllo**.  
  
     Nella sezione **Servizi** della finestra viene visualizzato il servizio.  
  
2.  Fare clic con il pulsante destro del mouse sul servizio dopo averlo selezionato dall'elenco, quindi scegliere **Avvia**.  
  
### Per avviare manualmente un servizio da codice  
  
1.  Creare un'istanza della classe <xref:System.ServiceProcess.ServiceController>, quindi configurarla in modo che interagisca con il servizio da amministrare.  
  
2.  Chiamare il metodo <xref:System.ServiceProcess.ServiceController.Start%2A> per avviare il servizio.  
  
## Vedere anche  
 [Introduction to Windows Service Applications](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)   
 [How to: Create Windows Services](../../../docs/framework/windows-services/how-to-create-windows-services.md)   
 [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)   
 [How to: Access and Initialize Server Explorer\/Database Explorer](../Topic/How%20to:%20Access%20and%20Initialize%20Server%20Explorer-Database%20Explorer.md)