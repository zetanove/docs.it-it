---
title: "Procedura dettagliata: implementazione della modalit&#224; virtuale nel controllo DataGridView Windows Form | Microsoft Docs"
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
  - "dati [Windows Form], gestione di set di dati di grandi dimensioni"
  - "DataGridView (controllo) [Windows Form], set di dati di grandi dimensioni"
  - "DataGridView (controllo) [Windows Form], modalità virtuale"
  - "modalità virtuale, procedure dettagliate"
  - "procedure dettagliate [Windows Form], DataGridView (controllo)"
ms.assetid: 74eb5276-5ab8-4ce0-8005-dae751d85f7c
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura dettagliata: implementazione della modalit&#224; virtuale nel controllo DataGridView Windows Form
Quando si desidera visualizzare quantità molto elevate di dati in formato tabulare in un controllo <xref:System.Windows.Forms.DataGridView>, è possibile impostare la proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> su `true` e gestire in modo esplicito l'interazione del controllo con il relativo archivio dati.  In questo modo è possibile regolare le prestazioni del controllo in una situazione di questo tipo.  
  
 Il controllo <xref:System.Windows.Forms.DataGridView> fornisce numerosi eventi che è possibile gestire per consentire l'interazione con un archivio dati personalizzato.  Questa procedura dettagliata rappresenta una guida nel processo di implementazione di questi gestori eventi.  Nell'esempio di codice riportato in questo argomento viene utilizzata un'origine dati semplice a scopo illustrativo.  Nell'impostazione di un ambiente la produzione, in genere vengono caricate solo le righe che è necessario visualizzare in una cache e vengono gestiti gli eventi <xref:System.Windows.Forms.DataGridView> per l'interazione con la cache e il relativo aggiornamento.  Per ulteriori informazioni, vedere [Implementazione del modo virtuale con caricamento dati JIT nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)  
  
 Per copiare il codice nell'argomento corrente come un elenco singolo, vedere [Procedura: implementare il modo virtuale nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-implement-virtual-mode-in-the-windows-forms-datagridview-control.md).  
  
## Creazione del form  
  
#### Per implementare la modalità virtuale  
  
