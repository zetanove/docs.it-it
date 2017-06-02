---
title: "Procedura dettagliata: eredit&#224; da un controllo di Windows Form con Visual C# | Microsoft Docs"
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
ms.assetid: 09476da0-8d4c-4a4c-b969-649519dfb438
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura dettagliata: eredit&#224; da un controllo di Windows Form con Visual C# #
[!INCLUDE[csprcslong](../../../../includes/csprcslong-md.md)] consente di creare controlli personalizzati avanzati sfruttando l'*ereditarietà*.  L'ereditarietà consente di creare nuovi controlli che non solo conservano tutte le funzionalità proprie dei controlli Windows Form standard, ma includono anche funzionalità personalizzate.  In questa procedura verrà creato un controllo ereditato semplice denominato `ValueButton`.  Questo pulsante eredita la funzionalità dal controllo standard Windows Form <xref:System.Windows.Forms.Button> ed espone una proprietà personalizzata denominata `ButtonValue`.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Creazione del progetto  
 Quando si crea un nuovo progetto è necessario specificarne il nome per impostare lo spazio dei nomi di primo livello, il nome dell'assembly e il nome del progetto e per assicurarsi che il componente predefinito sia inserito nello spazio dei nomi corretto.  
  
#### Per creare la libreria di controlli ValueButtonLib e il controllo ValueButton  
  
1.  Scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**. Verrà visualizzata la finestra di dialogo **Nuovo progetto**.  
  
2.  Selezionare il modello di progetto **Libreria di controlli Windows Form** dall'elenco dei progetti di [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], quindi digitare `ValueButtonLib` nella casella **Nome**.  
  
     Per impostazione predefinita il nome del progetto,`ValueButtonLib`, verrà assegnato anche allo spazio dei nomi di primo livello.  Lo spazio dei nomi di primo livello viene utilizzato per qualificare i nomi dei componenti dell'assembly.  Se ad esempio due assembly forniscono componenti denominati `ValueButton`, sarà possibile specificare il componente `ValueButton` utilizzando `ValueButtonLib.ValueButton`.  Per ulteriori informazioni, vedere [Spazi dei nomi](../Topic/Namespaces%20\(C%23%20Programming%20Guide\).md).  
  
3.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **UserControl1.cs**, quindi scegliere **Rinomina** dal menu di scelta rapida.  Modificare il nome del file in `ValueButton.cs`.  Scegliere il pulsante **Sì** quando richiesto per rinominare tutti i riferimenti all'elemento di codice '`UserControl1`'.  
  
4.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **ValueButton.cs** e scegliere **Visualizza codice**.  
  
5.  Individuare la riga di istruzione `class`, `public partial class ValueButton`, e cambiare il tipo da cui il controllo eredita da <xref:System.Windows.Forms.UserControl> in <xref:System.Windows.Forms.Button>.  In tal modo il controllo ereditato potrà ereditare tutte le funzionalità del controllo <xref:System.Windows.Forms.Button>.  
  
6.  In **Esplora soluzioni** aprire il nodo **ValueButton.cs** per visualizzare il file di codice **ValueButton.Designer.cs** generato nella finestra di progettazione.  Aprire il file nell'**editor di codice**.  
  
7.  Individuare il metodo `InitializeComponent` e rimuovere la riga che assegna la proprietà <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A>.  Tale proprietà non esiste nel controllo <xref:System.Windows.Forms.Button>.  
  
8.  Per salvare il progetto, scegliere **Salva tutto** dal menu **File**.  
  
    > [!NOTE]
    >  La finestra di progettazione visiva non sarà più disponibile.  Poiché il controllo <xref:System.Windows.Forms.Button> esegue il proprio disegno, non è possibile modificarne l'aspetto nella finestra di progettazione.  La rappresentazione visiva di tale controllo sarà identica a quella della classe da cui eredita, vale a dire <xref:System.Windows.Forms.Button>, a meno che non venga modificata nel codice.  È comunque possibile aggiungere nell'area di progettazione i componenti che non dispongono di elementi dell'interfaccia utente.  
  
## Aggiunta di una proprietà al controllo ereditato  
 Un possibile utilizzo dei controlli ereditati per Windows Form è la creazione di controlli aventi aspetto e funzionalità identici ai controlli standard per Windows Form, ma che espongono proprietà personalizzate.  In questa sezione verrà illustrata la modalità di aggiunta della proprietà `ButtonValue` al controllo.  
  
#### Per aggiungere la proprietà Value  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **ValueButton.cs**, quindi scegliere **Visualizza codice** dal menu di scelta rapida.  
  
