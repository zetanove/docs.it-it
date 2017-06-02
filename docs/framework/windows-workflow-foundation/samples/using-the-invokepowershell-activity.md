---
title: "Utilizzo dell&#39;attivit&#224; InvokePowerShell | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 956251a0-31ca-4183-bf76-d277c08585df
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Utilizzo dell&#39;attivit&#224; InvokePowerShell
Nell'esempio InvokePowerShell viene illustrato come richiamare i comandi di Windows PowerShell utilizzando l'attività `InvokePowerShell`.  
  
## Dimostrazione  
  
-   Semplice innovazione dei comandi di Windows PowerShell.  
  
-   Recupero di valori dalla pipeline di output di Windows PowerShell e relativa archiviazione nelle variabili del flusso di lavoro.  
  
-   Passaggio di dati in Windows PowerShell come pipeline di input per un comando di esecuzione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\PowerShell`  
  
## Discussione  
 In questo esempio sono contenuti i tre progetti seguenti.  
  
|Nome progetto|Descrizione|File principali|  
|-------------------|-----------------|---------------------|  
|CodedClient|Applicazione client di esempio che utilizza l'attività PowerShell.|-   **Program.cs**: crea, a livello di codice, un flusso di lavoro basato su sequenze che chiama l'attività InvokePowerShell.|  
|DesignerClient|Set di attività personalizzate che contengono l'attività personalizzata `InvokePowerShell` e altre varie attività personalizzate, nonché un flusso di lavoro che le utilizza.|<ul><li>Attività:<br /><br /> <ul><li>**PrintCollection.cs**: attività di supporto che stampa tutti gli elementi di una raccolta nella console.</li><li>**ReadLine.cs**: attività di supporto per la lettura di input dalla console.</li></ul></li><li>File system:<br /><br /> <ul><li>**Copy.xaml**: attività che copia un file.</li><li>**CreateFile.xaml**: attività che crea un file.</li><li>**DeleteFile.xaml**: attività che elimina un file.</li><li>**MakeDir.xaml**: attività che crea una directory.</li><li>**Move.xaml**: attività che sposta un file.</li><li>**ReadFile.xaml**: attività che legge un file e restituisce il relativo contenuto.</li><li>**TestPath.xaml**: attività che verifica l'esistenza di un percorso.</li></ul></li><li>Processo:<br /><br /> <ul><li>**GetProcess.xaml**: attività che ottiene un elenco dei processi in esecuzione.</li><li>**StopProcess.xaml**: attività che interrompe un processo specifico.</li></ul></li><li>**Program.cs**: chiama il flusso di lavoro Sequence1.</li><li>**Sequence1.xaml**: flusso di lavoro basato su sequenze.</li></ul>|  
|PowerShell|Attività `InvokePowerShell` e finestre di progettazione associate.|File di attività<br /><br /> -   **ExecutePowerShell.cs**: logica di esecuzione principale dell'attività.<br />-   **InvokePowerShell.cs**: wrapper della logica di esecuzione principale che contiene una versione generica \(valore restituito\) e una versione non generica \(valore non restituito\).Si tratta dell'interfaccia pubblica per l'attività.<br />-   **NoPersistZone.cs**: questa attività impedisce la persistenza di qualsiasi attività figlio.Questa classe viene utilizzata all'interno dell'implementazione dell'attività `InvokePowerShell` per evitare che l'attività venga resa persistente a metà esecuzione.<br /><br /> File delle finestre di progettazione:<br /><br /> 1.  **ArgumentDictionaryEditor.cs**: finestra di dialogo di Windows che consente all'utente di modificare gli argomenti dell'attività `InvokePowerShell`.<br />2.  **GenericInvokePowerShellDesigner.xaml** e **GenericInvokePowerShellDesigner.xaml.cs**: definiscono l'aspetto dell'attività `InvokePowerShell` generica in [!INCLUDE[wfd2](../../../../includes/wfd2-md.md)].<br />3.  **InvokePowerShellDesigner.xaml** e **InvokePowerShellDesigner.cs**: definiscono l'aspetto dell'attività `InvokePowerShell` non generica in [!INCLUDE[wfd2](../../../../includes/wfd2-md.md)].|  
  
 I progetti client vengono discussi per primi, poiché è più semplice capire la funzionalità interna dell'attività PowerShell una volta capito il relativo utilizzo.  
  
## Utilizzo dell'esempio  
 Nelle sezioni seguenti viene descritto come utilizzare i tre progetti dell'esempio.  
  
### Utilizzo del progetto CodedClient  
 Il client di esempio crea a livello di codice un'attività Sequence che contiene esempi di diversi metodi di utilizzo dell'attività `InvokePowerShell`.La prima chiamata avvia il Blocco note.  
  
```  
new InvokePowerShell()  
{  
    CommandText = "notepad"  
},  
  
