---
title: 'Procedura dettagliata: Modifica di file e directory in Visual Basic | Microsoft Docs'
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
- files, reading text
- reading files, text
- I/O [Visual Basic], walkthroughs
- text, writing to files
- text, reading from files
- reading text from files, walkthroughs
- Visual Basic code, file access
- files, writing text
- I/O [Visual Basic], writing text to files
- file access, walkthroughs
- writing to files, walkthroughs
- I/O [Visual Basic], reading text from files
ms.assetid: cae77565-9f78-4e46-8e42-eb2f9f8e1ffd
caps.latest.revision: 49
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 89137b3c927a7ac8ed126f2be3695c4aa72a85fb
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-manipulating-files-and-directories-in-visual-basic"></a>Procedura dettagliata: modifica di file e directory in Visual Basic
Questa procedura dettagliata offre un'introduzione ai principi di base degli elementi I/O di file in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. Descrive come creare una piccola applicazione in cui vengono elencati ed esaminati i file di testo di una directory. Per ogni file di testo selezionato, l'applicazione specifica gli attributi di file e la prima riga del contenuto. È disponibile un'opzione per la scrittura di informazioni in un file di log.  
  
 In questa procedura dettagliata vengono usati i membri di `My.Computer.FileSystem Object`, che sono disponibili in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. Vedere <xref:Microsoft.VisualBasic.FileIO.FileSystem> per altre informazioni. Al termine della procedura dettagliata è riportato un esempio equivalente che usa le classi dello spazio dei nomi <xref:System.IO>.  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-create-the-project"></a>Per creare il progetto  
  
1.  Scegliere **Nuovo progetto** dal menu **File**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
2.  Nel riquadro **Modelli installati** espandere **Visual Basic**, quindi fare clic su **Windows**. Nel riquadro **Modelli** al centro scegliere **Windows Forms Application**.  
  
3.  Nella casella **Nome** digitare `FileExplorer` per impostare il nome del progetto e quindi fare clic su **OK**.  
  
     [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] aggiunge il progetto a **Esplora soluzioni** e viene aperto Progettazione Windows Form.  
  
4.  Aggiungere i controlli della tabella seguente al form e impostare i valori corrispondenti per le relative proprietà.  
  
    |Controllo|Proprietà|Valore|  
    |-------------|--------------|-----------|  
    |**ListBox**|**Nome**|`filesListBox`|  
    |**Pulsante**|**Nome**<br /><br /> **Testo**|`browseButton`<br /><br /> **Sfoglia**|  
    |**Pulsante**|**Nome**<br /><br /> **Testo**|`examineButton`<br /><br /> **Esaminare**|  
    |**CheckBox**|**Nome**<br /><br /> **Testo**|`saveCheckBox`<br /><br /> **Salva risultati**|  
    |**FolderBrowserDialog**|**Nome**|`FolderBrowserDialog1`|  
  
### <a name="to-select-a-folder-and-list-files-in-a-folder"></a>Per selezionare una cartella ed elencare file di una cartella  
  
1.  Creare un gestore eventi `Click` per `browseButton` facendo doppio clic sul controllo nel form. Verrà aperto l'Editor di codice.  
  
