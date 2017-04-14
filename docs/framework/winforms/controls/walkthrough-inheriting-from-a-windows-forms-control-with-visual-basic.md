---
title: "Procedura dettagliata: eredit&#224; da un controllo Windows Form con Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli personalizzati [Windows Form], ereditarietà"
  - "ereditarietà, controllo"
  - "ereditarietà, controlli personalizzati"
  - "ereditarietà, procedure dettagliate"
  - "controlli Windows Form, ereditarietà"
ms.assetid: fb58d7c8-b702-4478-ad31-b00cae118882
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura dettagliata: eredit&#224; da un controllo Windows Form con Visual Basic
[!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] consente di creare controlli personalizzati avanzati sfruttando l'*ereditarietà*.  L'ereditarietà consente di creare nuovi controlli che non solo conservano tutte le funzionalità proprie dei controlli Windows Form standard, ma includono anche funzionalità personalizzate.  In questa procedura verrà creato un controllo ereditato semplice denominato `ValueButton`.  Questo pulsante eredita la funzionalità dal controllo standard Windows Form <xref:System.Windows.Forms.Button> ed espone una proprietà personalizzata denominata `ButtonValue`.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Creazione del progetto  
 Quando si crea un nuovo progetto è necessario specificarne il nome per impostare lo spazio dei nomi di primo livello, il nome dell'assembly e il nome del progetto e per assicurarsi che il componente predefinito sia inserito nello spazio dei nomi corretto.  
  
#### Per creare la libreria di controlli ValueButtonLib e il controllo ValueButton  
  
1.  Scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**. Verrà visualizzata la finestra di dialogo **Nuovo progetto**.  
  
2.  Selezionare il modello di progetto **Libreria di controlli Windows Form** dall'elenco dei progetti di [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)], quindi digitare `ValueButtonLib` nella casella **Nome**.  
  
     Per impostazione predefinita il nome del progetto,`ValueButtonLib`, verrà assegnato anche allo spazio dei nomi di primo livello.  Lo spazio dei nomi di primo livello viene utilizzato per qualificare i nomi dei componenti dell'assembly.  Se ad esempio due assembly forniscono componenti denominati `ValueButton`, sarà possibile specificare il componente `ValueButton` utilizzando `ValueButtonLib.ValueButton`.  Per ulteriori informazioni, vedere [Spazi dei nomi in Visual Basic](../Topic/Namespaces%20in%20Visual%20Basic.md).  
  
3.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **UserControl1.vb**, quindi scegliere **Rinomina**.  Cambiare il nome del file in `ValueButton.vb`.  Scegliere il pulsante **Sì** quando richiesto per rinominare tutti i riferimenti all'elemento di codice "UserControl1".  
  
4.  In **Esplora soluzioni** fare clic sul pulsante **Mostra tutti i file**.  
  
5.  Aprire il nodo **ValueButton.vb** per visualizzare il file del codice generato nella finestra di progettazione **ValueButton.Designer.vb**.  Aprire il file nell'**editor di codice**.  
  
6.  Individuare l'istruzione `Class`, `Partial Public Class ValueButton`, e cambiare il tipo da cui il controllo eredita da <xref:System.Windows.Forms.UserControl> in <xref:System.Windows.Forms.Button>.  In tal modo il controllo ereditato potrà ereditare tutte le funzionalità del controllo <xref:System.Windows.Forms.Button>.  
  
7.  Individuare il metodo `InitializeComponent` e rimuovere la riga che assegna la proprietà <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A>.  Tale proprietà non esiste nel controllo <xref:System.Windows.Forms.Button>.  
  
8.  Per salvare il progetto, scegliere **Salva tutto** dal menu **File**.  
  
     Si noti che non sarà più disponibile alcuna finestra di progettazione.  Poiché il controllo <xref:System.Windows.Forms.Button> esegue il proprio disegno, non è possibile modificarne l'aspetto nella finestra di progettazione.  La rappresentazione visiva di tale controllo sarà identica a quella della classe da cui eredita, vale a dire <xref:System.Windows.Forms.Button>, a meno che non venga modificata nel codice.  
  
> [!NOTE]
>  È comunque possibile aggiungere nell'area di progettazione i componenti che non dispongono di elementi dell'interfaccia utente.  
  
## Aggiunta di una proprietà al controllo ereditato  
 Un possibile utilizzo dei controlli Windows Form ereditati è la creazione di controlli aventi aspetto e funzionalità identici ai controlli standard Windows Form, ma che espongono proprietà personalizzate.  In questa sezione verrà illustrata la modalità di aggiunta della proprietà `ButtonValue` al controllo.  
  
#### Per aggiungere la proprietà Value  
  
1.  In **Esplora soluzioni**, fare clic con il pulsante destro del mouse su **ValueButton.vb**, quindi scegliere **Visualizza codice** dal menu di scelta rapida.  
  
