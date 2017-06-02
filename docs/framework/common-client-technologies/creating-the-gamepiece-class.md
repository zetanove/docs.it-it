---
title: "Creating the GamePiece Class | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 37a27a86-ac1c-47be-b477-cb4b819459d3
caps.latest.revision: 9
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 9
---
# Creating the GamePiece Class
La classe **GamePiece** incapsula tutte le funzionalità necessarie per caricare l'immagine di una parte del gioco di Microsoft XNA, tenere traccia dello stato del mouse in relazione alla parte del gioco, di acquisire il mouse, di fornire l'elaborazione delle manipolazioni e dell'inerzia e di fornire funzionalità di rimbalzo quando la parte del gioco raggiunge i limiti del viewport.  
  
## Membri privati  
 All'inizio della classe **GamePiece** vengono dichiarati numerosi membri privati.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_PrivateMembers](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_privatemembers)]  
  
## Proprietà pubbliche  
 Tre di questi membri privati vengono esposti tramite proprietà pubbliche.  Le proprietà **Scale** e **PieceColor** consentono all'applicazione di specificare, rispettivamente, le proporzioni e il colore della parte.  Le proprietà **Bounds** viene esposta per consentire a una parte di usare i limiti di un'altra parte per eseguire il rendering, come nei casi in cui una parte deve sovrapporsi a un'altra.  Il codice seguente illustra la dichiarazione delle proprietà pubbliche.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_PublicProperties](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_publicproperties)]  
  
## Costruttore di classe  
 Il costruttore per la classe **GamePiece** accetta i parametri seguenti:  
  
-   Un tipo [SpriteBatch](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.spritebatch.aspx).  Il riferimento passato in questo caso viene assegnato al membro privato `spriteBatch` e usato per accedere al metodo [SpriteBatch.Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.spritebatch.draw.aspx) durante il rendering della parte del gioco.  Inoltre, la proprietà [GraphicsDevice](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.spritebatch.graphicsdevice.aspx) viene usata per creare l'oggetto [Texture](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.texture.aspx) associato alla parte del gioco e per ottenere la dimensione del viewport, per individuare il momento in cui la parte del gioco rileva un limite della finestra per fare in modo che la parte possa rimbalzare.  
  
-   Una stringa che specifica il nome del file dell'immagine da usare per la parte del gioco.  
  
 Il costruttore crea anche un oggetto <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D> e un oggetto <xref:System.Windows.Input.Manipulations.InertiaProcessor2D> e stabilisce i gestori eventi per gli eventi corrispondenti.  
  
 Il codice seguente illustra il costruttore per la classe **GamePiece**.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_Constructor](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_constructor)]  
  
## Acquisizione dell'input del mouse  
 Il metodo **UpdateFromMouse** è responsabile del rilevamento del momento in cui un pulsante del mouse viene premuto mentre il mouse è all'interno dei limiti della parte del gioco e del momento in cui il pulsante del mouse viene rilasciato.  
  
 Quando viene premuto il pulsante sinistro del mouse \(mentre il mouse è all'interno dei limiti della parte\), il metodo imposta un flag per indicare che questa parte del gioco ha acquisito il mouse e che l'elaborazione della manipolazione ha inizio.  
  
 L'elaborazione della manipolazione viene iniziata creando una matrice di oggetti <xref:System.Windows.Input.Manipulations.Manipulator2D> e passandoli all'oggetto <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D>.  Questo fa in modo che il processore di manipolazione valuti i manipolatori \(in questo caso un solo manipolatore\) e generi eventi di manipolazione.  
  
 Inoltre, viene salvato il punto in cui si verifica il trascinamento.  Questo elemento viene usato in un secondo momento, durante l'evento <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D.Delta>, per regolare i valori della conversione delta in modo che la parte del gioco si allinei dietro al punto del trascinamento.  
  
 Infine, il metodo restituisce lo stato di acquisizione del mouse.  Questo consente all'oggetto [GamePieceCollection](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md) di gestire l'acquisizione quando sono presenti più parti del gioco.  
  
 Il codice seguente illustra il metodo **UpdateFromMouse**.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_UpdateFromMouse](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_updatefrommouse)]  
  