2.  Individuare l'istruzione `class`.  Immediatamente dopo il simbolo `{` digitare il seguente codice:  
  
     \[C\#\]  
  
    ```  
    // Creates the private variable that will store the value of your   
    // property.  
    private int varValue;  
    // Declares the property.  
    public int ButtonValue  
    {  
       // Sets the method for retrieving the value of your property.  
       get  
       {  
          return varValue;  
       }  
       // Sets the method for setting the value of your property.  
       set  
       {  
          varValue = value;  
       }  
    }  
    ```  
  
     Questo codice consente di impostare i metodi per la memorizzazione e il recupero della proprietà `ButtonValue`.  L'istruzione `get` imposta il valore restituito sul valore memorizzato nella variabile privata `varValue`, mentre l'istruzione `set` imposta il valore della variabile privata mediante la parola chiave `value`.  
  
3.  Per salvare il progetto, scegliere **Salva tutto** dal menu **File**.  
  
## Test del controllo  
 I controlli non sono progetti autonomi e devono pertanto essere inseriti in un contenitore.  Per testare il controllo, è necessario creare un progetto di test in cui eseguirlo.  È inoltre necessario rendere il controllo accessibile al progetto di test compilandolo.  In questa sezione verrà illustrato come compilare un controllo ed eseguirne il test in un Windows Form.  
  
#### Per compilare il controllo  
  
1.  Scegliere **Compila soluzione** dal menu **Compila**.  
  
     La compilazione dovrebbe essere completata correttamente senza avvisi o errori di compilazione.  
  
#### Per creare un progetto di test  
  
1.  Scegliere **Aggiungi** dal menu **File**, quindi fare clic su **Nuovo progetto**. Verrà visualizzata la finestra di dialogo **Aggiungi nuovo progetto**.  
  
2.  Selezionare il nodo **Windows** sotto il nodo **Visual C\#**, quindi fare clic su **Applicazione Windows Form**.  
  
3.  Nella casella **Nome**, digitare `Test`.  
  
4.  In **Esplora soluzioni**, fare clic con il pulsante destro del mouse sul nodo **Riferimenti** del progetto di test, quindi scegliere **Aggiungi riferimento** dal menu di scelta rapida per visualizzare la finestra di dialogo corrispondente.  
  
5.  Scegliere la scheda **Progetti**.  Il progetto `ValueButtonLib` verrà elencato in **Nome progetto**.  Fare doppio clic sul progetto per cui si desidera aggiungere il riferimento al progetto di test.  
  
6.  In **Esplora soluzioni**, fare doppio clic su **Test** e scegliere **Compila**.  
  
#### Per aggiungere il controllo al form  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Form1.cs** e scegliere **Visualizza finestra di progettazione** dal menu di scelta rapida.  
  
2.  Nella **Casella degli strumenti** fare clic su **Componenti ValueButtonLib**.  Fare doppio clic su **ValueButton**.  
  
     Nel form verrà visualizzato un controllo **ValueButton**.  
  
3.  Fare clic con il pulsante destro del mouse su **ValueButton**, quindi scegliere **Proprietà** dal menu di scelta rapida.  
  
4.  Nella finestra **Proprietà** esaminare le proprietà del controllo.  Tali proprietà sono identiche a quelle esposte da un pulsante standard, con la differenza che è disponibile anche la proprietà `ButtonValue`.  
  
5.  Impostare la proprietà `ButtonValue` su `5`.  
  
6.  Nella scheda **Tutti i Windows Form** della **Casella degli strumenti** fare doppio clic su **Label** per aggiungere un controllo <xref:System.Windows.Forms.Label> al form.  
  
7.  Posizionare l'etichetta al centro del form.  
  
8.  Doppio clic su `valueButton1`.  
  
     Nell'**editor di codice** verrà visualizzato l'evento `valueButton1_Click`.  
  
9. Inserire la seguente riga di codice:  
  
     \[C\#\]  
  
    ```  
    label1.Text = valueButton1.ButtonValue.ToString();  
    ```  
  
10. In **Esplora soluzioni**, fare clic con il pulsante destro del mouse su **Test** quindi scegliere **Imposta come progetto di avvio** dal menu di scelta rapida.  
  
11. Scegliere **Avvia debug** dal menu **Debug**.  
  
     Viene visualizzato `Form1`.  
  
12. Fare clic su `valueButton1`.  
  
     Il numero "5" verrà visualizzato in `label1` ad indicare che la proprietà `ButtonValue` del controllo ereditato è stata passata a `label1` mediante il metodo `valueButton1_Click`.  Il controllo `ValueButton` erediterà tutte le funzionalità del pulsante standard per Windows Form, ma esporrà una proprietà personalizzata aggiuntiva.  
  
## Vedere anche  
 [Programming with Components](../Topic/Programming%20with%20Components.md)   
 [Component Authoring Walkthroughs](../Topic/Component%20Authoring%20Walkthroughs.md)   
 [Procedura: visualizzare un controllo nella finestra di dialogo Scegli elementi della Casella degli strumenti](../../../../docs/framework/winforms/controls/how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)   
 [Procedura dettagliata: modifica di un controllo composito con Visual C\#](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-csharp.md)