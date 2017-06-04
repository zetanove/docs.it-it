---
title: "Procedura: navigare in avanti o indietro nella cronologia di navigazione | Microsoft Docs"
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
  - "history, navigazione, spostamento in avanti"
  - "navigazione, nella cronologia di navigazione (in avanti)"
ms.assetid: 5939d574-5f53-469e-85f5-1f2b13607caa
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: navigare in avanti o indietro nella cronologia di navigazione
In questo esempio viene illustrato come spostarsi in avanti o di nuovo sulle voci nella cronologia di navigazione.  
  
## Esempio  
 Il codice in esecuzione dal contenuto negli host possono spostarsi in avanti o indietro nella cronologia di navigazione, una voce per volta.  
  
-   <xref:System.Windows.Navigation.NavigationWindow> tramite  <xref:System.Windows.Navigation.NavigationService>  
  
-   <xref:System.Windows.Controls.Frame> tramite  <xref:System.Windows.Navigation.NavigationService>  
  
-   [!INCLUDE[TLA#tla_iegeneric](../../../../includes/tlasharptla-iegeneric-md.md)]  
  
 Prima che sia possibile spostarsi avanti di una voce, è necessario innanzitutto verificare che siano presenti voci nella cronologia di navigazione in avanti controllando **CanGoForward** proprietà.  Per spostarsi avanti di una voce, chiamate **GoForward** metodo.  Tale situazione è illustrata nell'esempio seguente:  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateForwardCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/HomePage.xaml.cs#navigateforwardcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateForwardCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/homepage.xaml.vb#navigateforwardcode)]  
  
 Prima di poter navigare all'indietro di una voce, è necessario innanzitutto verificare che siano presenti voci nella cronologia di navigazione indietro controllando **CanGoBack** proprietà.  Per spostarsi all'indietro di una voce, chiamate **GoBack** metodo.  Tale situazione è illustrata nell'esempio seguente:  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateBackCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/HomePage.xaml.cs#navigatebackcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateBackCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/homepage.xaml.vb#navigatebackcode)]  
  
 **CanGoForward**,  **GoForward**,  **CanGoBack**e  **GoBack** sono implementati da  <xref:System.Windows.Navigation.NavigationWindow>,  <xref:System.Windows.Controls.Frame>e  <xref:System.Windows.Navigation.NavigationService>.  
  
> [!NOTE]
>  Se si chiama **GoForward**e non sono presenti voci nella cronologia di navigazione in avanti, o se chiamate  **GoBack**e non sono presenti voci nella cronologia di navigazione indietro,  <xref:System.InvalidOperationException> viene generato l'evento.