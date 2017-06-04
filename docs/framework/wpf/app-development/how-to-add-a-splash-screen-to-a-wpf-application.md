---
title: "Procedura: aggiungere una schermata iniziale in un&#39;applicazione WPF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "schermata iniziale [WPF]"
  - "SplashScreen (classe) [WPF]"
  - "finestra di avvio [WPF]"
  - "WPF, schermata iniziale"
ms.assetid: d70a25c4-5fb9-4c27-b01d-b1b8ef39b3fd
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: aggiungere una schermata iniziale in un&#39;applicazione WPF
In questo argomento viene illustrato come aggiungere una finestra di avvio, o *schermata iniziale*, in un'applicazione WPF \(Windows Presentation Foundation\).  
  
### Per aggiungere un'immagine esistente come schermata iniziale  
  
1.  Creare o trovare un'immagine che si desidera utilizzare come schermata iniziale.  È possibile utilizzare qualsiasi formato di immagine supportato da Componente Windows Imaging \(WIC\).  È possibile, ad esempio, utilizzare i formati BMP, GIF, JPEG, PNG e TIFF.  
  
2.  Aggiungere il file di immagine al progetto di applicazione WPF.  Per ulteriori informazioni, vedere [NIB:How to: Add Existing Items to a Project](http://msdn.microsoft.com/it-it/15f4cfb7-78ab-457f-9f14-099a25a6a2d3).  
  
3.  In Esplora soluzioni selezionare l'immagine desiderata.  
  
4.  Nella finestra Proprietà fare clic sulla freccia a discesa della proprietà **Operazione di compilazione**.  
  
5.  Selezionare **Schermata iniziale** nell'elenco a discesa.  
  
    > [!NOTE]
    >  Se l'opzione **Schermata iniziale** non è visibile, accertarsi di utilizzare [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)] SP1 o versioni successive.  
  
6.  Premere F5 per compilare ed eseguire l'applicazione.  
  
     L'immagine della schermata iniziale viene visualizzata nella parte centrale dello schermo e si dissolve quando viene visualizzata la finestra dell'applicazione principale.  
  
### Per rimuovere la schermata iniziale da un'applicazione  
  
1.  In Esplora soluzioni selezionare l'immagine della schermata iniziale.  
  
2.  Nella finestra Proprietà impostare **Operazione di compilazione** su **Nessuna**.  
  
### Per rimuovere la schermata iniziale da un'applicazione  
  
-   In Esplora soluzioni eliminare l'immagine della schermata iniziale.  
  
-   Escludere l'immagine della schermata iniziale dal progetto.  
  
## Vedere anche  
 <xref:System.Windows.SplashScreen>   
 [NIB:How to: Add Existing Items to a Project](http://msdn.microsoft.com/it-it/15f4cfb7-78ab-457f-9f14-099a25a6a2d3)