```  
  
 La seconda chiamata ottiene un elenco dei processi in esecuzione nel computer locale.  
  
```  
new InvokePowerShell<Process>()  
{  
    CommandText = "Get-Process",  
    Output = processes1,  
},  
  
```  
  
 `Output` è la variabile utilizzata per archiviare l'output del comando.  
  
 La chiamata successiva mostra come eseguire un passaggio della post\-elaborazione in ogni singolo output della chiamata di PowerShell.`InitializationAction` viene impostato sulla funzione che restituisce una rappresentazione in forma di stringa per ogni processo.La raccolta di queste stringhe viene restituita nella variabile `Output` dall'attività `InvokePowerShell<string>`.  
  
 Le chiamate `InvokePowerShell` successive dimostrano il passaggio di dati nell'attività e la restituzione di output ed errori.  
  
### Utilizzo del progetto DesignerClient  
 Il progetto DesignerClient è costituito da un set di attività personalizzate, di cui gran parte è stata compilata con l'attività `InvokePowerShell`.La maggior parte delle attività chiama la versione non generica dell'attività `InvokePowerShell` e non prevede un valore restituito.Le altre attività utilizzano la versione generica dell'attività `InvokePowerShell` e l'argomento `InitializationAction` per elaborare i risultati in un secondo momento.  
  
## Utilizzo del progetto PowerShell  
 L'azione principale dell'attività si verifica nella classe `ExecutePowerShell`.Poiché l'esecuzione dei comandi di PowerShell non deve bloccare il thread del flusso di lavoro principale, l'attività viene creata in modo da essere un'attività asincrona ereditando dalla classe <xref:System.Activities.AsyncCodeActivity>.  
  
 Il metodo <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> viene chiamato dall'esecuzione del flusso di lavoro per iniziare l'esecuzione dell'attività.Inizia chiamando le API di PowerShell per creare una pipeline di PowerShell.  
  
```  
runspace = RunspaceFactory.CreateRunspace();  
runspace.Open();  
pipeline = runspace.CreatePipeline();  
  
```  
  
 Successivamente crea un comando di PowerShell e lo popola con parametri e variabili.  
  
```  
Command cmd = new Command(this.CommandText, this.IsScript);   
// loop over parameters and run: cmd.Parameters.Add(...)  
// loop over variables and run: runspace.SessionStateProxy.SetVariable(...)  
pipeline.Commands.Add(cmd);  
  
```  
  
 A questo punto, gli input inoltrati tramite pipe vengono inviati anche alla pipeline.Infine, la pipeline viene sottoposta a wrapping in un oggetto `PipelineInvokerAsyncResult` e restituita.L'oggetto `PipelineInvokerAsyncResult` registra un listener e richiama la pipeline.  
  
```  
pipeline.InvokeAsync();  
  
```  
  
 Al termine dell'esecuzione, gli output e gli errori vengono archiviati all'interno dello stesso oggetto `PipelineInvokerAsyncResult` e il controllo viene restituito all'esecuzione del flusso di lavoro chiamando il metodo di callback passato originariamente al metodo <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A>.  
  
 Alla fine dell'esecuzione del metodo, l'esecuzione del flusso di lavoro chiama il metodo <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> dell'attività.  
  
 La classe `InvokePowerShell` esegue il wrapping della classe `ExecutePowerShellCommand` e crea due versioni dell'attività: una generica e una non generica.La versione non generica restituisce direttamente l'output dell'esecuzione di PowerShell, mentre la versione generica trasforma i singoli risultati nel tipo generico.  
  
 La versione generica dell'attività viene implementata come un flusso di lavoro sequenziale che chiama l'oggetto `ExecutePowerShellCommand` ed elabora i risultati in un secondo momento.Per ogni elemento nella raccolta di risultati, la fase di post\-elaborazione chiama l'oggetto `InitializationAction` se impostato.In caso contrario, esegue un semplice cast.  
  
```  
new ForEach<PSObject>  
{  
    Values = psObjects,  
    Body = new ActivityAction<PSObject>  
    {  
        Argument = psObject,  
        Handler = new Sequence  
        {  
            Activities =  
            {  
                new If  
                {  
                    Condition = // Is InitializationAction set?  
                    Then = new InvokeFunc<PSObject, TResult>  
                    {  
                        Argument = psObject,  
                        Result = outputObject,  
                        Func = this.InitializationAction  
                    },  
                    Else = new Assign<TResult>  
                    {  
                        To = outputObject,  
                        Value = new InArgument<TResult>(ctx => (TResult) psObject.Get(ctx).BaseObject),  
                    }  
                },  
                new AddToCollection<TResult>  
                {  
                    Collection = outputObjects,  
                    Item = outputObject  
                },  
            }  
        }  
    }  
},  
  
