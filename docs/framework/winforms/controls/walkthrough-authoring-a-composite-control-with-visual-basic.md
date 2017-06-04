---
title: "Procedura dettagliata: modifica di un controllo composito con Visual Basic | Microsoft Docs"
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
  - "controlli composti, creazione"
  - "controlli [Windows Form], controlli composti"
  - "controlli personalizzati [Visual Basic]"
  - "controlli personalizzati [Windows Form], creazione"
  - "controlli utente [Visual Basic]"
  - "controlli utente [Windows Form], creazione con Visual Basic"
  - "UserControl (classe), procedure dettagliate"
ms.assetid: f50e270e-4db2-409a-8319-6db6ca5c7daf
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Procedura dettagliata: modifica di un controllo composito con Visual Basic
I controlli compositi consentono di creare e riutilizzare interfacce grafiche personalizzate.  Un controllo composito è sostanzialmente un componente con rappresentazione visiva.  Può essere composto da uno o più controlli per Windows Form, componenti o blocchi di codice in grado di estenderne le funzionalità convalidando l'input dell'utente, modificando le proprietà della visualizzazione o effettuando altre attività richieste dall'autore.  I controlli compositi possono essere inseriti in Windows Form al pari degli altri controlli.  Nella prima parte di questa procedura verrà creato un controllo composito semplice denominato `ctlClock`.  Nella seconda parte, le funzionalità di `ctlClock` verranno estese mediante ereditarietà.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Creazione del progetto  
 Quando si crea un nuovo progetto è necessario specificarne il nome per impostare lo spazio dei nomi di primo livello, il nome dell'assembly e il nome del progetto e assicurarsi che il componente predefinito venga inserito nello spazio dei nomi corretto.  
  
#### Per creare la libreria di controlli ctlClockLib e il controllo ctlClock  
  
1.  Scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**. Verrà visualizzata la finestra di dialogo **Nuovo progetto**.  
  
2.  Selezionare il modello di progetto **Libreria di controlli Windows** dall'elenco dei progetti di [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)], quindi digitare `ctlClockLib` nella casella **Nome** e scegliere **OK**.  
  
     Per impostazione predefinita il nome del progetto,`ctlClockLib`, verrà assegnato anche allo spazio dei nomi di primo livello.  Lo spazio dei nomi di primo livello viene utilizzato per qualificare i nomi dei componenti dell'assembly.  Se ad esempio due assembly forniscono componenti denominati `ctlClock`, sarà possibile specificare il componente `ctlClock` utilizzando il nome completo `ctlClockLib.ctlClock.` .  
  
3.  In Esplora soluzioni, fare clic con il pulsante destro del mouse su **UserControl1.vb**, quindi scegliere **Rinomina**.  Modificare il nome file in `ctlClock.vb`.  Scegliere il pulsante **Sì** quando richiesto per rinominare tutti i riferimenti all'elemento di codice "UserControl1".  
  
    > [!NOTE]
    >  Per impostazione predefinita, un controllo composito eredita dalla classe <xref:System.Windows.Forms.UserControl> fornita dal sistema.  La classe <xref:System.Windows.Forms.UserControl> fornisce le funzionalità necessarie per tutti i controlli compositi e consente di implementare metodi e proprietà standard.  
  
4.  Scegliere **Salva tutto** dal menu **File** per salvare il progetto.  
  
## Aggiunta di componenti e controlli Windows al controllo composito  
 L'interfaccia visiva è parte integrante del controllo composito  e viene implementata mediante l'aggiunta di uno o più controlli Windows nell'area di progettazione.  Nella procedura riportata di seguito i controlli Windows verranno incorporati nel controllo composito e verrà scritto il codice per l'implementazione delle funzionalità.  
  
#### Per aggiungere al controllo utente un oggetto Label e un oggetto Timer  
  
1.  In Esplora soluzioni, fare clic con il pulsante destro del mouse su **ctlClock.vb**, quindi scegliere **Visualizza finestra di progettazione**.  
  