2.  Individuare l'istruzione `Public Class ValueButton`.  Sotto questa istruzione digitare il seguente codice:  
  
     \[Visual Basic\]  
  
    ```  
    ' Creates the private variable that will store the value of your   
    ' property.  
    Private varValue as integer  
    ' Declares the property.  
    Property ButtonValue() as Integer  
    ' Sets the method for retrieving the value of your property.  
       Get  
          Return varValue  
       End Get  
    ' Sets the method for setting the value of your property.  
       Set(ByVal Value as Integer)  
          varValue = Value  
       End Set  
    End Property  
    ```  
  
     Questo codice consente di impostare i metodi per la memorizzazione e il recupero della proprietà `ButtonValue`.  L'istruzione `Get` consente di impostare il valore restituito sul valore memorizzato nella variabile privata `varValue`, mentre l'istruzione `Set` consente di impostare il valore della variabile privata mediante la parola chiave `Value`.  
  
3.  Per salvare il progetto, scegliere **Salva tutto** dal menu **File**.  
  
## Test del controllo  
 I controlli non sono progetti autonomi e devono pertanto essere inseriti in un contenitore.  Per testare il controllo, è necessario creare un progetto di test in cui eseguirlo.  È inoltre necessario rendere il controllo accessibile al progetto di test compilandolo.  In questa sezione verrà illustrato come compilare un controllo ed eseguirne il test in un Windows Form.  
  
#### Per compilare il controllo  
  
1.  Scegliere **Compila soluzione** dal menu **Compila**.  
  
     La compilazione dovrebbe essere completata correttamente senza avvisi o errori di compilazione.  
  
#### Per creare un progetto di test  
  
1.  Scegliere **Aggiungi** dal menu **File**, quindi fare clic su **Nuovo progetto**. Verrà visualizzata la finestra di dialogo **Aggiungi nuovo progetto**.  
  
2.  Selezionare il nodo dei progetti di [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)], quindi fare clic su **Applicazione Windows Form**.  
  
3.  Nella casella **Nome**, digitare `Test`.  
  
4.  In **Esplora soluzioni** fare clic sul pulsante **Mostra tutti i file**.  
  
5.  In **Esplora soluzioni**, fare clic con il pulsante destro del mouse sul nodo **Riferimenti** del progetto di test, quindi scegliere **Aggiungi riferimento** dal menu di scelta rapida per visualizzare la finestra di dialogo corrispondente.  
  
6.  Fare clic sulla scheda **Progetti**.  
  
7.  Scegliere la scheda **Progetti**.  Il progetto `ValueButtonLib` verrà elencato in **Nome progetto**.  Fare doppio clic sul progetto per cui si desidera aggiungere il riferimento al progetto di test.  
  
8.  In **Esplora soluzioni**, fare doppio clic su **Test** e scegliere **Compila**.  
  
#### Per aggiungere il controllo al form  
  
1.  In **Esplora soluzioni**, fare clic con il pulsante destro del mouse su **Form1.vb**, quindi scegliere **Visualizza finestra di progettazione** dal menu di scelta rapida.  
  
2.  Nella **Casella degli strumenti** fare clic su **Componenti ValueButtonLib**.  Fare doppio clic su **ValueButton**.  
  
     Nel form verrà visualizzato un controllo **ValueButton**.  
  
3.  Fare clic con il pulsante destro del mouse su **ValueButton**, quindi scegliere **Proprietà** dal menu di scelta rapida.  
  
4.  Nella finestra **Proprietà** esaminare le proprietà del controllo.  Tali proprietà sono identiche a quelle esposte da un pulsante standard, con la differenza che è disponibile anche la proprietà `ButtonValue`.  
  
5.  Impostare la proprietà `ButtonValue` su `5`.  
  
6.  Nella scheda **Tutti i Windows Form** della **Casella degli strumenti** fare doppio clic su **Etichetta** per aggiungere un controllo <xref:System.Windows.Forms.Label> al form.  
  
7.  Posizionare l'etichetta al centro del form.  
  
8.  Doppio clic su `ValueButton1`.  
  
     Nell'**editor di codice** verrà visualizzato l'evento `ValueButton1_Click`.  
  
9. Digitare la seguente riga di codice:  
  
     \[Visual Basic\]  
  
    ```  
    Label1.Text = CStr(ValueButton1.ButtonValue)  
    ```  
  
10. In **Esplora soluzioni**, fare clic con il pulsante destro del mouse su **Test** quindi scegliere **Imposta come progetto di avvio** dal menu di scelta rapida.  
  
11. Scegliere **Avvia debug** dal menu **Debug**.  
  
     Viene visualizzato `Form1`.  
  
12. Fare clic su `Valuebutton1`.  
  
     Il numero "5" verrà visualizzato in `Label1`, a significare che la proprietà `ButtonValue` del controllo ereditato è stata passata a `Label1` mediante il metodo `ValueButton1_Click`.  Il controllo `ValueButton` erediterà tutte le funzionalità del pulsante standard per Windows Form, ma esporrà una proprietà personalizzata aggiuntiva.  
  
## Vedere anche  
 [Procedura dettagliata: modifica di un controllo composito con Visual Basic](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md)   
 [Procedura: visualizzare un controllo nella finestra di dialogo Scegli elementi della Casella degli strumenti](../../../../docs/framework/winforms/controls/how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)   
 [Sviluppo di controlli Windows Form personalizzati con .NET Framework](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)   
 [NOT IN BUILD: Inheritance in Visual Basic](http://msdn.microsoft.com/it-it/e5e6e240-ed31-4657-820c-079b7c79313c)   
 [Component Authoring Walkthroughs](../Topic/Component%20Authoring%20Walkthroughs.md)