1.  Creare una classe derivante dalla classe <xref:System.Windows.Forms.Form> e che contenga un controllo <xref:System.Windows.Forms.DataGridView>.  
  
     Nel codice riportato di seguito viene fornita l'inizializzazione di base.  Vengono dichiarate alcune variabili da utilizzare nei passaggi successivi, viene fornito un metodo `Main` e viene fornito un layout di form semplice nel costruttore della classe.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#001](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#001)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#001](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#001)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#001](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#001)]  
    [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#002](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#002)]
    [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#002](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#002)]
    [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#002](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#002)]  
  
2.  Implementare un gestore per l'evento <xref:System.Windows.Forms.Form.Load> del form per inizializzare il controllo <xref:System.Windows.Forms.DataGridView> e inserire valori di esempio nell'archivio dati.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#110](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#110)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#110](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#110)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#110](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#110)]  
  
3.  Implementare un gestore per l'evento <xref:System.Windows.Forms.DataGridView.CellValueNeeded> per recuperare il valore di cella necessario dall'archivio dati o dall'oggetto `Customer` attualmente in fase di modifica.  
  
     Questo evento viene generato ogni volta che il controllo <xref:System.Windows.Forms.DataGridView> deve disegnare una cella.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#120](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#120)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#120](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#120)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#120](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#120)]  
  
4.  Implementare un gestore per l'evento <xref:System.Windows.Forms.DataGridView.CellValuePushed> per memorizzare un valore di cella modificato nell'oggetto `Customer` che rappresenta la riga modificata.  Questo evento viene generato ogni volta che l'utente esegue il commit di una modifica del valore di una cella.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#130](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#130)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#130](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#130)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#130](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#130)]  
  
5.  Implementare un gestore per l'evento <xref:System.Windows.Forms.DataGridView.NewRowNeeded> per creare un nuovo oggetto `Customer` che rappresenta una riga appena creata.  
  
     Questo evento viene generato quando l'utente inserisce una riga per immettere nuovi record.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#140](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#140)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#140](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#140)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#140](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#140)]  
  
6.  Implementare un gestore per l'evento <xref:System.Windows.Forms.DataGridView.RowValidated> per salvare le righe nuove e modificate nell'archivio dati.  
  
     Questo evento si verifica ogni volta che l'utente modifica la riga corrente.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#150](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#150)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#150](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#150)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#150](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#150)]  
  
7.  Implementare un gestore per l'evento <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded> per indicare se l'evento <xref:System.Windows.Forms.DataGridView.CancelRowEdit> verrà generato quando l'utente segnala l'annullamento della riga premendo due volte il tasto ESC in modalità di modifica o una sola volta al di fuori di tale modalità.  
  
     Per impostazione predefinita, l'evento <xref:System.Windows.Forms.DataGridView.CancelRowEdit> viene generato al momento dell'annullamento della riga quando le celle presenti nella riga corrente sono state modificate, a meno che la proprietà <xref:System.Windows.Forms.QuestionEventArgs.Response%2A?displayProperty=fullName> non sia impostata su `true` nel gestore eventi <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded>.  Questo evento è utile nel caso in cui l'ambito dell'operazione di commit sia determinata in fase di esecuzione.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#160](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#160)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#160](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#160)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#160](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#160)]  
  
8.  Implementare un gestore per l'evento <xref:System.Windows.Forms.DataGridView.CancelRowEdit> per eliminare i valori dell'oggetto `Customer` che rappresenta la riga corrente.  
  
     Questo evento viene generato quando l'utente segnala l'annullamento della riga premendo due volte il tasto ESC in modalità di modifica o una sola volta al di fuori di tale modalità.  Questo evento non viene generato se non sono state modificate celle all'interno della riga corrente oppure se il valore della proprietà <xref:System.Windows.Forms.QuestionEventArgs.Response%2A?displayProperty=fullName> è impostato su `false` in un gestore eventi <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded>.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#170](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#170)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#170](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#170)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#170](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#170)]  
  
9. Implementare un gestore per l'evento <xref:System.Windows.Forms.DataGridView.UserDeletingRow> per eliminare un oggetto `Customer` già presente dall'archivio dati o eliminare un oggetto `Customer` non salvato che rappresenta una riga appena creata.  
  
     Questo evento viene generato ogni volta che l'utente elimina una riga selezionando l'intestazione di una riga e premendo il tasto CANC.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#180](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#180)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#180](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#180)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#180](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#180)]  
  
10. Implementare una classe `Customers` semplice che rappresenti gli elementi di dati utilizzati in questo esempio di codice.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#200](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#200)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#200](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#200)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#200](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#200)]  
  
## Verifica dell'applicazione  
 È ora possibile verificare il form per assicurarsi che funzioni correttamente.  
  
#### Per eseguire il test del form  
  
-   Compilare l'applicazione ed eseguirla.  
  
     Verrà visualizzato un controllo <xref:System.Windows.Forms.DataGridView> in cui sono presenti tre record relativi al cliente.  È possibile modificare i valori di più celle in una riga e premere ESC due volte in modalità di modifica e una volta al di fuori di tale modalità per ripristinare i valori originali dell'intera riga.  Quando si modificano, aggiungono o eliminano righe all'interno del controllo, anche gli oggetti `Customer` all'interno dell'archivio dati vengono modificati, aggiunti o eliminati.  
  
## Passaggi successivi  
 Questa applicazione consente di comprendere i concetti di base degli eventi che è necessario gestire per implementare la modalità virtuale nel controllo <xref:System.Windows.Forms.DataGridView>.  Questa applicazione di base può essere resa più complessa in diversi modi:  
  
-   Implementando un archivio dati per la memorizzazione nella cache dei valori di un database esterno.  I valori memorizzati nella cache potranno essere recuperati ed eliminati secondo necessità, in modo che la cache contenga solo gli elementi necessari per la visualizzazione, utilizzando quindi una minore quantità di memoria sul computer client.  
  
-   Regolando le prestazioni dell'archivio dati in base alle esigenze.  Ad esempio, è possibile rimediare alla lentezza delle connessioni in rete invece alle limitazioni della memoria del computer client utilizzando dimensioni della memoria cache maggiori e riducendo il numero delle query sul database.  
  
 Per ulteriori informazioni sulla memorizzazione nella cache dei valori di un database esterno, vedere [Procedura: implementare la modalità virtuale con caricamento dati JIT nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/virtual-mode-with-just-in-time-data-loading-in-the-datagrid.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>   
 <xref:System.Windows.Forms.DataGridView.CellValueNeeded>   
 <xref:System.Windows.Forms.DataGridView.CellValuePushed>   
 <xref:System.Windows.Forms.DataGridView.NewRowNeeded>   
 <xref:System.Windows.Forms.DataGridView.RowValidated>   
 <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded>   
 <xref:System.Windows.Forms.DataGridView.CancelRowEdit>   
 <xref:System.Windows.Forms.DataGridView.UserDeletingRow>   
 [Ottimizzazione delle prestazioni nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)   
 [Procedure consigliate per ridimensionare il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)   
 [Implementazione del modo virtuale con caricamento dati JIT nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)   
 [Procedura: implementare il modo virtuale nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-implement-virtual-mode-in-the-windows-forms-datagridview-control.md)