2.  Nella Casella degli strumenti, espandere il nodo **Controlli comuni** e fare doppio clic su **Etichetta**.  
  
     Un controllo <xref:System.Windows.Forms.Label> denominato `Label1` viene aggiunto al controllo nell'area di progettazione.  
  
3.  Nella finestra di progettazione fare clic su **Label1**.  Nella finestra Proprietà impostare le proprietà seguenti.  
  
    |Proprietà|Modificare in|  
    |---------------|-------------------|  
    |**Nome**|`lblDisplay`|  
    |**Text**|`(vuoto)`|  
    |**TextAlign**|`MiddleCenter`|  
    |**Font.Size**|`14`|  
  
4.  Nella **Casella degli strumenti**, espandere il nodo **Componenti**, quindi fare doppio clic su **Timer**.  
  
     Poiché un <xref:System.Windows.Forms.Timer> è un componente ed è pertanto privo di rappresentazione visiva in fase di esecuzione,  non verrà visualizzato insieme ai controlli nell'area di progettazione bensì in Progettazione componenti, una barra delle applicazioni disposta nella parte inferiore dell'area di progettazione.  
  
5.  In Progettazione componenti, fare clic su **Timer1**, quindi impostare la proprietà <xref:System.Windows.Forms.Timer.Interval%2A> su `1000` e la proprietà <xref:System.Windows.Forms.Timer.Enabled%2A> su `True`.  
  
     La proprietà <xref:System.Windows.Forms.Timer.Interval%2A> controlla la frequenza con cui scatta il componente Timer.  Ogni volta che `Timer1` scatta, viene eseguito il codice nell'evento `Timer1_Tick`.  L'intervallo rappresenta i millesimi di secondo che intercorrono tra uno scatto e l'altro.  
  
6.  In Progettazione componenti, fare doppio clic su **Timer1** per passare all'evento `Timer1_Tick` di `ctlClock`.  
  
7.  Modificare il codice in modo che risulti simile al seguente.  Assicurarsi di cambiare il modificatore di accesso da `Private` a `Protected`.  
  
     \[Visual Basic\]  
  
    ```  
    Protected Sub Timer1_Tick(ByVal sender As Object, ByVal e As _  
        System.EventArgs) Handles Timer1.Tick  
        ' Causes the label to display the current time.    
        lblDisplay.Text = Format(Now, "hh:mm:ss")  
    End Sub  
    ```  
  
     Questo codice determinerà la visualizzazione dell'ora corrente in `lblDisplay`.  Poiché l'intervallo di `Timer1` è stato impostato su `1000`, l'evento verrà generato ogni mille millesimi di secondo, aggiornando quindi l'ora corrente ogni secondo.  
  
8.  Modificare il metodo in modo che sia sottoponibile a override.  Per ulteriori informazioni, vedere la sezione "Eredità da un controllo utente" riportata di seguito.  
  
     \[Visual Basic\]  
  
    ```  
    Protected Overridable Sub Timer1_Tick(ByVal sender As Object, ByVal _  
        e As System.EventArgs) Handles Timer1.Tick  
    ```  
  
9. Scegliere **Salva tutto** dal menu **File** per salvare il progetto.  
  
## Aggiunta di proprietà al controllo composito  
 A questo punto nel controllo sono stati incorporati un controllo <xref:System.Windows.Forms.Label> e un componente <xref:System.Windows.Forms.Timer>, ciascuno dotato di un insieme di proprietà intrinseche.  Benché le singole proprietà di questi controlli non siano accessibili ai futuri utenti del controllo, è possibile creare ed esporre proprietà personalizzate scrivendo i blocchi di codice appropriati.  Nella procedura riportata di seguito verrà illustrato come aggiungere al controllo proprietà che consentono all'utente di modificare il colore dello sfondo e del testo.  
  
#### Per aggiungere una proprietà al controllo composito  
  
1.  In Esplora soluzioni, fare clic con il pulsante destro del mouse su **ctlClock.vb**, quindi scegliere **Visualizza codice**.  
  
     Verrà visualizzato l'editor del codice per il controllo.  
  
