---
title: Definizione di classi (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- execution, ending
- objects [Visual Basic], initializing
- Initialize event
- files, closing
- programs, quitting
- code, exiting
- objects [Visual Basic], creating
- program termination
- classes [Visual Basic], walkthroughs
- class modules, walkthroughs
- Terminate event
- execution, stopping
ms.assetid: 07018828-2d49-4cf5-a44b-19fb15d9efea
caps.latest.revision: 21
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: aeaa5c2bb85c1a642da15c6a29546cf065380e27
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-defining-classes-visual-basic"></a>Procedura dettagliata: definizione delle classi (Visual Basic)
Questa procedura dettagliata viene illustrato come definire le classi, che è quindi possibile utilizzare per creare oggetti. Inoltre viene illustrato come aggiungere proprietà e metodi alla nuova classe e viene illustrato come inizializzare un oggetto.  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-define-a-class"></a>Per definire una classe  
  
1.  Creare un progetto facendo clic su **nuovo progetto** sul **File** menu. Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
2.  Selezionare applicazione Windows dall'elenco di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per visualizzare il nuovo progetto di modelli di progetto.  
  
3.  Aggiungere una nuova classe al progetto, fare clic su **Aggiungi classe** sul **progetto** menu. Il **Aggiungi nuovo elemento** viene visualizzata la finestra di dialogo.  
  
4.  Selezionare il **classe** modello.  
  
5.  Denominare la nuova classe `UserNameInfo.vb`, quindi fare clic su **Aggiungi** per visualizzare il codice per la nuova classe.  
  
     [!code-vb[VbVbalrOOP n.&5;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_1.vb)]  
  
    > [!NOTE]
    >  È possibile utilizzare il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] **Editor di codice** per aggiungere una classe al form di avvio digitando la `Class` (parola chiave) seguito dal nome della nuova classe. Il **Editor di codice** fornisce un oggetto corrispondente `End Class` istruzione per l'utente.  
  
6.  Definire un campo privato per la classe aggiungendo il codice seguente tra i `Class` e `End Class` istruzioni:  
  
     [!code-vb[VbVbalrOOP&#7;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_2.vb)]  
  
     La dichiarazione del campo come `Private` significa che può essere utilizzato solo all'interno della classe. È possibile rendere disponibili all'esterno di una classe campi utilizzando i modificatori di accesso, ad esempio `Public` che consentono un accesso maggiore. Per ulteriori informazioni, vedere [livelli di accesso in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
7.  Definire una proprietà per la classe aggiungendo il codice seguente:  
  
     [!code-vb[VbVbalrOOP n.&8;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_3.vb)]  
  
8.  Definire un metodo per la classe aggiungendo il codice seguente:  
  
     [!code-vb[9 VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_4.vb)]  
  
9. Definire un costruttore con parametri per la nuova classe aggiungendo una routine denominata `Sub New`:  
  
     [!code-vb[VbVbalrOOP&#10;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_5.vb)]  
  
     Il `Sub New` costruttore viene chiamato automaticamente quando viene creato un oggetto basato su questa classe. Questo costruttore imposta il valore del campo che contiene il nome utente.  
  
### <a name="to-create-a-button-to-test-the-class"></a>Per creare un pulsante per la classe di test  
  
1.  Impostare il form di avvio in modalità progettazione facendo clic con il nome **Esplora** e quindi fare clic su **Visualizza finestra di progettazione**. Per impostazione predefinita, il form di avvio per i progetti di applicazione Windows denominato Form1. vb. Verrà quindi visualizzato il form principale.  
  
2.  Aggiungere un pulsante al form principale e fare doppio clic per visualizzare il codice per il `Button1_Click` gestore dell'evento. Aggiungere il codice seguente per chiamare la routine di test:  
  
     [!code-vb[VbVbalrOOP&#12;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_6.vb)]  
  
### <a name="to-run-your-application"></a>Per eseguire l'applicazione  
  
1.  Eseguire l'applicazione premendo F5. Fare clic sul pulsante sul form per chiamare la routine di test. Viene visualizzato un messaggio che informa che originale `UserName` è "MOORE, BOBBY", perché la procedura chiamata di `Capitalize` metodo dell'oggetto.  
  
2.  Fare clic su **OK** per chiudere la finestra di messaggio. Il `Button1 Click` procedura modifica il valore di `UserName` proprietà e viene visualizzato un messaggio indicante che il nuovo valore di `UserName` è "Worden, Joe".  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione orientata agli oggetti](http://msdn.microsoft.com/library/1cf6e655-3f30-45f1-9a5d-4a88ca24a1c2)   
 [Oggetti e classi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)

