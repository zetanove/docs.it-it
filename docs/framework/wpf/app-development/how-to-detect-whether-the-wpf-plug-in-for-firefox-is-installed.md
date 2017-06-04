---
title: "Procedura: rilevare se il plug-in WPF per Firefox &#232; installato o meno | Microsoft Docs"
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
  - "controllo del plug-in per Firefox [WPF]"
  - "rilevamento di installazioni Firefox [WPF]"
  - "rilevamento dell'installazione del plug-in WPF per Firefox [WPF]"
  - "Firefox [WPF], rilevamento dell'installazione"
  - "plug-in per Firefox [WPF]"
ms.assetid: 5f839373-e3fb-44f1-88ad-4a0761f02189
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: rilevare se il plug-in WPF per Firefox &#232; installato o meno
Il plug\-in [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] per Firefox consente di eseguire nel browser Mozilla Firefox file di un'[!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] e file XAML separati.  In questo argomento viene fornito uno script HTML e JavaScript utilizzabile dagli amministratori per determinare se il plug\-in WPF per Firefox 2.0\+ è installato o meno.  
  
> [!NOTE]
>  Per ulteriori informazioni sull'installazione, la distribuzione e il rilevamento di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], vedere [Installazione di .NET Framework](../../../../docs/framework/install/guide-for-developers.md).  
  
## Esempio  
 Quando viene installato [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)], il computer client viene configurato con un plug\-in WPF per Firefox.  Lo script di esempio verifica la presenza del plug\-in WPF e quindi visualizza un messaggio di stato appropriato.  
  
```  
<HTML>  
  
  <HEAD>  
    <TITLE>Test for the WPF plug-in for Firefox</TITLE>  
    <META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=utf-8" />  
    <SCRIPT type="text/javascript">  
    <!--  
    function OnLoad()  
    {  
  
       // Check for the WPF plug-in for Firefox and report  
       var msg = "The WPF plug-in for Firefox is ";  
       var wpfPlugin = navigator.plugins["Windows Presentation Foundation"];  
       if( wpfPlugin != null ) {  
          document.writeln(msg + " installed.");  
       }  
       else {  
          document.writeln(msg + " not installed. Please install or reinstall the .NET Framework 3.5.");  
       }  
    }  
    -->  
    </SCRIPT>  
  </HEAD>  
  
  <BODY onload="OnLoad()" />  
  
</HTML>  
```  
  
 Se la verifica della presenza del plug\-in WPF per Firefox ha esito positivo, verrà visualizzato il messaggio di stato seguente:  
  
 `The WPF plug-in for Firefox is installed.`  
  
 In caso contrario, il messaggio di stato visualizzato sarà il seguente:  
  
 `The WPF plug-in for Firefox is not installed.  Please install or reinstall the .NET Framework 3.5.`  
  
## Vedere anche  
 [Verificare se .NET Framework 3.0 è installato](../../../../docs/framework/wpf/app-development/how-to-detect-whether-the-net-framework-3-0-is-installed.md)   
 [Verificare se .NET Framework 3.5 è installato](../../../../docs/framework/wpf/app-development/how-to-detect-whether-the-net-framework-3-5-is-installed.md)   
 [Panoramica delle applicazioni browser XAML di WPF](../../../../docs/framework/wpf/app-development/wpf-xaml-browser-applications-overview.md)