```  
  
 Per ognuna delle due attività `InvokePowerShell` \(generica e non generica\), è stata creata una finestra di progettazione.InvokePowerShellDesigner.xaml e il file con estensione cs associato definiscono l'aspetto in [!INCLUDE[wfd2](../../../../includes/wfd2-md.md)] per la versione non generica dell'attività `InvokePowerShell`.In InvokePowerShellDesigner.xaml, viene utilizzato un oggetto <xref:System.Windows.Controls.DockPanel> per rappresentare l'interfaccia grafica.  
  
```  
<DockPanel x:Uid="DockPanel_1" LastChildFill="True">  
        <TextBlock x:Uid="TextBlock_1" Text="CommandText" />  
        <TextBox x:Uid="TextBox_1" Text="{Binding Path=ModelItem.CommandText, Mode=TwoWay}"  
                 TextWrapping="WrapWithOverflow"  AcceptsReturn="True" MinLines="4" MaxLines="4"  
                 Background="{x:Null}" Margin="3" />  
    </DockPanel>  
  
```  
  
 Si noti che la proprietà `Text` della casella di testo è un'associazione bidirezionale che assicura che il valore della proprietà `CommandText` dell'attività sia equivalente al valore inserito nella finestra di progettazione.  
  
 GenericInvokePowerShellDesigner.xaml e il file con estensione cs associato definiscono l'interfaccia grafica per l'attività `InvokePowerShell` generica.La finestra di progettazione è leggermente più complessa perché consente agli utenti di impostare un oggetto `InitializationAction`.L'elemento principale è l'utilizzo dell'oggetto <xref:System.Activities.Presentation.WorkflowItemPresenter> per consentire il trascinamento delle attività figlio nell'area di progettazione di `InvokePowerShell`.  
  
```  
<sap:WorkflowItemPresenter x:Uid="sap:WorkflowItemPresenter_1" Margin="0,10,0,10"  
    HintText="Drop Activities Here"  
    AllowedItemType="{x:Type sa:Activity}"  
    Item="{Binding Path=ModelItem.InitializationAction.Handler, Mode=TwoWay}"  
    Grid.Row="1" Grid.Column="1" />  
  
```  
  
 La personalizzazione della finestra di progettazione non termina con i file con estensione xaml che definiscono l'aspetto dell'attività nell'area di disegno della progettazione.Anche le finestre di dialogo utilizzate per visualizzare i parametri dell'attività possono essere personalizzate.Questi parametri e le variabili PowerShell influiscono sul comportamento dei comandi di PowerShell.L'attività li espone come tipi <xref:System.Collections.Generic.Dictionary%601>.ArgumentDictionaryEditor.cs, PropertyEditorResources.xaml e PropertyEditorResources.cs definiscono la finestra di dialogo che consente di modificare questi tipi.  
  
## Per impostare, compilare ed eseguire l'esempio  
 È necessario installare Windows PowerShell per eseguire questo esempio.Windows PowerShell può essere installato da questo percorso: [Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=150383).  
  
#### Per eseguire il progetto CodedClient  
  
1.  Aprire PowerShell.sln tramite [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse sulla soluzione e compilarla.  
  
3.  Fare clic con il pulsante destro del mouse sul progetto **CodedClient** e selezionare **Imposta come progetto di avvio**.  
  
4.  Premere CTRL\+F5 per eseguire l'applicazione.  
  
#### Per eseguire il progetto DesignerClient  
  
1.  Aprire PowerShell.sln tramite [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse sulla soluzione e compilarla.  
  
3.  Fare clic con il pulsante destro del mouse sul progetto **DesignerClient** e selezionare **Imposta come progetto di avvio**.  
  
4.  Premere CTRL\+F5 per eseguire l'applicazione.  
  
## Problemi noti  
  
1.  Se si fa riferimento all'assembly o al progetto di attività `InvokePowerShell` da un altro progetto si verifica un errore di compilazione, pertanto potrebbe essere necessario aggiungere manualmente l'elemento `<SpecificVersion>True</SpecificVersion>` al file con estensione csproj del nuovo progetto sotto la riga che fa riferimento a `InvokePowerShell`.  
  
2.  Se Windows PowerShell non è installato, il seguente messaggio di errore viene visualizzato in Visual Studio non appena si aggiunge un'attività `InvokePowerShell` in un flusso di lavoro: `Progettazione flussi di lavoro ha riscontrato problemi con il documento. Impossibile caricare il file o l'assembly 'System.Management.Automation'... o una delle sue dipendenze. Il sistema non riesce a trovare il file specificato.`  
  
3.  In Windows PowerShell 2.0, la chiamata a livello di codice di `$input.MoveNext()` non viene eseguita correttamente e gli script che utilizzano `$input.MoveNext()` generano errori e risultati imprevisti.Per risolvere questo problema, utilizzare il verbo PowerShell `foreach` anziché chiamare `MoveNext()` quando si scorre una matrice.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\PowerShell`  
  
## Vedere anche