2.  Individuare l'istruzione `Public Class ctlClock`.  Sotto tale riga, aggiungere il seguente codice.  
  
     \[Visual Basic\]  
  
    ```  
    Private colFColor as Color  
    Private colBColor as Color  
    ```  
  
     Queste istruzioni consentono di creare le variabili private da utilizzare per la memorizzazione dei valori delle proprietà che verranno create.  
  
3.  Sotto le dichiarazioni delle variabili del passaggio 2 inserire il seguente codice.  
  
     \[Visual Basic\]  
  
    ```  
    ' Declares the name and type of the property.  
    Property ClockBackColor() as Color  
        ' Retrieves the value of the private variable colBColor.  
        Get  
            Return colBColor  
        End Get  
        ' Stores the selected value in the private variable colBColor, and   
        ' updates the background color of the label control lblDisplay.  
        Set(ByVal value as Color)  
            colBColor = value  
            lblDisplay.BackColor = colBColor     
        End Set  
  
    End Property  
    ' Provides a similar set of instructions for the foreground color.  
    Property ClockForeColor() as Color  
        Get  
            Return colFColor  
        End Get  
        Set(ByVal value as Color)  
            colFColor = value  
            lblDisplay.ForeColor = colFColor  
        End Set  
    End Property  
    ```  
  
     Nel codice riportato in precedenza vengono create due proprietà personalizzate, `ClockForeColor` e `ClockBackColor`, disponibili agli utenti successivi del controllo mediante l'utilizzo dell'istruzione `Property`.  Le istruzioni `Get` e `Set` consentono di archiviare e recuperare il valore della proprietà e di inserire il codice per implementare le funzionalità appropriate per la proprietà.  
  
4.  Scegliere **Salva tutto** dal menu **File** per salvare il progetto.  
  
## Test del controllo  
 I controlli non sono progetti autonomi e devono pertanto essere inseriti in un contenitore.  Eseguire il test del comportamento del controllo in fase di esecuzione e sperimentare le proprietà con **UserControl Test Container**.  Per ulteriori informazioni, vedere [Procedura: eseguire il test del comportamento in fase di esecuzione di UserControl](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md).  
  
#### Per eseguire il test del controllo  
  
1.  Per compilare il progetto ed eseguire il controllo in **UserControl Test Container**, premere F5.  
  
2.  Nella griglia della proprietà di Test Container, selezionare la proprietà `ClockBackColor`, quindi fare clic sulla freccia a discesa per visualizzare la tavolozza dei colori.  
  
3.  Per scegliere un colore, fare clic su di esso.  
  
     Il colore di sfondo del controllo cambierà in base al colore selezionato.  
  
4.  Utilizzare una sequenza di eventi simile per verificare il corretto funzionamento della proprietà `ClockForeColor`.  
  
5.  Per chiudere la finestra **UserControl Test Container**, scegliere **Chiudi**.  
  
     In questa sezione e in quelle precedenti, è stato illustrato come combinare componenti e controlli Windows con codici e package per aggiungere funzionalità personalizzate al form di un controllo composito.  Si è inoltre appreso come esporre le proprietà del controllo composito e come eseguire il test del controllo dopo averlo completato.  Nella sezione successiva verranno fornite informazioni sulla modalità di creazione di un controllo composito ereditato utilizzando `ctlClock` come base.  
  
## Eredità da un controllo composito  
 Nelle sezioni precedenti si è appreso come combinare controlli, componenti e codice Windows in controlli compositi riutilizzabili.  Il controllo composito può ora essere utilizzato come base per la compilazione di altri controlli.  Il processo di derivazione di una classe da una classe di base è detto *ereditarietà*.  In questa sezione verrà creato un controllo composito denominato `ctlAlarmClock`.  Il controllo verrà derivato dal relativo controllo padre, in questo caso `ctlClock`.  Verrà spiegato come estendere le funzionalità di `ctlClock` mediante l'override dei metodi padre e l'aggiunta di nuovi metodi e proprietà.  
  
 Per creare un controllo ereditato, è innanzitutto necessario derivare il controllo dal relativo elemento padre.  Questa operazione consente di creare un nuovo controllo, con le stesse proprietà, metodi e caratteristiche grafiche del controllo padre, che può essere anche utilizzato come base per l'aggiunta di una funzionalità nuova o modificata.  
  
