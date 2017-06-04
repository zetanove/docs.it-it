---
title: "Procedura dettagliata: dimostrazione dell&#39;ereditariet&#224; visiva | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "ereditarietà di form, procedure dettagliate"
  - "ereditarietà, procedure dettagliate"
  - "ereditarietà visiva"
  - "procedure dettagliate [Windows Form], ereditarietà visiva"
  - "Windows Form, ereditarietà"
ms.assetid: 01966086-3142-450e-8210-3fd4cb33f591
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# Procedura dettagliata: dimostrazione dell&#39;ereditariet&#224; visiva
L'ereditarietà visiva consente di visualizzare i controlli nel form di base e di aggiungere nuovi controlli.  In questa procedura dettagliata verrà creato un form di base che verrà compilato in una libreria di classi.  La libreria di classi verrà importata in un altro progetto e verrà creato un nuovo form che eredita dal form di base.  Durante questa procedura dettagliata, si apprenderà come:  
  
-   Creare un progetto di libreria di classi contenente un form di base.  
  
-   Aggiungere un pulsante con proprietà che le classi derivate del form di base possono modificare.  
  
-   Aggiungere un pulsante che non può essere modificato dagli eredi del form di base.  
  
-   Creare un progetto contenente un form che eredita da `BaseForm`.  
  
 Infine, questa procedura dettagliata illustrerà la differenza tra controlli privati e protetti in un form ereditato.  
  
> [!NOTE]
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/Esporta impostazioni** dal menu **Strumenti**.  Per altre informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
> [!CAUTION]
>  Non tutti i controlli supportano l'ereditarietà visiva da un form di base.  I controlli seguenti non supportano lo scenario descritto in questa procedura dettagliata:  
>   
>  <xref:System.Windows.Forms.WebBrowser>  
>   
>  <xref:System.Windows.Forms.ToolStrip>  
>   
>  <xref:System.Windows.Forms.ToolStripPanel>  
>   
>  <xref:System.Windows.Forms.TableLayoutPanel>  
>   
>  <xref:System.Windows.Forms.FlowLayoutPanel>  
>   
>  <xref:System.Windows.Forms.DataGridView>  
>   
>  Questi controlli nel form ereditato sono sempre di sola lettura, indipendentemente dai modificatori usati \(`private`, `protected` o `public`\).  
  
## Passaggi dello scenario  
 Il primo passaggio consiste nella creazione del form di base.  
  
#### Per creare un progetto di libreria di classi contenente un form di base  
  
1.  Scegliere **Nuovo** dal menu **File**, quindi selezionare **Progetto** per aprire la finestra di dialogo **Nuovo progetto**.  
  
2.  Creare una soluzione Windows Forms Application denominata `BaseFormLibrary`.  
  
3.  Per creare una libreria di classi anziché una soluzione Windows Forms Application standard, in **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto denominato **BaseFormLibrary** e quindi scegliere **Proprietà**.  
  
4.  Nelle proprietà del progetto modificare **Tipo di output** da **Applicazione Windows** a **Libreria di classi**.  
  
5.  Scegliere **Salva tutto** dal menu **File** per salvare il progetto e i file nella posizione predefinita.  
  
 Le due procedure seguenti consentono di aggiungere pulsanti al form di base.  Per dimostrare l'ereditarietà visiva, si assegneranno ai pulsanti livelli di accesso diversi impostando le relative proprietà `Modifiers`.  
  
#### Per aggiungere un pulsante che gli eredi del form di base possono modificare  
  
1.  Aprire **Form1** nella finestra di progettazione.  
  
2.  Nella scheda **Tutti i Windows Form** della **Casella degli strumenti** fare doppio clic su **Pulsante** per aggiungere un pulsante al form.  Usare il mouse per posizionare e ridimensionare il pulsante.  
  
3.  Nella finestra Proprietà impostare le seguenti proprietà del pulsante:  
  
    -   Impostare la proprietà **Text** su **Say Hello**.  
  
    -   Impostare la proprietà **\(Name\)** su **btnProtected**.  
  
    -   Impostare la proprietà **Modifiers** su **Protected**.  In questo modo, i form che ereditano da **Form1** possono modificare le proprietà di **btnProtected**.  
  
4.  Fare doppio clic sul pulsante **Say Hello** per aggiungere un gestore dell'evento **Click**.  
  
5.  Aggiungere la riga di codice seguente al gestore eventi:  
  
    ```vb  
    MessageBox.Show("Hello, World!")  
    ```  
  
    ```csharp  
    MessageBox.Show("Hello, World!");  
    ```  
  
#### Per aggiungere un pulsante che non può essere modificato dagli eredi del form di base  
  
1.  Passare alla visualizzazione Progettazione facendo clic sulla scheda **Form1.vb \[Progettazione\], Form1.cs \[Progettazione\] o Form1.jsl \[Progettazione\]** sopra l'editor di codice o premendo F7.  
  
