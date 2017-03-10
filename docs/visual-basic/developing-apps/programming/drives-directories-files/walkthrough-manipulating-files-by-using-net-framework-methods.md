---
title: "Walkthrough: Manipulating Files by Using .NET Framework Methods (Visual Basic) | Microsoft Docs"
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
  - "I/O [Visual Basic], walkthroughs"
  - "text files, writing to"
  - "reading text files"
  - "text, writing to files"
  - "files, searching"
  - "StreamReader class, walkthroughs"
  - "files, accessing"
  - "I/O [Visual Basic], writing text to files"
  - "writing to files, walkthroughs"
  - "StreamWriter class, walkthroughs"
  - "text files, reading"
  - "I/O [Visual Basic], reading text from files"
ms.assetid: 7d2109eb-f98a-4389-b43d-30f384aaa7d5
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Walkthrough: Manipulating Files by Using .NET Framework Methods (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questa procedura dettagliata viene illustrato come aprire e leggere un file mediante la classe <xref:System.IO.StreamReader>, verificare se altri utenti accedono al file, cercare una stringa nel corso della lettura di un file tramite un'istanza della classe <xref:System.IO.StreamReader> e scrivere in un file mediante la classe <xref:System.IO.StreamWriter>.  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
## Creazione dell'applicazione  
 Avviare [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs-md.md)] e iniziare il progetto creando un form che consenta agli utenti di scrivere nel file designato.  
  
#### Per creare il progetto  
  
1.  Scegliere **Nuovo progetto** dal menu **File**.  
  
2.  Nel riquadro **Nuovo progetto** scegliere **Applicazione Windows**.  
  
3.  Nella casella **Nome** digitare `MyDiary`, quindi scegliere **OK**.  
  
     [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs-md.md)] aggiungerà il progetto a **Esplora soluzioni** e verrà aperto **Progettazione Windows Form**.  
  
4.  Aggiungere al form i controlli riportati nella tabella che segue e impostare i valori corrispondenti per le relative proprietà.  
  
||||  
|-|-|-|  
|**Object**|**Proprietà**|**Valore**|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Text**|`Submit`<br /><br /> Submit Entry|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Text**|`Clear`<br /><br /> Clear Entry|  
|<xref:System.Windows.Forms.TextBox>|**Nome**<br /><br /> **Text**<br /><br /> **Multiline**|`Voce`<br /><br /> Please enter something.<br /><br /> `False`|  
  
## Scrittura nel file  
 Per aggiungere la possibilità di scrivere in un file tramite l'applicazione, utilizzare la classe <xref:System.IO.StreamWriter>.  <xref:System.IO.StreamWriter> è progettato per l'output di caratteri con una codifica particolare, mentre la classe <xref:System.IO.Stream> è progettata per l'input e l'output di byte.  Utilizzare <xref:System.IO.StreamWriter> per scrivere righe di informazioni in un file di testo standard.  Per ulteriori informazioni sulla classe <xref:System.IO.StreamWriter> vedere <xref:System.IO.StreamWriter>.  
  
#### Per aggiungere la funzionalità di scrittura  
  
1.  Scegliere **Codice** dal menu **Visualizza** per aprire l'editor di codice.  
  
