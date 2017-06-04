---
title: "Opzioni di ridimensionamento nel controllo DataGrid | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ridimensionamento automatico di DataGrid"
  - "DataGrid (controllo) [WPF], ridimensionamento"
  - "ridimensionamento [WPF], DataGrid"
ms.assetid: 96a0e47e-b010-4302-98ef-2daac446d8db
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Opzioni di ridimensionamento nel controllo DataGrid
Sono disponibili varie opzioni per controllare il ridimensionamento di <xref:System.Windows.Controls.DataGrid>.  È possibile impostare il controllo <xref:System.Windows.Controls.DataGrid> e le singole righe e colonne in <xref:System.Windows.Controls.DataGrid> in modo da essere ridimensionati automaticamente in base al contenuto o è possibile impostarli su valori specifici.  Per impostazione predefinita, le dimensioni del controllo <xref:System.Windows.Controls.DataGrid> vengono aumentate e ridotte per adattarsi alle dimensioni del relativo contenuto.  
  
## Ridimensionamento di DataGrid  
  
### Utilizzo del ridimensionamento automatico  
 Per impostazione predefinita, le proprietà <xref:System.Windows.FrameworkElement.Height%2A> e <xref:System.Windows.FrameworkElement.Width%2A> di <xref:System.Windows.Controls.DataGrid> sono impostate su <xref:System.Double.NaN?displayProperty=fullName> \("`Auto`" in XAML\) in modo da regolare le dimensioni del controllo <xref:System.Windows.Controls.DataGrid> in base al contenuto.  
  
 Quando inserito in un contenitore che non limita le dimensioni degli elementi figli, ad esempio <xref:System.Windows.Controls.Canvas> o <xref:System.Windows.Controls.StackPanel>, il controllo <xref:System.Windows.Controls.DataGrid> si estenderà oltre i limiti visibili del contenitore e non verranno visualizzate le barre di scorrimento.  Questa condizione ha implicazioni sia sull'usabilità che sulle prestazioni.  
  
 Quando associato a un set di dati, se per la proprietà <xref:System.Windows.FrameworkElement.Height%2A> del controllo <xref:System.Windows.Controls.DataGrid> non è impostata alcuna limitazione, verrà aggiunta una riga per ogni elemento di dati nel dataset associato.  In questo modo, con l'aggiunta delle righe, le dimensioni del controllo <xref:System.Windows.Controls.DataGrid> possono estendersi oltre i limiti visibili dell'applicazione.  In questo caso non vengono visualizzate le barre di scorrimento di <xref:System.Windows.Controls.DataGrid> poiché la proprietà <xref:System.Windows.FrameworkElement.Height%2A> continuerà ad aumentare per includere le nuove righe.  
  
 Per ogni nuova riga viene creato un oggetto in <xref:System.Windows.Controls.DataGrid>.  Se si utilizza un set di dati di grandi dimensioni e si attiva il ridimensionamento automatico di <xref:System.Windows.Controls.DataGrid>, la creazione di un gran numero di oggetti può influire sulle prestazioni dell'applicazione.  
  
 Per evitare questi problemi quando si utilizzano set di dati di grandi dimensioni, è consigliabile impostare la proprietà <xref:System.Windows.FrameworkElement.Height%2A> di <xref:System.Windows.Controls.DataGrid> in modo specifico o posizionare il controllo in un contenitore in cui sono previste limitazioni per <xref:System.Windows.FrameworkElement.Height%2A>, ad esempio <xref:System.Windows.Controls.Grid>.  Quando sono previste limitazioni per <xref:System.Windows.FrameworkElement.Height%2A>, il controllo <xref:System.Windows.Controls.DataGrid> creerà solo le righe che possono essere adattate in base alla proprietà <xref:System.Windows.FrameworkElement.Height%2A> specificata riciclando le righe necessarie per visualizzare i nuovi dati.  
  
### Impostazione delle dimensioni di DataGrid  
 È possibile impostare <xref:System.Windows.Controls.DataGrid> per il ridimensionamento automatico entro limiti specificati o è possibile impostare <xref:System.Windows.Controls.DataGrid> su una dimensione specifica.  Nella tabella seguente vengono illustrate le proprietà che è possibile impostare per controllare le dimensioni di <xref:System.Windows.Controls.DataGrid>.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Windows.FrameworkElement.Height%2A>|Imposta un'altezza specifica per il controllo <xref:System.Windows.Controls.DataGrid>.|  