2.  Aggiungere un secondo pulsante e impostarne le proprietà come indicato di seguito:  
  
    -   Impostare la proprietà **Text** su **Say Goodbye**.  
  
    -   Impostare la proprietà **\(Name\)** su **btnPrivate**.  
  
    -   Impostare la proprietà **Modifiers** su **Private**.  In questo modo, i form che ereditano da **Form1** non possono modificare le proprietà di **btnPrivate**.  
  
3.  Fare doppio clic sul pulsante **Say Goodbye** per aggiungere un gestore dell'evento **Click**.  Inserire la riga di codice seguente nella routine evento:  
  
    ```vb  
    MessageBox.Show("Goodbye!")  
    ```  
  
    ```csharp  
    MessageBox.Show("Goodbye!");  
    ```  
  
4.  Scegliere **Compila BaseFormLibrary** dal menu **Compila**  per compilare la libreria di classi.  
  
     Dopo aver compilato la libreria, è possibile creare un nuovo progetto che eredita dal form appena creato.  
  
#### Per creare un progetto contenente un form che eredita dal form di base  
  
1.  Scegliere **Aggiungi** dal menu **File**, quindi selezionare **Nuovo progetto** per aprire la finestra di dialogo **Aggiungi nuovo progetto**.  
  
2.  Creare una soluzione Windows Forms Application denominata `InheritanceTest`.  
  
#### Per aggiungere un form ereditato  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **InheritanceTest**, scegliere **Aggiungi** e quindi **Nuovo elemento**.  
  
2.  Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare la categoria **Windows Form** \(se è disponibile un elenco di categorie\) e quindi selezionare il modello **Form ereditato**.  
  
3.  Lasciare il nome predefinito `Form2` e fare clic su **Aggiungi**.  
  
4.  Nella finestra di dialogo **Selezione ereditarietà** selezionare **Form1** dal progetto **BaseFormLibrary** come form da cui ereditare e fare clic su **OK**.  
  
     Verrà creato un form nel progetto **InheritanceTest** derivato dal form in **BaseFormLibrary**.  
  
5.  Aprire il form ereditato \(**Form2**\) nella finestra di progettazione facendo doppio clic su di esso, se non è già aperto.  
  
     Nella finestra di progettazione, nell'angolo superiore dei pulsanti ereditati è visualizzato un simbolo \(![Schermata VisualBasicInheritanceSymbol](../../../../docs/framework/winforms/advanced/media/vbinheritanceglyph.png "vbInheritanceGlyph")\) che indica che sono ereditati.  
  
6.  Selezionare il pulsante **Say Hello** e osservare i quadratini di ridimensionamento.  Poiché questo pulsante è protetto, gli eredi possono spostarlo, ridimensionarlo, modificarne la didascalia e apportare altre modifiche.  
  
7.  Selezionare il pulsante privato **Say Goodbye** e osservare che non dispone di quadratini di ridimensionamento.  In aggiunta, nella finestra proprietà **Proprietà** le proprietà di questo pulsante sono in grigio, per indicare che non possono essere modificate.  
  
8.  Se si usa [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)]:  
  
    1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Form1** nel progetto **InheritanceTest** e quindi scegliere **Elimina**.  Nella finestra di messaggio visualizzata fare clic su **OK** per confermare l'eliminazione.  
  
    2.  Aprire il file Program.cs e modificare la riga `Application.Run(new Form1());` in `Application.Run(new Form2());`.  
  
9. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **InheritanceTest** e scegliere **Imposta come progetto di avvio**.  
  
10. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **InheritanceTest** e scegliere **Proprietà**.  
  
11. Nelle pagine delle proprietà di **InheritanceTest** impostare per **Oggetto di avvio** il form ereditato \(**Form2**\).  
  
12. Premere F5 per eseguire l'applicazione e osservare il comportamento del form ereditato.  
  
## Passaggi successivi  
 L'ereditarietà per i controlli utente funziona in modo analogo.  Aprire un nuovo progetto di libreria di classi e aggiungere un controllo utente.  Inserire controlli costitutivi e compilare il progetto.  Aprire un altro progetto di libreria di classi e aggiungere un riferimento alla libreria di classi compilata.  Provare inoltre ad aggiungere al progetto un controllo ereditato \(tramite la finestra di dialogo per l'aggiunta di nuovielementi\) e a usare **Selezione ereditarietà**.  Aggiungere un controllo utente e modificare l'istruzione `Inherits` \(`:` in [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)]\).  Per altre informazioni, vedere [Procedura: ereditare Windows Form](../../../../docs/framework/winforms/advanced/how-to-inherit-windows-forms.md).  
  
## Vedere anche  
 [Procedura: ereditare Windows Form](../../../../docs/framework/winforms/advanced/how-to-inherit-windows-forms.md)   
 [Ereditarietà visiva di Windows Form](../../../../docs/framework/winforms/advanced/windows-forms-visual-inheritance.md)   
 [Windows Form](../../../../docs/framework/winforms/index.md)