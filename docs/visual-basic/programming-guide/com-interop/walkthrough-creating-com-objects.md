---
title: "Walkthrough: Creating COM Objects with Visual Basic | Microsoft Docs"
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
  - "COM interop, creating COM objects"
  - "COM objects, creating"
  - "COM interop, walkthroughs"
  - "object creation, COM objects"
  - "COM objects, walkthroughs"
ms.assetid: 7b07a463-bc72-4392-9ba0-9dfcb697a44f
caps.latest.revision: 30
caps.handback.revision: 30
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Walkthrough: Creating COM Objects with Visual Basic
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Quando si creano applicazioni o componenti nuovi, è consigliabile creare assembly .NET Framework.  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] semplifica tuttavia l'esposizione di un componente .NET Framework anche per COM.  In questo modo è possibile fornire nuovi componenti per le suite di applicazioni precedenti che richiedono i componenti COM.  In questa procedura dettagliata viene illustrato come utilizzare [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per esporre oggetti [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] come oggetti COM, utilizzando o meno il modello della classe COM.  
  
 Il modo più semplice per esporre oggetti COM è quello di utilizzare il modello della classe COM.  Tale modello consente di creare una nuova classe, quindi configurare il progetto per la creazione della classe e del layer di interoperabilità come oggetto COM e per la relativa registrazione nel sistema operativo.  
  
> [!NOTE]
>  Sebbene sia possibile esporre come oggetto COM anche una classe creata con [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per consentirne l'utilizzo da parte del codice non gestito, non si tratta di un vero oggetto COM che non può essere usato da [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  Per ulteriori informazioni, vedere [COM Interoperability in .NET Framework Applications](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md).  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### Per creare un oggetto COM utilizzando il modello di classe COM  
  
1.  Aprire un nuovo progetto Applicazione Windows scegliendo **Nuovo progetto** dal menu **File**.  
  
2.  Nel campo **Tipi progetto** della finestra di dialogo **Nuovo progetto** verificare che sia selezionata la voce Windows.  Selezionare **Libreria di classi** dall'elenco **Modelli** e fare clic su **OK**.  Verrà visualizzato il nuovo progetto.  
  
3.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  Verrà visualizzata la finestra di dialogo **Aggiungi nuovo elemento**.  
  
4.  Selezionare **Classe COM** dall'elenco **Modelli**, quindi scegliere **Aggiungi**.  In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] verrà aggiunta una nuova classe e verrà configurato il nuovo progetto per l'interoperabilità COM.  
  
5.  Aggiungere codice, ad esempio proprietà, metodi ed eventi alla classe COM.  
  
6.  Selezionare **Compila ClassLibrary1** dal menu **Compila**.  In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] verrà compilato l'assembly e l'oggetto COM verrà registrato nel sistema operativo.  
  
## Creazione di oggetti COM senza il modello di classe COM  
 È anche possibile creare una classe COM manualmente, senza utilizzare il modello di classe COM.  Questa procedura è utile quando si utilizza la riga di comando o quando si desidera un maggiore controllo sulla definizione degli oggetti COM.  
  
#### Per impostare il progetto per la creazione di un oggetto COM  
  
1.  Aprire un nuovo progetto Applicazione Windows dal menu **File** facendo clic su **Nuovo Progetto**.  
  
2.  Nel campo **Tipi progetto** della finestra di dialogo **Nuovo progetto** verificare che sia selezionata la voce Windows.  Selezionare **Libreria di classi** dall'elenco **Modelli** e fare clic su **OK**.  Verrà visualizzato il nuovo progetto.  
  
3.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Proprietà**.  Verrà visualizzata la finestra **Progettazione progetti**.  
  
4.  Fare clic sulla scheda **Compila**.  
  
5.  Selezionare la casella di controllo **Registra per interoperabilità COM**.  
  
#### Per impostare il codice della classe per la creazione di un oggetto COM  
  
1.  In **Esplora soluzioni** fare doppio clic su **Class1.vb** per visualizzare il relativo codice.  
  
2.  Rinominare la classe come `ComClass1`.  
  
3.  Aggiungere a `ComClass1` le costanti riportate di seguito  che memorizzeranno le costanti GUID \(Globally Unique Identifier\) richieste negli oggetti COM.  
  
     [!code-vb[VbVbalrInterop#2](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_1.vb)]  
  
4.  Scegliere **Crea GUID** dal menu **Strumenti**.  Nella finestra di dialogo **Crea GUID** fare clic sull'opzione relativa al formato del registro, quindi su **Copia**.  Fare clic su **Esci**.  
  
5.  Sostituire la stringa vuota relativa a `ClassId` con il GUID, rimuovendo le parentesi graffe di apertura e chiusura.  Se il GUID fornito da Guidgen è, ad esempio, `"{2C8B0AEE-02C9-486e-B809-C780A11530FE}"` il codice deve essere simile a quello riportato di seguito.  
  
     [!code-vb[VbVbalrInterop#3](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_2.vb)]  
  
6.  Ripetere i passaggi precedenti per le costanti `InterfaceId` e `EventsId`, come nell'esempio che segue.  
  
     [!code-vb[VbVbalrInterop#4](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_3.vb)]  
  
    > [!NOTE]
    >  Accertarsi che i GUID siano nuovi ed univoci. In caso contrario, potrebbe verificarsi un conflitto tra il componente COM e gli altri componenti COM.  
  
7.  Aggiungere l'attributo `ComClass` a `ComClass1`, specificando i GUID per l'ID di classe, l'ID di interfaccia e gli ID di eventi, come nell'esempio seguente:  
  
     [!code-vb[VbVbalrInterop#5](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_4.vb)]  
  
8.  Le classi COM devono avere un costruttore `Public Sub New()` senza parametri. In caso contrario, la classe non potrà essere registrata correttamente.  Aggiungere un costruttore senza parametri alla classe:  
  
     [!code-vb[VbVbalrInterop#6](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_5.vb)]  
  
9. Aggiungere proprietà, metodi ed eventi alla classe, terminando con un'istruzione `End Class`.  Scegliere **Compila soluzione** dal menu **Compila**.  In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] verrà compilato l'assembly e l'oggetto COM verrà registrato nel sistema operativo.  
  
    > [!NOTE]
    >  Gli oggetti COM generati con [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non possono essere utilizzati con altre applicazioni [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] in quanto non sono veri oggetti COM.  Se si cerca di aggiungere riferimenti a tali oggetti COM, verrà generato un errore.  Per informazioni dettagliate, vedere [COM Interoperability in .NET Framework Applications](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.ComClassAttribute>   
 [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Walkthrough: Implementing Inheritance with COM Objects](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [\#Region Directive](../../../visual-basic/language-reference/directives/region-directive.md)   
 [COM Interoperability in .NET Framework Applications](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)   
 [Troubleshooting Interoperability](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)