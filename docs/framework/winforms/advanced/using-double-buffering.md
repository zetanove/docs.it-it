---
title: "Utilizzo del doppio buffer | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "inserimento nel buffer, doppio buffer"
  - "doppio buffer"
  - "sfarfallio, riduzione in Windows Form"
  - "grafica, doppio buffer"
ms.assetid: dc484e33-7101-4e4b-ada5-d3c96155fbcd
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Utilizzo del doppio buffer
È possibile utilizzare grafica con doppio buffer per ridurre lo sfarfallio nelle applicazioni che prevedono operazioni di disegno complesse.  .NET Framework fornisce supporto incorporato per il doppio buffer; in alternativa, è possibile gestire ed eseguire manualmente il rendering della grafica.  
  
## In questa sezione  
 [Grafica a doppio buffer](../../../../docs/framework/winforms/advanced/double-buffered-graphics.md)  
 Viene illustrato il concetto di doppio buffer e descritto il supporto .NET Framework.  
  
 [Procedura: ridurre lo sfarfallio nella grafica con il doppio buffering per form e controlli](../../../../docs/framework/winforms/advanced/how-to-reduce-graphics-flicker-with-double-buffering-for-forms-and-controls.md)  
 Viene illustrato come utilizzare il supporto predefinito del doppio buffer in .NET Framework.  
  
 [Procedura: gestire manualmente le immagini memorizzate nel buffer](../../../../docs/framework/winforms/advanced/how-to-manually-manage-buffered-graphics.md)  
 Viene illustrato come gestire il doppio buffer nelle applicazioni.  
  
 [Procedura: eseguire il rendering manuale di grafica memorizzata nel buffer](../../../../docs/framework/winforms/advanced/how-to-manually-render-buffered-graphics.md)  
 Viene illustrato come eseguire il rendering della grafica con doppio buffer.  
  
## Riferimenti  
 <xref:System.Windows.Forms.Control.SetStyle%2A> ,  
 Metodo di controllo che attiva il doppio buffer.  
  
 <xref:System.Drawing.BufferedGraphicsContext> ,  
 Fornisce i metodi per la creazione dei buffer di grafica.  
  
 <xref:System.Drawing.BufferedGraphicsManager>  
 Fornisce accesso al contesto della grafica con buffer per un dominio di applicazione.