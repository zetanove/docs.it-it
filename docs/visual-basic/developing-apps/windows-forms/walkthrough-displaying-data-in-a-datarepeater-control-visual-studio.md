---
title: 'Procedura dettagliata: Visualizzazione dei dati in un controllo DataRepeater (Visual Studio) | Documenti di Microsoft'
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- DataRepeater, walkthrough
ms.assetid: 65dcdb95-6c3e-47cc-987d-190000f71653
caps.latest.revision: 12
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 09f15c94c3d5a3387935c8d3f4758c0ecfd7cfcd
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-displaying-data-in-a-datarepeater-control-visual-studio"></a>Procedura dettagliata: visualizzazione di dati in un controllo DataRepeater (Visual Studio)
Questa procedura dettagliata fornisce uno scenario di inizio alla fine di base per visualizzare i dati associati in un <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="prerequisite"></a>Prerequisito  
 Per questa procedura dettagliata è richiesto il database di esempio Northwind.  
  
 Se questo database non è presente nel computer di sviluppo, è possibile scaricarlo dall' [Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=98088). Per istruzioni, vedere [download dei database di esempio](https://msdn.microsoft.com/library/bb399411).  
  
## <a name="overview"></a>Panoramica  
 La prima parte di questa procedura dettagliata è costituita da quattro attività principali:  
  
-   Creazione di una soluzione.  
  
-   Aggiunta di un <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
-   Aggiunta di un'origine dati.  
  
-   Aggiunta di controlli con associazione a dati.  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## <a name="creating-a-datarepeater-solution"></a>Creazione di una soluzione DataRepeater  
 Il primo passaggio consiste nel creare un progetto e una soluzione.  
  
#### <a name="to-create-a-datarepeater-solution"></a>Per creare una soluzione DataRepeater  
  
1.  Scegliere **Nuovo progetto** dal menu **File**di Visual Studio.  
  
2.  Nel riquadro **Tipi progetto** della finestra di dialogo **Nuovo progetto** espandere **Visual Basic**, quindi fare clic su **Windows**  
  
3.  Nel riquadro **Modelli** scegliere **Applicazione Windows Form**.  
  
4.  Nella casella **Nome** digitare `DataRepeaterApp`.  
  
5.  Fare clic su **OK**.  
  
     Verrà aperto Progettazione Windows Form.  
  
6.  Selezionare il form in Progettazione Windows Form. Nella finestra **Proprietà** impostare la proprietà **Size** su `800, 700`.  
  
## <a name="adding-a-datarepeater-control"></a>Aggiunta di un controllo DataRepeater  
 In questo passaggio, aggiungere un <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>al form.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-add-a-datarepeater-control"></a>Per aggiungere un controllo DataRepeater  
  
1.  Scegliere **Casella degli strumenti** dal menu **Visualizza**.  
  
     Verrà aperta la **Casella degli strumenti** .  
  
2.  Selezionare la scheda **Visual Basic PowerPacks** .  
  
3.  Trascinare un <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo **Form1**.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
4.  Nella finestra Proprietà impostare la proprietà **Location** su `0, 25`.  
  
5.  Impostare la proprietà **Size** su `460, 600`.  
  
## <a name="adding-a-data-source"></a>Aggiunta di un'origine dati  
 In questo passaggio si aggiunge un'origine dati per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-add-a-data-source"></a>Per aggiungere un'origine dati  
  
1.  Scegliere **Mostra origini dati** dal menu **Dati**.  
  
2.  Nella finestra **Origini dati** fare clic su **Aggiungi nuova origine dati**.  
  
3.  Selezionare **Database** nella pagina **Scegliere un tipo di origine dati** e scegliere **Avanti**.  
  
