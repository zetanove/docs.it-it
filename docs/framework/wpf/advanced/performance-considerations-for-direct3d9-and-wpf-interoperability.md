---
title: "Considerazioni sulle prestazioni per l&#39;interoperabilit&#224; fra Direct3D9 e WPF | Microsoft Docs"
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
  - "Direct3D9 [interoperabilità WPF], prestazioni"
  - "WPF, prestazioni di interoperabilità Direct3D9"
ms.assetid: ea8baf91-12fe-4b44-ac4d-477110ab14dd
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Considerazioni sulle prestazioni per l&#39;interoperabilit&#224; fra Direct3D9 e WPF
È possibile eseguire l'hosting di contenuto Direct3D9 utilizzando la classe <xref:System.Windows.Interop.D3DImage>.  L'hosting di contenuto Direct3D9 può influire sulle prestazioni dell'applicazione.  In questo argomento vengono descritte le procedure consigliate per ottimizzare le prestazioni quando si esegue l'hosting di contenuto Direct3D9 in un'applicazione WPF \(Windows Presentation Foundation\).  Rientrano nelle procedure consigliate la modalità di utilizzo di <xref:System.Windows.Interop.D3DImage> e le prassi migliori quando si utilizzano Windows Vista, Windows XP e visualizzazioni con più monitor.  
  
> [!NOTE]
>  Per gli esempi di codice che illustrano le procedure consigliate, vedere [Interoperatività di WPF e Direct3D9](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md).  
  
## Utilizzare D3DImage con parsimonia  
 Il rendering del contenuto Direct3D9 ospitato in un'istanza di <xref:System.Windows.Interop.D3DImage> non viene eseguito con la stessa velocità riscontrabile in un'applicazione Direct3D pura.  La copia della superficie e lo svuotamento del buffer dei comandi possono essere operazioni onerose.  Man mano che aumenta il numero delle istanze di <xref:System.Windows.Interop.D3DImage>, le oprazioni di svuotamento aumentano e di conseguenza le prestazioni peggiorano.  Pertanto è necessario utilizzare <xref:System.Windows.Interop.D3DImage> con parsimonia.  
  
## Procedure consigliate in Windows Vista  
 Per ottenere prestazioni ottimali in Windows Vista con una visualizzazione configurata per l'utilizzo di WDDM \(Windows Display Driver Model\), creare la superficie Direct3D9 in un dispositivo `IDirect3DDevice9Ex`.  Ciò abilita la condivisione della superficie.  È necessario che la scheda video supporti le funzionalità dei driver `D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES` e `D3DCAPS2_CANSHARERESOURCE` in Windows Vista.  Con qualsiasi altra impostazione la superficie viene copiata attraverso il software, con una conseguente significativa riduzione delle prestazioni.  
  
> [!NOTE]
>  Se in Windows Vista la visualizzazione è configurata per l'utilizzo di XDDM \(Windows XP Display Driver Model\), la superficie viene copiata sempre tramite software, indipendentemente dalle impostazioni.  Con le impostazioni e la scheda video appropriate si noteranno prestazioni migliori in Windows Vista quando si utilizza WDDM perché le copie della superficie vengono eseguite a livello di hardware.  
  
## Procedure consigliate in Windows XP  
 Per ottenere prestazioni ottimali in Windows XP, in cui è utilizzato XDDM \(Windows XP Display Driver Model\), creare una superficie bloccabile che si comporta correttamente quando viene chiamato il metodo `IDirect3DSurface9::GetDC`.  Internamente il metodo `BitBlt` trasferisce la superficie ai vari dispositivi a livello di hardware.  Il metodo `GetDC` funziona sempre sulle superfici XRGB.  Tuttavia, se nel computer client viene eseguito Windows XP con SP3 o SP2 e se il client dispone inoltre dell'aggiornamento rapido per la funzionalità delle finestre sovrapposte, il metodo funziona solo su superfici ARGB.  La scheda video deve supportare la funzionalità del driver `D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES`.  
  
 La profondità dello schermo di un desktop a 16 bit può ridurre significativamente le prestazioni.  È consigliabile un desktop a 32 bit.  
  
 Se si sviluppa per Windows Vista e Windows XP, testare le prestazioni in Windows XP.  L'esaurimento della memoria video in Windows XP costituisce un problema.  In Windows XP, inoltre, <xref:System.Windows.Interop.D3DImage> utilizza più memoria video e larghezza di banda rispetto a Windows Vista WDDM, in quanto è necessaria una copia di memoria video aggiuntiva.  Pertanto, per lo stesso hardware video è possibile prevedere prestazioni peggiori in Windows XP rispetto a Windows Vista.  
  
