---
title: "Risoluzione dei problemi relativi alla modifica di controlli e componenti | Microsoft Docs"
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
  - "componenti [Windows Form], risoluzione dei problemi"
  - "controlli [Windows Form], risoluzione dei problemi"
  - "risoluzione dei problemi dei componenti"
  - "risoluzione dei problemi dei controlli"
  - "controlli Windows Form, debug"
ms.assetid: e9c8c099-2271-4737-882f-50f336c7a55e
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# Risoluzione dei problemi relativi alla modifica di controlli e componenti
In questo argomento è riportato l'elenco dei problemi comuni riscontrati durante lo sviluppo di componenti e controlli.  Per ulteriori informazioni, vedere [Programming with Components](../Topic/Programming%20with%20Components.md).  
  
-   Impossibile aggiungere il controllo alla Casella degli strumenti  
  
-   Impossibile eseguire il debug del componente o del controllo utente Windows Form  
  
-   Evento generato due volte in un controllo o un componente ereditato  
  
-   Errore di progettazione: "Impossibile creare il componente '*nome componente*'".  
  
-   STAThreadAttribute  
  
-   L'icona del componente non viene visualizzata nella Casella degli strumenti  
  
## Impossibile aggiungere il controllo alla Casella degli strumenti  
 L'aggiunta di un controllo personalizzato creato in un altro progetto o di un controllo di terze parti alla **Casella degli strumenti** è un'operazione manuale.  Il controllo o il componente, se contenuto nel progetto corrente, viene automaticamente visualizzato nella **Casella degli strumenti**.  Per ulteriori informazioni, vedere [Procedura dettagliata: compilare automaticamente la casella degli strumenti con componenti personalizzati](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md).  
  
#### Per aggiungere un controllo alla Casella degli strumenti  
  
1.  Fare clic con il pulsante destro del mouse sulla **Casella degli strumenti** e selezionare **Scegli elementi** dal menu di scelta rapida.  
  
2.  Nella finestra di dialogo **Scegli elementi della Casella degli strumenti**, aggiungere il componente:  
  
    -   Se si desidera aggiungere un componente o un controllo .NET Framework, fare clic sulla scheda **Componenti di .NET Framework**.  
  
         Oppure  
  
    -   Se si desidera aggiungere un componente COM o un controllo ActiveX, fare clic sulla scheda **Componenti COM**.  
  
3.  Se il controllo è incluso nell'elenco visualizzato nella finestra di dialogo, verificare che sia selezionato, quindi scegliere **OK**.  
  
     Il controllo verrà aggiunto alla **Casella degli strumenti**.  
  
4.  Se il controllo è incluso nell'elenco visualizzato nella finestra di dialogo, effettuare quanto riportato di seguito:  
  
    1.  Scegliere il pulsante **Browse**.  
  
    2.  Individuare la cartella che contiene il file DLL in cui è presente il controllo.  
  
    3.  Selezionare il file DLL e fare clic su **Apri**.  
  
         Il controllo verrà visualizzato nella finestra di dialogo.  
  
    4.  Assicurarsi che il controllo sia selezionato, quindi scegliere **OK**.  
  
         Il controllo verrà aggiunto alla **Casella degli strumenti**.  
  
## Impossibile eseguire il debug del componente o del controllo utente Windows Form  
 Se il controllo deriva dalla classe <xref:System.Windows.Forms.UserControl>, è possibile eseguire il debug del comportamento in fase di esecuzione con Test Container.  Per ulteriori informazioni, vedere [Procedura: eseguire il test del comportamento in fase di esecuzione di UserControl](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md).  
  
 Altri controlli e componenti personalizzati non sono progetti autonomi.  e devono essere ospitati da un'applicazione, quale un progetto Windows Form.  Per eseguire il debug di un controllo o di un componente, è quindi necessario aggiungerlo a un progetto Windows Form.  
  
#### Per eseguire il debug di un controllo o di un componente  
  
1.  Scegliere **Compila soluzione** dal menu **Compila** per compilare la soluzione.  
  
