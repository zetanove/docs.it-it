---
title: "Procedura: garantire che la riga selezionata in una tabella figlio rimanga nella posizione corretta | Microsoft Docs"
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
  - "memorizzazione nella cache [.NET Framework], elementi figlio (posizione)"
  - "elementi figlio (posizione)"
  - "tabelle figlio (selezione di riga)"
  - "posizione corrente di elementi figlio"
  - "associazione dati [.NET Framework], selezione di righe"
  - "Master-Details (visualizzazione) [Windows Form]"
  - "visualizzazione Master-Details"
  - "padre-figlio (visualizzazione) [Windows Form]"
  - "reimpostazione della posizione di elementi figlio"
  - "posizione della riga [Windows Form]"
ms.assetid: c5fa2562-43a4-46fa-a604-52d8526a87bd
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: garantire che la riga selezionata in una tabella figlio rimanga nella posizione corretta
Quando si usa il data binding in Windows Form, spesso i dati vengono mostrati in una visualizzazione denominata padre\/figlio o master\/dettagli  Si tratta di uno scenario di data binding in cui i dati provenienti dalla stessa origine vengono visualizzati in due controlli.  Se si modifica la selezione in un controllo, automaticamente vengono modificati anche i dati visualizzati nel secondo controllo.  Ad esempio, il primo controllo può contenere un elenco di clienti e il secondo un elenco di ordini correlati al cliente selezionato nel primo controllo.  
  
 A partire da .NET Framework versione 2.0, quando si visualizzano i dati in una visualizzazione padre\/figlio può essere necessario effettuare alcuni passaggi aggiuntivi per assicurarsi che la riga attualmente selezionata nella tabella figlio non venga reimpostata sulla prima riga della tabella.  A tale scopo, è necessario memorizzare nella cache la posizione della tabella figlio e reimpostarla dopo aver modificato la tabella padre.  In genere, la tabella figlio viene reimpostata la prima volta che si modifica un campo in una riga della tabella padre.  
  
### Per memorizzare nella cache la posizione corrente della tabella figlio  
  
1.  Dichiarare una variabile Integer per archiviare la posizione dell'elenco figlio e una variabile booleana per archiviare se memorizzare nella cache la posizione della tabella figlio.  
  
     [!code-csharp[System.Windows.Forms.CurrencyManagerReset#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.CurrencyManagerReset#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#4)]  
  
2.  Gestire l'evento <xref:System.Windows.Forms.CurrencyManager.ListChanged> per l'oggetto <xref:System.Windows.Forms.CurrencyManager> del binding e individuare un oggetto <xref:System.ComponentModel.ListChangedType> di <xref:System.ComponentModel.ListChangedType>.  
  
3.  Controllare la posizione corrente dell'oggetto <xref:System.Windows.Forms.CurrencyManager>.  Se è maggiore del primo elemento dell'elenco, in genere 0, salvarlo in una variabile.  
  
     [!code-csharp[System.Windows.Forms.CurrencyManagerReset#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.CurrencyManagerReset#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#2)]  
  
4.  Gestire l'evento <xref:System.Windows.Forms.BindingManagerBase.CurrentChanged> dell'elenco padre per l'oggetto CurrencyManager padre.  Nel gestore impostare il valore booleano per indicare che non si tratta di uno scenario di memorizzazione nella cache.  Se si verifica l'evento <xref:System.Windows.Forms.BindingManagerBase.CurrentChanged>, la modifica all'elemento padre sarà una modifica alla posizione dell'elenco e non una modifica al valore dell'elemento.  
  
     [!code-csharp[System.Windows.Forms.CurrencyManagerReset#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.CurrencyManagerReset#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#5)]  
  
### Per reimpostare la posizione dell'elemento figlio  
  
1.  Gestire l'evento <xref:System.Windows.Forms.BindingManagerBase.PositionChanged> per l'oggetto <xref:System.Windows.Forms.CurrencyManager> del binding figlio.  
  
2.  Reimpostare la posizione della tabella figlio sulla posizione memorizzata nella cache salvata nella procedura precedente.  
  
     [!code-csharp[System.Windows.Forms.CurrencyManagerReset#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.CurrencyManagerReset#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#3)]  
  
## Esempio  
 L'esempio seguente illustra come salvare la posizione corrente nell'oggetto <xref:System.Windows.Forms.CurrencyManager> per una tabella figlio e reimpostare la posizione dopo aver effettuato una modifica nella tabella padre.  In questo esempio sono presenti due controlli <xref:System.Windows.Forms.DataGridView> associati a due tabelle in un oggetto <xref:System.Data.DataSet> mediante un componente <xref:System.Windows.Forms.BindingSource>.  Tra le due tabelle viene stabilita una relazione, che viene aggiunta all'oggetto <xref:System.Data.DataSet>.  La posizione nella tabella figlio viene impostata inizialmente sulla terza riga a mero scopo esemplificativo.  
  
 [!code-csharp[System.Windows.Forms.CurrencyManagerReset#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.CurrencyManagerReset#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#1)]  
  
 Per testare l'esempio di codice, eseguire la procedura seguente:  
  
1.  Eseguire l'esempio.  
  
2.  Verificare che la casella di controllo **Memorizza nella cache e reimposta posizione** sia selezionata.  
  
3.  Fare clic sul pulsante **Cancella campo padre** per provocare una modifica in un campo della tabella padre.  Notare che la riga selezionata nella tabella figlio non cambia.  
  
4.  Chiudere ed eseguire nuovamente l'esempio.  È necessario eseguire questa procedura perché la reimpostazione si verifica solo in seguito alla prima modifica nella riga padre.  
  
5.  Deselezionare la casella di controllo **Memorizza nella cache e reimposta posizione**.  
  
6.  Fare clic sul pulsante **Cancella campo padre**.  Notare che la riga selezionata nella tabella figlio diventa la prima riga.  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System, System.Data, System.Drawing, System.Windows.Forms e System.XML.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 [Procedura: garantire la sincronizzazione di più controlli associati alla stessa origine dati](../../../docs/framework/winforms/multiple-controls-bound-to-data-source-synchronized.md)   
 [Il componente BindingSource](../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [Associazione dati e Windows Form](../../../docs/framework/winforms/data-binding-and-windows-forms.md)