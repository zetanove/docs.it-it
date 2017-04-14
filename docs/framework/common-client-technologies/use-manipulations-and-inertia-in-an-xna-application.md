---
title: "Using Manipulations and Inertia in an XNA Application | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b7c18905-850c-4da4-8977-a074406a4263
caps.latest.revision: 7
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 7
---
# Using Manipulations and Inertia in an XNA Application
Questo articolo descrive come è possibile usare l'elaborazione basata sulle modifiche e sull'inerzia in un'applicazione Microsoft XNA per controllare il movimento delle parti del gioco.  Prima di leggere questo articolo, è necessario conoscere l'argomento [Manipulations and Inertia Overview](../../../docs/framework/common-client-technologies/manipulations-and-inertia-overview.md) e i concetti di programmazione XNA di base.  
  
 Per eseguire le attività descritte in questo articolo, il progetto XNA deve fare riferimento all'assembly <xref:System.Windows.Input.Manipulations> e [XNA Game Studio](http://msdn.microsoft.com/library/bb200104.aspx) \([download](http://www.microsoft.com/downloads/details.aspx?FamilyId=7D70D6ED-1EDD-4852-9883-9A33C0AD8FEE&displaylang=en)\) deve essere installato nel computer per permettere al progetto di fare riferimento agli assembly XNA.  
  
## Panoramica delle funzionalità  
 Questo articolo mostra come creare una classe personalizzata che rappresenta una parte del gioco che usa l'elaborazione basata sull'inerzia e sulle modifiche.  Questa classe consente di modificare una parte del gioco sullo schermo trascinandola con il mouse e quindi rilasciandola.  Una volta rilasciata, l'elaborazione basata sull'inerzia fa muovere la parte del gioco come se stesse rallentando gradualmente.  Il movimento è sia lineare che angolare.  
  
 ![Semplice applicazione di modifiche e inerzia.](../../../docs/framework/common-client-technologies/media/ndp-gamexna.png "NDP\_GameXna")  
  
 Inoltre, viene creata una raccolta personalizzata che gestisce più parti del gioco.  Ciò semplifica la gestione richiesta dalla classe XNA Game.  
  
 [Creating the GamePiece Class](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md)  
  
 [Creating the GamePieceCollection Class](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)  
  
 [Creating the Game1 Class](../../../docs/framework/common-client-technologies/creating-the-game1-class.md)  
  
 [Full Code Listings](../../../docs/framework/common-client-technologies/full-code-listings.md)  
  
## Vedere anche  
 <xref:System.Windows.Input.Manipulations>   
 [Manipulations and Inertia Overview](../../../docs/framework/common-client-technologies/manipulations-and-inertia-overview.md)