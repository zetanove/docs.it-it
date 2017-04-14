---
title: "Procedura: accedere agli oggetti in un elenco a discesa DataGridViewComboBoxCell Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "caselle combinate, accesso agli oggetti negli elenchi a discesa DataGridViewComboBoxCell"
  - "caselle combinate, nel controllo DataGridView"
  - "DataGridView (controllo) [Windows Form], accesso agli oggetti nelle celle di caselle combinate"
ms.assetid: bcbe794a-d1fa-47f8-b5a3-5f085b32097d
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: accedere agli oggetti in un elenco a discesa DataGridViewComboBoxCell Windows Form
Analogamente al controllo <xref:System.Windows.Forms.ComboBox>, i tipi <xref:System.Windows.Forms.DataGridViewComboBoxColumn> e <xref:System.Windows.Forms.DataGridViewComboBoxCell> consentono di aggiungere oggetti arbitrari agli elenchi a discesa.  Con questa funzionalità, è possibile rappresentare stati complessi in un elenco a discesa senza dover archiviare gli oggetti corrispondenti in una raccolta distinta.  
  
 A differenza del controllo <xref:System.Windows.Forms.ComboBox>, i tipi <xref:System.Windows.Forms.DataGridView> non includono una proprietà <xref:System.Windows.Forms.ComboBox.SelectedItem%2A> per il recupero dell'oggetto attualmente selezionato.  È invece necessario impostare la proprietà <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A?displayProperty=fullName> o <xref:System.Windows.Forms.DataGridViewComboBoxCell.ValueMember%2A?displayProperty=fullName> sul nome di una proprietà nell'oggetto business.  Quando l'utente effettua una selezione, la proprietà dell'oggetto business indicata imposta la proprietà <xref:System.Windows.Forms.DataGridViewCell.Value%2A> della cella.  
  
 Per recuperare l'oggetto business tramite il valore della cella, è necessario che la proprietà `ValueMember` indichi una proprietà che restituisce un riferimento all'oggetto business stesso.  Pertanto, se il tipo dell'oggetto business non è sotto controllo, è necessario aggiungere tale proprietà estendendo il tipo tramite l'ereditarietà.  
  
 Nelle procedure seguenti viene illustrato come compilare un elenco a discesa con oggetti business e recuperare gli oggetti tramite la proprietà <xref:System.Windows.Forms.DataGridViewCell.Value%2A> della cella.  
  
### Per aggiungere oggetti business all'elenco a discesa  
  
1.  Creare un nuovo controllo <xref:System.Windows.Forms.DataGridViewComboBoxColumn> e compilare la relativa raccolta <xref:System.Windows.Forms.DataGridViewComboBoxColumn.Items%2A>.  In alternativa, è possibile impostare la proprietà <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DataSource%2A> della colonna sulla raccolta di oggetti business.  In tal caso, tuttavia, non è possibile aggiungere "unassigned" all'elenco a discesa senza creare un oggetto business corrispondente nella raccolta.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#110](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#110)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#110](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#110)]  
  
2.  Impostare le proprietà <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DisplayMember%2A> e <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A>.  <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DisplayMember%2A> indica la proprietà che restituisce un riferimento all'oggetto business.  <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A> indica la proprietà che restituisce un riferimento all'oggetto business.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#115](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#115)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#115](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#115)]  
  
3.  Assicurarsi che il tipo di oggetto business contenga una proprietà che restituisce un riferimento all'istanza corrente.  Questa proprietà deve essere denominata con il valore assegnato a <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A> nel passaggio precedente.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#310](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#310)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#310](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#310)]  
  
### Per recuperare l'oggetto business attualmente selezionato  
  
-   Ottenere la proprietà <xref:System.Windows.Forms.DataGridViewCell.Value%2A> della cella ed eseguirne il casting sul tipo di oggetto business.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#120](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#120)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#120](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#120)]  
  
## Esempio  
 Nell'esempio completo viene illustrato l'utilizzo degli oggetti business nell'elenco a discesa.  Un controllo <xref:System.Windows.Forms.DataGridView> viene associato a una raccolta di oggetti `Task`.  Ogni oggetto `Task` include una proprietà `AssignedTo` che indica l'oggetto `Employee` attualmente assegnato a tale attività.  Nella colonna `Assigned To` viene visualizzato il valore della proprietà `Name` per ogni dipendente assegnato, o "unassigned" se il valore della proprietà `Task.AssignedTo` è `null`.  
  
 Per visualizzare il comportamento di questo esempio, attenersi alla procedura seguente:  
  
1.  Modificare le assegnazioni nella colonna `Assigned To` selezionando valori diversi dagli elenchi a discesa o premendo CTRL\+0 in una cella della casella combinata.  
  
2.  Fare clic su `Generate Report` per visualizzare le assegnazioni correnti.  Questo dimostra che eseguendo una modifica nella colonna `Assigned To` viene automaticamente aggiornata la raccolta `tasks`.  
  
3.  Fare clic su un pulsante `Request Status` per eseguire una chiamata al metodo `RequestStatus` dell'oggetto `Employee` corrente per tale riga.  Questo dimostra che l'oggetto selezionato è stato recuperato correttamente.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#000](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#000)]
 [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#000](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#000)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Riferimenti agli assembly System e System.Windows.Forms.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewComboBoxColumn>   
 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.Items%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DataSource%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewComboBoxCell>   
 <xref:System.Windows.Forms.DataGridViewComboBoxCell.Items%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewComboBoxCell.DataSource%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewComboBoxCell.ValueMember%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCell.Value%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ComboBox>   
 [Visualizzazione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)