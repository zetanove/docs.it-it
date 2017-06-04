---
title: "Procedura: creare una tabella di ricerca con il componente BindingSource di Windows Form | Microsoft Docs"
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
  - "BindingSource (componente) [Windows Form], creazione di una tabella di ricerca"
  - "BindingSource (componente) [Windows Form], esempi"
  - "tabelle di ricerca"
  - "tabelle [Windows Form], creazione di tabelle di ricerca"
ms.assetid: 622fce80-879d-44be-abbf-8350ec22ca2b
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: creare una tabella di ricerca con il componente BindingSource di Windows Form
Una tabella di ricerca è una tabella di dati che include una colonna che mostra i dati presenti nei record di una tabella correlata.  Nelle procedure seguenti sarà usato un controllo <xref:System.Windows.Forms.ComboBox> per visualizzare il campo che include la relazione di chiave esterna dalla tabella padre alla tabella figlio.  
  
 Per semplificare la visualizzazione delle due tabelle e della relazione corrispondente, di seguito è disponibile un esempio di una tabella padre e una tabella figlio:  
  
 CustomersTable \(tabella padre\)  
  
|CustomerID|CustomerName|  
|----------------|------------------|  
|712|Davide Milano|  
|713|Fiamma Greco|  
  
 OrdersTable \(tabella figlio\)  
  
|OrderID|OrderDate|CustomerID|  
|-------------|---------------|----------------|  
|903|Lunedì, 12.02.04|712|  
|904|Lunedì, 13.02.04|713|  
  
 In questo scenario, in una tabella, CustomersTable, sono archiviate le informazioni effettive da visualizzare e salvare.  Per risparmiare spazio, tuttavia, la tabella esclude dati che possono rendere più chiare le informazioni.  L'altra tabella, OrdersTable, include solo informazioni correlate all'aspetto e relative alle corrispondenze tra numero di ID, data di ordine e ID ordine.  Non include informazioni sui nomi dei clienti.  
  
 Nel controllo [Controllo ComboBox](../../../../docs/framework/winforms/controls/combobox-control-windows-forms.md) sono impostate quattro proprietà importanti per creare la tabella di ricerca.  
  
-   La proprietà <xref:System.Windows.Forms.ComboBox.DataSource%2A> include il nome della tabella.  
  
-   La proprietà <xref:System.Windows.Forms.ListControl.DisplayMember%2A> include la colonna di dati della tabella da visualizzare per il testo del controllo \(nome del cliente\).  
  
-   La proprietà <xref:System.Windows.Forms.ListControl.ValueMember%2A> include la colonna di dati della tabella con le informazioni archiviate \(numero di ID nella tabella padre\).  
  
-   La proprietà <xref:System.Windows.Forms.ListControl.SelectedValue%2A> fornisce il valore di ricerca per la tabella figlio, in base a <xref:System.Windows.Forms.ListControl.ValueMember%2A>.  
  
 Le procedure seguenti mostrano come definire il layout del form come tabella di ricerca e associare i dati ai controlli disponibili nel form.  Per completare correttamente le procedure, è necessario avere un'origine dati con tabelle padre e figlio con una relazione di chiave esterna, come indicato in precedenza.  
  
### Per creare l'interfaccia utente  
  
1.  Dalla **Casella degli strumenti** trascinare un controllo <xref:System.Windows.Forms.ComboBox> nel form.  
  
     Il controllo mostrerà una colonna della tabella padre.  
  
2.  Trascinare altri controlli per visualizzare i dettagli disponibili nella tabella figlio.  La scelta dei controlli dovrebbe dipendere dal formato dei dati nella tabella.  Per altre informazioni, vedere [Controlli Windows Form per funzione](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md).  
  
3.  Trascinare un controllo <xref:System.Windows.Forms.BindingNavigator> nel form, per permettere di esplorare i dati nella tabella figlio.  
  
### Per connettersi ai dati e associarli ai controlli  
  
1.  Selezionare <xref:System.Windows.Forms.ComboBox> e fare clic sul glifo Smart Task per visualizzare la finestra di dialogo Smart Task.  
  
2.  Selezionare **Usa elementi associati a dati**.  
  
3.  Fare clic sulla freccia accanto alla casella di riepilogo a discesa **Origine dati**.  Se un'origine dati è stata configurata in precedenza per il progetto o il form, sarà visualizzata. In caso contrario, completare i passaggi seguenti. In questo esempio sono usate le tabelle Customers e Orders del database di esempio Northwind e tali tabelle sono indicate tra parentesi.  
  
    1.  Fare clic su **Aggiungi origine dati progetto** per connettersi ai dati e creare un'origine dati.  
  
    2.  Nella pagina iniziale della **Configurazione guidata origine dati** fare clic su **Avanti**.  
  
    3.  Selezionare **Database** nella pagina **Scegliere un tipo di origine dati**.  
  
    4.  Selezionare una connessione dati dall'elenco di connessioni disponibili nella pagina **Seleziona connessione dati**.  Se la connessione dati desiderata non è disponibile selezionare **Nuova connessione** per creare una nuova connessione dati.  
  
    5.  Fare clic su **Sì, salva la connessione con nome** per salvare la stringa di connessione nel file di configurazione dell'applicazione.  
  
    6.  Selezionare gli oggetti database da inserire nell'applicazione.  In questo caso, selezionare la tabella padre e la tabella figlio \(ad esempio, Customers e Orders\) con una relazione di chiave esterna.  
  
    7.  Se si vuole, sostituire il nome predefinito del set di dati.  
  
    8.  Scegliere **Fine**.  
  
4.  Nella casella di riepilogo a discesa **Visualizza membro** selezionare il nome di colonna \(ad esempio, ContactName\) da visualizzare nella casella combinata.  
  
5.  Nella casella di riepilogo a discesa **Membro valore** selezionare la colonna \(ad esempio, CustomerID\) per l'esecuzione dell'operazione di ricerca nella tabella figlio.  
  
6.  Nella casella di riepilogo a discesa **Valore selezionato** passare a **Origini dati del progetto** e al set di dati appena creato che include le tabelle padre e figlio.  Selezionare la stessa proprietà della tabella figlio che corrisponde al Membro valore della tabella padre \(ad esempio, Orders.CustomerID\).  I componenti appropriati per <xref:System.Windows.Forms.BindingSource>, set di dati e adattatori di tabelle saranno creati e aggiunti al form.  
  
7.  Associare il controllo <xref:System.Windows.Forms.BindingNavigator> a <xref:System.Windows.Forms.BindingSource> della tabella figlio \(ad esempio, `OrdersBindingSource`\).  
  
8.  Associare i controlli diversi dal controllo <xref:System.Windows.Forms.ComboBox> e <xref:System.Windows.Forms.BindingNavigator> ai campi di dettagli da <xref:System.Windows.Forms.BindingSource> della tabella figlio \(ad esempio, `OrdersBindingSource`\) da visualizzare.  
  
## Vedere anche  
 <xref:System.Windows.Forms.BindingSource>   
 [Il componente BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [Controllo ComboBox](../../../../docs/framework/winforms/controls/combobox-control-windows-forms.md)   
 [Associazione di controlli ai dati in Visual Studio](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md)