2.  Aggiungere il codice seguente al gestore eventi `Click`.  
  
     [!code-vb[VbVbcnMyFileSystem#103](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_1.vb)]  
  
     La chiamata a `FolderBrowserDialog1.ShowDialog` apre la finestra di dialogo **Sfoglia per cartelle**. Dopo che l'utente ha fatto clic su **OK** la proprietà <xref:System.Windows.Forms.FolderBrowserDialog.SelectedPath%2A> viene inviata come argomento al metodo `ListFiles`, che viene aggiunto nel passaggio successivo.  
  
3.  Aggiungere il seguente metodo `ListFiles`.  
  
     [!code-vb[VbVbcnMyFileSystem#104](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_2.vb)]  
  
     Questo codice per prima cosa cancella il contenuto dell'oggetto **ListBox**.  
  
     Il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A> recupera quindi una raccolta di stringhe, una per ogni file nella directory. Il metodo `GetFiles` accetta un argomento dei criteri di ricerca per recuperare i file che corrispondono a un criterio specifico. In questo esempio vengono restituiti solo i file con estensione TXT.  
  
     Le stringhe restituite dal metodo `GetFiles` vengono quindi aggiunte all'oggetto **ListBox**.  
  
4.  Eseguire l'applicazione. Fare clic sul pulsante **Sfoglia**. Nella finestra di dialogo **Sfoglia per cartelle** passare a una cartella che contiene file TXT, quindi selezionare la cartella e fare clic su **OK**.  
  
     L'oggetto `ListBox` contiene un elenco di file TXT presenti nella cartella selezionata.  
  
5.  Arrestare l'esecuzione dell'applicazione.  
  
### <a name="to-obtain-attributes-of-a-file-and-content-from-a-text-file"></a>Per ottenere gli attributi di un file e il contenuto di un file di testo  
  
1.  Creare un gestore eventi `Click` per `examineButton` facendo doppio clic sul controllo nel form.  
  
2.  Aggiungere il codice seguente al gestore eventi `Click`.  
  
     [!code-vb[VbVbcnMyFileSystem#105](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_3.vb)]  
  
     Il codice verifica se un elemento è selezionato nell'oggetto `ListBox`. Ottiene quindi la voce del percorso del file da `ListBox`. Il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.FileExists%2A> viene usato per verificare se il file esiste ancora.  
  
     Il percorso del file viene inviato come argomento al metodo `GetTextForOutput`, che viene aggiunto nel passaggio successivo. Questo metodo restituisce una stringa che contiene informazioni sul file. Le informazioni sul file appaiono in un oggetto **MessageBox**.  
  
3.  Aggiungere il seguente metodo `GetTextForOutput`.  
  
     [!code-vb[VbVbcnMyFileSystem#107](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_4.vb)]  
  
     Il codice usa il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFileInfo%2A> per ottenere i parametri del file. I parametri del file vengono aggiunti a un oggetto <xref:System.Text.StringBuilder>.  
  
     Il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileReader%2A> legge il contenuto del file in un oggetto <xref:System.IO.StreamReader>. La prima riga del contenuto viene ottenuta da `StreamReader` e viene aggiunta a `StringBuilder`.  
  
4.  Eseguire l'applicazione. Fare clic su **Sfoglia** e passare a una cartella che contiene file TXT. Fare clic su **OK**.  
  
     Selezionare un file in `ListBox`, quindi fare clic su **Esaminare**. L'oggetto `MessageBox` contiene le informazioni sul file.  
  
5.  Arrestare l'esecuzione dell'applicazione.  
  
### <a name="to-add-a-log-entry"></a>Per aggiungere una voce di log  
  
1.  Aggiungere il codice seguente alla fine del gestore eventi `examineButton_Click` .  
  
     [!code-vb[VbVbcnMyFileSystem#106](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_5.vb)]  
  
     Il codice imposta il percorso del file di log in modo da inserire il file di log nella stessa directory del file selezionato. Il testo della voce di log è impostato su data e ora correnti seguite dalle informazioni sul file.  
  
     Il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>, con l'argomento `append` impostato su `True`, viene usato per creare la voce di log.  
  
2.  Eseguire l'applicazione. Individuare un file di testo, selezionarlo in `ListBox`, selezionare la casella di controllo **Salva risultati** e quindi fare clic su **Esaminare**. Verificare che la voce di log sia scritta nel file `log.txt`.  
  
3.  Arrestare l'esecuzione dell'applicazione.  
  
### <a name="to-use-the-current-directory"></a>Per usare la directory corrente  
  
1.  Creare un gestore eventi per `Form1_Load` facendo doppio clic sul form.  
  
2.  Aggiungere il codice seguente al gestore eventi.  
  
     [!code-vb[VbVbcnMyFileSystem#102](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_6.vb)]  
  
     Questo codice imposta la directory predefinita del browser delle cartelle sulla directory corrente.  
  
3.  Eseguire l'applicazione. Quando si fa clic su **Sfoglia** per la prima volta la finestra di dialogo **Sfoglia per cartelle** si apre visualizzando la directory corrente.  
  
4.  Arrestare l'esecuzione dell'applicazione.  
  
### <a name="to-selectively-enable-controls"></a>Per abilitare selettivamente i controlli  
  
1.  Aggiungere il seguente metodo `SetEnabled`.  
  
     [!code-vb[VbVbcnMyFileSystem#108](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_7.vb)]  
  
     Il metodo `SetEnabled` abilita o disabilita i controlli a seconda se è selezionato un elemento nell'oggetto `ListBox`.  
  
2.  Creare un gestore eventi `SelectedIndexChanged` per `filesListBox` facendo doppio clic sul controllo `ListBox` nel form.  
  
3.  Aggiungere una chiamata a `SetEnabled` nel nuovo gestore eventi `filesListBox_SelectedIndexChanged`.  
  
4.  Aggiungere una chiamata a `SetEnabled` alla fine del gestore eventi `browseButton_Click`.  
  
5.  Aggiungere una chiamata a `SetEnabled` alla fine del gestore eventi `Form1_Load`.  
  
6.  Eseguire l'applicazione. La casella di controllo **Salva risultati** e il pulsante **Esaminare** sono disabilitati se non è selezionato un elemento in `ListBox`.  
  
## <a name="full-example-using-mycomputerfilesystem"></a>Esempio completo di uso di My.Computer.FileSystem  
 Di seguito è riportato l'esempio completo.  
  
 [!code-vb[VbVbcnMyFileSystem#101](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_8.vb)]  
  
## <a name="full-example-using-systemio"></a>Esempio completo usando System.IO  
 Nel seguente esempio equivalente vengono usate le classi dello spazio dei nomi <xref:System.IO> anziché gli oggetti `My.Computer.FileSystem`.  
  
 [!code-vb[VbVbcnMyFileSystem#111](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-and-directories_9.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IO>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CurrentDirectory%2A>   
 [Procedura dettagliata: Modifica di file mediante i metodi .NET Framework](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-by-using-net-framework-methods.md)

