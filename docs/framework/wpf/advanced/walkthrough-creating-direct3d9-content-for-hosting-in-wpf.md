---
title: "Procedura dettagliata: creazione di contenuto Direct3D9 per l&#39;hosting in WPF | Microsoft Docs"
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
  - "Direct3D9 [interoperabilità WPF], creazione di contenuto Direct3D9"
  - "WPF, creazione di contenuto Direct3D9"
ms.assetid: 286e98bc-1eaa-4b5e-923d-3490a9cca5fc
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura dettagliata: creazione di contenuto Direct3D9 per l&#39;hosting in WPF
In questa procedura dettagliata viene illustrato come creare contenuto Direct3D9 adatto per l'hosting in un'applicazione Windows Presentation Foundation \(WPF\).  Per ulteriori informazioni sull'hosting del contenuto Direct3D9 nelle applicazioni WPF, vedere [Interoperatività di WPF e Direct3D9](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md).  
  
 Questa procedura dettagliata prevede l'esecuzione delle attività seguenti:  
  
-   Creazione di un progetto Direct3D9.  
  
-   Configurazione del progetto Direct3D9 per l'hosting in un'applicazione WPF.  
  
 Al termine si disporrà di una DLL con contenuto Direct3D9 adatto per l'utilizzo in un'applicazione WPF.  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
-   DirectX SDK 9 o versione successiva  
  
## Creazione del progetto Direct3D9  
 Il primo passaggio consiste nella creazione e nella configurazione del progetto Direct3D9.  
  
#### Per creare il progetto Direct3D9  
  
1.  Creare un nuovo progetto Win32 in C\+\+ denominandolo `D3DContent`.  
  
     Verrà visualizzata la schermata iniziale della Creazione guidata applicazione Win32.  
  
2.  Scegliere **Avanti**.  
  
     Verrà visualizzata la schermata Impostazioni applicazione.  
  
3.  Nella sezione **Tipo di applicazione** selezionare l'opzione **DLL**.  
  
4.  Fare clic su **Fine**.  
  
     Il progetto D3DContent verrà generato.  
  
5.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto D3DContent e scegliere **Proprietà**.  
  
     Verrà visualizzata la finestra di dialogo **Pagine delle proprietà di D3DContent**.  
  
6.  Scegliere il nodo **C\/C\+\+**.  
  
7.  Nel campo **Directory di inclusione aggiuntive** specificare il percorso della cartella di inclusione DirectX.  Il percorso predefinito della cartella è %Programmi%\\Microsoft DirectX SDK \(*versione*\)\\Include.  
  
8.  Fare doppio clic sul nodo **Linker** per espanderlo.  
  
9. Nel campo **Directory librerie aggiuntive** specificare il percorso della cartella delle librerie DirectX.  Il percorso predefinito della cartella è %Programmi%\\Microsoft DirectX SDK \(*versione*\)\\Lib\\x86.  
  
10. Scegliere il nodo **Input**.  
  
11. Nel campo **Dipendenze aggiuntive** aggiungere i file `d3d9.lib` e `d3dx9.lib`.  
  
12. In Esplora soluzioni aggiungere al progetto un nuovo file di definizione moduli \(.def\) denominandolo `D3DContent.def`.  
  
## Creazione del contenuto Direct3D9  
 Per ottenere le prestazioni migliori, è necessario che il contenuto Direct3D9 utilizzi impostazioni particolari.  Nel codice seguente viene indicato come creare una superficie Direct3D9 con le caratteristiche di prestazione migliori.  Per ulteriori informazioni, vedere [Considerazioni sulle prestazioni per l'interoperabilità fra Direct3D9 e WPF](../../../../docs/framework/wpf/advanced/performance-considerations-for-direct3d9-and-wpf-interoperability.md).  
  
#### Per creare il contenuto Direct3D9  
  
1.  Utilizzando Esplora soluzioni, aggiungere tre classi C\+\+ al progetto denominato nel modo seguente.  
  
     `CRenderer` \(con distruttore virtuale\)  
  
     `CRendererManager`  
  
     `CTriangleRenderer`  
  
2.  Aprire Renderer.h nell'editor del codice e sostituire il codice generato automaticamente con il codice seguente.  
  
     [!code-cpp[System.Windows.Interop.D3DImage#RendererH](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.h#rendererh)]  
  
3.  Aprire Renderer.cpp nell'editor del codice e sostituire il codice generato automaticamente con il codice seguente.  
  
     [!code-cpp[System.Windows.Interop.D3DImage#RendererCPP](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderercpp)]  
  
4.  Aprire RendererManager.h nell'editor del codice e sostituire il codice generato automaticamente con il codice seguente.  
  
     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerH](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.h#renderermanagerh)]  
  
5.  Aprire RendererManager.cpp nell'editor del codice e sostituire il codice generato automaticamente con il codice seguente.  
  
     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerCPP](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanagercpp)]  
  
6.  Aprire TriangleRenderer.h nell'editor del codice e sostituire il codice generato automaticamente con il codice seguente.  
  
     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererH](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.h#trianglerendererh)]  
  
7.  Aprire TriangleRenderer.cpp nell'editor del codice e sostituire il codice generato automaticamente con il codice seguente.  
  
     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererCPP](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.cpp#trianglerenderercpp)]  
  
8.  Aprire stdafx.h nell'editor del codice e sostituire il codice generato automaticamente con il codice seguente.  
  
     [!code-cpp[System.Windows.Interop.D3DImage#StdafxH](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/stdafx.h#stdafxh)]  
  
9. Aprire dllmain.cpp nell'editor del codice e sostituire il codice generato automaticamente con il codice seguente.  
  
     [!code-cpp[System.Windows.Interop.D3DImage#DllMain](../../../../samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/dllmain.cpp#dllmain)]  
  
10. Aprire D3DContent.def nell'editor del codice.  
  
11. Sostituire il codice generato automaticamente con il codice seguente.  
  
    ```  
  
    LIBRARY "D3DContent"  
  
    EXPORTS  
  
    SetSize  
    SetAlpha  
    SetNumDesiredSamples  
    SetAdapter  
  
    GetBackBufferNoRef  
    Render  
    Destroy  
  
    ```  
  
12. Compilare il progetto.  
  
## Passaggi successivi  
  
-   Ospitare il contenuto Direct3D9 in un'applicazione WPF.  Per ulteriori informazioni, vedere [Procedura dettagliata: hosting di contenuto Direct3D9 in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-direct3d9-content-in-wpf.md).  
  
## Vedere anche  
 <xref:System.Windows.Interop.D3DImage>   
 [Considerazioni sulle prestazioni per l'interoperabilità fra Direct3D9 e WPF](../../../../docs/framework/wpf/advanced/performance-considerations-for-direct3d9-and-wpf-interoperability.md)   
 [Procedura dettagliata: hosting di contenuto Direct3D9 in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-direct3d9-content-in-wpf.md)