---
title: 'Procedura dettagliata: Creazione di oggetti COM con Visual Basic | Documenti di Microsoft'
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
- COM interop, creating COM objects
- COM objects, creating
- COM interop, walkthroughs
- object creation, COM objects
- COM objects, walkthroughs
ms.assetid: 7b07a463-bc72-4392-9ba0-9dfcb697a44f
caps.latest.revision: 30
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
ms.openlocfilehash: cce28e2be5914880107334bf2c4dc4dc645b4793
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-creating-com-objects-with-visual-basic"></a>Procedura dettagliata: creazione di oggetti COM con Visual Basic
Quando si creano nuove applicazioni o componenti, è consigliabile creare gli assembly di .NET Framework. Tuttavia, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] rende facile per esporre un componente di .NET Framework a COM. In questo modo è possibile fornire nuovi componenti per la suite di applicazioni precedenti che richiedono i componenti COM. Questa procedura dettagliata viene illustrato come utilizzare [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per esporre [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] oggetti come oggetti COM, con e senza il modello di classe COM.  
  
 Il modo più semplice per esporre gli oggetti COM è tramite il modello classe COM. Il modello di classe COM crea una nuova classe e quindi Configura il progetto per generare il livello di classe e l'interoperabilità come oggetto COM e registrarlo con il sistema operativo.  
  
> [!NOTE]
>  Sebbene sia possibile esporre anche una classe creata [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] come oggetto COM per codice non gestito da utilizzare, non è un vero oggetto COM e non può essere utilizzato da [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. Per ulteriori informazioni, vedere [l'interoperabilità COM nelle applicazioni .NET Framework](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md).  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-create-a-com-object-by-using-the-com-class-template"></a>Per creare un oggetto COM utilizzando il modello classe COM  
  
1.  Aprire un nuovo progetto applicazione Windows dal **File** menu facendo **nuovo progetto**.  
  
2.  Nel **nuovo progetto** della finestra di dialogo di **tipi di progetto** campo, verificare che Windows sia selezionata. Selezionare **libreria di classi** dal **modelli** elenco e quindi fare clic su **OK**. Viene visualizzato il nuovo progetto.  
  
3.  Selezionare **Aggiungi nuovo elemento** dal **progetto** menu. Il **Aggiungi nuovo elemento** viene visualizzata la finestra di dialogo.  
  
4.  Selezionare **classe COM** dal **modelli** elenco e quindi fare clic su **Aggiungi**. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Aggiunge una nuova classe e configura il nuovo progetto per l'interoperabilità COM.  
  
5.  Aggiungere il codice, ad esempio proprietà, metodi ed eventi della classe COM.  
  
6.  Selezionare **Compila ClassLibrary1** dal **compilare** menu. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]compilare l'assembly e registrare l'oggetto COM con il sistema operativo.  
  
## <a name="creating-com-objects-without-the-com-class-template"></a>Creazione di oggetti COM senza il modello classe COM  
 È inoltre possibile creare una classe COM manualmente invece di utilizzare il modello classe COM. Questa procedura è utile quando si utilizza dalla riga di comando o quando si desidera maggiore controllo sul modo in cui sono definiti oggetti COM.  
  
#### <a name="to-set-up-your-project-to-generate-a-com-object"></a>Per configurare il progetto per generare un oggetto COM  
  
1.  Aprire un nuovo progetto applicazione Windows dal **File** menu facendo **NewProject**.  
  
2.  Nel **nuovo progetto** della finestra di dialogo di **tipi di progetto** campo, verificare che Windows sia selezionata. Selezionare **libreria di classi** dal **modelli** elenco e quindi fare clic su **OK**. Viene visualizzato il nuovo progetto.  
  
3.  In **Esplora**, mouse sul progetto e quindi fare clic su **proprietà**. Il **progettazione** viene visualizzato.  
  
4.  Fare clic sulla scheda **Compila**.  
  
5.  Selezionare il **Registra per interoperabilità COM** casella di controllo.  
  
#### <a name="to-set-up-the-code-in-your-class-to-create-a-com-object"></a>Per impostare il codice nella classe per creare un oggetto COM  
  
1.  In **Esplora**, fare doppio clic su **Class1. vb** per visualizzare il relativo codice.  
  
2.  Rinominare la classe come `ComClass1`.  
  
3.  Aggiungere le seguenti costanti per `ComClass1`. Memorizzano le costanti di identificatore univoco globale (GUID) che sono necessari per disporre gli oggetti COM.  
  
     [!code-vb[VbVbalrInterop n.&2;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_1.vb)]  
  
4.  Nel **strumenti** menu, fare clic su **crea Guid**. Nel **Crea GUID** la finestra di dialogo, fare clic su **il formato del Registro di sistema** e quindi fare clic su **copia**. Fare clic su **Esci**.  
  
5.  Sostituire la stringa vuota per il `ClassId` con il GUID, rimuovendo le iniziali e finali parentesi graffe. Ad esempio, se il GUID fornito da Guidgen è `"{2C8B0AEE-02C9-486e-B809-C780A11530FE}"` quindi il codice dovrebbe risultare come segue.  
  
     [!code-vb[VbVbalrInterop n.&3;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_2.vb)]  
  
6.  Ripetere i passaggi precedenti per il `InterfaceId` e `EventsId` costanti, come nell'esempio seguente.  
  
     [!code-vb[VbVbalrInterop n.&4;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_3.vb)]  
  
    > [!NOTE]
    >  Assicurarsi che i GUID siano nuovi e univoci. in caso contrario, il componente COM potrebbe entrare in conflitto con altri componenti COM.  
  
7.  Aggiungere il `ComClass` attributo `ComClass1`, specificando i GUID per l'ID di classe, l'ID di interfaccia e ID degli eventi, come nell'esempio seguente:  
  
     [!code-vb[VbVbalrInterop n.&5;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_4.vb)]  
  
8.  Classi COM devono avere un costruttore `Public Sub New()` costruttore o la classe non registrare correttamente. Aggiungere un costruttore senza parametri alla classe:  
  
     [!code-vb[6 VbVbalrInterop](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_5.vb)]  
  
9. Aggiungere proprietà, metodi ed eventi alla classe, terminando con un `End Class` istruzione. Selezionare **Compila soluzione** dal **compilare** menu. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]compilare l'assembly e registrare l'oggetto COM con il sistema operativo.  
  
    > [!NOTE]
    >  Gli oggetti COM è generare con [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non può essere utilizzato da altri [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] applicazioni perché non sono veri oggetti COM. Tenta di aggiungere riferimenti a tali oggetti COM genererà un errore. Per informazioni dettagliate, vedere [l'interoperabilità COM nelle applicazioni .NET Framework](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.ComClassAttribute></xref:Microsoft.VisualBasic.ComClassAttribute>   
 [Interoperabilità COM](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Procedura dettagliata: Implementazione dell'ereditarietà con gli oggetti COM](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [#Region (direttiva)](../../../visual-basic/language-reference/directives/region-directive.md)   
 [Interoperabilità COM nelle applicazioni .NET Framework](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)   
 [Risoluzione dei problemi relativi all'interoperabilità](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)