#### Per creare il controllo ereditato  
  
1.  In Esplora soluzioni, fare clic con il pulsante destro del mouse su **ctlClockLib**, scegliere **Aggiungi**, quindi **Controllo utente**.  
  
     Viene aperta la finestra di dialogo **Aggiungi nuovo elemento**.  
  
2.  Selezionare il modello **Controllo utente ereditato**.  
  
3.  Nella casella **Nome** digitare `ctlAlarmClock.vb`, quindi scegliere **Aggiungi**.  
  
     Viene visualizzata la finestra di dialogo **Selezione ereditarietà**.  
  
4.  In **Nome componente** fare doppio clic su **ctlClock**.  
  
5.  In Esplora soluzioni scorrere i progetti correnti.  
  
    > [!NOTE]
    >  Nel progetto corrente è stato aggiunto il file denominato **ctlAlarmClock.vb**.  
  
### Aggiunta delle proprietà per l'allarme  
 Le modalità di aggiunta delle proprietà a un controllo ereditato sono analoghe a quelle utilizzate per i controlli compositi.  Mediante la sintassi di dichiarazione delle proprietà si aggiungeranno ora al controllo due proprietà: `AlarmTime`, in cui viene memorizzato il valore della data e dell'ora in cui l'allarme deve essere disattivato, e `AlarmSet`, che indica se l'allarme è impostato o meno.  
  
##### Per aggiungere proprietà al controllo composito  
  
1.  In Esplora soluzioni, fare clic con il pulsante destro del mouse su **ctlAlarmClock**, quindi scegliere **Visualizza codice**.  
  
2.  Individuare la dichiarazione di classe per il controllo ctlAlarmClock, visualizzato come `Public Class ctlAlarmClock`.  Inserire il codice seguente nella dichiarazione di classe:  
  
     \[Visual Basic\]  
  
    ```  
    Private dteAlarmTime As Date  
    Private blnAlarmSet As Boolean  
    ' These properties will be declared as Public to allow future   
    ' developers to access them.  
    Public Property AlarmTime() As Date  
        Get  
            Return dteAlarmTime  
        End Get  
        Set(ByVal value as Date)  
            dteAlarmTime = value  
        End Set  
    End Property  
    Public Property AlarmSet() As Boolean  
        Get  
            Return blnAlarmSet  
        End Get  
        Set(ByVal value as Boolean)  
            blnAlarmSet = value  
        End Set  
    End Property  
    ```  
  
### Aggiunta di elementi all'interfaccia grafica del controllo  
 Il controllo ereditato presenta un'interfaccia grafica identica a quella del controllo dal quale eredita  e possiede gli stessi controlli costitutivi del controllo padre, ma le proprietà dei controlli costitutivi non sono disponibili, a meno che non siano state specificamente esposte.  Analogamente a qualsiasi altro controllo composito, è possibile aggiungere elementi all'interfaccia grafica di un controllo composito ereditato, utilizzando la medesima procedura.  In questo esempio verrà utilizzato un controllo label che consentirà di aggiungere un effetto intermittente alla grafica del controllo ctlAlarmClock quando l'allarme suona.  
  
##### Per aggiungere il controllo label  
  
1.  In Esplora soluzioni, fare clic con il pulsante destro del mouse su **ctlAlarmClock**, quindi scegliere **Visualizza finestra di progettazione**.  
  
     Nella finestra principale verrà aperta la finestra di progettazione per `ctlAlarmClock`.  
  