2.  Scegliere **Aggiungi** dal menu **File**, quindi **Nuovo progetto** per aggiungere un progetto di test all'applicazione.  
  
3.  Nella finestra di dialogo **Aggiungi nuovo progetto** scegliere **Applicazione Windows** come tipo del progetto.  
  
4.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo **Riferimenti** del nuovo progetto.  Scegliere **Aggiungi riferimento** dal menu di scelta rapida per aggiungere un riferimento al progetto che contiene il controllo o il componente.  
  
5.  Creare un'istanza del controllo o del componente nel progetto di test.  Se il componente si trova nella **Casella degli strumenti**, è possibile trascinarlo nell'area di progettazione oppure creare l'istanza a livello di codice come riportato nell'esempio di codice che segue:  
  
    ```vb  
    Dim Component1 As New MyNeatComponent()  
    ```  
  
    ```csharp  
    MyNeatComponent Component1 = new MyNeatComponent();  
    ```  
  
     È ora possibile eseguire il debug del controllo o del componente seguendo la normale procedura.  
  
 Per ulteriori informazioni sul debug, vedere [Debug in Visual Studio](../Topic/Debugging%20in%20Visual%20Studio.md) e [Procedura dettagliata: debug di controlli di Windows Form personalizzati in fase di progettazione](../../../../docs/framework/winforms/controls/walkthrough-debugging-custom-windows-forms-controls-at-design-time.md).  
  
## Evento generato due volte in un controllo o un componente ereditato  
 Il problema potrebbe dipendere da una clausola `Handles` duplicata.  Per ulteriori informazioni, vedere [Troubleshooting Inherited Event Handlers in Visual Basic](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md).  
  
## Errore in fase di progettazione: "Impossibile creare il componente 'nome del componente'"  
 È necessario che il componente o il controllo forniscano un costruttore predefinito senza parametri.  Quando l'ambiente di progettazione crea un'istanza del componente o del controllo, non tenta di fornire i parametri agli overload del costruttore che accettano i parametri.  
  
## STAThreadAttribute  
 <xref:System.STAThreadAttribute> informa Common Language Runtime \(CLR\) che Windows Form utilizza un modello di apartment a thread singolo.  Si potrebbe notare un comportamento non previsto se non si applica l'attributo al metodo `Main` dell'applicazione Windows Form.  Ad esempio, le immagini di sfondo potrebbero non essere visualizzate per i controlli come <xref:System.Windows.Forms.ListView>.  Per alcuni controlli potrebbe inoltre essere necessario questo attributo per il corretto comportamento delle operazioni di trascinamento della selezione e completamento automatico.  
  
## L'icona del componente non viene visualizzata nella Casella degli strumenti  
 Quando si utilizza <xref:System.Drawing.ToolboxBitmapAttribute> per associare un'icona al componente personalizzato, la bitmap non viene visualizzata nella casella degli strumenti per i componenti generati automaticamente.  Per vedere la bitmap, ricaricare il controllo utilizzando la finestra di dialogo **Scegli elementi della Casella degli strumenti**.  Per ulteriori informazioni, vedere [Procedura: specificare una bitmap nella casella degli strumenti per un controllo](../../../../docs/framework/winforms/controls/how-to-provide-a-toolbox-bitmap-for-a-control.md).  
  
## Vedere anche  
 [Sviluppo di controlli Windows Form in fase di progettazione](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)   
 [Procedura dettagliata: compilare automaticamente la casella degli strumenti con componenti personalizzati](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)   
 [Procedura: eseguire il test del comportamento in fase di esecuzione di UserControl](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)   
 [Procedura dettagliata: debug di controlli di Windows Form personalizzati in fase di progettazione](../../../../docs/framework/winforms/controls/walkthrough-debugging-custom-windows-forms-controls-at-design-time.md)   
 [Component Authoring](../Topic/Component%20Authoring.md)   
 [Troubleshooting Design\-Time Development](../Topic/Troubleshooting%20Design-Time%20Development.md)   
 [Programming with Components](../Topic/Programming%20with%20Components.md)