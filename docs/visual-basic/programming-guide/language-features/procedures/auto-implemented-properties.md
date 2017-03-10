---
title: "Auto-Implemented Properties (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.AutoProperty"
  - "vb.AutoImplementedProperty"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "properties [Visual Basic], auto-implemented"
  - "properties, auto-implemented [Visual Basic]"
  - "auto-implemented properties [Visual Basic]"
ms.assetid: 5c669f0b-cf95-4b4e-ae84-9cc55212ca87
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Auto-Implemented Properties (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Le *proprietà implementate automaticamente* consentono di specificare rapidamente una proprietà di una classe senza dover scrivere codice per ottenere \(`Get`\) e impostare \(`Set`\) la proprietà.  Quando si scrive il codice per una proprietà implementata automaticamente, il compilatore Visual Basic crea automaticamente un campo privato per archiviare la variabile della proprietà oltre a creare le routine `Get` e `Set` associate.  
  
 Con le proprietà implementate automaticamente, una proprietà, incluso un valore predefinito, può essere dichiarata in una sola riga.  L'esempio seguente illustra tre dichiarazioni di proprietà.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#1](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/auto-implemented-propert_1_1.vb)]  
  
 Una proprietà implementata automaticamente equivale a una proprietà il cui valore viene archiviato in un campo privato.  L'esempio di codice seguente illustra una proprietà implementata automaticamente.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#5](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/auto-implemented-propert_1_2.vb)]  
  
 L'esempio seguente illustra il codice equivalente per il precedente esempio di proprietà implementata automaticamente.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#2](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/auto-implemented-propert_1_3.vb)]  
  
 Il codice seguente illustra l'implementazione delle proprietà di sola lettura:  
  
```vb  
Class Customer  
   Public ReadOnly Property Tags As New List(Of String)  
   Public ReadOnly Property Name As String = ""  
   Public ReadOnly Property File As String  
  
   Sub New(file As String)  
      Me.File = file  
   End Sub  
End Class  
  
```  
  
 È possibile assegnare alla proprietà con espressioni di inizializzazione, come illustrato nell'esempio, oppure nel costruttore del tipo contenitore.  È possibile assegnare ai campi sottostanti delle proprietà di sola lettura in qualsiasi momento.  
  
## Campo sottostante  
 Quando si dichiara una proprietà implementata automaticamente, Visual Basic crea automaticamente un campo privato nascosto denominato *campo sottostante* per contenere il valore della proprietà.  Il nome del campo sottostante è il nome della proprietà implementata automaticamente preceduto da un carattere di sottolineatura \(\_\).  Ad esempio, se si dichiara una proprietà implementata automaticamente denominata `ID`, il campo sottostante viene denominato `_ID`.  Se si include un membro della classe con il medesimo nome `_ID`, si produce un conflitto di denominazione e in Visual Basic viene segnalato un errore del compilatore.  
  
 Il campo sottostante presenta inoltre le caratteristiche seguenti:  
  
-   Il modificatore di accesso per il campo sottostante è sempre `Private`, anche quando la proprietà stessa dispone di un livello di accesso diverso, ad esempio `Public`.  
  
-   Se la proprietà è contrassegnata come `Shared`, anche il campo sottostante è condiviso.  
  
-   Gli attributi specificati per la proprietà non si applicano al campo sottostante.  
  
-   L'accesso al campo sottostante può essere eseguito dal codice all'interno della classe e dagli strumenti di debug, ad esempio la finestra Espressioni di controllo.  Tuttavia, il campo sottostante non viene visualizzato in un elenco di completamento di parole di IntelliSense.  
  
## Inizializzazione di una proprietà implementata automaticamente  
 Qualsiasi espressione utilizzabile per inizializzare un campo è valida per l'inizializzazione di una proprietà implementata automaticamente.  Quando si inizializza una proprietà implementata automaticamente, l'espressione viene valutata e passata alla routine `Set` per la proprietà.  Gli esempi di codice seguenti mostrano alcune proprietà implementate automaticamente che includono i valori iniziali.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#3](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/auto-implemented-propert_1_4.vb)]  
  
 Non è possibile inizializzare una proprietà implementata automaticamente che sia membro di un `Interface` o una che sia contrassegnata come `MustOverride`.  
  
 Quando si dichiara una proprietà implementata automaticamente come membro di una `Structure`, è possibile inizializzarla solo se è contrassegnata come `Shared`.  
  
 Quando si dichiara una proprietà implementata automaticamente come matrice, non è possibile specificare limiti di matrice espliciti.  Tuttavia, si può specificare un valore usando un inizializzatore di matrice, come illustrato negli esempi seguenti.  
  
 [!code-vb[VbVbalrAutoImplementedProperties#4](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/auto-implemented-propert_1_5.vb)]  
  
## Definizioni di proprietà che richiedono la sintassi standard  
 Le proprietà implementate automaticamente sono semplici da usare e supportano molti scenari di programmazione.  In alcune situazioni, tuttavia, non è possibile usare una proprietà implementata automaticamente ed è invece necessario usare la sintassi della proprietà standard o *espansa*.  
  
 È necessario usare la sintassi di definizione della proprietà espansa se si vuole eseguire una delle operazioni seguenti:  
  
-   Aggiungere codice alla routine `Get` o `Set` di una proprietà, ad esempio il codice per convalidare i valori in ingresso nella routine `Set`.  È possibile, ad esempio, verificare che una stringa che rappresenta un numero di telefono contenga il numero obbligatorio di numerali prima di impostare il valore della proprietà.  
  
-   Specificare un'accessibilità diversa per le routine `Get` e `Set`.  Ad esempio, si può impostare la routine `Set` come `Private` e la routine `Get` come `Public`.  
  
-   Creare proprietà `WriteOnly`.  
  
-   Usare proprietà con parametri \(incluse le proprietà `Default`\).  È necessario dichiarare una proprietà espansa per specificare un parametro per la proprietà o per specificare parametri aggiuntivi per la routine `Set`.  
  
-   Inserire un attributo nel campo sottostante o modificare il livello di accesso del campo sottostante.  
  
-   Fornire commenti XML per il campo sottostante.  
  
## Espansione di una proprietà implementata automaticamente  
 Se è necessario convertire una proprietà implementata automaticamente in una proprietà espansa contenente una routine `Get` o `Set`, l'editor di codice di Visual Basic può generare automaticamente le routine `Get` e `Set` e l'istruzione `End Property` per la proprietà.  Il codice viene generato se si posiziona il cursore su una riga vuota che segue l'istruzione `Property`, si digita una `G` \(per `Get`\) o una `S` \(per `Set`\) e si preme INVIO.  L'editor di codice di Visual Basic genera automaticamente la routine `Get` o `Set` per le proprietà di sola lettura e di sola scrittura quando si preme INVIO alla fine di un'istruzione `Property`.  
  
## Vedere anche  
 [How to: Declare and Call a Default Property in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [How to: Declare a Property with Mixed Access Levels](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [Property Statement](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [ReadOnly](../../../../visual-basic/language-reference/modifiers/readonly.md)   
 [WriteOnly](../../../../visual-basic/language-reference/modifiers/writeonly.md)   
 [Objects and Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)