---
title: "Creating the GamePieceCollection Class | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e4b037ee-1201-4a55-b198-0d6532ed6f35
caps.latest.revision: 8
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 8
---
# Creating the GamePieceCollection Class
La classe **GamePieceCollection** deriva dalla classe generica List e introduce metodi per gestire più facilmente più oggetti **GamePiece**.  
  
## Creazione del codice  
 Il costruttore della classe **GamePieceCollection** inizializza il membro privato *capturedIndex*.  Questo campo viene usato per tenere traccia delle parti del gioco che hanno attualmente lo stato mouse capture.  
  
 [!code-csharp[ManipulationXNA#_GamePieceCollection_PrivateMembersAndConstructor](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiececollection.cs#_gamepiececollection_privatemembersandconstructor)]  
  
 I metodi **ProcessInertia** e **Draw** semplificano il codice richiesto nei metodi [Game.Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) e [Game.Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) enumerando tutte le parti del gioco nella raccolta e chiamando il rispettivo metodo per ogni oggetto **GamePiece**.  
  
 [!code-csharp[ManipulationXNA#_GamePieceCollection_ProcessInertiaAndDraw](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiececollection.cs#_gamepiececollection_processinertiaanddraw)]  
  
 Il metodo **UpdateFromMouse** viene chiamato anche durante l'aggiornamento del gioco.  Consente a una sola parte del gioco di avere lo stato mouse capture, verificando innanzitutto se lo stato corrente, se presente, è ancora attivo.  In questo caso, a nessun'altra parte sarà consentito di verificare lo stato capture.  
  
 Se nessuna parte presenta attualmente lo stato capture, il metodo **UpdateFromMouse** enumera ogni parte del gioco dall'ultima alla prima e verifica se quella parte segnala uno stato mouse capture.  In questo caso, la parte diventa la parte attualmente con lo stato mouse capture e non vengono eseguite altre elaborazioni.  Il metodo **UpdateFromMouse** controlla per primo l'ultimo elemento della raccolta in modo che, se due parti sono sovrapposte, quella con l'ordine Z più elevato otterrà lo stato capture.  L'ordine Z non è esplicito né può essere modificato. È governato semplicemente dall'ordine in cui le parti del gioco vengono aggiunte alla raccolta.  
  
 [!code-csharp[ManipulationXNA#_GamePieceCollection_UpdateFromMouse](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiececollection.cs#_gamepiececollection_updatefrommouse)]  
  
## Vedere anche  
 [Manipulations and Inertia](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md)   
 [Using Manipulations and Inertia in an XNA Application](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md)   
 [Creating the GamePiece Class](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md)   
 [Creating the Game1 Class](../../../docs/framework/common-client-technologies/creating-the-game1-class.md)   
 [Full Code Listings](../../../docs/framework/common-client-technologies/full-code-listings.md)