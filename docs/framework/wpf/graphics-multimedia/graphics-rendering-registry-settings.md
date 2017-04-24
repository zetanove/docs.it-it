---
title: "Impostazioni del Registro di sistema per il rendering della grafica | Microsoft Docs"
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
  - "grafica [WPF], rendering"
  - "rendering della grafica"
  - "rendering della grafica, Registro di sistema (impostazioni)"
  - "rendering della grafica, risoluzione dei problemi"
  - "risoluzione dei problemi relativi al rendering della grafica"
ms.assetid: f4b41b42-327d-407c-b398-3ed5f505df8b
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Impostazioni del Registro di sistema per il rendering della grafica
In questo argomento viene fornita una panoramica delle impostazioni del Registro di sistema per il rendering della grafica di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che influiscono sulle applicazioni di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
   
  
<a name="overview"></a>   
## Utilizzo delle impostazioni del Registro di sistema per il rendering della grafica  
 Le impostazioni del Registro di sistema vengono fornite per la risoluzione dei problemi, per il debug e per il supporto tecnico.  Poiché le modifiche apportate al Registro di sistema influiscono su tutte le applicazioni di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è necessario che l'applicazione non modifichi queste chiavi del Registro di sistema, automaticamente o durante l'installazione.  
  
<a name="xpdmandwddm"></a>   
## Definizione di XPDM e WDDM  
 Alcune impostazioni del Registro di sistema per il rendering della grafica dispongono di valori predefiniti diversi, a seconda che la scheda video utilizzi un driver XPDM o WDDM.  XPDM è il modello di driver video di [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] e WDDM è il modello di driver video di Windows.  WDDM è disponibile nei computer che eseguono [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] e [!INCLUDE[win7](../../../../includes/win7-md.md)].  XPDM è disponibile nei computer che eseguono [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)], [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] e [!INCLUDE[TLA#tla_winnetsvrfam](../../../../includes/tlasharptla-winnetsvrfam-md.md)].  Per ulteriori informazioni su WDDM, vedere la [Guida alla progettazione del modello di driver video di Windows](http://go.microsoft.com/fwlink/?LinkId=178394) \(la pagina potrebbe essere in inglese\).  
  
<a name="registry_settings"></a>   
## Impostazioni del Registro di sistema  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono disponibili quattro impostazioni del Registro di sistema per il controllo del rendering in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:  
  
|Impostazione|Descrizione|  
|------------------|-----------------|  
|**Opzione Disabilita accelerazione hardware**|Specifica se l'accelerazione hardware deve essere abilitata.|  
|**Valore massimo di campionamento multiplo**|Specifica il grado di campionamento multiplo per l'anti\-aliasing del contenuto [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)].|  
|**Impostazione Data driver video necessaria**|Specifica se il sistema disabilita l'accelerazione hardware per i driver rilasciati prima di novembre 2004.|  
|**Opzione Utilizza unità di rasterizzazione dei riferimenti**|Specifica se [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] deve utilizzare l'unità di rasterizzazione dei riferimenti.|  
  
 A queste impostazioni è possibile accedere tramite qualsiasi utilità di configurazione esterna in cui sia possibile fare riferimento alle impostazioni del Registro di sistema di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  È possibile creare o modificare queste impostazioni accedendo direttamente ai valori utilizzando l'editor del Registro di sistema di [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)].  
  
<a name="disablehardwareacceleration"></a>   
## Opzione Disabilita accelerazione hardware  
  
|Chiave del Registro di sistema|Tipo di valore|  
|------------------------------------|--------------------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\DisableHWAcceleration`|DWORD|  
  
 L'**opzione Disabilita accelerazione hardware** consente di disabilitare l'accelerazione hardware con finalità di debug e di verifica.  Se in un'applicazione si notano elementi di rendering, provare a disattivare l'accelerazione hardware.  Se tali elementi scompaiono, potrebbe trattarsi di un problema del driver video.  
  
 L'**opzione Disabilita accelerazione hardware** è un valore DWORD pari a 0 o 1.  Un valore pari a 1 disabilita l'accelerazione hardware.  Un valore pari a 0 abilita l'accelerazione hardware, purché il sistema soddisfi i requisiti di accelerazione hardware. Per ulteriori informazioni, vedere [Livelli di rendering della grafica](../../../../docs/framework/wpf/advanced/graphics-rendering-tiers.md).  
  
<a name="maxmultisample"></a>   
## Valore massimo di campionamento multiplo  
  
|Chiave del Registro di sistema|Tipo di valore|  
|------------------------------------|--------------------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\MaxMultisampleType`|DWORD|  
  
 Il **valore massimo di campionamento multiplo** consente di regolare la quantità massima di anti\-aliasing del contenuto [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)].  Utilizzare questo livello per disabilitare l'anti\-aliasing [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)] in [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] o per abilitarlo in [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)].  
  
 Il **valore massimo di campionamento multiplo** è un valore DWORD compreso tra 0 e 16.  Un valore pari a 0 specifica la disabilitazione dell'anti\-aliasing del contenuto 3\-D, mentre un valore pari a 16 determinerà il tentativo di utilizzare un anti\-aliasing di campionamento multiplo fino a 16x, se supportato da una scheda video.  Prestare attenzione in quanto l'impostazione di questo valore della chiave del Registro di sistema nei computer mediante driver XPDM comporterà l'utilizzo di una grande quantità di memoria video aggiuntiva da parte delle applicazioni, una riduzione delle prestazioni del rendering di [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)], nonché possibili errori di rendering e problemi di stabilità.  
  
 Quando la chiave del Registro di sistema non è impostata, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è impostato su 0 per driver XPDM e su 4 per driver WDDM.  
  
<a name="requiredvideodriverdatesetting"></a>   
## Impostazione Data driver video necessaria  
  
|Chiave del Registro di sistema|Tipo di valore|  
|------------------------------------|--------------------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\RequiredVideoDriverDate`|String|  
  
 Nel novembre 2004, [!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] è stata rilasciata una nuova versione del driver che testa le linee guida; i driver scritti dopo tale data offrono una migliore stabilità.  Per impostazione predefinita, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizza la pipeline di accelerazione hardware per questi driver ed esegue il fallback al rendering del software per i driver XPDM pubblicati prima di tale data.  
  
 L'**impostazione Data driver video necessaria** consente di specificare una data alternativa minima per i driver XPDM.  È necessario specificare solo una data precedente a novembre 2004 se si prevede che il driver video sia stabile abbastanza per supportare [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 L'impostazione driver video necessaria viene applicata a un stringa nel formato seguente:  
  
||  
|-|  
|*AAAA* `/` *MM* `/` *GG*|  
  
 Dove *AAAA* è l'anno a quattro cifre, *MM* è il mese a due cifre e *GG* è il giorno a due cifre.  Se questo valore non è impostato, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizza novembre 2004 come data necessaria per il driver video.  
  
<a name="usereferencerasterizeroption"></a>   
## Opzione Utilizza unità di rasterizzazione dei riferimenti  
  
|Chiave del Registro di sistema|Tipo di valore|  
|------------------------------------|--------------------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\UseReferenceRasterizer`|DWORD|  
  
 L'**opzione Utilizza unità di rasterizzazione dei riferimenti** consente di forzare [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una modalità di rendering dell'hardware simulato per il debug: [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] entra in modalità hardware, ma utilizza l'unità di rasterizzazione software dei riferimenti [!INCLUDE[TLA#tla_d3d](../../../../includes/tlasharptla-d3d-md.md)], d3dref9.dll, anziché un dispositivo hardware effettivo.  
  
 L'unità di rasterizzazione dei riferimenti è molto lenta ma consente di ignorare il driver video per evitare qualsiasi problema di rendering causato da problemi legati al driver.  Per questo motivo, utilizzare l'unità di rasterizzazione dei riferimenti per determinare se i problemi di rendering sono causati dal driver video.  Il file d3dref9.dll deve trovarsi in un percorso accessibile all'applicazione, ad esempio in un percorso qualsiasi del percorso di sistema oppure nella directory locale dell'applicazione.  
  
 Nell'**opzione Utilizza unità di rasterizzazione dei riferimenti** viene applicato un valore DWORD.  Un valore 0 indica che l'unità di rasterizzazione dei riferimenti non è utilizzata.  Qualsiasi valore diverso da 0 determina l'utilizzo dell'unità di rasterizzazione dei riferimenti da parte di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
## Vedere anche  
 [Livelli di rendering della grafica](../../../../docs/framework/wpf/advanced/graphics-rendering-tiers.md)   
 [Cenni preliminari sul rendering della grafica WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)