2.  Fare clic su `lblDisplay` \(parte visualizzata del controllo\) e osservare la finestra Proprietà.  
  
    > [!NOTE]
    >  Tutte le proprietà sono presenti ma inattive, ossia visualizzate in grigio.  Ciò indica che le proprietà sono native di `lblDisplay` e non è possibile accedervi né modificarle nella finestra Proprietà.  Per impostazione predefinita i controlli contenuti in un controllo composito sono `Private` e le relative proprietà non sono accessibili.  
  
    > [!NOTE]
    >  Se si desidera che gli utenti successivi del controllo composito abbiano accesso ai relativi controlli interni, dichiararli come `Public` o `Protected`.  Sarà così possibile impostare e modificare le proprietà dei controlli contenuti nel controllo composito mediante il codice appropriato.  
  
3.  Aggiungere un controllo <xref:System.Windows.Forms.Label> al controllo composito.  
  
4.  Trascinare con il mouse il controllo <xref:System.Windows.Forms.Label> ponendolo immediatamente sotto la casella di visualizzazione.  Nella finestra Proprietà impostare le proprietà seguenti.  
  
    |Proprietà|Impostazione|  
    |---------------|------------------|  
    |**Nome**|`lblAlarm`|  
    |**Text**|Alarm\!|  
    |**TextAlign**|`MiddleCenter`|  
    |**Visible**|`False`|  
  
### Aggiunta della funzionalità di allarme  
 Nelle procedure precedenti sono state aggiunte proprietà e un controllo in grado di abilitare la funzionalità di allarme nel controllo composito.  In questa procedura verrà aggiunto un codice che consente di confrontare l'ora corrente con l'ora dell'allarme e, se le ore risultano identiche, attivare un allarme sonoro e lampeggiante.  Eseguendo l'override del metodo `Timer1_Tick` di `ctlClock` e aggiungendovi ulteriore codice sarà possibile estendere le capacità di `ctlAlarmClock` e conservare allo stesso le funzionalità intrinseche di `ctlClock`.  
  
##### Per eseguire l'override del metodo Timer1\_Tick di ctlClock  
  
1.  In Esplora soluzioni, fare clic con il pulsante destro del mouse su **ctlAlarmClock.vb**, quindi scegliere **Visualizza codice**.  
  
2.  Individuare l'istruzione `Private blnAlarmSet As Boolean`.  e aggiungere subito dopo la seguente istruzione.  
  
     \[Visual Basic\]  
  
    ```  
    Dim blnColorTicker as Boolean  
    ```  
  
3.  Individuare l'istruzione `End Class` nella parte inferiore della pagina.  Prima dell'istruzione `End Class` aggiungere il seguente codice.  
  
     \[Visual Basic\]  
  
    ```  
    Protected Overrides Sub Timer1_Tick(ByVal sender As Object, ByVal e _  
        As System.EventArgs)  
        ' Calls the Timer1_Tick method of ctlClock.  
        MyBase.Timer1_Tick(sender, e)  
        ' Checks to see if the Alarm is set.  
        If AlarmSet = False Then  
            Exit Sub  
        End If  
        ' If the date, hour, and minute of the alarm time are the same as  
        ' now, flash and beep an alarm.   
        If AlarmTime.Date = Now.Date And AlarmTime.Hour = Now.Hour And _  
            AlarmTime.Minute = Now.Minute Then  
            ' Sounds an audible beep.  
            Beep()  
            ' Sets lblAlarmVisible to True, and changes the background color based on the   
            ' value of blnColorTicker. The background color of the label will   
            ' flash once per tick of the clock.  
            lblAlarm.Visible = True  
            If blnColorTicker = False Then  
                lblAlarm.BackColor = Color.PeachPuff  
                blnColorTicker = True  
            Else  
                lblAlarm.BackColor = Color.Plum  
                blnColorTicker = False  
            End If  
        Else  
            ' Once the alarm has sounded for a minute, the label is made   
            ' invisible again.  
            lblAlarm.Visible = False  
        End If  
    End Sub  
    ```  
  
     Il codice appena aggiunto ha diverse funzioni.  Se si utilizza l'istruzione `Overrides`, il controllo utilizzerà questo metodo anziché il metodo ereditato dal controllo di base.  Una volta chiamato, questo metodo chiamerà il metodo di cui esegue l'override utilizzando l'istruzione `MyBase.Timer1_Tick` e assicurando che tutte le funzionalità incorporate nel controllo originale vengano riprodotte in questo controllo.  Verrà quindi eseguito il codice aggiuntivo per incorporare la funzionalità di allarme.  Quando l'allarme viene attivato, viene visualizzato un controllo etichetta lampeggiante e viene emesso un segnale acustico.  
  
    > [!NOTE]
    >  Poiché si esegue l'override di un gestore eventi ereditato, non è necessario specificare l'evento tramite la parola chiave `Handles`.  L'evento risulta già associato.  L'override riguarda l'implementazione del gestore.  
  
     Il controllo ctlAlarmClock è quasi completo.  L'unica operazione rimasta è l'implementazione di un sistema di disattivazione.  A tal fine, è necessario aggiungere codice al metodo `lblAlarm_Click`:  
  
