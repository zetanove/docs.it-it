---
title: "Procedura: eseguire l&#39;override del metodo Panel OnRender | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "overriding OnRender method"
  - "Panel control, overriding OnRender method"
  - "OnRender method"
  - "controls, Panel, overriding OnRender method"
helpviewer_keywords: 
  - "OnRender (metodo), override"
  - "override del metodo OnRender del controllo Panel"
  - "Panel (controllo), override del metodo OnRender"
ms.assetid: 57397834-a085-4e36-90ab-416fad98f341
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: eseguire l&#39;override del metodo Panel OnRender
In questo esempio viene illustrato come eseguire l'override del metodo <xref:System.Windows.Controls.Panel.OnRender%2A> dell'oggetto <xref:System.Windows.Controls.Panel> per aggiungere effetti grafici personalizzati a un elemento del layout.  
  
## Esempio  
 Utilizzare il metodo <xref:System.Windows.Controls.Panel.OnRender%2A> per aggiungere effetti grafici a un elemento del pannello di cui è stato eseguito il rendering.  È ad esempio possibile utilizzare questo metodo per aggiungere bordi personalizzati o effetti di sfondo.  L'oggetto <xref:System.Windows.Media.DrawingContext> viene passato come un argomento che fornisce metodi per disegnare forme, testo, immagini o video.  Di conseguenza, questo metodo è utile per personalizzare un oggetto del pannello.  
  
 [!code-csharp[LightWeightCustomPanel#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LightWeightCustomPanel/CSharp/OffsetPanel.cs#1)]
 [!code-vb[LightWeightCustomPanel#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/LightWeightCustomPanel/visualbasic/offsetpanel.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Panel>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Esempio di pannello radiale personalizzato](http://go.microsoft.com/fwlink/?LinkID=159982)   
 [Procedure relative](../../../../docs/framework/wpf/controls/panel-how-to-topics.md)