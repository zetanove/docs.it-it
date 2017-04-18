---
title: 'Procedura dettagliata: Modifica di file con i metodi .NET Framework (Visual Basic) | Microsoft Docs'
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
- I/O [Visual Basic], walkthroughs
- text files, writing to
- reading text files
- text, writing to files
- files, searching
- StreamReader class, walkthroughs
- files, accessing
- I/O [Visual Basic], writing text to files
- writing to files, walkthroughs
- StreamWriter class, walkthroughs
- text files, reading
- I/O [Visual Basic], reading text from files
ms.assetid: 7d2109eb-f98a-4389-b43d-30f384aaa7d5
caps.latest.revision: 18
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e8bf73f32dba51455542778ed91ef3bfd2898754
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-manipulating-files-by-using-net-framework-methods-visual-basic"></a>Procedura dettagliata: modifica di file mediante i metodi .NET Framework (Visual Basic)
Questa procedura dettagliata spiega come aprire e leggere un file usando la classe <xref:System.IO.StreamReader>, verificare se un file è accessibile, cercare una stringa all'interno di un file letto con un'istanza della classe <xref:System.IO.StreamReader> e scrivere in un file usando la classe <xref:System.IO.StreamWriter>.  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## <a name="creating-the-application"></a>Creare l'applicazione  
 Avviare [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] e iniziare il progetto creando un form che l'utente può usare per scrivere il file specificato.  
  
#### <a name="to-create-the-project"></a>Per creare il progetto  
  
1.  Nel menu **File** selezionare **Nuovo progetto**.  
  
2.  Nel riquadro **Nuovo progetto** fare clic su **Applicazione Windows**.  
  
3.  Nella casella **Nome** digitare `MyDiary` e fare clic su **OK**.  
  
     [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] aggiunge il progetto a **Esplora soluzioni** e viene aperto **Progettazione Windows Form**.  
  
4.  Aggiungere i controlli della tabella seguente al form e impostare i valori corrispondenti per le relative proprietà.  
  
|**Oggetto**|**Proprietà**|**Valore**|  
|---|---|---|   
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Testo**|`Submit`<br /><br /> **Invia voce**|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Testo**|`Clear`<br /><br /> **Cancella voce**|  
|<xref:System.Windows.Forms.TextBox>|**Nome**<br /><br /> **Testo**<br /><br /> **Multiline**|`Entry`<br /><br /> **Immettere un valore.**<br /><br /> `False`|  
  
## <a name="writing-to-the-file"></a>Scrivere nel file  
 Per aggiungere la possibilità di scrivere in un file usando l'applicazione, usare la classe <xref:System.IO.StreamWriter>. La classe <xref:System.IO.StreamWriter> è progettata per l'output di caratteri in una codifica particolare, mentre la classe <xref:System.IO.Stream> è progettata per l'input e l'output di byte. Usare <xref:System.IO.StreamWriter> per scrivere righe di informazioni in un file di testo standard. Per altre informazioni sulla classe <xref:System.IO.StreamWriter>, vedere <xref:System.IO.StreamWriter>.  
  
#### <a name="to-add-writing-functionality"></a>Per aggiungere la funzionalità di scrittura  
  
1.  Scegliere **Codice** dal menu **Visualizza** per aprire l'editor di codice.  
  
