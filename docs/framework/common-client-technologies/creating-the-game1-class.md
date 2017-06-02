---
title: "Creating the Game1 Class | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 47932ce3-2ba5-476f-a26b-3ddfd5226f27
caps.latest.revision: 8
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 8
---
# Creating the Game1 Class
Come per tutti i progetti di Microsoft XNA, la classe Game1 deriva dalla classe [Microsoft.Xna.Framework.Game](http://msdn.microsoft.com/library/microsoft.xna.framework.game.aspx), che fornisce l'inizializzazione dei dispositivi grafici di base, la logica del gioco e il codice di rendering per i giochi XNA.  La classe Game1 è alquanto semplice perché la maggior parte del lavoro spetta alle classi GamePiece e GamePieceCollection.  
  
## Creazione del codice  
 I membri privati per la classe sono costituiti da un oggetto **GamePieceCollection** che include le parti del gioco, un oggetto [GraphicsDeviceManager](http://msdn.microsoft.com/library/microsoft.xna.framework.graphicsdevicemanager.aspx) e un oggetto [SpriteBatch](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.spritebatch.aspx) usato per il rendering delle parti del gioco.  
  
 [!code-csharp[ManipulationXNA#_Game1_PrivateMembers](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_privatemembers)]  
  
 Durante l'inizializzazione del gioco, viene creata un'istanza di questi oggetti.  
  
 [!code-csharp[ManipulationXNA#_Game1_ConstructorInitialize](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_constructorinitialize)]  
  
 Quando il metodo [LoadContent](http://msdn.microsoft.com/library/microsoft.xna.framework.game.loadcontent.aspx) viene chiamato, vengono create le parti del gioco che verranno assegnate all'oggetto **GamePieceCollection**.  Sono disponibili due tipi di parti del gioco.  Il fattore di scala per le parti viene modificato leggermente in modo che siano disponibili alcune parti più piccole e altre più grandi.  
  
 [!code-csharp[ManipulationXNA#_Game1_LoadContent](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_loadcontent)]  
  
 Il metodo [Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) viene chiamato ripetutamente da XNA Framework durante l'esecuzione del gioco.  Il metodo [Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) chiama i metodi **ProcessInertia** e **UpdateFromMouse** nella raccolta di parti del gioco.  Questi metodi sono descritti in [Creating the GamePieceCollection Class](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md).  
  
 [!code-csharp[ManipulationXNA#_Game1_UpdateGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_updategame)]  
  
 Anche il metodo [Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) viene chiamato ripetutamente da XNA Framework mentre il gioco è in esecuzione.  Il metodo [Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) esegue il rendering delle parti del gioco chiamando il metodo **Draw** dell'oggetto **GamePieceCollection**.  Questo metodo viene descritto in [Creating the GamePieceCollection Class](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md).  
  
 [!code-csharp[ManipulationXNA#_Game1_DrawGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_drawgame)]  
  
## Vedere anche  
 [Manipulations and Inertia](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md)   
 [Using Manipulations and Inertia in an XNA Application](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md)   
 [Creating the GamePiece Class](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md)   
 [Creating the GamePieceCollection Class](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)   
 [Full Code Listings](../../../docs/framework/common-client-technologies/full-code-listings.md)