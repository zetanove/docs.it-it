---
title: "Procedura dettagliata: debug di controlli di Windows Form personalizzati in fase di progettazione | Microsoft Docs"
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
  - "controlli [Windows Form], debug"
  - "controlli personalizzati [Windows Form], debug"
  - "controlli personalizzati [Windows Form], procedure dettagliate"
  - "debug [Visual Studio], procedure dettagliate"
  - "debug [Visual Studio], Windows Form"
  - "finestre di progettazione"
  - "debug in fase di progettazione"
  - "editor visivi"
  - "procedure dettagliate [Windows Form], debug"
ms.assetid: 1fd83ccd-3798-42fc-85a3-6cba99467387
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura dettagliata: debug di controlli di Windows Form personalizzati in fase di progettazione
Quando si crea un controllo personalizzato, è spesso necessario eseguire il debug del comportamento in fase di progettazione  specialmente se per il controllo si sta creando una finestra di progettazione personalizzata.  Per informazioni dettagliate, vedere [Procedura dettagliata: creazione di un controllo di Windows Form che usufruisca delle funzionalità offerte da Visual Studio in fase di progettazione](../../../../docs/framework/winforms/controls/creating-a-wf-control-design-time-features.md).  
  
 È possibile eseguire il debug dei controlli personalizzati utilizzando Visual Studio esattamente come per qualsiasi altra classe .NET Framework.  La differenza consiste nel fatto che si eseguirà il debug dell'istanza separata di Visual Studio con il codice del controllo personalizzato in esecuzione.  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione di un progetto Windows Form per contenere il controllo personalizzato  
  
-   Creazione di un progetto di libreria di controlli  
  
-   Aggiunta di una proprietà al controllo personalizzato  
  
-   Aggiunta del controllo personalizzato al form host  
  
-   Impostazione del progetto per il debug in fase di progettazione  
  
-   Debug del controllo personalizzato in fase di progettazione  
  
 Al termine, si saranno acquisite le informazioni sulle attività necessarie per l'esecuzione del debug del comportamento in fase di progettazione di un controllo personalizzato.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Creazione del progetto  
 Il primo passaggio consiste nella creazione del progetto di applicazione,  che verrà utilizzato per compilare l'applicazione che contiene il controllo personalizzato.  
  
#### Per creare il progetto  
  
-   Creare un progetto Applicazione Windows chiamato "DebuggingExample".  Per informazioni dettagliate, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
## Creazione di un progetto di libreria di controlli  
 Il passaggio successivo consiste nella creazione del progetto di libreria di controlli e impostazione del controllo personalizzato.  
  
#### Per creare il progetto di libreria di controlli  
  
1.  Aggiungere alla soluzione un progetto **Libreria di controlli Windows**.  
  
