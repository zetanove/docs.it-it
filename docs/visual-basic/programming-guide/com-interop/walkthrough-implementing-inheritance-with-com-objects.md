---
title: "Procedura dettagliata: Implementazione dell&quot;ereditarietà con gli oggetti COM (Visual Basic) | Documenti di Microsoft"
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
- inheritance, COM reusability
- base classes, COM reusability
- inheritance, walkthroughs
- derived classes, COM reusability
ms.assetid: f8e7263a-de13-48d1-b67c-ca1adf3544d9
caps.latest.revision: 16
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
ms.openlocfilehash: fa7753847619f14600c924cba01e55651c4f17c2
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-implementing-inheritance-with-com-objects-visual-basic"></a>Procedura dettagliata: implementazione dell'ereditarietà con gli oggetti COM (Visual Basic)
È possibile derivare classi di Visual Basic da `Public` classi di oggetti COM, anche quelli creati in versioni precedenti di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. Le proprietà e metodi delle classi ereditate da oggetti COM possono essere sottoposto a override o sottoposto a overload solo come proprietà e metodi di qualsiasi altra classe di base possono essere sottoposto a override o di overload. Ereditarietà da oggetti COM è utile quando si dispone di una libreria di classi esistenti che non si desidera ricompilare.  
  
 La procedura seguente viene illustrato come utilizzare Visual Basic 6.0 per creare un oggetto COM che contiene una classe e quindi utilizzarlo come classe base.  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-build-the-com-object-that-is-used-in-this-walkthrough"></a>Per creare l'oggetto COM che viene utilizzato in questa procedura dettagliata  
  
1.  In Visual Basic 6.0, aprire un nuovo progetto DLL ActiveX. Un progetto denominato `Project1` viene creato. Dispone di una classe denominata `Class1`.  
  
2.  Nel **Project Explorer**, fare doppio clic su **Project1**, quindi fare clic su **proprietà Project1**. Il **le proprietà del progetto** viene visualizzata la finestra di dialogo.  
  
3.  Nel **generale** scheda della finestra il **le proprietà del progetto** finestra di dialogo, modificare il nome del progetto digitando `ComObject1` nel **nome progetto** campo.  
  
4.  Nel **Project Explorer**, fare doppio clic su `Class1`, quindi fare clic su **proprietà**. Il **proprietà** verrà visualizzata la finestra per la classe.  
  
5.  Modifica il `Name` proprietà `MathFunctions`.  
  
6.  Nel **Project Explorer**, fare doppio clic su `MathFunctions`, quindi fare clic su **Visualizza codice**. Il **Editor di codice** viene visualizzato.  
  
7.  Aggiungere una variabile locale per contenere il valore della proprietà:  
  
    ```  
    ' Local variable to hold property value  
    Private mvarProp1 As Integer  
    ```  
  
8.  Aggiungere proprietà `Let` e proprietà `Get` le routine di proprietà:  
  
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
  
9. Aggiungere una funzione:  
  
    ```  
    Function AddNumbers(   
       ByVal SomeNumber As Integer,   
       ByVal AnotherNumber As Integer) As Integer  
  
       AddNumbers = SomeNumber + AnotherNumber  
    End Function  
    ```  
  