2.  Poiché l'applicazione fa riferimento allo spazio dei nomi <xref:System.IO>, aggiungere le istruzioni seguenti all'inizio del codice, prima della dichiarazione di classe per il form, che inizia con `Public Class Form1`.  
  
     [!code-vb[VbVbcnMyFileSystem#35](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_1.vb)]  
  
     Prima di scrivere nel file è necessario creare un'istanza di una classe <xref:System.IO.StreamWriter>.  
  
3.  Scegliere **Finestra di progettazione** dal menu **Visualizza** per tornare a **Progettazione Windows Form**. Fare doppio clic sul pulsante `Submit` per creare un gestore eventi <xref:System.Windows.Forms.Control.Click> per il pulsante e quindi aggiungere il codice seguente.  
  
     [!code-vb[VbVbcnMyFileSystem#36](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_2.vb)]  
  
> [!NOTE]
>  L'ambiente di sviluppo integrato (IDE) di Visual Studio torna all'editor di codice e posiziona il punto di inserimento all'interno del gestore eventi in cui deve essere aggiunto il codice.  
  
1.  Per scrivere nel file, usare il metodo <xref:System.IO.StreamWriter.Write%2A> della classe <xref:System.IO.StreamWriter>. Aggiungere il codice seguente direttamente dopo `Dim fw As StreamWriter`. Non è necessario preoccuparsi del fatto che venga generata un'eccezione se il file non viene trovato, poiché verrà creato se non esiste già.  
  
     [!code-vb[VbVbcnMyFileSystem#37](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_3.vb)]  
  
2.  Assicurarsi che l'utente non possa immettere uno spazio vuoto aggiungendo il codice seguente subito dopo `Dim ReadString As String`.  
  
     [!code-vb[VbVbcnMyFileSystem#38](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_4.vb)]  
  
3.  Poiché si tratta di un diario, l'utente dovrà assegnare una data a ogni voce. Inserire il codice seguente dopo `fw = New StreamWriter("C:\MyDiary.txt", True)` per impostare la variabile `Today` sulla data corrente.  
  
     [!code-vb[VbVbcnMyFileSystem#39](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_5.vb)]  
  
4.  Aggiungere infine il codice per cancellare <xref:System.Windows.Forms.TextBox>. Aggiungere il codice seguente all'evento <xref:System.Windows.Forms.Control.Click> del pulsante `Clear`.  
  
     [!code-vb[VbVbcnMyFileSystem#40](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_6.vb)]  
  
## <a name="adding-display-features-to-the-diary"></a>Aggiungere funzionalità di visualizzazione al diario  
 In questa sezione, si aggiunge una funzionalità che consente di visualizzare l'ultima voce dell'oggetto <xref:System.Windows.Forms.TextBox> `DisplayEntry`. È anche possibile aggiungere un oggetto <xref:System.Windows.Forms.ComboBox> che visualizza le diverse voci e da cui un utente può selezionare una voce da visualizzare nell'oggetto <xref:System.Windows.Forms.TextBox> `DisplayEntry`. Un'istanza della classe <xref:System.IO.StreamReader> legge da `MyDiary.txt`. Come la classe <xref:System.IO.StreamWriter>, la classe <xref:System.IO.StreamReader> deve essere usata con i file di testo.  
  
 Per questa sezione della procedura, aggiungere i controlli della tabella seguente al form e impostare i valori corrispondenti per le relative proprietà.  
  
|Controllo|Proprietà|Valori|  
|-------------|----------------|------------|  
|<xref:System.Windows.Forms.TextBox>|**Nome**<br /><br /> **Visible**<br /><br /> **Dimensione**<br /><br /> **Multiline**|`DisplayEntry`<br /><br /> `False`<br /><br /> `120,60`<br /><br /> `True`|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Testo**|`Display`<br /><br /> **Visualizza**|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Testo**|`GetEntries`<br /><br /> **Ottieni voci**|  
|<xref:System.Windows.Forms.ComboBox>|**Nome**<br /><br /> **Testo**<br /><br /> **Enabled**|`PickEntries`<br /><br /> **Seleziona una voce**<br /><br /> `False`|  
  
#### <a name="to-populate-the-combo-box"></a>Per popolare la casella combinata  
  
1.  L'oggetto <xref:System.Windows.Forms.ComboBox> `PickEntries` viene usato per visualizzare le date in cui un utente immette ogni voce, in modo che l'utente possa selezionare una voce da una data specifica. Creare un gestore eventi <xref:System.Windows.Forms.Control.Click> per il pulsante `GetEntries` e aggiungere il codice seguente.  
  
     [!code-vb[VbVbcnMyFileSystem#41](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_7.vb)]  
  
2.  Per testare il codice, premere F5 per compilare l'applicazione e quindi fare clic su **Ottieni voci**. Fare clic sulla freccia giù nell'oggetto <xref:System.Windows.Forms.ComboBox> per visualizzare le date delle voci.  
  
#### <a name="to-choose-and-display-individual-entries"></a>Per scegliere e visualizzare le singole voci  
  
1.  Creare un gestore eventi <xref:System.Windows.Forms.Control.Click> per il pulsante `Display` e aggiungere il codice seguente.  
  
     [!code-vb[VbVbcnMyFileSystem#42](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_8.vb)]  
  
2.  Per testare il codice, premere F5 per compilare l'applicazione e quindi inviare una voce. Fare clic su **Ottieni voci**, selezionare una voce in <xref:System.Windows.Forms.ComboBox>, quindi fare clic su **Visualizza**. Il contenuto della voce selezionata viene visualizzato nell'oggetto <xref:System.Windows.Forms.TextBox> `DisplayEntry`.  
  
## <a name="enabling-users-to-delete-or-modify-entries"></a>Consentire agli utenti di eliminare o modificare le voci  
 Infine, è possibile includere funzionalità aggiuntive che consentono agli utenti di eliminare o modificare una voce usando i pulsanti `DeleteEntry` e `EditEntry`. Entrambi i pulsanti restano disabilitati a meno che non sia visualizzata una voce.  
  
 Aggiungere i controlli della tabella seguente al form e impostare i valori corrispondenti per le relative proprietà.  
  
|Controllo|Proprietà|Valori|  
|-------------|----------------|------------|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Testo**<br /><br /> **Enabled**|`DeleteEntry`<br /><br /> **Elimina voce**<br /><br /> `False`|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Testo**<br /><br /> **Enabled**|`EditEntry`<br /><br /> **Modifica voce**<br /><br /> `False`|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Testo**<br /><br /> **Enabled**|`SubmitEdit`<br /><br /> **Invia modifica**<br /><br /> `False`|  
  
#### <a name="to-enable-deletion-and-modification-of-entries"></a>Per abilitare l'eliminazione e la modifica delle voci  
  
1.  Aggiungere il codice seguente all'evento <xref:System.Windows.Forms.Control.Click> del pulsante `Display`, dopo `DisplayEntry.Text = ReadString`.  
  
     [!code-vb[VbVbcnMyFileSystem#43](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_9.vb)]  
  
2.  Creare un gestore eventi <xref:System.Windows.Forms.Control.Click> per il pulsante `DeleteEntry` e aggiungere il codice seguente.  
  
     [!code-vb[VbVbcnMyFileSystem#44](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_10.vb)]  
  
3.  Quando un utente visualizza una voce, il pulsante `EditEntry` viene abilitato. Aggiungere il codice seguente all'evento <xref:System.Windows.Forms.Control.Click> del pulsante `Display`, dopo `DisplayEntry.Text = ReadString`.  
  
     [!code-vb[VbVbcnMyFileSystem#45](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_11.vb)]  
  
4.  Creare un gestore eventi <xref:System.Windows.Forms.Control.Click> per il pulsante `EditEntry` e aggiungere il codice seguente.  
  
     [!code-vb[VbVbcnMyFileSystem#46](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_12.vb)]  
  
5.  Creare un gestore eventi <xref:System.Windows.Forms.Control.Click> per il pulsante `SubmitEdit` e aggiungere il codice seguente  
  
     [!code-vb[VbVbcnMyFileSystem#47](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_13.vb)]  
  
 Per testare il codice, premere F5 per compilare l'applicazione. Fare clic su **Ottieni voci**, selezionare una voce e quindi fare clic su **Visualizza**. La voce viene visualizzata nell'oggetto <xref:System.Windows.Forms.TextBox> `DisplayEntry`. Fare clic su **Modifica voce**. La voce viene visualizzata nell'oggetto <xref:System.Windows.Forms.TextBox> `Entry`. Modificare la voce nell'oggetto <xref:System.Windows.Forms.TextBox> `Entry` e fare clic su **Invia modifica**. Aprire il file `MyDiary.txt` per confermare la correzione. Ora selezionare una voce e fare clic su **Elimina voce**. Quando l'oggetto <xref:System.Windows.Forms.MessageBox> richiede una conferma, fare clic su **OK**. Chiudere l'applicazione e aprire `MyDiary.txt` per confermare l'eliminazione.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IO.StreamReader>   
 <xref:System.IO.StreamWriter>   
 [Procedure dettagliate](../../../../visual-basic/walkthroughs.md)