2.  Aggiungere un nuovo elemento **UserControl** al progetto DebugControlLibrary.  Per informazioni dettagliate, vedere [NIB:How to: Add New Project Items](http://msdn.microsoft.com/it-it/63d3e16b-de6e-4bb5-a0e3-ecec762201ce).  Assegnare al nuovo file di origine il nome di base "DebugControl".  
  
3.  Utilizzando **Esplora soluzioni**, eliminare il controllo predefinito del progetto cancellando il file di codice con il nome di base "`UserControl1`".  Per informazioni dettagliate, vedere [NIB:How to: Remove, Delete, and Exclude Items](http://msdn.microsoft.com/it-it/6dffdc86-29c8-4eff-bcd8-e3a0dd9e9a73).  
  
4.  Compilare la soluzione.  
  
## Verifica  
 A questo punto il controllo personalizzato sarà visibile nella **Casella degli strumenti**.  
  
#### Per verificare lo stato dell'attività  
  
-   Individuare la nuova scheda **Componenti DebugControlLibrary** e selezionarla.  Una volta aperta, sarà possibile osservare che il controllo è presente nell'elenco come **DebugControl** con accanto l'icona predefinita.  
  
## Aggiunta di una proprietà al controllo personalizzato  
 Per verificare che il codice del controllo personalizzato viene eseguito in fase di progettazione, si aggiungerà una proprietà e si imposterà un punto di interruzione nel codice per implementare la proprietà.  
  
#### Per aggiungere una proprietà al controllo personalizzato  
  
1.  Aprire **DebugControl** nell'**editor di codice**.  Aggiungere il seguente codice alla definizione della classe.  
  
    ```vb  
    Private demoStringValue As String = Nothing  
    <BrowsableAttribute(true)>  
    Public Property DemoString() As String  
  
        Get  
            Return Me.demoStringValue  
        End Get  
  
        Set(ByVal value As String)  
            Me.demoStringValue = value  
        End Set  
  
    End Property  
    ```  
  
    ```csharp  
    private string demoStringValue = null;  
    [Browsable(true)]  
    public string DemoString  
    {  
        get  
        {  
            return this.demoStringValue;  
        }  
        set  
        {  
            demoStringValue = value;  
        }  
    }  
    ```  
  
2.  Compilare la soluzione.  
  
## Aggiunta del controllo personalizzato al form host  
 Per eseguire il debug del comportamento in fase di progettazione del controllo personalizzato, si inserirà un'istanza della classe del controllo personalizzato in un form host.  
  
#### Per aggiungere il controllo personalizzato al form host  
  
1.  Nel progetto "DebuggingExample", aprire Form1 in **Progettazione Windows Form**.  
  
2.  Nella **Casella degli strumenti**, aprire la scheda **Componenti DebugControlLibrary** e trascinare un'istanza di **DebugControl** nel form.  
  
3.  Individuare la proprietà personalizzata `DemoString` nella finestra **Proprietà**.  È possibile modificarne il valore in modo analogo a quello di qualsiasi altra proprietà.  Quando si seleziona la proprietà `DemoString`, viene visualizzata una stringa descrittiva nella parte inferiore della finestra **Proprietà**.  
  
## Impostazione del progetto per il debug in fase di progettazione  
 Per eseguire il debug del comportamento in fase di progettazione del controllo personalizzato, si eseguirà il debug dell'istanza separata di Visual Studio con il codice del controllo personalizzato in esecuzione.  
  
#### Per impostare il progetto per il debug in fase di progettazione  
  
1.  In **Esplora soluzioni**, fare clic con il pulsante destro del mouse sul progetto **DebugControlLibrary** e scegliere **Proprietà**.  
  
2.  Nella finestra della proprietà **DebugControlLibrary** selezionare la scheda **Debug**.  
  
     Nella sezione **Azione di avvio**, selezionare **Avvia programma esterno**.  Verrà eseguito il debug di un'istanza distinta di Visual Studio. A questo scopo fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) per individuare l'IDE di Visual Studio.  Il nome del file eseguibile è **devenv.exe** e, se è stato installato nel percorso predefinito, il relativo percorso %programfiles%\\Microsoft Visual Studio 9.0\\Common7\\IDE\\devenv.exe.  
  
3.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
4.  Fare clic con il pulsante destro del mouse sul progetto **DebugControlLibrary** e scegliere **Imposta come progetto di avvio** per attivare la configurazione di debug.  
  
## Debug del controllo personalizzato in fase di progettazione  
 A questo punto è possibile eseguire il debug del controllo personalizzato come fosse in esecuzione in modalità di progettazione.  Quando si avvia la sessione di debug, viene creata una nuova istanza di Visual Studio che verrà utilizzata per caricare la soluzione "DebuggingExample".  Quando si apre Form1 in **Progettazione Windows Form**, un'istanza del controllo personalizzato viene creata ed eseguita.  
  
#### Per eseguire il debug del controllo personalizzato in fase di progettazione  
  
1.  Aprire il file di origine**DebugControl** nell'**editor di codice** e inserire un punto di interruzione nella funzione di accesso `Set` della proprietà `DemoString`.  
  
2.  Premere F5 per avviare la sessione di debug.  Si noti che verrà creata una nuova istanza di Visual Studio.  È possibile distinguere le istanze in due modi:  
  
    -   L'istanza di debug contiene la parola **In esecuzione** nella barra del titolo.  
  
    -   Il pulsante **Avvia** dell'istanza di debug è disabilitato nella barra degli strumenti **Debug**.  
  
     Il punto di interruzione è impostato nell'istanza di debug.  
  
3.  Nella nuova istanza di Visual Studio, aprire la soluzione "DebuggingExample".  È possibile trovare facilmente la soluzione selezionando **Progetti recenti** dal menu **File**.  Il file di soluzione "DebuggingExample.sln" sarà il file utilizzato più di recente nell'elenco.  
  
4.  Aprire Form1 in **Progettazione Windows Form** e selezionare il controllo **DebugControl**.  
  
5.  Modificare il valore della proprietà `DemoString`.  Si noti che, eseguita la modifica, l'istanza di debug di Visual Studio acquisisce lo stato attivo e l'esecuzione si interrompe al punto di interruzione.  La funzione di accesso della proprietà viene eseguita tramite un'unica procedura come si farebbe per qualsiasi altro codice.  
  
6.  Una volta terminata la sessione di debug, è possibile uscire chiudendo l'istanza host di Visual Studio o facendo clic sul pulsante **Termina debug** nell'istanza di debug.  
  
## Passaggi successivi  
 Dopo aver eseguito il debug dei controlli personalizzati in fase di progettazione, vi sono diverse possibilità per espandere l'interazione del controllo con l'IDE di Visual Studio.  
  
-   È possibile utilizzare la proprietà <xref:System.ComponentModel.Component.DesignMode%2A> della classe <xref:System.ComponentModel.Component> per scrivere il codice che verrà eseguito solo in fase di progettazione.  Per informazioni dettagliate, vedere <xref:System.ComponentModel.Component.DesignMode%2A>.  
  
-   Alle proprietà del controllo si possono applicare diversi attributi per gestire l'interazione del controllo personalizzato con la finestra di progettazione.  Tali attributi si trovano nello spazio dei nomi <xref:System.ComponentModel?displayProperty=fullName>.  
  
-   È possibile scrivere una finestra di progettazione personalizzata per il controllo personalizzato.  In tal modo si ottiene il controllo completo della fase di progettazione utilizzando l'infrastruttura di progettazione estendibile esposta da Visual Studio.  Per informazioni dettagliate, vedere [Procedura dettagliata: creazione di un controllo di Windows Form che usufruisca delle funzionalità offerte da Visual Studio in fase di progettazione](../../../../docs/framework/winforms/controls/creating-a-wf-control-design-time-features.md).  
  
## Vedere anche  
 [Procedura dettagliata: creazione di un controllo di Windows Form che usufruisca delle funzionalità offerte da Visual Studio in fase di progettazione](../../../../docs/framework/winforms/controls/creating-a-wf-control-design-time-features.md)   
 [How to: Access Design\-Time Services](../Topic/How%20to:%20Access%20Design-Time%20Services.md)   
 [How to: Access Design\-Time Support in Windows Forms](../Topic/How%20to:%20Access%20Design-Time%20Support%20in%20Windows%20Forms.md)