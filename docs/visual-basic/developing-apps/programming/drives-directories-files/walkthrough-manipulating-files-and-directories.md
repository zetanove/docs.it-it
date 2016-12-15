---
title: "Walkthrough: Manipulating Files and Directories in Visual Basic | Microsoft Docs"
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
  - "files, reading text"
  - "reading files, text"
  - "I/O [Visual Basic], walkthroughs"
  - "text, writing to files"
  - "text, reading from files"
  - "reading text from files, walkthroughs"
  - "Visual Basic code, file access"
  - "files, writing text"
  - "I/O [Visual Basic], writing text to files"
  - "file access, walkthroughs"
  - "writing to files, walkthroughs"
  - "I/O [Visual Basic], reading text from files"
ms.assetid: cae77565-9f78-4e46-8e42-eb2f9f8e1ffd
caps.latest.revision: 49
caps.handback.revision: 49
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Walkthrough: Manipulating Files and Directories in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questa procedura dettagliata viene fornita un'introduzione ai principi fondamentali relativi a I\/O di file in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  Viene descritto come creare un'applicazione di piccole dimensioni che consente di elencare ed esaminare i file di testo in una directory.  Per ogni file di testo selezionato, l'applicazione fornisce i relativi attributi e la prima riga di contenuto.  È disponibile un'opzione per scrivere le informazioni in un file di log.  
  
 In questa procedura dettagliata vengono utilizzati membri di `My.Computer.FileSystem Object` disponibili in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.FileIO.FileSystem>.  Alla fine della procedura dettagliata viene fornito un esempio equivalente in cui vengono utilizzate le classi dello spazio dei nomi <xref:System.IO>.  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### Per creare il progetto  
  
1.  Scegliere **Nuovo progetto** dal menu **File**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto**.  
  
2.  Nel riquadro **Modelli installati** espandere **Visual Basic**, quindi fare clic su **Windows**.  Al centro del riquadro **Modelli** fare clic su **Applicazione Windows Form**.  
  
3.  Nella casella **Nome** digitare `FileExplorer` per impostare il nome del progetto, quindi fare clic su **OK**.  
  
     Il progetto verrà aggiunto a **Esplora soluzioni** in [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] e verrà avviato Progettazione Windows Form.  
  
4.  Aggiungere al form i controlli riportati nella tabella che segue e impostare i valori corrispondenti per le relative proprietà.  
  
    |Controllo|Proprietà|Valore|  
    |---------------|---------------|------------|  
    |**ListBox**|**Nome**|`filesListBox`|  
    |**Button**|**Nome**<br /><br /> **Text**|`browseButton`<br /><br /> Sfoglia|  
    |**Button**|**Nome**<br /><br /> **Text**|`examineButton`<br /><br /> Examine|  
    |**CheckBox**|**Nome**<br /><br /> **Text**|`saveCheckBox`<br /><br /> Save Results|  
    |**FolderBrowserDialog**|**Nome**|`FolderBrowserDialog1`|  
  
### Per selezionare una cartella ed elencare i file in una cartella  
  
1.  Creare un gestore eventi `Click` per `browseButton` facendo doppio clic sul controllo nel form.  Verrà aperto l'editor di codice.  
  
