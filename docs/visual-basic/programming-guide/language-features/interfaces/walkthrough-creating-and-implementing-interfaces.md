---
title: Creazione e implementazione di interfacce (Visual Basic) | Documenti di Microsoft
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
- interfaces, walkthroughs
- interfaces, testing
- interface implementation, walkthrough
- interfaces, creating
ms.assetid: ded82af2-9f52-4232-98ef-fe458180f112
caps.latest.revision: 22
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 076bc8d33e97286c31f27a2016e39a25e9cec22c
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-creating-and-implementing-interfaces-visual-basic"></a>Procedura dettagliata: creazione e implementazione di interfacce (Visual Basic)
Interfacce descrivono le caratteristiche di proprietà, metodi ed eventi, ma i dettagli relativi all'implementazione fino a strutture o classi.  
  
 Questa procedura dettagliata viene illustrato come dichiarare e implementare un'interfaccia.  
  
> [!NOTE]
>  Questa procedura dettagliata non fornisce informazioni su come creare un'interfaccia utente.  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-define-an-interface"></a>Per definire un'interfaccia  
  
1.  Aprire un nuovo [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] progetto applicazione Windows.  
  
2.  Aggiungere un nuovo modulo per il progetto facendo clic su **Aggiungi modulo** sul **Project** menu.  
  
3.  Nome del nuovo modulo `Module1.vb` e fare clic su **Aggiungi**. Viene visualizzato il codice per il nuovo modulo.  
  
4.  Definire un'interfaccia denominata `TestInterface` all'interno di `Module1` digitando `Interface TestInterface` tra il `Module` e `End Module` istruzioni e quindi premere INVIO. Il **Editor di codice** rientri il `Interface` (parola chiave) e aggiunge un `End Interface` istruzione in modo da formare un blocco di codice.  
  
5.  Definire un proprietà, metodi ed eventi per l'interfaccia inserendo il codice seguente tra i `Interface` e `End Interface` istruzioni:  
  
     [!code-vb[&#98; VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_1.vb)]  
  
## <a name="implementation"></a>Implementazione  
 È possibile notare che la sintassi utilizzata per dichiarare i membri di interfaccia è diversa da quella utilizzata per dichiarare i membri della classe. La differenza è dovuta al fatto che le interfacce non possono contenere codice di implementazione.  
  
#### <a name="to-implement-the-interface"></a>Per implementare l'interfaccia  
  
1.  Aggiungere una classe denominata `ImplementationClass` aggiungendo l'istruzione seguente alle `Module1`, dopo il `End Interface` istruzione ma prima che il `End Module` istruzione e quindi premere INVIO:  
  
     [!code-vb[VbVbalrOOP&#99;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_2.vb)]  
  
     Se si lavora all'interno dell'ambiente di sviluppo integrato, il **Editor di codice** fornisce un corrispondente `End Class` istruzione quando si preme INVIO.  
  
2.  Aggiungere il codice seguente `Implements` istruzione `ImplementationClass`, quali nome dell'interfaccia implementata dalla classe:  
  
     [!code-vb[VbVbalrOOP&#100;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_3.vb)]  
  
     Quando elencata separatamente da altri elementi nella parte superiore di una classe o struttura, il `Implements` istruzione indica che la classe o struttura implementa un'interfaccia.  
  
     Se si lavora all'interno dell'ambiente di sviluppo integrato, il **Editor di codice** implementa i membri di classe richiesti da `TestInterface` quando si preme INVIO, e si può ignorare il passaggio successivo.  
  
3.  Se non si lavora all'interno dell'ambiente di sviluppo integrato, è necessario implementare tutti i membri dell'interfaccia `MyInterface`. Aggiungere il codice seguente a `ImplementationClass` implementare `Event1`, `Method1`, e `Prop1`:  
  
     [!code-vb[VbVbalrOOP&#101;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_4.vb)]  
  
     Il `Implements` istruzione denomina l'interfaccia e un membro di interfaccia implementati.  
  
4.  Completare la definizione di `Prop1` aggiungendo un campo privato per la classe che è archiviato il valore della proprietà:  
  
     [!code-vb[&#102; VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_5.vb)]  
  
     Restituisce il valore di `pval` dalla proprietà get.  
  
     [!code-vb[VbVbalrOOP&#103;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_6.vb)]  
  
     Impostare il valore di `pval` nel set di proprietà della funzione di accesso.  
  
     [!code-vb[&#104; VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_7.vb)]  
  
5.  Completare la definizione di `Method1` aggiungendo il codice seguente.  
  
     [!code-vb[&#105; VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_8.vb)]  
  
#### <a name="to-test-the-implementation-of-the-interface"></a>Per testare l'implementazione dell'interfaccia  
  
1.  Fare doppio clic su form di avvio per il progetto nel **Esplora**, fare clic su **Visualizza codice**. L'editor visualizza la classe del form di avvio. Per impostazione predefinita, viene chiamato il form di avvio `Form1`.  
  
2.  Aggiungere il codice seguente `testInstance` campo la `Form1` classe:  
  
     [!code-vb[&#120; VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_9.vb)]  
  
     Dichiarando `testInstance` come `WithEvents`, `Form1` classe può gestire gli eventi.  
  
3.  Aggiungere il seguente gestore eventi per il `Form1` classe per gestire gli eventi generati da `testInstance`:  
  
     [!code-vb[&#106; VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_10.vb)]  
  
4.  Aggiungere una subroutine denominata `Test` per la `Form1` classe da testare l'implementazione della classe:  
  
     [!code-vb[&#107; VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_11.vb)]  
  
     Il `Test` procedura crea un'istanza della classe che implementa `MyInterface`, assegna l'istanza di `testInstance` imposta una proprietà, campo e viene eseguito un metodo tramite l'interfaccia.  
  
5.  Aggiungere codice per chiamare il `Test` procedura il `Form1 Load` routine del form di avvio:  
  
     [!code-vb[&#108; VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_12.vb)]  
  
6.  Eseguire il `Test` procedura premendo F5. Viene visualizzato il messaggio "Prop1 è stato impostato su 9". Viene visualizzato dopo aver fatto clic su OK, il messaggio "il parametro X per Method1 is 5". Fare clic su OK e viene visualizzato il messaggio "il gestore dell'evento rilevata l'evento".  
  
## <a name="see-also"></a>Vedere anche  
 [Implements (istruzione)](../../../../visual-basic/language-reference/statements/implements-statement.md)   
 [Interfacce](../../../../visual-basic/programming-guide/language-features/interfaces/index.md)   
 [Istruzione Interface](../../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Istruzione Event](../../../../visual-basic/language-reference/statements/event-statement.md)

