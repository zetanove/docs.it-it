---
title: "Walkthrough: Creating and Implementing Interfaces (Visual Basic) | Microsoft Docs"
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
  - "interfaces, walkthroughs"
  - "interfaces, testing"
  - "interface implementation, walkthrough"
  - "interfaces, creating"
ms.assetid: ded82af2-9f52-4232-98ef-fe458180f112
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Walkthrough: Creating and Implementing Interfaces (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Le interfacce descrivono le caratteristiche di proprietà, metodi ed eventi, mentre i dettagli relativi all'implementazione sono definiti attraverso strutture o classi.  
  
 In questa procedura dettagliata viene illustrato come dichiarare e implementare un'interfaccia.  
  
> [!NOTE]
>  In questa procedura dettagliata non vengono fornite informazioni su come creare un'interfaccia utente.  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### Per definire un'interfaccia  
  
1.  Aprire un nuovo progetto Applicazione Windows di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
2.  Aggiungere un nuovo modulo al progetto scegliendo **Aggiungi modulo** dal menu **Progetto**.  
  
3.  Assegnare al nuovo modulo il nome `Module1.vb` e scegliere **Aggiungi**.  Verrà visualizzato il codice del nuovo modulo.  
  
4.  Definire un'interfaccia denominata `TestInterface` in `Module1` digitando `Interface TestInterface` tra le istruzioni `Module` ed `End Module`, quindi premere INVIO.  Nell'editor di codice verranno inseriti rientri nella parola chiave `Interface` e verrà aggiunta un'istruzione `End Interface` per formare un blocco di codice.  
  
5.  Definire una proprietà, un metodo e un evento per l'interfaccia inserendo tra le istruzioni `Interface` ed `End Interface` il seguente codice:  
  
     [!code-vb[VbVbalrOOP#98](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#98)]  
  
## Implementazione  
 La sintassi utilizzata per dichiarare membri di interfaccia è diversa da quella utilizzata per dichiarare membri di classe.  La differenza è dovuta al fatto che le interfacce non possono contenere codice di implementazione.  
  
#### Per implementare l'interfaccia  
  
1.  Aggiungere una classe denominata `ImplementationClass` aggiungendo l'istruzione riportata di seguito a `Module1` dopo l'istruzione `End Interface` ma prima dell'istruzione `End Module`, quindi premere INVIO:  
  
     [!code-vb[VbVbalrOOP#99](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#99)]  
  
     Se si utilizza l'ambiente di sviluppo integrato \(IDE\), nell'editor di codice viene fornita un'istruzione `End Class` corrispondente quando viene premuto INVIO.  
  
2.  Aggiungere la seguente istruzione `Implements` a `ImplementationClass` per assegnare un nome all'interfaccia implementata dalla classe:  
  
     [!code-vb[VbVbalrOOP#100](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#100)]  
  
     Quando elencata separatamente da altri elementi all'inizio di una classe o di una struttura, l'istruzione `Implements` indica che la classe o la struttura implementa un'interfaccia.  
  
     Se si utilizza l'ambiente di sviluppo integrato, nell'editor di codice vengono implementati i membri di classe richiesti da `TestInterface` quando viene premuto INVIO. È quindi possibile ignorare il passaggio successivo.  
  
3.  Se non si utilizza l'ambiente di sviluppo integrato, è necessario implementare tutti i membri dell'interfaccia `MyInterface`.  Aggiungere il seguente codice a `ImplementationClass` per implementare `Event1`, `Method1` e `Prop1`:  
  
     [!code-vb[VbVbalrOOP#101](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#101)]  
  
     L'istruzione `Implements` assegna un nome all'interfaccia e al membro di interfaccia implementati.  
  
4.  Completare la definizione di `Prop1` aggiungendo un campo privato alla classe in cui è stato memorizzato il valore della proprietà:  
  
     [!code-vb[VbVbalrOOP#102](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#102)]  
  
     Restituire il valore di `pval` dalla funzione di accesso get della proprietà.  
  
     [!code-vb[VbVbalrOOP#103](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#103)]  
  
     Impostare il valore di `pval` nella funzione di accesso set della proprietà.  
  
     [!code-vb[VbVbalrOOP#104](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#104)]  
  
5.  Completare la definizione di `Method1` aggiungendo il seguente codice:  
  
     [!code-vb[VbVbalrOOP#105](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#105)]  
  
#### Per testare l'implementazione dell'interfaccia  
  
1.  Fare clic con il pulsante destro del mouse sul form di avvio del progetto in **Esplora soluzioni**, quindi scegliere **Visualizza codice**.  Verrà visualizzata la classe del form di avvio.  Per impostazione predefinita, il form di avvio viene denominato `Form1`.  
  
2.  Aggiungere il seguente campo `testInstance` alla classe `Form1`.  
  
     [!code-vb[VbVbalrOOP#120](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#120)]  
  
     Dichiarando `testInstance` come `WithEvents`, la classe `Form1` può gestire i relativi eventi.  
  
3.  Aggiungere il seguente gestore eventi alla classe `Form1` per gestire gli eventi generati da `testInstance`:  
  
     [!code-vb[VbVbalrOOP#106](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#106)]  
  
4.  Aggiungere una subroutine denominata `Test` alla classe `Form1` per testare l'implementazione della classe:  
  
     [!code-vb[VbVbalrOOP#107](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#107)]  
  
     La routine `Test` crea un'istanza della classe che implementa `MyInterface`, assegna l'istanza al campo `testInstance`, imposta una proprietà ed esegue un metodo mediante l'interfaccia.  
  
5.  Aggiungere codice per chiamare la routine `Test` dalla routine `Form1 Load` del form di avvio:  
  
     [!code-vb[VbVbalrOOP#108](../../../../visual-basic/misc/codesnippet/visualbasic/VbVbalrOOP/OOP.vb#108)]  
  
6.  Premere F5 per eseguire la routine `Test`.  Verrà visualizzato un messaggio che informa che Prop1 è stato impostato su 9.  Scegliere OK. Verrà visualizzato un messaggio che informa che il parametro X per il metodo Method1 è 5.  Scegliere nuovamente OK. Verrà visualizzato un messaggio che informa che l'evento è stato rilevato dal gestore eventi.  
  
## Vedere anche  
 [Implements Statement](../../../../visual-basic/language-reference/statements/implements-statement.md)   
 [Interfaces](../../../../visual-basic/programming-guide/language-features/interfaces/index.md)   
 [Interface Statement](../../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Event Statement](../../../../visual-basic/language-reference/statements/event-statement.md)