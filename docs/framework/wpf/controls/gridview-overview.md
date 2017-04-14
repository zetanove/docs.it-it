---
title: "Cenni preliminari su GridView | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "controlli, ListView"
  - "GridView (modalità di visualizzazione)"
  - "ListView (controlli), GridView (modalità di visualizzazione)"
ms.assetid: b2d02267-32b3-40ce-8e9f-06972d8749d9
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# Cenni preliminari su GridView
La modalità di visualizzazione <xref:System.Windows.Controls.GridView> rappresenta una delle modalità di visualizzazione di un controllo <xref:System.Windows.Controls.ListView>.  La classe <xref:System.Windows.Controls.GridView> e le relative classi di supporto consentono agli utenti di visualizzare raccolte di elementi in una tabella che utilizza in genere i pulsanti come intestazioni di colonna interattive.  In questo argomento viene presentata la classe <xref:System.Windows.Controls.GridView> e ne viene definito l'utilizzo.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="DefiningaListViewthatusesGridViewView"></a>   
## Definizione di visualizzazione GridView  
 La modalità di visualizzazione <xref:System.Windows.Controls.GridView> consente di elencare gli elementi dei dati associando i campi dati alle colonne e visualizzando un'intestazione di colonna che identifichi il campo.  Lo stile <xref:System.Windows.Controls.GridView> predefinito implementa i pulsanti come intestazioni di colonna.  Utilizzando i pulsanti per le intestazioni di colonna, è possibile implementare importanti funzionalità di interazione dell'utente; ad esempio, gli utenti possono fare clic sull'intestazione della colonna per ordinare i dati <xref:System.Windows.Controls.GridView> in base al contenuto di una specifica colonna.  
  
