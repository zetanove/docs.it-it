---
title: "Walkthrough: Implementing Inheritance with COM Objects (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "inheritance, COM reusability"
  - "base classes, COM reusability"
  - "inheritance, walkthroughs"
  - "derived classes, COM reusability"
ms.assetid: f8e7263a-de13-48d1-b67c-ca1adf3544d9
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Walkthrough: Implementing Inheritance with COM Objects (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È possibile derivare classi di Visual Basic da classi `Public` di oggetti COM, anche se creati con versioni precedenti di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  È possibile eseguire l'override o l'overload di proprietà e metodi delle classi ereditate da oggetti COM con le stesse modalità utilizzate per le proprietà e i metodi di qualsiasi altra classe base.  L'ereditarietà da oggetti COM è utile se si dispone di una libreria di classi esistente che non si desidera ricompilare.  
  
 Nella procedura descritta di seguito viene illustrato come creare in Visual Basic 6.0 un oggetto COM contenente una classe e in che modo utilizzarlo come classe base.  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### Per compilare l'oggetto COM utilizzato in questa procedura dettagliata  
  
1.  In Visual Basic 6.0 aprire un nuovo progetto DLL ActiveX.  È stato creato un progetto denominato `Project1` con una classe denominata `Class1`.  
  
2.  In **Esplora progetti** fare clic con il pulsante destro del mouse su **Project1**, quindi scegliere **Proprietà Project1**.  Verrà visualizzata la finestra di dialogo **Proprietà progetto**.  
  
3.  Nella scheda **Generale** della finestra di dialogo **Proprietà progetto**, modificare il nome del progetto digitando `ComObject1` nel campo **Nome progetto**.  
  
4.  In **Esplora progetti** fare clic con il pulsante destro del mouse su `Class1`, quindi scegliere **Proprietà**.  Verrà visualizzata la finestra **Proprietà** relativa alla classe.  
  
5.  Modificare la proprietà `Name` in `MathFunctions`.  
  
6.  In **Esplora progetti** fare clic con il pulsante destro del mouse su `MathFunctions`, quindi scegliere **Visualizza codice**.  Verrà visualizzato l'**Editor di codice**.  
  
7.  Aggiungere una variabile locale per contenere il valore della proprietà.  
  
    ```  
    ' Local variable to hold property value  
    Private mvarProp1 As Integer  
    ```  
  
8.  Aggiungere le routine di proprietà Property `Let` e Property `Get`:  
  
    ```  
    Public Property Let Prop1(ByVal vData As Integer)  
       'Used when assigning a value to the property.  
       mvarProp1 = vData  
    End Property  
    Public Property Get Prop1() As Integer  
       'Used when retrieving a property's value.  
       Prop1 = mvarProp1  
    End Property  
    ```  
  
9. Aggiungere una funzione.  
  
    ```  
    Function AddNumbers(   
       ByVal SomeNumber As Integer,   
       ByVal AnotherNumber As Integer) As Integer  
  
       AddNumbers = SomeNumber + AnotherNumber  
    End Function  
    ```  
  
10. Creare e registrare l'oggetto COM scegliendo **Crea ComObject1.dll** dal menu **File**.  
  
    > [!NOTE]
    >  Sebbene sia anche possibile esporre una classe creata con [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] come oggetto COM, non si tratta di un vero e proprio oggetto COM e non può essere utilizzato in questa procedura dettagliata.  Per informazioni dettagliate, vedere [COM Interoperability in .NET Framework Applications](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md).  
  
## Assembly di interoperabilità  
 Nella procedura riportata di seguito viene illustrato come creare un assembly di interoperabilità, che funge da ponte tra il codice non gestito, ad esempio un oggetto COM, e il codice gestito utilizzato da [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)].  L'assembly di interoperabilità creato in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gestisce molti dei dettagli relativi all'utilizzo degli oggetti COM, ad esempio il *marshalling di interoperabilità*, ovvero il processo di inserimento dei parametri e dei valori restituiti in tipi di dati equivalenti durante lo spostamento da e in oggetti COM.  Il riferimento nelle applicazioni [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] punta all'assembly di interoperabilità e non all'oggetto COM vero e proprio.  
  