## Elaborazione delle manipolazioni  
 Quando inizia la manipolazione viene generato l'evento <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D.Started>.  Il gestore per questo evento interrompe l'elaborazione dell'inerzia, se in corso, e imposta il flag *processInertia* su `false`.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnManipulationStarted](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_onmanipulationstarted)]  
  
 Quando i valori associati alla manipolazione cambiano viene generato l'evento <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D.Delta>.  Il gestore per questo evento usa i valori delta passati negli argomenti dell'evento per apportare modifiche ai valori della posizione e della rotazione della parte del gioco.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnManipulationDelta](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_onmanipulationdelta)]  
  
 Quando tutti i manipolatori \(in questo caso un solo manipolatore\) associati a una manipolazione vengono rimossi, il processore di manipolazione genera l'evento <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D.Completed>.  Il gestore per questo evento inizia l'elaborazione dell'inerzia impostando le velocità iniziali del processore di inerzia su quelle indicate dagli argomenti dell'evento e imposta il flag *processInertia* su `true`  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnManipulationCompleted](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_onmanipulationcompleted)]  
  
## Elaborazione dell'inerzia  
 Mentre l'elaborazione dell'inerzia estrapola i nuovi valori per le velocità angolari e lineari, le coordinate della posizione \(traslazione\) e la rotazione, viene generato l'evento <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Delta>.  Il gestore per questo evento usa i valori delta passati negli argomenti dell'evento per modificare la posizione e della rotazione della parte del gioco.  
  
 Se le nuove coordinate comportano lo spostamento della parte del gioco oltre i limiti del viewport, la velocità di elaborazione dell'inerzia viene invertita.  Ciò fa in modo che la parte del gioco rimbalzi in corrispondenza del limite del viewport che ha incontrato.  
  
 Non è possibile modificare le proprietà di un oggetto <xref:System.Windows.Input.Manipulations.InertiaProcessor2D> mentre è in corso l'estrapolazione.  Pertanto, durante l'inversione della velocità X o Y, il gestore dell'evento interrompe innanzi tutto l'inerzia chiamando il metodo <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Complete%2A>.  Assegna quindi i nuovi valori della velocità iniziale perché corrispondano ai valori di velocità correnti \(regolati per il comportamento di sponge\) e imposta il flag *processInertia* su `true`.  
  
 Il codice seguente illustra il gestore dell'evento <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Delta>.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnInertiaDelta](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_oninertiadelta)]  
  
 Al termine dell'elaborazione dell'inerzia. il processore di inerzia genera l'evento <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Completed>.  Il gestore per questo evento imposta il flag *processInertia* su `false`.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnInertiaCompleted](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_oninertiacompleted)]  
  
 Nessun elemento della logica presentato finora consente l'estrapolazione dell'inerzia vera e propria.  A questo scopo viene usato il metodo **ProcessInertia**.  Questo metodo, che viene chiamato ripetutamente dal ciclo di aggiornamento del gioco \(il metodo [Game.Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx)\) verifica se il flag *processInertia* è impostato su `true` e, in tal caso, chiama il metodo <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Process%2A>.  La chiamata di questo metodo fa in modo che si verifichi l'estrapolazione e genera l'evento <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Delta>.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_ProcessInertia](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_processinertia)]  
  
 Il rendering effettivo della parte del gioco non viene eseguito finché non viene chiamato uno degli overload del metodo Draw.  Il primo overload di questo metodo viene chiamato ripetutamente dal ciclo di disegno del gioco \(il metodo [Game.Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx)\).  Questo consente di eseguire il rendering della parte del gioco con la posizione, la rotazione e i fattori di scala correnti.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_Draw](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_draw)]  
  
## Proprietà aggiuntive  
 La classe **GamePiece** usa tre proprietà private.  
  
1.  **Timestamp**: ottiene un valore di timestamp che verrà usato dai processori di manipolazione e inerzia.  
  
2.  **X**: ottiene o imposta la coordinata X della parte del gioco.  Durante l'impostazione, regolare i limiti usati per l'hit test e il percorso di rotazione del processore di manipolazione.  
  
3.  **X**: ottiene o imposta la coordinata Y della parte del gioco.  Durante l'impostazione, regolare i limiti usati per l'hit test e il percorso di rotazione del processore di manipolazione.  
  
 [!code-csharp[ManipulationXNA#_GamePiece_PrivateProperties](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_privateproperties)]  
  
## Vedere anche  
 [Manipulations and Inertia](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md)   
 [Using Manipulations and Inertia in an XNA Application](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md)   
 [Creating the GamePieceCollection Class](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)   
 [Creating the Game1 Class](../../../docs/framework/common-client-technologies/creating-the-game1-class.md)