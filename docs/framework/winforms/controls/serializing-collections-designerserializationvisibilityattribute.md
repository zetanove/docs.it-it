---
title: "Procedura dettagliata: serializzazione di raccolte di tipi standard tramite DesignerSerializationVisibilityAttribute | Microsoft Docs"
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
  - "raccolte, serializzazione"
  - "raccolte, tipi standard"
  - "DesiginerSerializationVisibilityAttribute (classe)"
  - "serializzazione, raccolte"
  - "tipi standard, raccolte"
ms.assetid: 020c9df4-fdc5-4dae-815a-963ecae5668c
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura dettagliata: serializzazione di raccolte di tipi standard tramite DesignerSerializationVisibilityAttribute
I controlli personalizzati talvolta espongono una raccolta come una proprietà.  In questa procedura dettagliata viene indicato come utilizzare la classe <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute> per controllare come una raccolta viene serializzata in fase di progettazione.  Tramite l'applicazione del valore <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content> alla proprietà della raccolta si assicura che la proprietà venga serializzata.  
  
 Per copiare il codice relativo a questo argomento come un listato unico, vedere [How to: Serialize Collections of Standard Types with the DesignerSerializationVisibilityAttribute](../Topic/How%20to:%20Serialize%20Collections%20of%20Standard%20Types%20with%20the%20DesignerSerializationVisibilityAttribute.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Prerequisiti  
 Per completare questa procedura dettagliata, è necessario disporre di quanto segue:  
  
-   Disporre di autorizzazioni sufficienti per creare ed eseguire progetti di applicazioni Windows Form nel computer dove è installato Visual Studio.  
  
## Creazione di un controllo contenente una raccolta serializzabile  
 Il primo passaggio consiste nella creazione di un controllo che contiene una raccolta serializzabile come una proprietà.  È possibile modificare il contenuto della raccolta utilizzando l'**editor della raccolta** dalla finestra **Proprietà**.  
  
#### Per creare un controllo con una raccolta serializzabile  
  
1.  Creare un progetto Libreria di controlli Windows denominato `SerializationDemoControlLib`.  Per ulteriori informazioni, vedere [Windows Control Library Template](http://msdn.microsoft.com/it-it/722f4e2d-1310-4ed5-8f33-593337ab66b4).  
  
2.  Rinominare `UserControl1` in `SerializationDemoControl`.  Per ulteriori informazioni, vedere [How to: Rename Identifiers](http://msdn.microsoft.com/it-it/2430f732-2b70-4516-8cf6-a7bb71cc9724).  
  
3.  Nella finestra **Proprietà** impostare il valore della proprietà <xref:System.Windows.Forms.Padding.All%2A?displayProperty=fullName> su `10`.  
  
4.  Inserire un controllo <xref:System.Windows.Forms.TextBox> in `SerializationDemoControl`.  
  
5.  Fare clic sul controllo <xref:System.Windows.Forms.TextBox>.  Nella finestra **Proprietà** impostare le seguenti proprietà:  
  
    |Proprietà|Modificare in|  
    |---------------|-------------------|  
    |**Multiline**|`true`|  
    |**Dock**|<xref:System.Windows.Forms.DockStyle>|  
    |**ScrollBars**|<xref:System.Windows.Forms.ScrollBars>|  
    |**ReadOnly**|`true`|  
  
6.  Nell'**editor di codice**, dichiarare un campo di matrice di stringhe denominato `stringsValue` in `SerializationDemoControl`.  
  
     [!code-cpp[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/cpp/form1.cpp#4)]
     [!code-csharp[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/CS/form1.cs#4)]
     [!code-vb[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/VB/form1.vb#4)]  
  
7.  Definire la proprietà `Strings` in `SerializationDemoControl`.  
  
> [!NOTE]
>  Il valore <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content> viene utilizzato per attivare la serializzazione della raccolta.  
  
 [!code-cpp[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/cpp/form1.cpp#5)]
 [!code-csharp[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/CS/form1.cs#5)]
 [!code-vb[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/VB/form1.vb#5)]  
  
1.  Per compilare il progetto ed eseguire il controllo in **UserControl Test Container**, premere F5.  
  
2.  Trovare la proprietà `Strings` nell'oggetto <xref:System.Windows.Forms.PropertyGrid> di **UserControl Test Container**.  Fare clic sulla proprietà `Strings`, quindi fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) per aprire l'**editor della raccolta String**.  
  
3.  Immettere diverse stringhe nell'**editor della raccolta String**.  Separarle premendo INVIO alla fine di ogni stringa.  Una volta aggiunte tutte le stringhe, premere **OK**.  
  
> [!NOTE]
>  Le stringhe digitate vengono visualizzate nella <xref:System.Windows.Forms.TextBox> di `SerializationDemoControl`.  
  
## Serializzazione di una proprietà della raccolta  
 Per verificare il comportamento di serializzazione di un controllo, si inserisce il controllo in un form e si modifica il contenuto della raccolta con l'**editor della raccolta**.  È possibile osservare lo stato della raccolta serializzato in un file speciale della finestra di progettazione in cui **Progettazione Windows Form** emette il codice.  
  
#### Per serializzare una raccolta  
  
1.  Aggiungere alla soluzione un progetto Applicazione Windows.  Assegnare al progetto il nome `SerializationDemoControlTest`.  
  
2.  Nella **Casella degli strumenti**, individuare la scheda **Componenti SerializationDemoControlLib** dove si troverà il controllo `SerializationDemoControl`.  Per ulteriori informazioni, vedere [Procedura dettagliata: compilare automaticamente la casella degli strumenti con componenti personalizzati](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md).  
  
3.  Inserire un `SerializationDemoControl` nel form.  
  
4.  Trovare la proprietà `Strings` nella finestra **Proprietà**.  Fare clic sulla proprietà `Strings`, quindi fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) per aprire l'**editor della raccolta String**.  
  
5.  Digitare diverse stringhe nell'**editor della raccolta String**.  Separarle premendo INVIO alla fine di ogni stringa.  Una volta aggiunte tutte le stringhe, premere **OK**.  
  
> [!NOTE]
>  Le stringhe digitate vengono visualizzate nella <xref:System.Windows.Forms.TextBox> di `SerializationDemoControl`.  
  
1.  In **Esplora soluzioni** fare clic sul pulsante **Mostra tutti i file**.  
  
2.  Aprire il nodo **Form1** in cui è presente un file chiamato **Form1.Designer.cs** o **Form1.Designer.vb**.  Si tratta del file in cui **Progettazione Windows Form** emette il codice che rappresenta lo stato in fase di progettazione del form e dei controlli figlio.  Aprire il file nell'**editor di codice**.  
  
3.  Aprire la regione **Codice generato da Progettazione Windows Form** e individuare la sezione **serializationDemoControl1**.  In questa etichetta è contenuto il codice che rappresenta lo stato serializzato del controllo.  Le stringhe digitate al passaggio 5 sono presenti in un'assegnazione alla proprietà `Strings`.  Il seguente codice di esempio mostra ciò che si otterrebbe se si digitassero stringhe "red", "orange" e "yellow".  
  
4.  \[Visual Basic\]  
  
    ```  
    Me.serializationDemoControl1.Strings = New String() {"red", "orange", "yellow"}  
    ```  
  
5.  \[C\#\]  
  
    ```  
    this.serializationDemoControl1.Strings = new string[] {  
            "red",  
            "orange",  
            "yellow"};  
    ```  
  
6.  Nell'**editor di codice** modificare il valore di <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute> sulla proprietà `Strings` in <xref:System.ComponentModel.DesignerSerializationVisibility>.  
  
7.  \[Visual Basic\]  
  
    ```  
    <DesignerSerializationVisibility(DesignerSerializationVisibility.Hidden)> _  
    ```  
  
8.  \[C\#\]  
  
    ```  
    [DesignerSerializationVisibility(DesignerSerializationVisibility.Hidden)]  
    ```  
  
9. Ricompilare la soluzione e ripetere i passaggi da 4 a 8.  
  
> [!NOTE]
>  In tal caso, **Progettazione Windows Form** non emette alcuna assegnazione alla proprietà `Strings`.  
  
## Passaggi successivi  
 Una volta appreso come serializzare una raccolta di tipi standard, provare a integrare i controlli personalizzati in modo più specifico nell'ambiente della fase di progettazione.  Negli argomenti riportati di seguito viene descritto come aumentare l'integrazione della fase di progettazione dei controlli personalizzati.  
  
-   [Design\-Time Architecture](../Topic/Design-Time%20Architecture.md)  
  
-   [Attributi nei controlli Windows Form](../../../../docs/framework/winforms/controls/attributes-in-windows-forms-controls.md)  
  
-   [Designer Serialization Overview](../Topic/Designer%20Serialization%20Overview.md)  
  
-   [Procedura dettagliata: creazione di un controllo di Windows Form che usufruisca delle funzionalità offerte da Visual Studio in fase di progettazione](../../../../docs/framework/winforms/controls/creating-a-wf-control-design-time-features.md)  
  
## Vedere anche  
 <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute>   
 [Designer Serialization Overview](../Topic/Designer%20Serialization%20Overview.md)   
 [How to: Serialize Collections of Standard Types with the DesignerSerializationVisibilityAttribute](../Topic/How%20to:%20Serialize%20Collections%20of%20Standard%20Types%20with%20the%20DesignerSerializationVisibilityAttribute.md)   
 [Procedura dettagliata: compilare automaticamente la casella degli strumenti con componenti personalizzati](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)