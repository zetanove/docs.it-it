---
title: "Procedura: utilizzare un layout automatico per creare un pulsante | Microsoft Docs"
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
  - "layout automatico, creazione di pulsanti"
  - "Button (controlli), creazione con layout automatico"
  - "creazione, pulsanti con layout automatico"
ms.assetid: 96c206d0-9e77-4784-9d2d-5045aed2021c
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: utilizzare un layout automatico per creare un pulsante
Nell'esempio viene descritto come utilizzare un approccio basato sul layout automatico per la creazione di un pulsante in un'applicazione localizzabile.  
  
 La localizzazione di un'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] può richiedere molto tempo.  Spesso sono necessari il ridimensionamento e il riposizionamento degli elementi, oltre alla traduzione del testo.  In passato ogni lingua per la quale un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] veniva adattata richiedeva delle modifiche.  Ora, le funzionalità di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] consentono di progettare elementi che riducono l'esigenza di modifiche.  L'approccio alla scrittura di applicazioni che è possibile ridimensionare e riposizionare con maggiore semplicità viene definito `automatic layout`.  
  
 I due esempi [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] riportati di seguito consentono di creare applicazioni che creano un'istanza di un pulsante, uno con il testo in inglese e uno con il testo in spagnolo.  Il codice è uguale a eccezione del testo. Il pulsante si regola per adattarsi al testo.  
  
## Esempio  
 [!code-xml[LocalizationBtn_snip#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn_snip/CS/Pane1.xaml#1)]  
  
 [!code-xml[LocalizationBtn#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn/CS/Pane1.xaml#1)]  
  
 Nell'immagine riportata di seguito viene illustrato l'output degli esempi di codice.  
  
 ![Lo stesso pulsante con testo in lingue diverse](../../../../docs/framework/wpf/advanced/media/globalizationbutton.png "GlobalizationButton")  
Pulsante a ridimensionamento automatico  
  
## Vedere anche  
 [Cenni preliminari sull'utilizzo del layout automatico](../../../../docs/framework/wpf/advanced/use-automatic-layout-overview.md)   
 [Utilizzare una griglia per il layout automatico](../../../../docs/framework/wpf/advanced/how-to-use-a-grid-for-automatic-layout.md)