|<xref:System.Windows.FrameworkElement.MaxHeight%2A>|Imposta il limite superiore per l'altezza dell'oggetto <xref:System.Windows.Controls.DataGrid>.  L'oggetto <xref:System.Windows.Controls.DataGrid> verrà ingrandito verticalmente finché non raggiungerà questa altezza.|  
|<xref:System.Windows.FrameworkElement.MinHeight%2A>|Imposta il limite inferiore per l'altezza dell'oggetto <xref:System.Windows.Controls.DataGrid>.  L'oggetto <xref:System.Windows.Controls.DataGrid> verrà ridotto verticalmente finché non raggiungerà questa altezza.|  
|<xref:System.Windows.FrameworkElement.Width%2A>|Imposta una larghezza specifica per il controllo <xref:System.Windows.Controls.DataGrid>.|  
|<xref:System.Windows.FrameworkElement.MaxWidth%2A>|Imposta il limite superiore per la larghezza dell'oggetto <xref:System.Windows.Controls.DataGrid>.  L'oggetto <xref:System.Windows.Controls.DataGrid> verrà ingrandito orizzontalmente finché non raggiungerà questa larghezza.|  
|<xref:System.Windows.FrameworkElement.MinWidth%2A>|Imposta il limite inferiore per la larghezza dell'oggetto <xref:System.Windows.Controls.DataGrid>.  L'oggetto <xref:System.Windows.Controls.DataGrid> verrà ridotto orizzontalmente finché non raggiungerà questa larghezza.|  
  
## Ridimensionamento delle righe e delle intestazioni di riga  
  
### Righe di DataGrid  
 Per impostazione predefinita, la proprietà <xref:System.Windows.FrameworkElement.Height%2A> di una riga di <xref:System.Windows.Controls.DataGrid> è impostata su <xref:System.Double.NaN?displayProperty=fullName> \("`Auto`" in XAML\) in modo che l'altezza di riga possa espandersi in base alle dimensioni del contenuto.  È possibile specificare l'altezza di tutte le righe in <xref:System.Windows.Controls.DataGrid> impostando la proprietà <xref:System.Windows.Controls.DataGrid.RowHeight%2A?displayProperty=fullName>.  Gli utenti possono modificare l'altezza di riga trascinando i separatori di intestazione di riga.  
  
### Intestazioni di riga di DataGrid  
 Per visualizzare le intestazioni di riga, è necessario impostare la proprietà <xref:System.Windows.Controls.DataGrid.HeadersVisibility%2A> su <xref:System.Windows.Controls.DataGridHeadersVisibility?displayProperty=fullName> o <xref:System.Windows.Controls.DataGridHeadersVisibility?displayProperty=fullName>.  Per impostazione predefinita, le intestazioni di riga sono visualizzate e vengono ridimensionate automaticamente per adattarsi al contenuto.  È possibile fornire alle intestazioni di riga una larghezza specifica impostando la proprietà <xref:System.Windows.Controls.DataGrid.RowHeaderWidth%2A?displayProperty=fullName>.  
  
## Ridimensionando delle colonne e delle intestazioni di colonna  
  
### Colonne di DataGrid  
 <xref:System.Windows.Controls.DataGrid> utilizza i valori della struttura di <xref:System.Windows.Controls.DataGridLength> e di <xref:System.Windows.Controls.DataGridLengthUnitType> per specificare le modalità di ridimensionamento automatico o assoluto.  
  
 Nella tabella seguente vengono illustrati i valori forniti dalla struttura di <xref:System.Windows.Controls.DataGridLengthUnitType>.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|<xref:System.Windows.Controls.DataGridLengthUnitType>|La modalità di ridimensionamento automatico predefinita ridimensiona le colonne di <xref:System.Windows.Controls.DataGrid> in base al contenuto delle celle e delle intestazioni di colonna.|  
