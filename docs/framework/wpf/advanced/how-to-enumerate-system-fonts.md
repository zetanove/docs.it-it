---
title: "Procedura: enumerare i caratteri del sistema | Microsoft Docs"
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
  - "enumerazione, caratteri del sistema"
  - "tipi di carattere, enumerazione"
  - "caratteri del sistema, enumerazione"
  - "tipografia, enumerazione dei tipi di carattere del sistema"
ms.assetid: 36e37791-55b9-4f01-a496-5cc10335e6a6
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: enumerare i caratteri del sistema
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come enumerare i tipi di carattere della raccolta dei tipi di carattere del sistema.  Il nome della famiglia di caratteri di ogni <xref:System.Windows.Media.FontFamily> all'interno di <xref:System.Windows.Media.Fonts.SystemFontFamilies%2A> viene aggiunto come elemento a una casella combinata.  
  
 [!code-csharp[TextOverview#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextOverview/CSharp/Window1.xaml.cs#100)]
 [!code-vb[TextOverview#100](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextOverview/visualbasic/window1.xaml.vb#100)]  
  
 Se più versioni della stessa famiglia di caratteri risiedono nella stessa directory, l'enumerazione dei tipi di carattere [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] restituisce la versione più recente del tipo di carattere.  Se le informazioni sulla versione non forniscono la risoluzione, viene restituito il tipo di carattere con il timestamp più recente.  Se le informazioni sul timestamp sono uguali, viene restituito il primo file del tipo di carattere nell'ordine alfabetico.