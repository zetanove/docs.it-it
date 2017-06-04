---
title: "Procedura dettagliata: hosting di contenuto Direct3D9 in WPF | Microsoft Docs"
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
  - "Direct3D9 [interoperabilità WPF], hosting di contenuto Direct3D9"
  - "WPF, hosting di contenuto Direct3D9"
ms.assetid: 60983736-0ab5-42cc-8b16-e9fbde261a43
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura dettagliata: hosting di contenuto Direct3D9 in WPF
In questa procedura dettagliata viene illustrato come eseguire l'hosting di contenuto Direct3D9 in un'applicazione WPF \(Windows Presentation Foundation\).  
  
 Questa procedura dettagliata prevede l'esecuzione delle attività seguenti:  
  
-   Creazione di un progetto WPF per ospitare il contenuto Direct3D9.  
  
-   Importazione del contenuto Direct3D9.  
  
-   Visualizzazione del contenuto Direct3D9 mediante la classe <xref:System.Windows.Interop.D3DImage>.  
  
 Al termine, si sarà in grado di eseguire l'hosting di contenuto Direct3D9 in un'applicazione WPF.  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
-   DirectX SDK 9 o versione successiva  
  
-   Una DLL con contenuto Direct3D9 in un formato compatibile con WPF.  Per ulteriori informazioni, vedere [Interoperatività di WPF e Direct3D9](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md) e [Procedura dettagliata: creazione di contenuto Direct3D9 per l'hosting in WPF](../../../../docs/framework/wpf/advanced/walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md).  
  
## Creazione del progetto WPF  
 Il primo passaggio consiste nella creazione del progetto per l'applicazione WPF.  
  
#### Per creare il progetto WPF  
  
-   Creare un nuovo progetto Applicazione WPF in Visual C\# denominato `D3DHost`.  Per ulteriori informazioni, vedere [Procedura: creare un nuovo progetto di applicazione WPF](http://msdn.microsoft.com/it-it/1f6aea7a-33e1-4d3f-8555-1daa42e95d82).  
  
     MainWindow.xaml viene aperto in [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].  
  
## Importazione del contenuto Direct3D9  
 Per importare il contenuto Direct3D9 da una DLL non gestita si utilizza l'attributo `DllImport`.  
  
#### Per importare il contenuto Direct3D9  
  
1.  Aprire MainWindow.xaml.cs nell'editor di codice.  
  
2.  Sostituire il codice generato automaticamente con il codice seguente.  
  
     [!code-csharp[System.Windows.Interop.D3DImage#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml.cs#1)]  
  
## Hosting del contenuto Direct3D9  
 Utilizzare infine la classe <xref:System.Windows.Interop.D3DImage> per ospitare il contenuto Direct3D9.  
  
#### Per ospitare il contenuto Direct3D9  
  
1.  In MainWindow.xaml sostituire il codice XAML generato automaticamente con il codice XAML seguente.  
  
     [!code-xml[System.Windows.Interop.D3DImage#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml#10)]  
  
2.  Compilare il progetto.  
  
3.  Copiare la DLL con il contenuto Direct3D9 nella cartella bin\/Debug.  
  
4.  Premere F5 per eseguire il progetto.  
  
     Il contenuto Direct3D9 verrà visualizzato nell'applicazione WPF.  
  
## Vedere anche  
 <xref:System.Windows.Interop.D3DImage>   
 [Considerazioni sulle prestazioni per l'interoperabilità fra Direct3D9 e WPF](../../../../docs/framework/wpf/advanced/performance-considerations-for-direct3d9-and-wpf-interoperability.md)