> [!NOTE]
>  XDDM è disponibile sia in Windows XP sia in Windows Vista mentre WDDM è disponibile solo in Windows Vista.  
  
## Procedure consigliate generali  
 Quando si crea il dispositivo, utilizzare il flag di creazione `D3DCREATE_MULTITHREADED`.  In tal modo le prestazioni peggiorano ma il sistema di rendering WPF esegue chiamate ai metodi in questo dispositivo da un altro thread.  Avere cura di seguire correttamente il protocollo di blocco per evitare che due thread accedano contemporaneamente al dispositivo.  
  
 Se il rendering viene eseguito in un thread gestito da WPF, è vivamente consigliabile creare il dispositivo con il flag di creazione `D3DCREATE_FPU_PRESERVE`.  Senza questa impostazione, il rendering D3D può ridurre l'accuratezza di operazioni a precisione doppia WPF e introdurre problemi di rendering.  
  
 L'affiancamento di un oggetto <xref:System.Windows.Interop.D3DImage> è veloce, a meno che si affianchi una superficie non\-pow2 senza supporto hardware o a meno che si affianchi un oggetto <xref:System.Windows.Media.DrawingBrush> o <xref:System.Windows.Media.VisualBrush> contenente un oggetto <xref:System.Windows.Interop.D3DImage>.  
  
## Procedure consigliate per le visualizzazioni con più monitor  
 Se si utilizza un computer collegato a più monitor, è necessario attenersi alle procedure consigliate descritte in precedenza.  Per la configurazione di più monitor vi sono inoltre altre considerazioni sulle prestazioni.  
  
 Al momento della creazione il buffer nascosto viene creato in un dispositivo e in un adattatore specifici ma WPF è in grado di visualizzare il front buffer in qualsiasi adattatore.  La copia tra i vari adattatori per aggiornare il front buffer può essere molto onerosa.  In Windows Vista, configurato per l'utilizzo di WDDM con più schede video e con un dispositivo `IDirect3DDevice9Ex`, se il front buffer è su una scheda diversa ma con la stessa scheda video, le prestazioni non ne risentono.  In Windows XP e XDDM con più schede video, tuttavia, la riduzione delle prestazioni è significativa quando il front buffer viene visualizzato in una scheda diversa rispetto al buffer nascosto.  Per ulteriori informazioni, vedere [Interoperatività di WPF e Direct3D9](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md).  
  
## Riepilogo delle prestazioni  
 Nella tabella seguente sono indicate le prestazioni dell'aggiornamento del front buffer in funzione della bloccabilità del sistema operativo, del formato pixel e della superficie.  Si presume che front buffer e buffer nascosto siano sulla stessa scheda.  A seconda della configurazione della scheda, gli aggiornamenti hardware sono generalmente molto più veloci degli aggiornamenti software.  
  
|Formato pixel della superficie|Windows Vista, WDDM e 9Ex|Altre configurazioni di Windows Vista|Windows XP SP3 o SP2 con aggiornamento rapido|Windows XP SP2|  
|------------------------------------|-------------------------------|-------------------------------------------|---------------------------------------------------|--------------------|  
|D3DFMT\_X8R8G8B8 \(non bloccabile\)|**Aggiornamento hardware**|Aggiornamento software|Aggiornamento software|Aggiornamento software|  
|D3DFMT\_X8R8G8B8 \(bloccabile\)|**Aggiornamento hardware**|Aggiornamento software|**Aggiornamento hardware**|**Aggiornamento hardware**|  
|D3DFMT\_A8R8G8B8 \(non bloccabile\)|**Aggiornamento hardware**|Aggiornamento software|Aggiornamento software|Aggiornamento software|  
|D3DFMT\_A8R8G8B8 \(bloccabile\)|**Aggiornamento hardware**|Aggiornamento software|**Aggiornamento hardware**|Aggiornamento software|  
  
## Vedere anche  
 <xref:System.Windows.Interop.D3DImage>   
 [Interoperatività di WPF e Direct3D9](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md)   
 [Procedura dettagliata: creazione di contenuto Direct3D9 per l'hosting in WPF](../../../../docs/framework/wpf/advanced/walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)   
 [Procedura dettagliata: hosting di contenuto Direct3D9 in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-direct3d9-content-in-wpf.md)