10. Creare e registrare l'oggetto COM scegliendo **Crea ComObject1. dll** sul **File** menu.  
  
    > [!NOTE]
    >  Sebbene sia possibile esporre anche una classe creata con [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] come oggetto COM non è un vero oggetto COM e non può essere utilizzato in questa procedura dettagliata. Per informazioni dettagliate, vedere [l'interoperabilità COM nelle applicazioni .NET Framework](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md).  
  
## <a name="interop-assemblies"></a>Assembly di interoperabilità  
 Nella procedura seguente, si creerà un assembly di interoperabilità, che funge da ponte tra codice non gestito (ad esempio un oggetto COM) e il codice gestito [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] utilizza. L'assembly di interoperabilità che [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] crea gestisce molti dei dettagli relativi all'utilizzo con COM oggetti, ad esempio *il marshalling di interoperabilità*, il processo di creazione dei pacchetti parametri e valori restituiti in dati equivalenti tipi durante lo spostamento da e verso oggetti COM. Il riferimento nel [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] punti dell'applicazione per l'assembly di interoperabilità, non all'oggetto COM.  
  
#### <a name="to-use-a-com-object-with-visual-basic-2005-and-later-versions"></a>Per utilizzare un oggetto COM con Visual Basic 2005 e versioni successive  
  
1.  Aprire un nuovo [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] progetto applicazione Windows.  
  
2.  Nel **progetto** menu, fare clic su **Aggiungi riferimento**.  
  
     Il **Aggiungi riferimento** viene visualizzata la finestra di dialogo.  
  
3.  Nel **COM** scheda, fare doppio clic su `ComObject1` nel **nome componente** elenco e fare clic su **OK**.  
  
4.  Nel menu **Progetto** fare clic su **Aggiungi nuovo elemento**.  
  
     Il **Aggiungi nuovo elemento** viene visualizzata la finestra di dialogo.  
  
5.  Nel **modelli** riquadro, fare clic su **classe**.  
  
     Il nome file predefinito, `Class1.vb`, è presente il **nome** campo. Modificare questo campo per MathClass e fare clic su **Aggiungi**. Verrà creata una classe denominata `MathClass`e verrà visualizzato il codice.  
  
6.  Aggiungere il codice seguente all'inizio del `MathClass` per ereditare dalla classe COM.  
  
     [!code-vb[VbVbalrInterop&#31;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_1.vb)]  
  
7.  Eseguire l'overload del metodo pubblico della classe di base aggiungendo il codice seguente al `MathClass`:  
  
     [!code-vb[VbVbalrInterop n.&32;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_2.vb)]  
  
8.  Estendere la classe ereditata aggiungendo il codice seguente al `MathClass`:  
  
     [!code-vb[VbVbalrInterop n.&33;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_3.vb)]  
  
 La nuova classe eredita le proprietà della classe di base dell'oggetto COM, un metodo di overload e definisce un nuovo metodo per estendere la classe.  
  
#### <a name="to-test-the-inherited-class"></a>Per testare la classe ereditata  
  
1.  Aggiungere un pulsante al form di avvio e quindi fare doppio clic per visualizzare il codice.  
  
2.  Il pulsante `Click` routine del gestore eventi, aggiungere il codice seguente per creare un'istanza di `MathClass` e chiamare i metodi di overload:  
  
     [!code-vb[VbVbalrInterop&#34;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_4.vb)]  
  
3.  Eseguire il progetto premendo F5.  
  
 Quando si fa clic sul pulsante nel form, il `AddNumbers` prima chiamata al metodo con `Short` numeri del tipo di dati e [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] sceglie il metodo appropriato dalla classe di base. La seconda chiamata a `AddNumbers` viene indirizzata al metodo di overload da `MathClass`. La terza chiamata richiama il `SubtractNumbers` (metodo), che estende la classe. La proprietà nella classe di base è impostata e viene visualizzato il valore.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Si è notato che il metodo di overload `AddNumbers` funzione sembra avere dati dello stesso tipo del metodo ereditato dalla classe di base dell'oggetto COM. Questo avviene perché gli argomenti e parametri del metodo della classe base sono definiti come numeri interi a 16 bit in Visual Basic 6.0, ma sono esposti come integer a 16 bit di tipo `Short` nelle versioni successive di Visual Basic. La nuova funzione accetta valori integer a 32 bit ed esegue l'overload di funzione di classe base.  
  
 Quando si utilizzano oggetti COM, assicurarsi di verificare le dimensioni e tipi di dati dei parametri. Ad esempio, quando si utilizza un oggetto COM che accetta un oggetto raccolta di Visual Basic 6.0 come argomento, è possibile fornire un insieme di una versione successiva di Visual Basic.  
  
 Possono essere ignorati le proprietà e metodi ereditati dalle classi COM, vale a dire che è possibile dichiarare una proprietà locale o un metodo che sostituisce una proprietà o metodo ereditato da una classe COM. Le regole per eseguire l'override delle proprietà COM ereditate sono simili alle regole per eseguire l'override di altre proprietà e metodi con le eccezioni seguenti:  
  
-   Se si esegue l'override di proprietà o metodi ereditati da una classe COM, è necessario sostituire tutte le altre proprietà ereditate e metodi.  
  
-   Le proprietà che utilizzano `ByRef` parametri non possono essere sottoposto a override.  
  
## <a name="see-also"></a>Vedere anche  
 [Interoperabilità COM nelle applicazioni .NET Framework](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)   
 [Inherits (istruzione)](../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [Tipo di dati Short](../../../visual-basic/language-reference/data-types/short-data-type.md)