> [!NOTE]
>  Il pulsante consente di controllare che gli utilizzi di <xref:System.Windows.Controls.GridView> per le intestazioni di colonna siano derivati da <xref:System.Windows.Controls.Primitives.ButtonBase>.  
  
 Nell'immagine seguente viene mostrata una visualizzazione <xref:System.Windows.Controls.GridView> del contenuto di <xref:System.Windows.Controls.ListView>.  
  
 **Visualizzazione GridView del contenuto di ListView**  
  
 ![ListView con stile](../../../../docs/framework/wpf/controls/media/styledlistview.png "StyledListView")  
  
 Le colonne <xref:System.Windows.Controls.GridView> sono rappresentate da oggetti <xref:System.Windows.Controls.GridViewColumn> che è possibile ridimensionare automaticamente in base al contenuto.  Se si desidera, è possibile impostare in modo esplicito un oggetto <xref:System.Windows.Controls.GridViewColumn> su una larghezza specifica.  È possibile ridimensionare le colonne trascinando la barra gripper tra le intestazioni di colonna.  È possibile inoltre aggiungere in modo dinamico, rimuovere, sostituire e riordinare le colonne, dal momento che tali funzionalità sono incorporate in <xref:System.Windows.Controls.GridView>.  Tuttavia, <xref:System.Windows.Controls.GridView> non è in grado di aggiornare direttamente i dati visualizzati.  
  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.Controls.GridView> in cui vengono visualizzati i dati dei dipendenti.  In questo esempio, <xref:System.Windows.Controls.ListView> definisce l'oggetto `EmployeeInfoDataSource` come <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>.  Le definizioni delle proprietà di <xref:System.Windows.Controls.GridViewColumn> associano il contenuto <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> alle categorie di dati `EmployeeInfoDataSource`.  
  
 [!code-xml[ListViewCode#ListViewEmployee](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#listviewemployee)]  
  
 Nella figura seguente viene mostrata la tabella creata nell'esempio precedente.  
  
 **Visualizzazione GridView dei dati provenienti da ItemsSource**  
  
 ![ListView con output GridView](../../../../docs/framework/wpf/controls/media/listviewgridview.png "ListViewGridView")  
  
<a name="GridViewLayoutandStyle"></a>   
## Layout e stile di una GridView  
 Le celle e l'intestazione delle colonne di un oggetto <xref:System.Windows.Controls.GridViewColumn> hanno la stessa larghezza.  Per impostazione predefinita, la larghezza di ogni colonna viene ridimensionata in base al contenuto.  Se lo si desidera, è possibile impostare una colonna su una larghezza fissa.  
  
 Il contenuto dei dati correlati viene visualizzato nelle righe orizzontali.  Ad esempio, nell'illustrazione precedente, il cognome, il nome e il numero ID di ciascun dipendente vengono visualizzati come un insieme, poiché sono disposti su una riga orizzontale.  
  
<a name="DefiningandStylingColumnsinaGridView"></a>   
### Definizione e applicazione di stili alle colonne in una GridView  
 Nella definizione del campo dati da visualizzare in un oggetto <xref:System.Windows.Controls.GridViewColumn>, utilizzare le proprietà <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A>, <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> o <xref:System.Windows.Controls.GridViewColumn.CellTemplateSelector%2A>.  La proprietà <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> ha la precedenza sulle proprietà dei modelli.  
  
 Per specificare l'allineamento del contenuto in una colonna di un oggetto <xref:System.Windows.Controls.GridView>, definire una proprietà <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A>.  Non utilizzare le proprietà <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> e <xref:System.Windows.Controls.Control.VerticalContentAlignment%2A> per il contenuto <xref:System.Windows.Controls.ListView> visualizzato utilizzando un oggetto <xref:System.Windows.Controls.GridView>.  
  
 Per specificare le proprietà di modello e stile per le intestazioni di colonna, utilizzare le classi <xref:System.Windows.Controls.GridView>, <xref:System.Windows.Controls.GridViewColumn> e <xref:System.Windows.Controls.GridViewColumnHeader>.  Per ulteriori informazioni, vedere [Panoramica sui modelli e sugli stili di intestazione delle colonne in GridView](../../../../docs/framework/wpf/controls/gridview-column-header-styles-and-templates-overview.md).  
  
<a name="AddingVisualElementstoaGridViewView"></a>   
### Aggiunta di elementi visivi a una GridView  
 Per aggiungere elementi visivi, ad esempio i controlli <xref:System.Windows.Controls.CheckBox> e <xref:System.Windows.Controls.Button>, a una modalità di visualizzazione <xref:System.Windows.Controls.GridView>, utilizzare i modelli o gli stili.  
  
 Se si definisce in modo esplicito un elemento visivo come elemento dei dati, sarà possibile visualizzarlo solo una volta in un oggetto <xref:System.Windows.Controls.GridView>.  Questa limitazione è dovuta al fatto che un elemento può avere un solo elemento padre e pertanto potrà essere visualizzato solo una volta nella [struttura ad albero visuale](GTMT).  
  
<a name="StylingRowsinaGridViewView"></a>   
### Applicazione di stili alle righe in una GridView  
 Utilizzare le classi <xref:System.Windows.Controls.GridViewRowPresenter> e <xref:System.Windows.Controls.GridViewHeaderRowPresenter> per formattare e visualizzare le righe di un oggetto <xref:System.Windows.Controls.GridView>.  Per un esempio della procedura di applicazione di stili alle righe in una modalità di visualizzazione <xref:System.Windows.Controls.GridView>, vedere [Applicare uno stile a una riga in un ListView che implementa una GridView](../../../../docs/framework/wpf/controls/how-to-style-a-row-in-a-listview-that-implements-a-gridview.md).  
  
<a name="AlignmentIssuesWhenUsingItemContainerStyle"></a>   
### Problemi di allineamento durante l'utilizzo di ItemContainerStyle  
 Per evitare problemi di allineamento tra le intestazioni di colonna e le celle, non impostare una proprietà o specificare un modello che incida sulla larghezza di un elemento in un oggetto <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>.  Ad esempio, non impostare la proprietà <xref:System.Windows.FrameworkElement.Margin%2A> o specificare un oggetto <xref:System.Windows.Controls.ControlTemplate> che aggiunge un oggetto <xref:System.Windows.Controls.CheckBox> a un elemento <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> definito in un controllo <xref:System.Windows.Controls.ListView>.  Specificare invece le proprietà e i modelli che incidono direttamente sulla larghezza delle colonne nelle classi che definiscono una modalità di visualizzazione <xref:System.Windows.Controls.GridView>.  
  
 Ad esempio, per aggiungere un oggetto <xref:System.Windows.Controls.CheckBox> alle righe nella modalità di visualizzazione <xref:System.Windows.Controls.GridView>, aggiungere l'oggetto <xref:System.Windows.Controls.CheckBox> a un oggetto <xref:System.Windows.DataTemplate> e impostare quindi la proprietà <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> su tale oggetto <xref:System.Windows.DataTemplate>.  
  
<a name="InteractingwithaGridViewControl"></a>   
## Interazioni dell'utente con una GridView  
 Quando si utilizza un oggetto <xref:System.Windows.Controls.GridView> nell'applicazione, gli utenti possono interagire con l'oggetto <xref:System.Windows.Controls.GridView> e modificarne la formattazione.  Possono, ad esempio, riordinare le colonne, ridimensionare una colonna, selezionare gli elementi di una tabella e scorrere il contenuto.  È anche possibile definire un gestore eventi che risponda quando un utente fa clic sul pulsante dell'intestazione di colonna.  Il gestore eventi può eseguire operazioni quali l'ordinamento dei dati visualizzati nell'oggetto <xref:System.Windows.Controls.GridView> in base al contenuto di una colonna.  
  
 Nell'elenco seguente vengono analizzate più dettagliatamente le funzionalità offerte dall'utilizzo di <xref:System.Windows.Controls.GridView> in relazione all'interazione dell'utente:  
  
-   **Riordinare le colonne con il metodo di trascinamento della selezione.**  
  
     Gli utenti possono riordinare le colonne in un oggetto <xref:System.Windows.Controls.GridView> premendo il pulsante sinistro del mouse quando è posizionato su un'intestazione di colonna e trascinando quindi quella colonna in una nuova posizione.  Mentre l'utente trascina l'intestazione di colonna, viene visualizzata una versione mobile dell'intestazione, nonché una linea nera continua che indica dove inserire la colonna.  
  
     Se si desidera modificare lo stile predefinito per la versione mobile di un'intestazione, specificare un oggetto <xref:System.Windows.Controls.ControlTemplate> per un tipo <xref:System.Windows.Controls.GridViewColumnHeader> che viene attivato quando la proprietà <xref:System.Windows.Controls.GridViewColumnHeader.Role%2A> è impostata su <xref:System.Windows.Controls.GridViewColumnHeaderRole>.  Per ulteriori informazioni, vedere [Creare uno stile per un'intestazione di colonna GridView trascinata](../../../../docs/framework/wpf/controls/how-to-create-a-style-for-a-dragged-gridview-column-header.md).  
  
-   **Ridimensionare una colonna in base al contenuto.**  
  
     Gli utenti possono fare doppio clic sulla barra gripper a destra di un'intestazione di colonna per adattare le dimensioni di una colonna al relativo contenuto.  
  
    > [!NOTE]
    >  È possibile impostare la proprietà <xref:System.Windows.Controls.GridViewColumn.Width%2A> su `Double.NaN` per ottenere lo stesso risultato.  
  
-   **Selezionare gli elementi di una riga.**  
  
     Gli utenti possono selezionare uno o più elementi di un oggetto <xref:System.Windows.Controls.GridView>.  
  
     Se si desidera modificare lo <xref:System.Windows.Style> di un elemento selezionato, vedere [Utilizzare i trigger per applicare uno stile agli elementi selezionati in un controllo ListView](../../../../docs/framework/wpf/controls/how-to-use-triggers-to-style-selected-items-in-a-listview.md).  
  
-   **Scorrere il contenuto per visualizzare gli elementi inizialmente non visibili sullo schermo.**  
  
     Se le dimensioni dell'oggetto <xref:System.Windows.Controls.GridView> non sono abbastanza ampie da visualizzare tutti gli elementi, gli utenti possono scorrere in senso orizzontale o verticale utilizzando le barre di scorrimento, fornite da un controllo <xref:System.Windows.Controls.ScrollViewer>.  Un oggetto <xref:System.Windows.Controls.Primitives.ScrollBar> viene nascosto se tutto il contenuto è visibile in una direzione specifica.  Le intestazioni di colonna non scorrono mediante una barra di scorrimento verticale, ma scorrono in senso orizzontale.  
  
-   **Interagire con le colonne facendo clic sui pulsanti delle intestazioni di colonna.**  
  
     Quando gli utenti fanno clic su un pulsante dell'intestazione di colonna, possono ordinare i dati visualizzati nella colonna, se è stato fornito un algoritmo di ordinamento.  
  
     È possibile gestire l'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> per i pulsanti dell'intestazione di colonna in modo da rendere disponibili funzionalità quali un algoritmo di ordinamento.  Per gestire l'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> per una singola intestazione di colonna, impostare un gestore eventi su <xref:System.Windows.Controls.GridViewColumnHeader>.  Per impostare un gestore eventi in modo che gestisca l'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> per tutte le intestazioni di colonna, specificare per tale gestore il controllo <xref:System.Windows.Controls.ListView>.  
  
<a name="Obtaining_Other_Custom_Views"></a>   
## Come ottenere altre visualizzazioni personalizzate  
 La classe <xref:System.Windows.Controls.GridView>, derivata dalla classe astratta <xref:System.Windows.Controls.ViewBase>, rappresenta solo una delle possibili modalità di visualizzazione della classe <xref:System.Windows.Controls.ListView>.  È possibile creare altre visualizzazioni personalizzate per <xref:System.Windows.Controls.ListView> derivandole dalla classe <xref:System.Windows.Controls.ViewBase>.  Per un esempio di una modalità di visualizzazione personalizzata, vedere [Creare una modalità di visualizzazione personalizzata per un oggetto ListView](../../../../docs/framework/wpf/controls/how-to-create-a-custom-view-mode-for-a-listview.md).  
  
<a name="GridViewSupportingClasses"></a>   
## Classi che supportano GridView  
 Le classi seguenti supportano la modalità di visualizzazione <xref:System.Windows.Controls.GridView>.  
  
-   <xref:System.Windows.Controls.GridViewColumn>  
  
-   <xref:System.Windows.Controls.GridViewColumnHeader>  
  
-   <xref:System.Windows.Controls.GridViewRowPresenter>  
  
-   <xref:System.Windows.Controls.GridViewHeaderRowPresenter>  
  
-   <xref:System.Windows.Controls.GridViewColumnCollection>  
  
-   <xref:System.Windows.Controls.GridViewColumnHeaderRole>  
  
## Vedere anche  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.ListViewItem>   
 <xref:System.Windows.Controls.GridViewColumn>   
 <xref:System.Windows.Controls.GridViewColumnHeader>   
 <xref:System.Windows.Controls.GridViewRowPresenter>   
 <xref:System.Windows.Controls.GridViewHeaderRowPresenter>   
 <xref:System.Windows.Controls.ViewBase>   
 [Panoramica sul controllo ListView](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [Ordinare una colonna GridView quando si fa clic su un'intestazione](../../../../docs/framework/wpf/controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)