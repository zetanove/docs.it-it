---
title: "Walkthrough: Defining Classes (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "execution, ending"
  - "objects [Visual Basic], initializing"
  - "Initialize event"
  - "files, closing"
  - "programs, quitting"
  - "code, exiting"
  - "objects [Visual Basic], creating"
  - "program termination"
  - "classes [Visual Basic], walkthroughs"
  - "class modules, walkthroughs"
  - "Terminate event"
  - "execution, stopping"
ms.assetid: 07018828-2d49-4cf5-a44b-19fb15d9efea
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# Walkthrough: Defining Classes (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questa procedura dettagliata viene illustrato come definire classi da utilizzare per creare oggetti.  Viene inoltre descritto come aggiungere proprietà e metodi alla nuova classe, nonché come inizializzare un oggetto.  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### Per definire una classe  
  
1.  Creare un progetto scegliendo **Nuovo progetto** dal menu **File**.  Verrà visualizzata la finestra di dialogo **Nuovo progetto**.  
  
2.  Selezionare Applicazione Windows dall'elenco dei modelli di progetto di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] per visualizzare il nuovo progetto.  
  
3.  Aggiungere una nuova classe al progetto scegliendo **Aggiungi classe** dal menu **Progetto**.  Verrà visualizzata la finestra di dialogo **Aggiungi nuovo elemento**.  
  
4.  Selezionare il modello **Classe**.  
  
5.  Assegnare alla nuova classe il nome `UserNameInfo.vb`, quindi fare clic su **Aggiungi** per visualizzare il codice della nuova classe.  
  
     [!code-vb[VbVbalrOOP#5](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_1.vb)]  
  
    > [!NOTE]
    >  È possibile utilizzare l'editor di codice di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] per aggiungere una classe al form di avvio digitando la parola chiave `Class` seguita dal nome della nuova classe.  Verrà automaticamente fornita un'istruzione `End Class` corrispondente.  
  
6.  Definire un campo privato per la classe aggiungendo il codice seguente tra le istruzioni `Class` e `End Class`:  
  
     [!code-vb[VbVbalrOOP#7](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_2.vb)]  
  
     Se il campo viene dichiarato come `Private` sarà possibile utilizzarlo solo all'interno della classe.  Per rendere disponibili i campi dall'esterno di una classe, è possibile utilizzare modificatori di accesso che consentono un accesso maggiore, ad esempio `Public`.  Per ulteriori informazioni, vedere [Access Levels in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
7.  Definire una proprietà per la classe aggiungendo il seguente codice:  
  
     [!code-vb[VbVbalrOOP#8](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_3.vb)]  
  
8.  Definire un metodo per la classe aggiungendo il seguente codice:  
  
     [!code-vb[VbVbalrOOP#9](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_4.vb)]  
  
9. Definire un costruttore con parametri per la nuova classe aggiungendo una routine denominata `Sub New`:  
  
     [!code-vb[VbVbalrOOP#10](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_5.vb)]  
  
     Il costruttore `Sub New` viene chiamato automaticamente quando viene creato un oggetto basato su questa classe,  e imposta il valore del campo che contiene il nome utente.  
  
### Per creare un pulsante per testare la classe  
  
1.  Impostare il form di avvio in modalità progettazione facendo clic con il pulsante destro del mouse sul nome corrispondente in **Esplora soluzioni** e scegliendo **Visualizza finestra di progettazione**.  Per impostazione predefinita, il form di avvio dei progetti Applicazione Windows è denominato Form1.vb.  Verrà visualizzato il form principale.  
  
2.  Aggiungere un pulsante al form principale e fare doppio clic su di esso per visualizzare il codice per il gestore eventi `Button1_Click`.  Per chiamare la routine di verifica, aggiungere il codice seguente:  
  
     [!code-vb[VbVbalrOOP#12](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_6.vb)]  
  
### Per eseguire l'applicazione  
  
1.  Premere F5 per eseguire l'applicazione,  Fare clic sul pulsante del form per chiamare la routine di verifica.  Viene visualizzato un messaggio in cui si dichiara che la proprietà `UserName` originale è "MOORE, BOBBY", dal momento che la routine ha richiamato il metodo `Capitalize` dell'oggetto.  
  
2.  Scegliere **OK** per chiudere la finestra del messaggio.  La routine `Button1 Click` modifica il valore della proprietà `UserName` e visualizza un messaggio in cui si dichiara che il nuovo valore di `UserName` è "Worden, Joe".  
  
## Vedere anche  
 [Programmazione orientata ad oggetti](../Topic/Object-Oriented%20Programming%20\(C%23%20and%20Visual%20Basic\).md)   
 [Objects and Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)