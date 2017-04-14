---
title: "Configurazione dell&#39;applicazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a2f995b0-669d-4721-b00f-4561ec7eb6a4
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Configurazione dell&#39;applicazione
In [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene utilizzato il sistema di configurazione .NET ed è possibile configurare i servizi sia nell'ambito del computer che nell'ambito dell'applicazione.  
  
 Le impostazioni di configurazione definite da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si trovano nel gruppo di sezioni `<system.serviceModel>`.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] come configurare un servizio di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere gli argomenti seguenti:  
  
-   [Configurazione dei servizi](../../../../docs/framework/wcf/configuring-services.md)  
  
-   [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)  
  
 Le impostazioni delle configurazioni definite dall'applicazione sono definite nel gruppo di sezioni `<appSettings>`.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] impostazioni dell'applicazione nei file di configurazione .NET, vedere la pagina relativa a [\<appSettings\>](http://go.microsoft.com/fwlink/?LinkId=95159).  
  
## Utilizzo dell'Editor di configurazione  
 [Strumento Editor di configurazione \(SvcConfigEditor.exe\)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md) di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente ad amministratori e sviluppatori di creare e modificare le impostazioni di configurazione per i servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tramite un'interfaccia utente grafica.Con questo strumento è possibile gestire le impostazioni di associazioni, comportamenti, servizi e diagnostica di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] senza la necessità di modificare direttamente i file di configurazione XML.  
  
## Modifica dei file di configurazione in Visual Studio  
 Per modificare il file di configurazione di un progetto di servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)], selezionarlo con il pulsante destro del mouse in **Esplora soluzioni** e scegliere l'elemento del menu di scelta rapida **Modifica config WCF**.Verrà avviato [Strumento Editor di configurazione \(SvcConfigEditor.exe\)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md).  
  
> [!NOTE]
>  Se si modifica il file di configurazione di un progetto di servizio Web [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] facendo clic con il tasto destro del mouse su di esso in **Esplora soluzioni**, si noti che l'elemento del menu di scelta rapida**Modifica config WCF** è mancante.Per risolvere questo problema, fare clic sul menu  **Strumenti** e scegliere **Editor di configurazione del servizio WCF**.Quindi, fare clic con il tasto destro del mouse su un file di configurazione e utilizzare l'elemento del menu di scelta rapida **Modifica config WCF**.  
  
## Vedere anche  
 [Strumento Editor di configurazione \(SvcConfigEditor.exe\)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)   
 [Configurazione dei servizi](../../../../docs/framework/wcf/configuring-services.md)   
 [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)