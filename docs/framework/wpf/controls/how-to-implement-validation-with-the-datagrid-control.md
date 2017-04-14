---
title: "Procedura: implementare la convalida con il controllo DataGrid | Microsoft Docs"
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
  - "DataGrid [WPF], convalida"
  - "convalida [WPF], DataGrid"
ms.assetid: ec6078a8-1e42-4648-b414-f4348e81bda1
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: implementare la convalida con il controllo DataGrid
Il controllo <xref:System.Windows.Controls.DataGrid> consente di eseguire la convalida a livello sia di cella che di riga.  Con la convalida a livello di cella, si convalidano le singole proprietà di un oggetto con dati associati quando un utente aggiorna un valore.  Con la convalida a livello di riga, si convalidano interi oggetti dati quando un utente esegue il commit delle modifiche in una riga.  È inoltre possibile fornire feedback visivo personalizzato per gli errori di convalida o utilizzare il feedback visivo predefinito disponibile nel controllo <xref:System.Windows.Controls.DataGrid>.  
  
 Nelle procedure seguenti viene descritto come applicare le regole di convalida alle associazioni <xref:System.Windows.Controls.DataGrid> e come personalizzare il feedback visivo.  
  
### Per convalidare singoli valori di cella  
  
-   Specificare uno o più regole di convalida nell'associazione utilizzata con una colonna.  Questa operazione è simile alla convalida dei dati nei controlli semplici, come descritto in [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
     Nell'esempio riportato di seguito viene illustrato un controllo <xref:System.Windows.Controls.DataGrid> con quattro colonne associate a proprietà diverse di un oggetto business.  Tre delle colonne specificano l'oggetto <xref:System.Windows.Controls.ExceptionValidationRule> impostando la proprietà <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> su `true`.  
  
     [!code-xml[DataGrid_Validation#BasicXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/window1.xaml#basicxaml)]  
  
     Quando un utente immette un valore non valido \(ad esempio un numero non intero nella colonna dell'ID del corso\), attorno alla cella viene visualizzato un bordo rosso.  È possibile modificare questo feedback di convalida predefinito come descritto nella procedura seguente.  
  
### Per personalizzare il feedback di convalida per le celle  
  
-   Impostare la proprietà <xref:System.Windows.Controls.DataGridBoundColumn.EditingElementStyle%2A> della colonna su uno stile appropriato per il controllo di modifica della colonna.  Poiché i controlli di modifica vengono creati in fase di esecuzione, non è possibile utilizzare la proprietà associata <xref:System.Windows.Controls.Validation.ErrorTemplate%2A?displayProperty=fullName> come con i controlli semplici.  
  
     Nell'esempio seguente viene aggiornato l'esempio precedente aggiungendo uno stile di errore condiviso dalle tre colonne con le regole di convalida.  Quando un utente immette un valore non valido, lo stile modifica il colore di sfondo della cella e aggiunge una descrizione comando.  Si noti l'utilizzo di un trigger per determinare se è presente un errore di convalida.  È necessario perché attualmente non esistono modelli di errore dedicati per le celle.  
  
     [!code-xml[DataGrid_Validation#CellValidationXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#cellvalidationxaml)]  
  
     È possibile implementare una personalizzazione più estensiva sostituendo la proprietà <xref:System.Windows.Controls.DataGridColumn.CellStyle%2A> utilizzata dalla colonna.  
  
### Per convalidare più valori in una sola riga  
  
1.  Implementare una sottoclasse <xref:System.Windows.Controls.ValidationRule> che controlla più proprietà dell'oggetto con dati associati.  Nell'implementazione del metodo <xref:System.Windows.Controls.ValidationRule.Validate%2A> trasmette il valore di parametro `value` a un'istanza di <xref:System.Windows.Data.BindingGroup>.  Sarà quindi possibile accedere all'oggetto dati tramite la proprietà <xref:System.Windows.Data.BindingGroup.Items%2A>.  
  
     Nell'esempio seguente viene illustrato il processo per convalidare che il valore della proprietà `StartDate` per un oggetto `Course` sia precedente al valore della proprietà `EndDate`.  
  
     [!code-csharp[DataGrid_Validation#CourseValidationRule](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#coursevalidationrule)]
     [!code-vb[DataGrid_Validation#CourseValidationRule](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#coursevalidationrule)]  
  
2.  Aggiungere la regola di convalida alla raccolta <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A?displayProperty=fullName>.  La proprietà <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> fornisce l'accesso diretto alla proprietà <xref:System.Windows.Data.BindingGroup.ValidationRules%2A> di un'istanza di <xref:System.Windows.Data.BindingGroup> che raggruppa tutte le associazioni utilizzate dal controllo.  
  
     Nell'esempio riportato di seguito la proprietà <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> viene impostata in XAML.  La proprietà <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> viene impostata su <xref:System.Windows.Controls.ValidationStep> in modo che la convalida si verifichi solo dopo l'aggiornamento dell'oggetto con dati associati.  
  
     [!code-xml[DataGrid_Validation#RowValidationRulesXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationrulesxaml)]  
  
     Quando un utente specifica una data di fine precedente alla data di inizio, viene visualizzato un punto esclamativo rosso \(\!\) nell'intestazione della riga.  È possibile modificare questo feedback di convalida predefinito come descritto nella procedura seguente.  
  
### Per personalizzare il feedback di convalida per le righe  
  
-   Impostare la proprietà <xref:System.Windows.Controls.DataGrid.RowValidationErrorTemplate%2A?displayProperty=fullName>.  Questa proprietà consente di personalizzare feedback di convalida per le righe per i singoli controlli <xref:System.Windows.Controls.DataGrid>.  È inoltre possibile modificare più controlli utilizzando uno stile di riga implicito per impostare la proprietà <xref:System.Windows.Controls.DataGridRow.ValidationErrorTemplate%2A?displayProperty=fullName>.  
  
     Nell'esempio seguente il feedback di convalida per le righe predefinito viene sostituito con un indicatore più visibile.  Quando un utente immette un valore non valido, nell'intestazione della riga viene visualizzato un cerchio rosso con un punto esclamativo bianco.  Questo accade per gli errori di convalida sia delle righe che delle celle.  Il messaggio di errore associato viene visualizzato in una descrizione comando.  
  
     [!code-xml[DataGrid_Validation#RowValidationFeedbackXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationfeedbackxaml)]  
  
## Esempio  
 Nell'esempio seguente viene fornita una dimostrazione completa per la convalida delle celle e delle righe.  La classe `Course` fornisce un oggetto dati di esempio che implementa <xref:System.ComponentModel.IEditableObject> per supportare le transazioni.  Il controllo <xref:System.Windows.Controls.DataGrid> interagisce con <xref:System.ComponentModel.IEditableObject> per consentire agli utenti di annullare le modifiche premendo ESC.  
  
> [!NOTE]
>  Se si utilizza Visual Basic, nella prima riga di MainWindow.xaml sostituire `x:Class="DataGridValidation.MainWindow"` con `x:Class="MainWindow"`.  
  
 Per testare la convalida, provare a effettuare le operazioni seguenti:  
  
-   Nella colonna dell'ID del corso immettere un valore non intero.  
  
-   Nella colonna della data di fine immettere una data precedente alla data di inizio.  
  
-   Eliminare il valore nella colonna dell'ID del corso, della data di inizio o della data di fine.  
  
-   Per annullare un valore di cella non valido, inserire nuovamente il cursore nella cella e premere ESC.  
  
-   Per annullare le modifiche per un'intera riga quando la cella corrente è in modalità di modifica, premere ESC due volte.  
  
-   Quando si verifica un errore di convalida, spostare il puntatore del mouse sull'indicatore nell'intestazione della riga per visualizzare il messaggio di errore associato.  
  
 [!code-csharp[DataGrid_Validation#FullCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#fullcode)]
 [!code-vb[DataGrid_Validation#FullCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#fullcode)]  
  
 [!code-xml[DataGrid_Validation#FullXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#fullxaml)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.DataGrid>   
 [DataGrid](../../../../docs/framework/wpf/controls/datagrid.md)   
 [Data binding](../../../../docs/framework/wpf/data/data-binding-wpf.md)   
 [Implementare la convalida dell'associazione](../../../../docs/framework/wpf/data/how-to-implement-binding-validation.md)   
 [Implementare la logica di convalida negli oggetti personalizzati](../../../../docs/framework/wpf/data/how-to-implement-validation-logic-on-custom-objects.md)