4.  Nella pagina **Seleziona connessione dati** , eseguire una delle operazioni seguenti:  
  
    -   Se disponibile nell'elenco a discesa, scegliere la connessione dati al database di esempio Northwind.  
  
         -oppure-  
  
    -   Scegliere **Nuova connessione** per configurare una nuova connessione dati. Per ulteriori informazioni, vedere [procedura: creare connessioni a database di SQL Server](http://msdn.microsoft.com/en-us/360c340d-e5a6-4a7e-a569-e95d500be43d).  
  
5.  Se il database richiede una password, selezionare l'opzione che consente di includere dati riservati, quindi fare clic su **Avanti**.  
  
    > [!NOTE]
    >  Se viene visualizzata una finestra di dialogo, scegliere **Sì** per salvare il file nel progetto.  
  
6.  Nella pagina **Salva stringa di connessione nel file di configurazione dell'applicazione** fare clic su **Avanti** .  
  
7.  Espandere il nodo **Tabelle** nella pagina **Seleziona oggetti di database** .  
  
8.  Selezionare le caselle di controllo accanto alle tabelle **Customers** e **Orders** , quindi fare clic su **Fine**.  
  
     L'oggetto**NorthwindDataSet** viene aggiunto al progetto e le tabelle **Customers** e **Orders** vengono visualizzate nella finestra **Origini dati** .  
  
## <a name="adding-data-bound-controls"></a>Aggiunta di controlli con associazione a dati  
 In questo passaggio, aggiungere controlli associati a dati <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-add-data-bound-controls"></a>Per aggiungere controlli con associazione a dati  
  
1.  Nella finestra **Origini dati** selezionare il nodo di livello principale della tabella **Customers** .  
  
2.  Modificare il tipo di rilascio della tabella in **Dettagli** selezionando **Dettagli** dall'elenco a discesa nel nodo della tabella.  
  
3.  Selezionare il **clienti** tabella nodo e trascinarlo nell'area del modello di elemento (l'area superiore) del <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
     Oggetto <xref:System.Windows.Forms.BindingNavigator>controllo viene aggiunto al form e **NorthwindDataSet**, **CustomersBindingSource**, **CustomersTableAdapter**, **TableAdapterManager**, e **CustomersBindingNavigator** componenti vengono aggiunti alla barra dei componenti.</xref:System.Windows.Forms.BindingNavigator>  
  
4.  Selezionare tutti i campi e le etichette corrispondenti e posizionarli vicino al bordo sinistro dell'area modello dell'elemento.  
  
5.  Selezionare gli ultimi cinque campi (**Region**, **Postal Code**, **Country**, **Phone**e **Fax**) e le etichette corrispondenti e spostarli in alto e a destra dei primi sei campi.  
  