#### Per utilizzare un oggetto COM con Visual Basic 2005 e versioni più recenti  
  
1.  Aprire un nuovo progetto Applicazione Windows di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
2.  Scegliere **Aggiungi riferimento** dal menu **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Aggiungi riferimento**.  
  
3.  Nella scheda **COM** fare doppio clic su `ComObject1` nell'elenco **Nome componente**, quindi scegliere **OK**.  
  
4.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Aggiungi nuovo elemento**.  
  
5.  Nel riquadro **Modelli** selezionare **Classe**.  
  
     Il nome file predefinito, `Class1.vb`, viene visualizzato nel campo **Nome**.  Assegnare al campo il nome MathClass.vb e fare clic su **Aggiungi**.  Verrà quindi creata una classe denominata `MathClass` e ne verrà visualizzato il codice.  
  
6.  Aggiungere all'inizio della classe `MathClass` il codice che segue per ereditare dalla classe COM.  
  
     [!code-vb[VbVbalrInterop#31](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_1.vb)]  
  
7.  Eseguire l'overload del metodo pubblico della classe base aggiungendo a `MathClass` il seguente codice:  
  
     [!code-vb[VbVbalrInterop#32](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_2.vb)]  
  
8.  Estendere la classe ereditata aggiungendo a `MathClass` il seguente codice:  
  
     [!code-vb[VbVbalrInterop#33](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_3.vb)]  
  
 La nuova classe eredita le proprietà della classe base dell'oggetto COM, esegue l'overload di un metodo e definisce un nuovo metodo per estendere la classe.  
  
#### Per testare della classe ereditata  
  
1.  Aggiungere un pulsante al form di avvio, quindi fare doppio clic su di esso per visualizzarne il codice.  
  
2.  Nella routine del gestore eventi `Click` del pulsante aggiungere il codice riportato di seguito per creare un'istanza di `MathClass` e chiamare i metodi di cui è stato eseguito l'overload.  
  
     [!code-vb[VbVbalrInterop#34](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_4.vb)]  
  
3.  Premere F5 per eseguire il progetto.  
  
 Quando si fa clic sul pulsante nel form, viene chiamato il metodo `AddNumbers` con numeri del tipo di dati `Short` e viene scelto il metodo appropriato dalla classe base.  La seconda chiamata a `AddNumbers` è diretta al metodo di overload da `MathClass`.  La terza chiamata richiama il metodo `SubtractNumbers`, che estende la classe.  Viene impostata la proprietà della classe base e viene visualizzato il valore.  
  
## Passaggi successivi  
 La funzione `AddNumbers` in overload sembra avere lo stesso tipo di dati del metodo ereditato dalla classe base dell'oggetto COM.  I parametri e gli argomenti del metodo della classe base infatti sono definiti come Integer a 16 bit in Visual Basic 6.0, ma sono esposti come Integer a 16 bit di tipo `Short` nelle versioni successive di Visual Basic.  La nuova funzione accetta Integer a 32 bit ed esegue l'overload della funzione di classe base.  
  
 Quando si utilizzano oggetti COM, è importante verificare le dimensioni e i tipi di dati dei parametri.  Quando ad esempio si utilizza un oggetto COM che accetta un oggetto Collection di Visual Basic 6.0 come argomento, non è possibile fornire una raccolta da una versione successiva di Visual Basic.  
  
 È possibile eseguire l'override di proprietà e metodi ereditati da classi COM e questo significa che è possibile dichiarare una proprietà o metodo locale che sostituisce una proprietà o metodo ereditato da una classe COM base.  Le regole per l'override di proprietà COM ereditate sono simili a quelle relative all'override di altre proprietà e metodi con le seguenti eccezioni:  
  
-   Se si esegue l'override di proprietà o metodi ereditati da una classe COM, è necessario di eseguire l'override di tutti gli altri metodi e proprietà ereditati.  
  
-   Non è possibile eseguire l'override di proprietà che utilizzano parametri `ByRef`.  
  
## Vedere anche  
 [COM Interoperability in .NET Framework Applications](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)   
 [Inherits Statement](../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [Short Data Type](../../../visual-basic/language-reference/data-types/short-data-type.md)