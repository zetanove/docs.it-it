---
title: "Associazione dati in un client Windows Presentation Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bb8c8293-5973-4aef-9b07-afeff5d3293c
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Associazione dati in un client Windows Presentation Foundation
In questo esempio viene illustrato come usare un'associazione dati in un client Windows Presentation Foundation \(WPF\).  L'esempio usa un servizio di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] che genera casualmente una matrice di album da restituire al client.  Ogni album è dotato di un nome, di un prezzo e di un elenco di tracce.  Le tracce dell'album sono dotate di un nome e di una durata.  Le informazioni restituite dal servizio vengono associate automaticamente all'interfaccia utente fornita dal client [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)].  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 L'associazione dati fa sì che un'origine dati venga associata automaticamente a un'interfaccia utente.  Questa operazione semplifica il modello di programmazione, perché non richiede che ogni elemento dell'interfaccia utente venga aggiornato a livello di programmazione con i dati da un oggetto dati o da una matrice di oggetti dati.  È possibile associare un oggetto a un singolo elemento dell'interfaccia utente oppure una matrice a un controllo che accetta più input, ad esempio un oggetto `ListBox`.  Nell'esempio di codice seguente viene illustrato come associare i dati al `DataContext` di un elemento dell'interfaccia utente.  
  
```  
// Event handler executed when call is complete  
void client_GetAlbumListCompleted(object sender, GetAlbumListCompletedEventArgs e)  
{  
    // This is on the UI thread, myPanel can be accessed directly  
    myPanel.DataContext = e.Result;   
}  
  
```  
  
 Nell'esempio precedente, il `DataContext` per l'elemento del layout `grid` denominato `myPanel` viene impostato sui dati restituiti dal metodo `GetAlbumList`.  Il `DataContext` consente agli elementi di ereditare informazioni dagli elementi padre sull'origine dati usata per l'associazione e su altre caratteristiche dell'associazione, ad esempio il percorso.  La riga di codice deve essere eseguita ogni volta che i dati nel server vengono aggiornati.  Ad esempio, viene eseguita quando viene avviata la finestra e quando viene aggiunto un nuovo album.  
  
 Nell'esempio di codice XAML seguente, il `ListBox` specifica `ItemsSource="{Binding }"`.  
  
```  
<ListBox   
          ItemTemplate="{StaticResource AlbumStyle}"  
          ItemsSource="{Binding }"   
          IsSynchronizedWithCurrentItem="true" />  
  
```  
  
 In questo modo specifica che i dati associati all'elemento dell'interfaccia utente di livello superiore venga associato anche a questo controllo \(ovvero, la matrice di album\).  `ItemTemplate="{StaticResource AlbumStyle}"` specifica inoltre il modello di dati da usare per ogni elemento in `ListBox`.  È inoltre possibile definire modelli di dati per specificare come formattare i dati.  Questi modelli di dati possono essere riusati per altri elementi dell'interfaccia utente dell'applicazione. Il vantaggio è che il modello di dati viene definito e gestito in un solo posto.  
  
 Il modello di dati `AlbumStyle` crea una griglia con due `TextBlock`, uno accanto all'altro.  Uno specifica il nome dell'album e l'altro il numero di tracce contenute nell'album.  
  
```  
<DataTemplate x:Key="AlbumStyle">  
    <Grid>  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition Width="260" />  
            <ColumnDefinition Width="60" />  
        </Grid.ColumnDefinitions>  
        <TextBlock Grid.Column="0" TextContent="{Binding Path=Title}" />  
        <TextBlock Grid.Column="1" TextContent="{Binding Path=Tracks#.Count}" HorizontalAlignment="Right" />  
    </Grid>  
</DataTemplate>  
  
```  
  
 Il codice XAML seguente crea un secondo `ListBox`.  
  
```  
<ListBox Grid.Row="2"   
            Grid.ColumnSpan="2"   
            ItemTemplate="{StaticResource TrackStyle}"  
            ItemsSource="{Binding Path=Tracks}" />  
  
```  
  
 Il codice specifica un percorso per `ItemsSource`.  Questo indica che i dati associati a questo controllo non sono i dati di livello superiore, ma una proprietà dei dati di livello superiore denominata `Tracks`.  Questa proprietà rappresenta la matrice di tracce contenute all'interno dell'album.  Viene inoltre specificato un `DataTemplate` diverso, denominato `TrackStyle`.  Il layout del modello `TrackStyle` è simile a quello del modello `AlbumStyle`, ma i `TextBlock` sono associati a proprietà diverse.  Questo succede perché i due modelli vengono usati con oggetti dati diversi.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Scenario\DataBinding\WPFDataBinding`  
  
## Vedere anche