6.  Selezionare il modello di elemento (l'area superiore del controllo).  
  
7.  Nella finestra Proprietà impostare la proprietà **Size** su `427, 170`.  
  
 A questo punto si dispone di un'applicazione funzionante che visualizzerà un elenco ripetuto di clienti. Premere F5 per eseguire l'applicazione, modificare i dati e aggiungere o eliminare i record cliente.  
  
 Nei passaggi facoltativi, si apprenderà come personalizzare il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="next-steps-optional"></a>Passaggi successivi (facoltativi)  
 Questa parte della procedura dettagliata è costituita da quattro attività facoltative:  
  
-   Modifica dell'aspetto di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
-   Impedire agli utenti di aggiungere o eliminare record.  
  
-   Aggiunta di funzionalità di ricerca per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
-   Aggiunta di una tabella master e di dettaglio per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="changing-the-appearance-of-the-datarepeater-control"></a>Modifica dell'aspetto di un controllo DataRepeater  
 In questo passaggio facoltativo, si modifica il `BackColor` del <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo in fase di progettazione.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> È anche possibile aggiungere codice per visualizzare le righe in colori alternati e modificare il `ForeColor` di un'etichetta in modo condizionale.  
  
#### <a name="to-change-the-appearance-of-the-control"></a>Per modificare l'aspetto del controllo  
  
1.  In Progettazione Windows Form, selezionare l'area principale (inferiore) del <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
2.  Nella finestra Proprietà impostare la proprietà `BackColor` su bianco.  
  
3.  Fare doppio clic su di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>per aprire l'Editor di codice.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
4.  Nell'elenco a discesa Event dell'editor di codice, selezionare **DrawItem**.  
  
5.  Nel <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>gestore dell'evento, aggiungere il codice seguente per alternare il `BackColor`:</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>  
  
     [!code-cs[N.&1; VbPowerPacksDataRepeaterWalkthrough](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_1.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough n.&1;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_1.vb)]  
  
6.  Nel <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>gestore dell'evento, aggiungere il codice seguente per modificare il `ForeColor` di un'etichetta in base a una condizione:</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>  
  
     [!code-cs[N.&2; VbPowerPacksDataRepeaterWalkthrough](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_2.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough n.&2;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_2.vb)]  
  
7.  Premere F5 per eseguire l'applicazione e visualizzare la personalizzazione.  
  
## <a name="preventing-users-from-adding-or-deleting-records"></a>Impedire agli utenti di aggiungere o eliminare record  
 In questo passaggio facoltativo, aggiungere il codice che impedisce agli utenti di aggiungere o eliminare i record di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-prevent-users-from-adding-and-deleting-records"></a>Per impedire agli utenti di aggiungere o eliminare record  
  
1.  In Progettazione Windows Form, fare doppio clic sul form per aprire l'editor di codice.  
  
2.  Aggiungere il codice seguente all'evento `Form_Load` :  
  
     [!code-cs[N.&3; VbPowerPacksDataRepeaterWalkthrough](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_3.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough n.&3;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_3.vb)]  
  
3.  Nell'elenco a discesa Class Name, fare clic su **BindingNavigatorDeleteItem**. Nell'elenco a discesa Method Name, fare clic su **EnabledChanged**.  
  
4.  Aggiungere il codice seguente al gestore eventi `BindingNavigatorDeleteItem_EnabledChanged` :  
  
     [!code-cs[N.&4; VbPowerPacksDataRepeaterWalkthrough](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_4.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough n.&4;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_4.vb)]  
  
    > [!NOTE]
    >  Questa operazione è necessaria perché il <xref:System.Windows.Forms.BindingSource>consentirà di **DeleteItem** pulsante ogni volta che viene modificato il record corrente.</xref:System.Windows.Forms.BindingSource>  
  
5.  Premere F5 per eseguire l'applicazione. Notare che il pulsante **DeleteItem** pulsante è disabilitato e non è possibile eliminare elementi premendo il tasto CANC.  
  
## <a name="adding-search-capability-to-the-datarepeater-control"></a>Aggiunta di funzionalità di ricerca al controllo DataRepeater  
 In questo passaggio facoltativo, si implementa la funzionalità di ricerca per un valore di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Se viene individuata la stringa di ricerca, il controllo seleziona l'elemento che contiene il valore e scorre l'elemento nella visualizzazione.  
  
#### <a name="to-add-search-capability"></a>Per aggiungere funzionalità di ricerca  
  
1.  Trascinare un <xref:System.Windows.Forms.TextBox>da controllare il **della casella degli strumenti** nel form che contiene il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> </xref:System.Windows.Forms.TextBox>  
  
     Posizionarlo sotto il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
2.  Nella finestra Proprietà modificare la proprietà **Name** in **SearchTextBox**.  
  
3.  Trascinare un <xref:System.Windows.Forms.Button>da controllare il **della casella degli strumenti** nel form che contiene il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> </xref:System.Windows.Forms.Button> Posizionarlo sotto il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
4.  Nella finestra Proprietà modificare la proprietà **Name** in **SearchButton**. Impostare la proprietà **Text** su **Search**.  
  
5.  Fare doppio clic su di <xref:System.Windows.Forms.Button>di controllo per aprire l'Editor di codice e aggiungere il codice seguente per il `SearchButton_Click` gestore dell'evento.</xref:System.Windows.Forms.Button>  
  
     [!code-cs[N.&5; VbPowerPacksDataRepeaterWalkthrough](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_5.cs) ] 
     [!code-vb [VbPowerPacksDataRepeaterWalkthrough n.&5;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio_5.vb)]  
  
6.  Premere F5 per eseguire l'applicazione. Digitare un ID cliente in **SearchTextBox** e fare clic sul pulsante **Search** .  
  
## <a name="adding-a-master-and-detail-table-to-the-datarepeater"></a>Aggiunta di una tabella master e di dettaglio per il controllo  
 In questo passaggio facoltativo, verrà aggiunta una seconda <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo per visualizzare gli ordini correlati per ogni cliente.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
#### <a name="to-add-a-master-and-detail-table"></a>Per aggiungere una tabella master e di dettaglio  
  
1.  Trascinare una seconda <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo il **Visual Basic Power Packs** nella scheda il **della casella degli strumenti** nel form.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
2.  Nella finestra Proprietà impostare la proprietà **Location** su `465, 25`.  
  
3.  Impostare la proprietà **Size** su `315, 600`.  
  
4.  Nella finestra **Origini dati** espandere il nodo della tabella **Customers** e selezionare il nodo dettaglio della tabella **Orders** .  
  
5.  Modificare il tipo di rilascio della tabella **Orders** selezionando **Details** dall'elenco a discesa nel nodo della tabella.  
  
6.  Trascinare questo **ordini** area del modello di elemento (l'area superiore) del secondo nodo della tabella <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
     Alla barra dei componenti vengono aggiunti il componente **OrdersBindingSource** e il componente **OrdersTableAdapter** .  
  
7.  Premere F5 per eseguire l'applicazione. Quando si seleziona ogni cliente nel primo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllare, gli ordini per quel cliente vengono visualizzati nella seconda <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione al controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [Procedura: visualizzare i dati associati in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [Procedura: visualizzazione controlli non associati in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)   
 [Procedura: modificare il Layout di un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-layout-of-a-datarepeater-control-visual-studio.md)   
 [Procedura: visualizzare le intestazioni degli elementi in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-display-item-headers-in-a-datarepeater-control-visual-studio.md)   
 [Procedura: cercare dati in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-search-data-in-a-datarepeater-control-visual-studio.md)   
 [Procedura: creare un Form Master-Details mediante due controlli DataRepeater (Visual Studio)](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)   
 [Procedura: modificare l'aspetto di un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [Procedura: disabilitare l'aggiunta e l'eliminazione di elementi DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio.md)   
 [Risoluzione dei problemi relativi al controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)
