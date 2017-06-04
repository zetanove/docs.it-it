---
title: "Procedura: specificare una posizione personalizzata per un controllo Popup | Microsoft Docs"
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
  - "Popup (controllo), specifica di posizioni personalizzate"
ms.assetid: 28c24f39-d3aa-4ee2-b950-384b4a5dab92
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: specificare una posizione personalizzata per un controllo Popup
In questo esempio viene illustrato come specificare una posizione personalizzata per un controllo <xref:System.Windows.Controls.Primitives.Popup> quando la proprietà <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è impostata su <xref:System.Windows.Controls.Primitives.PlacementMode>.  
  
## Esempio  
 Quando la proprietà <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è impostata su <xref:System.Windows.Controls.Primitives.PlacementMode>, l'oggetto <xref:System.Windows.Controls.Primitives.Popup> chiama un'istanza definita del delegato <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback>.  Questo delegato restituisce un insieme di possibili punti relativi all'angolo superiore sinistro dell'area di destinazione e all'angolo superiore sinistro dell'oggetto <xref:System.Windows.Controls.Primitives.Popup>.  L'oggetto <xref:System.Windows.Controls.Primitives.Popup> viene posizionato nel punto che offre la migliore visibilità.  
  
 Nell'esempio riportato di seguito viene illustrato come definire la posizione di un oggetto <xref:System.Windows.Controls.Primitives.Popup> impostando la proprietà <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> su <xref:System.Windows.Controls.Primitives.PlacementMode>.  Viene inoltre illustrato come creare e assegnare un delegato <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> per posizionare l'oggetto <xref:System.Windows.Controls.Primitives.Popup>.  Il delegato di callback restituisce due oggetti <xref:System.Windows.Controls.Primitives.CustomPopupPlacement>.  Se l'oggetto <xref:System.Windows.Controls.Primitives.Popup> è nascosto da un bordo dello schermo nella prima posizione, l'oggetto <xref:System.Windows.Controls.Primitives.Popup> viene collocato nella seconda posizione.  
  
 [!code-xml[PopupCustomPlacement#CustomPlacement](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml#customplacement)]  
  
 [!code-csharp[PopupCustomPlacement#DelegateInstance](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml.cs#delegateinstance)]
 [!code-vb[PopupCustomPlacement#DelegateInstance](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PopupCustomPlacement/visualbasic/window1.xaml.vb#delegateinstance)]  
  
 [!code-csharp[PopupCustomPlacement#DelegateDefinition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml.cs#delegatedefinition)]
 [!code-vb[PopupCustomPlacement#DelegateDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PopupCustomPlacement/visualbasic/window1.xaml.vb#delegatedefinition)]  
  
 Per l'esempio completo, vedere [Esempio di posizionamento di un oggetto Popup](http://go.microsoft.com/fwlink/?LinkID=160032) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Controls.Primitives.Popup>   
 [Cenni preliminari sul controllo Popup](../../../../docs/framework/wpf/controls/popup-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/popup-how-to-topics.md)