2.  Aggiungere il codice seguente al gestore eventi `Click`.  
  
     [!code-vb[VbVbcnMyFileSystem#103](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_1.vb)]  
  
     La chiamata di `FolderBrowserDialog1.ShowDialog` consente di visualizzare la finestra di dialogo **Sfoglia per cartelle**.  Una volta che si è fatto clic su **OK**, la proprietà <xref:System.Windows.Forms.FolderBrowserDialog.SelectedPath%2A> viene inviata come argomento al metodo `ListFiles` che viene aggiunto nel passaggio successivo.  
  
3.  Aggiungere il seguente metodo `ListFiles`.  
  
     [!code-vb[VbVbcnMyFileSystem#104](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_2.vb)]  
  
     Questo codice dapprima consente di cancellare **ListBox**.  
  
     Il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A> consente quindi di recuperare una raccolta di stringhe, una per ogni file nella directory.  Il metodo `GetFiles` accetta un argomento del criterio di ricerca per recuperare i file che corrispondono a un modello particolare.  Nell'esempio riportato di seguito vengono restituiti solo i file con estensione txt.  
  
     Le stringhe restituite dal metodo `GetFiles` vengono quindi aggiunte a **ListBox**.  
  
4.  Eseguire l'applicazione.  Scegliere il pulsante **Browse**.  Nella finestra di dialogo **Sfoglia per cartelle** cercare una cartella contenente i file txt, quindi selezionare la cartella e fare clic su **OK**.  
  
     Il controllo `ListBox` contiene un elenco di file txt della cartella selezionata.  
  
5.  Arrestare l'esecuzione dell'applicazione.  
  
### Per ottenere gli attributi di un file e il contenuto da un file di testo  
  
1.  Creare un gestore eventi `Click` per `examineButton` facendo doppio clic sul controllo nel form.  
  
2.  Aggiungere il codice seguente al gestore eventi `Click`.  
  
     [!code-vb[VbVbcnMyFileSystem#105](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_3.vb)]  
  
     Il codice verifica che un elemento venga selezionato nel controllo `ListBox`.  Ottiene quindi la voce del percorso del file dal controllo `ListBox`.  Il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.FileExists%2A> viene utilizzato per controllare se il file esiste ancora.  
  
     Il percorso del file viene inviato come argomento al metodo `GetTextForOutput` che viene aggiunto nel passaggio successivo.  Questo metodo restituisce una stringa contenente le informazioni sul file.  Le informazioni sul file vengono visualizzate in **MessageBox**.  
  
3.  Aggiungere il seguente metodo `GetTextForOutput`.  
  
     [!code-vb[VbVbcnMyFileSystem#107](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_4.vb)]  
  
     Il codice utilizza il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFileInfo%2A> per ottenere i parametri del file.  I parametri del file vengono aggiunti a <xref:System.Text.StringBuilder>.  
  
     Il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileReader%2A> legge il contenuto del file in un <xref:System.IO.StreamReader>.  La prima riga del contenuto viene ottenuta da `StreamReader` e viene aggiunta a `StringBuilder`.  
  
4.  Eseguire l'applicazione.  Fare clic su **Sfoglia** e cercare una cartella contenente i file txt.  Scegliere **OK**.  
  
     Selezionare un file nel controllo `ListBox`, quindi fare clic su **Esamina**.  `MessageBox` consente di visualizzare le informazioni sul file.  
  
5.  Arrestare l'esecuzione dell'applicazione.  
  
### Per aggiungere una voce di log  
  
1.  Aggiungere il seguente codice alla fine del gestore eventi `examineButton_Click`.  
  
     [!code-vb[VbVbcnMyFileSystem#106](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_5.vb)]  
  
     Il codice imposta il percorso del file di log per inserire il file di log nella stessa directory del file selezionato.  Il testo della voce di log viene impostato sulla data e ora correnti seguiti dalle informazioni sul file.  
  
     Il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>, con l'argomento impostato su `append` a `True` viene utilizzato per creare la voce di log.  
  
2.  Eseguire l'applicazione.  Cercare un file di testo, selezionarlo nel controllo `ListBox`, selezionare la casella di controllo **Salva risultati**, quindi fare clic su **Esamina**.  Verificare che la voce di log venga scritta nel file `log.txt`.  
  
3.  Arrestare l'esecuzione dell'applicazione.  
  
### Per utilizzare la directory corrente  
  
1.  Creare un gestore di eventi per `Form1_Load` facendo doppio clic sul form.  
  
2.  Aggiungere il codice seguente al gestore eventi.  
  
     [!code-vb[VbVbcnMyFileSystem#102](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_6.vb)]  
  
     Questo codice consente di impostare la directory predefinita del visualizzatore cartelle sulla directory corrente.  
  
3.  Eseguire l'applicazione.  Quando si fa clic su **Sfoglia** per la prima volta, viene visualizzata la finestra di dialogo **Sfoglia per cartelle** con la directory corrente.  
  
4.  Arrestare l'esecuzione dell'applicazione.  
  
### Per abilitare in modo selettivo i controlli  
  
1.  Aggiungere il seguente metodo `SetEnabled`.  
  
     [!code-vb[VbVbcnMyFileSystem#108](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_7.vb)]  
  
     Il metodo `SetEnabled` abilita o disabilita i controlli a seconda se un elemento è selezionato in `ListBox`.  
  
2.  Creare un gestore eventi `SelectedIndexChanged` per `filesListBox` facendo doppio clic sul controllo `ListBox` nel form.  
  
3.  Aggiungere una chiamata a `SetEnabled` nel nuovo gestore eventi `filesListBox_SelectedIndexChanged`.  
  
4.  Aggiungere una chiamata a `SetEnabled` alla fine del gestore eventi `browseButton_Click`.  
  
5.  Aggiungere una chiamata a `SetEnabled` alla fine del gestore eventi `Form1_Load`.  
  
6.  Eseguire l'applicazione.  La casella di controllo **Salva risultati** e il pulsante **Esamina** sono disattivati se un elemento non è selezionato in `ListBox`.  
  
## Esempio completo di utilizzo di My.Computer.FileSystem  
 Di seguito è riportato un esempio completo.  
  
 [!code-vb[VbVbcnMyFileSystem#101](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_8.vb)]  
  
## Esempio completo di utilizzo di System.IO  
 Nell'esempio equivalente seguente, anziché oggetti `My.Computer.FileSystem`. vengono utilizzate le classi dallo spazio dei nomi <xref:System.IO>.  
  
 [!code-vb[VbVbcnMyFileSystem#111](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_9.vb)]  
  
## Vedere anche  
 <xref:System.IO>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CurrentDirectory%2A>   
 [Walkthrough: Manipulating Files by Using .NET Framework Methods](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-by-using-net-framework-methods.md)