2.  Poiché l'applicazione fa riferimento allo spazio dei nomi <xref:System.IO>, aggiungere le istruzioni riportate di seguito all'inizio del codice, prima della dichiarazione di classe per il form, che inizia con `Public Class Form1`.  
  
     [!code-vb[VbVbcnMyFileSystem#35](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_1.vb)]  
  
     Prima di scrivere nel file, è necessario creare un'istanza della classe <xref:System.IO.StreamWriter>.  
  
3.  Scegliere **Progettazione** dal menu **Visualizza** per ritornare a **Progettazione Windows Form**.  Fare doppio clic sul pulsante `Submit` per creare un gestore eventi <xref:System.Windows.Forms.Control.Click> per il pulsante, quindi aggiungere il codice seguente.  
  
     [!code-vb[VbVbcnMyFileSystem#36](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_2.vb)]  
  
> [!NOTE]
>  L'ambiente di sviluppo integrato \(IDE\) di Visual Studio ritorna all'editor di codice, con il punto di inserimento posizionato all'interno del gestore di eventi in cui è necessario aggiungere il codice.  
  
1.  Per scrivere nel file, utilizzare il metodo <xref:System.IO.StreamWriter.Write%2A> della classe <xref:System.IO.StreamWriter>.  Aggiungere il codice seguente subito dopo `Dim fw As StreamWriter`.  Non è necessario preoccuparsi della generazione di eccezioni nel caso in cui il file non venga trovato, poiché il file necessario verrà creato, se non esiste già.  
  
     [!code-vb[VbVbcnMyFileSystem#37](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_3.vb)]  
  
2.  Assicurarsi che l'utente non possa lasciare il campo vuoto aggiungendo il codice seguente subito dopo `Dim ReadString As String`.  
  
     [!code-vb[VbVbcnMyFileSystem#38](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_4.vb)]  
  
3.  Trattandosi di un diario, è probabile che l'utente desideri assegnare una data a ogni voce.  Inserire il codice seguente dopo `fw = New StreamWriter("C:\MyDiary.txt", True)` per impostare la variabile `Today` sulla data corrente.  
  
     [!code-vb[VbVbcnMyFileSystem#39](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_5.vb)]  
  
4.  Aggiungere infine il codice necessario per la rimozione di <xref:System.Windows.Forms.TextBox>.  Aggiungere il codice seguente all'evento <xref:System.Windows.Forms.Control.Click> del pulsante `Clear`.  
  
     [!code-vb[VbVbcnMyFileSystem#40](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_6.vb)]  
  
## Aggiunta delle funzionalità di visualizzazione al diario  
 In questa sezione viene illustrato come aggiungere una funzionalità che consente la visualizzazione dell'ultima voce aggiunta a `DisplayEntry` <xref:System.Windows.Forms.TextBox>.  È inoltre possibile aggiungere un controllo <xref:System.Windows.Forms.ComboBox> in cui vengono visualizzate le diverse voci e da cui gli utenti potranno selezionare la voce da visualizzare nel controllo `DisplayEntry`<xref:System.Windows.Forms.TextBox>.  Da `MyDiary.txt` viene creata un'istanza della classe <xref:System.IO.StreamReader>.  Al pari della classe <xref:System.IO.StreamWriter>, <xref:System.IO.StreamReader> deve essere utilizzata con file di testo.  
  
 Per questa sezione della procedura, aggiungere al form i controlli riportati nella tabella che segue e impostare i valori corrispondenti per le relative proprietà.  
  
|Controllo|Proprietà|Valori|  
|---------------|---------------|------------|  
|<xref:System.Windows.Forms.TextBox>|**Nome**<br /><br /> **Visible**<br /><br /> **Dimensione**<br /><br /> **Multiline**|`DisplayEntry`<br /><br /> `False`<br /><br /> `120,60`<br /><br /> `True`|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Text**|`Visualizzazione`<br /><br /> Visualizzazione|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Text**|`GetEntries`<br /><br /> Get Entries|  
|<xref:System.Windows.Forms.ComboBox>|**Nome**<br /><br /> **Text**<br /><br /> **Enabled**|`PickEntries`<br /><br /> Select an Entry<br /><br /> `False`|  
  
#### Per inserire la casella combinata  
  
1.  Il controllo <xref:System.Windows.Forms.ComboBox> `PickEntries` viene utilizzato per visualizzare le date di immissione di ogni voce da parte dell'utente, affinché sia possibile selezionare una voce con una data specifica.  Creare un gestore di eventi <xref:System.Windows.Forms.Control.Click> per il pulsante `GetEntries` e aggiungere il seguente codice.  
  
     [!code-vb[VbVbcnMyFileSystem#41](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_7.vb)]  
  
2.  Per eseguire il test del codice, premere F5 per compilare l'applicazione e fare clic su **Get Entries**.  Fare clic sulla freccia a discesa nel controllo <xref:System.Windows.Forms.ComboBox> per visualizzare le date delle voci.  
  
#### Per scegliere e visualizzare le singole voci  
  
1.  Creare un gestore di eventi <xref:System.Windows.Forms.Control.Click> per il pulsante `Display` e aggiungere il seguente codice.  
  
     [!code-vb[VbVbcnMyFileSystem#42](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_8.vb)]  
  
2.  Per eseguire il test del codice, premere F5 per compilare l'applicazione, quindi immettere una voce.  Fare clic su **Get Entries**, selezionare una voce dal controllo <xref:System.Windows.Forms.ComboBox>, quindi scegliere **Display**.  Nel controllo <xref:System.Windows.Forms.TextBox> `DisplayEntry` verrà visualizzato il contenuto della voce selezionata.  
  
## Abilitazione degli utenti a eliminare o modificare le voci  
 Infine, è possibile includere un'ulteriore funzionalità che consente agli utenti di eliminare o modificare una voce mediante i pulsanti `DeleteEntry` e `EditEntry`,  attivati solo quando viene visualizzata una voce.  
  
 Aggiungere al form i controlli riportati nella tabella che segue e impostare i valori corrispondenti per le relative proprietà.  
  
|Controllo|Proprietà|Valori|  
|---------------|---------------|------------|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Text**<br /><br /> **Enabled**|`DeleteEntry`<br /><br /> Delete Entry<br /><br /> `False`|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Text**<br /><br /> **Enabled**|`EditEntry`<br /><br /> Edit Entry<br /><br /> `False`|  
|<xref:System.Windows.Forms.Button>|**Nome**<br /><br /> **Text**<br /><br /> **Enabled**|`SubmitEdit`<br /><br /> Submit Edit<br /><br /> `False`|  
  
#### Per attivare l'eliminazione e la modifica delle voci  
  
1.  Aggiungere il codice seguente all'evento <xref:System.Windows.Forms.Control.Click> del pulsante `Display`, dopo `DisplayEntry.Text = ReadString`.  
  
     [!code-vb[VbVbcnMyFileSystem#43](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_9.vb)]  
  
2.  Creare un gestore di eventi <xref:System.Windows.Forms.Control.Click> per il pulsante `DeleteEntry` e aggiungere il seguente codice.  
  
     [!code-vb[VbVbcnMyFileSystem#44](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_10.vb)]  
  
3.  Quando una voce viene visualizzata dall'utente, il pulsante `EditEntry` viene attivato.  Aggiungere il codice riportato di seguito all'evento <xref:System.Windows.Forms.Control.Click> del pulsante `Display`, dopo `DisplayEntry.Text = ReadString`.  
  
     [!code-vb[VbVbcnMyFileSystem#45](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_11.vb)]  
  
4.  Creare un gestore di eventi <xref:System.Windows.Forms.Control.Click> per il pulsante `EditEntry` e aggiungere il seguente codice.  
  
     [!code-vb[VbVbcnMyFileSystem#46](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_12.vb)]  
  
5.  Creare un gestore di eventi <xref:System.Windows.Forms.Control.Click> per il pulsante `SubmitEdit` e aggiungere il seguente codice.  
  
     [!code-vb[VbVbcnMyFileSystem#47](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/walkthrough-manipulating_1_13.vb)]  
  
 Per eseguire il test del codice, premere F5 per compilare l'applicazione.  Fare clic su **Get Entries**, selezionare una voce, quindi scegliere **Display**.  La voce verrà visualizzata nel controllo <xref:System.Windows.Forms.TextBox> `DisplayEntry`.  Fare clic su **Edit Entry**.  La voce verrà visualizzata nel controllo <xref:System.Windows.Forms.TextBox> `Entry`.  Modificare la voce nel controllo <xref:System.Windows.Forms.TextBox> `Entry` e fare clic su **Submit Edit**.  Aprire il file `MyDiary.txt` per confermare la correzione,  quindi selezionare una voce e fare clic su **Delete Entry**.  Quando viene richiesta una conferma da <xref:System.Windows.Forms.MessageBox>, scegliere **OK**.  Chiudere l'applicazione e aprire `MyDiary.txt` per confermare l'eliminazione.  
  
## Vedere anche  
 <xref:System.IO.StreamReader>   
 <xref:System.IO.StreamWriter>   
 [Walkthroughs](../../../../visual-basic/walkthroughs.md)