##### Per implementare il metodo di disattivazione dell'allarme  
  
1.  In Esplora soluzioni, fare clic con il pulsante destro del mouse su **ctlAlarmClock.vb** e scegliere **Visualizza finestra di progettazione**.  
  
2.  Nella finestra di progettazione fare doppio clic su **lblAlarm**.  Nell'**editor di codice** verrà visualizzata la riga `Private Sub lblAlarm_Click`.  
  
3.  Modificare il metodo in modo che risulti simile al seguente codice.  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub lblAlarm_Click(ByVal sender As Object, ByVal e As _  
     System.EventArgs) Handles lblAlarm.Click  
        ' Turns off the alarm.  
        AlarmSet = False  
        ' Hides the flashing label.  
        lblAlarm.Visible = False  
    End Sub  
    ```  
  
4.  Scegliere **Salva tutto** dal menu **File** per salvare il progetto.  
  
### Utilizzo del controllo ereditato in un form  
 È possibile eseguire il test del controllo ereditato esattamente come si esegue quello del controllo classe base, `ctlClock`: premere F5 per compilare il progetto ed eseguire il controllo in **UserControl Test Container**.  Per ulteriori informazioni, vedere [Procedura: eseguire il test del comportamento in fase di esecuzione di UserControl](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md).  
  
 Per utilizzare il controllo è necessario inserirlo in un form.  Come i controlli compositi standard, i controlli compositi ereditati non possono essere autonomi e devono essere inclusi in un form o in un altro contenitore.  Poiché `ctlAlarmClock` include un maggior numero di funzionalità, per eseguire il test è necessario aggiungere del codice.  In questa procedura verrà scritto un semplice programma per la verifica delle funzionalità di `ctlAlarmClock`.  Verrà inoltre scritto il codice per impostare e visualizzare la proprietà `AlarmTime` di `ctlAlarmClock` e verrà eseguito il test delle funzionalità intrinseche del controllo.  
  
##### Per compilare e aggiungere il controllo a un form di test  
  
1.  In Esplora soluzioni, fare clic con il pulsante destro del mouse su **ctlClockLib**, quindi scegliere **Compila**.  
  
2.  Scegliere **Aggiungi** dal menu **File**, quindi **Nuovo progetto**.  
  
3.  Aggiungere un nuovo progetto **Applicazione Windows** alla soluzione e denominarlo `Test`.  
  
     Il progetto **Test** verrà aggiunto a Esplora soluzioni.  
  
4.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul nodo di progetto `Test`, quindi scegliere **Aggiungi riferimento** per visualizzare la finestra di dialogo corrispondente.  
  
5.  Scegliere la scheda **Progetti**.  Il progetto **ctlClockLib** verrà elencato in **Nome progetto**.  Fare doppio clic su **ctlClockLib** per aggiungere il riferimento al progetto di test.  
  
6.  In Esplora soluzioni, fare clic con il pulsante destro del mouse su **Test** e scegliere **Compila**.  
  
7.  Nella **Casella degli strumenti** espandere il nodo **Componenti ctlClockLib**.  
  
8.  Fare doppio clic su **ctlAlarmClock** per aggiungere un'istanza di `ctlAlarmClock` al form.  
  
9. Nella **Casella degli strumenti** individuare e fare doppio clic su **DateTimePicker** per aggiungere un controllo <xref:System.Windows.Forms.DateTimePicker> al form, quindi fare doppio clic su **Etichetta** per aggiungere un controllo <xref:System.Windows.Forms.Label>.  
  
10. Posizionare mediante il mouse i controlli in un punto del form di facile accesso.  
  
11. Impostare le proprietà dei controlli come indicato di seguito.  
  
    |Controllo|Proprietà|Valore|  
    |---------------|---------------|------------|  
    |`label1`|**Text**|`(vuoto)`|  
    ||**Nome**|`lblTest`|  
    |`dateTimePicker1`|**Nome**|`dtpTest`|  
    ||**Format**|<xref:System.Windows.Forms.DateTimePickerFormat>|  
  
12. Nella finestra di progettazione fare doppio clic su **dtpTest**.  
  
     Nell'**Editor di codice** viene visualizzato `Private Sub dtpTest_ValueChanged`.  
  
13. Modificare il codice in modo che risulti simile al seguente.  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub dtpTest_ValueChanged(ByVal sender As Object, ByVal e As _  
        System.EventArgs) Handles dtpTest.ValueChanged  
        ctlAlarmClock1.AlarmTime = dtpTest.Value  
        ctlAlarmClock1.AlarmSet = True  
        lblTest.Text = "Alarm Time is " & Format(ctlAlarmClock1.AlarmTime, _  
            "hh:mm")  
    End Sub  
    ```  
  