|<xref:System.Windows.Controls.DataGridLengthUnitType>|La modalità di ridimensionamento automatico basata sulle celle ridimensiona le colonne di <xref:System.Windows.Controls.DataGrid> in base al contenuto delle celle della colonna senza includere le intestazioni di colonna.|  
|<xref:System.Windows.Controls.DataGridLengthUnitType>|La modalità di ridimensionamento automatico basata sulle intestazioni ridimensiona le colonne di <xref:System.Windows.Controls.DataGrid> solo in base al contenuto delle intestazioni di colonna.|  
|<xref:System.Windows.Controls.DataGridLengthUnitType>|La modalità di ridimensionamento basata su pixel ridimensiona le colonne di <xref:System.Windows.Controls.DataGrid> in base al valore numerico fornito.|  
|<xref:System.Windows.Controls.DataGridLengthUnitType>|La modalità di ridimensionamento proporzionale viene utilizzata per distribuire lo spazio disponibile in base a proporzioni ponderate.<br /><br /> In XAML, i valori proporzionali vengono espressi come n\* dove n rappresenta un valore numerico.  1\* equivale a \*.  Ad esempio, se due colonne in un oggetto <xref:System.Windows.Controls.DataGrid> dispongono di larghezze pari a \* e 2\*, la prima colonna dovrebbe ricevere una parte dello spazio disponibile e la seconda due parti.|  
  
 La classe <xref:System.Windows.Controls.DataGridLengthConverter> può essere utilizzata per convertire i dati tra valori numerici o stringa e valori <xref:System.Windows.Controls.DataGridLength>.  
  
 Per impostazione predefinita, la proprietà <xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=fullName> viene impostata su <xref:System.Windows.Controls.DataGridLength.SizeToHeader%2A> mentre la proprietà <xref:System.Windows.Controls.DataGridColumn.Width%2A?displayProperty=fullName> viene impostata su <xref:System.Windows.Controls.DataGridLength.Auto%2A>.  Quando la modalità di ridimensionamento viene impostata su <xref:System.Windows.Controls.DataGridLength.Auto%2A> o <xref:System.Windows.Controls.DataGridLength.SizeToCells%2A>, le dimensioni delle colonne aumentano in base alla larghezza del contenuto visibile più ampio.  Durante lo scorrimento, queste modalità di ridimensionamento eseguono l'espansione delle colonne se nella visualizzazione si scorre il contenuto di una colonna che è più ampio della dimensione della colonna corrente.  La colonna non viene compressa dopo che è stato eseguito lo scorrimento del contenuto al di fuori della visualizzazione.  
  
 Le colonne di <xref:System.Windows.Controls.DataGrid> possono essere impostate anche per il ridimensionamento automatico solo entro limiti specificati o possono essere impostate su una dimensione specifica.  Nella tabella seguente vengono illustrate le proprietà che è possibile impostare per controllare le dimensioni delle colonne.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Windows.Controls.DataGrid.MaxColumnWidth%2A?displayProperty=fullName>|Imposta il limite superiore per tutte le colonne del controllo <xref:System.Windows.Controls.DataGrid>.|  
|<xref:System.Windows.Controls.DataGridColumn.MaxWidth%2A?displayProperty=fullName>|Imposta il limite superiore per una singola colonna.  Esegue l'override di <xref:System.Windows.Controls.DataGrid.MaxColumnWidth%2A?displayProperty=fullName>.|  
|<xref:System.Windows.Controls.DataGrid.MinColumnWidth%2A?displayProperty=fullName>|Imposta il limite inferiore per tutte le colonne del controllo <xref:System.Windows.Controls.DataGrid>.|  
|<xref:System.Windows.Controls.DataGridColumn.MinWidth%2A?displayProperty=fullName>|Imposta il limite inferiore per una singola colonna.  Esegue l'override di <xref:System.Windows.Controls.DataGrid.MinColumnWidth%2A?displayProperty=fullName>.|  
|<xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=fullName>|Imposta una larghezza specifica per tutte le colonne del controllo <xref:System.Windows.Controls.DataGrid>.|  
|<xref:System.Windows.Controls.DataGridColumn.Width%2A?displayProperty=fullName>|Imposta una larghezza specifica per una singola colonna.  Esegue l'override di <xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=fullName>.|  
  
### Intestazioni di colonna di DataGrid  
 Le intestazioni di colonna del controllo <xref:System.Windows.Controls.DataGrid> vengono visualizzate per impostazione predefinita.  Per nascondere le intestazioni di colonna, è necessario impostare la proprietà <xref:System.Windows.Controls.DataGrid.HeadersVisibility%2A> su <xref:System.Windows.Controls.DataGridHeadersVisibility?displayProperty=fullName> o <xref:System.Windows.Controls.DataGridHeadersVisibility?displayProperty=fullName>.  Per impostazione predefinita, le intestazioni di colonna quando sono visualizzate vengono ridimensionate automaticamente per adattarsi al contenuto.  È possibile fornire alle intestazioni di colonna un'altezza specifica impostando la proprietà <xref:System.Windows.Controls.DataGrid.ColumnHeaderHeight%2A?displayProperty=fullName>.  
  
### Ridimensionamento con il mouse  
 È possibile ridimensionare righe e colonne di <xref:System.Windows.Controls.DataGrid> trascinando i separatori di intestazione di riga o colonna.  <xref:System.Windows.Controls.DataGrid> supporta inoltre il ridimensionamento automatico di righe e colonne eseguito facendo doppio clic sul separatore di intestazione di riga o colonna.  Per impedire a un utente di ridimensionare determinate colonne, impostare la proprietà <xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=fullName> su `false` per le singole colonne.  Per impedire agli utenti di ridimensionare tutte le colonne, impostare la proprietà <xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=fullName> su `false`.  Per impedire agli utenti di ridimensionare tutte le righe, impostare la proprietà <xref:System.Windows.Controls.DataGrid.CanUserResizeRows%2A?displayProperty=fullName> su `false`.  
  
## Vedere anche  
 <xref:System.Windows.Controls.DataGrid>   
 <xref:System.Windows.Controls.DataGridColumn>   
 <xref:System.Windows.Controls.DataGridLength>   
 <xref:System.Windows.Controls.DataGridLengthConverter>