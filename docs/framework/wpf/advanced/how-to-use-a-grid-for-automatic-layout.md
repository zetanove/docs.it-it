---
title: "Procedura: utilizzare una griglia per il layout automatico | Microsoft Docs"
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
  - "layout automatico, utilizzo della griglia"
  - "griglie, layout automatico"
ms.assetid: ab9de407-e0c1-4047-bdf0-24951bf73879
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: utilizzare una griglia per il layout automatico
Nell'esempio viene descritto l'utilizzo di una griglia nell'approccio basato sul layout automatico per la creazione di un'applicazione localizzabile.  
  
 La localizzazione di un'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] può richiedere molto tempo.  Spesso sono necessari il ridimensionamento e il riposizionamento degli elementi, oltre alla traduzione del testo.  In passato ogni lingua per la quale un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] veniva adattata richiedeva delle modifiche.  Ora, le funzionalità di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] consentono di progettare elementi che riducono l'esigenza di modifiche.  L'approccio alla scrittura di applicazioni che è possibile ridimensionare e un riposizionare con maggiore semplicità viene definito `auto layout`.  
  
 Nell'esempio di linguaggio [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] riportato di seguito viene mostrato l'utilizzo di una griglia per posizionare alcuni pulsanti e del testo.  Notare che l'altezza e la larghezza delle celle sono impostate su `Auto`; di conseguenza la cella che contiene il pulsante con un'immagine viene modificata in modo da adattarsi all'immagine.  Poiché l'elemento <xref:System.Windows.Controls.Grid> può essere regolato in base al relativo contenuto, può rivelarsi utile se per la progettazione di applicazioni localizzabili si utilizza l'approccio basato sul layout automatico.  
  
## Esempio  
 Nel seguente esempio viene illustrata la modalità di utilizzo di una griglia.  
  
 [!code-xml[LocalizationGrid#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#1)]  
  
 Nell'immagine riportata di seguito viene mostrato l'output dell'esempio di codice.  
  
 ![Esempio di Grid](../../../../docs/framework/wpf/advanced/media/glob-grid.png "glob\_grid")  
Grid  
  
## Vedere anche  
 [Cenni preliminari sull'utilizzo del layout automatico](../../../../docs/framework/wpf/advanced/use-automatic-layout-overview.md)   
 [Utilizzare il layout automatico per creare un pulsante](../../../../docs/framework/wpf/advanced/how-to-use-automatic-layout-to-create-a-button.md)