14. In Esplora soluzioni, fare clic con il pulsante destro del mouse su **Test** e scegliere **Imposta come progetto di avvio**.  
  
15. Scegliere **Avvia debug** dal menu **Debug**.  
  
     Verrà avviato il programma di test.  Si noti che l'ora corrente viene aggiornata nel controllo `ctlAlarmClock` e che l'ora di inizio viene visualizzata nel controllo <xref:System.Windows.Forms.DateTimePicker>.  
  
16. Fare clic su <xref:System.Windows.Forms.DateTimePicker> nel punto in cui vengono visualizzati i minuti.  
  
17. Utilizzando la tastiera, impostare un valore per i minuti maggiore di un minuto rispetto all'ora corrente visualizzata da `ctlAlarmClock`.  
  
     L'ora per l'impostazione dell'allarme è visualizzata in `lblTest`.  Attendere che l'ora visualizzata raggiunga l'ora di impostazione dell'allarme.  Quando l'ora visualizzata raggiunge l'ora su cui è impostato l'allarme, verrà emesso un segnale acustico e `lblAlarm` lampeggerà.  
  
18. Disattivare l'allarme facendo clic su `lblAlarm`.  A questo punto è possibile reimpostare l'allarme.  
  
     In questa procedura dettagliata sono stati trattati diversi concetti chiave.  Si è appreso come creare un controllo composito combinando controlli e componenti in un contenitore controllo composito e  come aggiungere proprietà al controllo e scrivere il codice per l'implementazione di funzionalità personalizzate.  Nell'ultima sezione sono state illustrate l'estensione delle funzionalità di uno specifico controllo composito mediante ereditarietà e la modifica delle funzionalità dei metodi host mediante override.  
  
## Vedere anche  
 [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)   
 [Procedura: modificare controlli compositi](../../../../docs/framework/winforms/controls/how-to-author-composite-controls.md)   
 [Procedura: visualizzare un controllo nella finestra di dialogo Scegli elementi della Casella degli strumenti](../../../../docs/framework/winforms/controls/how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)   
 [Component Authoring Walkthroughs](../Topic/Component%20Authoring%20Walkthroughs.md)