---
title: "Passaggio di un URI a Windows Runtime | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Windows Runtime, supporto per .NET Framework"
  - "Windows Runtime, passare un URI al"
ms.assetid: 3eb5ce6f-f304-4f87-8e81-0f25092f5ad4
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 10
---
# Passaggio di un URI a Windows Runtime
I metodi di Windows Runtime accettano solo URI assoluti. Se si passa un URI relativo a un metodo [!INCLUDE[wrt](../../../includes/wrt-md.md)], viene generata un'eccezione <xref:System.ArgumentException>. Motivo: quando si usa [!INCLUDE[wrt](../../../includes/wrt-md.md)] nel codice di .NET Framework, la classe [Windows.Foundation.Uri](http://go.microsoft.com/fwlink/p/?LinkId=238376) viene visualizzata come <xref:System.Uri?displayProperty=fullName> in IntelliSense. La classe <xref:System.Uri?displayProperty=fullName> accetta URI relativi, a differenza della classe [Windows.Foundation.Uri](http://go.microsoft.com/fwlink/p/?LinkId=238376). Questo accade anche per i metodi esposti nei componenti [!INCLUDE[wrt](../../../includes/wrt-md.md)]. Se il componente espone un metodo che accetta un URI, la firma nel codice include <xref:System.Uri?displayProperty=fullName>. Tuttavia, per gli utenti del componente, la firma include [Windows.Foundation.Uri](http://go.microsoft.com/fwlink/p/?LinkId=238376). Un URI che viene passato al componente deve essere un URI assoluto.  
  
 In questo argomento viene illustrato come rilevare un URI assoluto e come crearne uno quando si fa riferimento a una risorsa nel pacchetto dell'app.  
  
## Rilevamento e utilizzo di un URI assoluto  
 Usare la proprietà <xref:System.Uri.IsAbsoluteUri%2A?displayProperty=fullName> per verificare che un URI sia assoluto prima di passarlo a [!INCLUDE[wrt](../../../includes/wrt-md.md)]. È consigliabile usare questa proprietà anziché ricevere l'eccezione <xref:System.ArgumentException> e gestirla.  
  
## Uso di un URI assoluto per una risorsa nel pacchetto dell'app  
 Se si vuole specificare un URI per una risorsa contenuta nel pacchetto dell'app, è possibile usare lo schema `ms-appx` o `ms-appx-web` per creare un URI assoluto.  
  
 L'esempio seguente illustra come impostare la proprietà [Source](http://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.webview.source.aspx) per un controllo [WebView](http://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.webview.aspx) e la proprietà [Source](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.image.source.aspx) per un controllo [Image](http://msdn.microsoft.com/library/windows/apps/br242752.aspx) su risorse contenute in una cartella denominata Pages usando sia XAML sia codice.  
  
 [!code-xml[System.URIToWindowsURI#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.uritowindowsuri/cs/mainpage.xaml#1)]  
[!code-csharp[System.URIToWindowsURI#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.uritowindowsuri/cs/mainpage.xaml.cs#2)]
[!code-vb[System.URIToWindowsURI#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.uritowindowsuri/vb/mainpage.xaml.vb#2)]  
  
 Per altre informazioni su questi schemi, vedere [Schemi URI](http://msdn.microsoft.com/library/windows/apps/jj655406.aspx) nel Centro sviluppatori Windows.  
  
## Vedere anche  
 [Supporto .NET Framework per applicazioni Windows Store e Windows Runtime](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)