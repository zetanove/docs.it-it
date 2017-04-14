---
title: "Procedura: impostare il valore visualizzato da un controllo ProgressBar Windows Form | Microsoft Docs"
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
  - "Increment (metodo)"
  - "PerformStep (metodo)"
  - "stato (controlli), impostazione valore visualizzato"
  - "ProgressBar (controllo) [Windows Form], impostazione valore visualizzato"
  - "Step (proprietà)"
  - "Value (proprietà)"
ms.assetid: 0e5010ad-1e9a-4271-895e-5a3d24d37a26
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: impostare il valore visualizzato da un controllo ProgressBar Windows Form
> [!IMPORTANT]
>  Benché il controllo <xref:System.Windows.Forms.ToolStripProgressBar> sostituisca il controllo <xref:System.Windows.Forms.ProgressBar> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.ProgressBar> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  
  
 In [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] sono disponibili vari modi per visualizzare un determinato valore all'interno del controllo <xref:System.Windows.Forms.ProgressBar>.  La scelta dell'approccio da utilizzare dipende dall'attività da eseguire o dal problema che si intende risolvere.  Nella tabella che segue sono elencati gli approcci utilizzabili.  
  
|Approccio|Descrizione|  
|---------------|-----------------|  
|Impostare direttamente il valore del controllo <xref:System.Windows.Forms.ProgressBar>.|Questo tipo di approccio è utile per le attività in cui è noto il totale dell'elemento misurato, ad esempio per la lettura di record da un'origine dati.  È inoltre un metodo semplice per impostare il valore una o due volte.  Questa procedura, infine, è ottimale per ridurre il valore visualizzato nell'indicatore di stato.|  
|Aumentare il valore visualizzato dal controllo <xref:System.Windows.Forms.ProgressBar> in base a un valore fisso.|Si tratta di un approccio utile quando si visualizza un conteggio semplice tra il valore minimo e quello massimo, ad esempio il tempo trascorso o il numero di file elaborati su un totale noto.|  
|Aumentare il valore visualizzato dal controllo <xref:System.Windows.Forms.ProgressBar> in base a un valore variabile.|Questo approccio è invece utile quando occorre modificare il valore visualizzato più volte con quantità diverse.  Un esempio di questa situazione è dato dalla visualizzazione dello spazio su disco rigido impiegato per la scrittura di una serie di file sul disco.|  
  
 Il modo più diretto per impostare il valore visualizzato da un indicatore di stato consiste nell'impostare la proprietà <xref:System.Windows.Forms.ProgressBar.Value%2A>.  Questa operazione può essere eseguita in fase di progettazione o in fase di esecuzione.  
  
### Per impostare direttamente il valore di ProgressBar  
  
1.  Impostare i valori <xref:System.Windows.Forms.ProgressBar.Minimum%2A> e <xref:System.Windows.Forms.ProgressBar.Maximum%2A> del controllo <xref:System.Windows.Forms.ProgressBar>.  
  
2.  Nel codice impostare la proprietà <xref:System.Windows.Forms.ProgressBar.Value%2A> del controllo su un valore integer compreso tra i valori minimo e massimo stabiliti.  
  
    > [!NOTE]
    >  Se si imposta la proprietà <xref:System.Windows.Forms.ProgressBar.Value%2A> su un valore non incluso nell'intervallo compreso tra i valori stabiliti per le proprietà <xref:System.Windows.Forms.ProgressBar.Minimum%2A> e <xref:System.Windows.Forms.ProgressBar.Maximum%2A>, verrà generata un'eccezione <xref:System.ArgumentException>.  
  
     Nell'esempio di codice seguente viene illustrata l'impostazione diretta del valore <xref:System.Windows.Forms.ProgressBar>.  Nel codice vengono letti i record da un'origine dati, l'indicatore di stato viene aggiornato e viene applicata un'etichetta per ogni lettura di record di dati.  Per l'esempio è necessario che sul form siano presenti un controllo <xref:System.Windows.Forms.Label>, un controllo <xref:System.Windows.Forms.ProgressBar> e una tabella di dati con una riga denominata`CustomerRow` con campi`FirstName` e`Last Name` .  
  
    ```vb  
    Public Sub CreateNewRecords()  
       ' Sets the progress bar's Maximum property to  
       ' the total number of records to be created.  
       ProgressBar1.Maximum = 20  
  
       ' Creates a new record in the dataset.  
       ' NOTE: The code below will not compile, it merely  
       ' illustrates how the progress bar would be used.  
       Dim anyRow As CustomerRow = DatasetName.ExistingTable.NewRow  
       anyRow.FirstName = "Stephen"  
       anyRow.LastName = "James"  
       ExistingTable.Rows.Add(anyRow)  
  
       ' Increases the value displayed by the progress bar.  
       ProgressBar1.Value += 1  
       ' Updates the label to show that a record was read.  
       Label1.Text = "Records Read = " & ProgressBar1.Value.ToString()  
    End Sub  
  
    ```  
  
    ```csharp  
    public void createNewRecords()  
    {  
       // Sets the progress bar's Maximum property to  
       // the total number of records to be created.  
       progressBar1.Maximum = 20;  
  
       // Creates a new record in the dataset.  
       // NOTE: The code below will not compile, it merely  
       // illustrates how the progress bar would be used.  
       CustomerRow anyRow = DatasetName.ExistingTable.NewRow();  
       anyRow.FirstName = "Stephen";  
       anyRow.LastName = "James";  
       ExistingTable.Rows.Add(anyRow);  
  
       // Increases the value displayed by the progress bar.  
       progressBar1.Value += 1;  
       // Updates the label to show that a record was read.  
       label1.Text = "Records Read = " + progressBar1.Value.ToString();  
    }  
    ```  
  
     Per visualizzare uno stato che progredisce in base a un intervallo fisso, è possibile impostare il valore e chiamare un metodo che aumenta il valore del controllo <xref:System.Windows.Forms.ProgressBar> in base a tale intervallo.  Questa soluzione è utile per i timer e per altri scenari in cui il progresso non viene misurato come percentuale del totale.  
  
### Per aumentare il valore dell'indicatore di stato in base a un valore fisso  
  
1.  Impostare i valori <xref:System.Windows.Forms.ProgressBar.Minimum%2A> e <xref:System.Windows.Forms.ProgressBar.Maximum%2A> del controllo <xref:System.Windows.Forms.ProgressBar>.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.ProgressBar.Step%2A> del controllo su un intero che rappresenta la quantità in base alla quale aumentare il valore visualizzato dell'indicatore di stato.  
  
3.  Chiamare il metodo <xref:System.Windows.Forms.ProgressBar.PerformStep%2A> per modificare il valore visualizzato in base alla quantità impostata nella proprietà <xref:System.Windows.Forms.ProgressBar.Step%2A>.  
  
     Nell'esempio di codice seguente viene illustrato in che modo mantenere il conteggio dei file in un'operazione di copia mediante un indicatore di stato.  
  
     Nell'esempio, man mano che ogni file viene letto in memoria, l'indicatore di stato e l'etichetta vengono aggiornati per riflettere il numero totale di file letti.  Per l'esempio è necessario che sul form siano presenti un controllo <xref:System.Windows.Forms.Label> e un controllo <xref:System.Windows.Forms.ProgressBar>.  
  
    ```vb  
    Public Sub LoadFiles()  
       ' Sets the progress bar's minimum value to a number representing  
       ' no operations complete -- in this case, no files read.  
       ProgressBar1.Minimum = 0  
       ' Sets the progress bar's maximum value to a number representing  
       ' all operations complete -- in this case, all five files read.  
       ProgressBar1.Maximum = 5  
       ' Sets the Step property to amount to increase with each iteration.  
       ' In this case, it will increase by one with every file read.  
       ProgressBar1.Step = 1  
  
       ' Dimensions a counter variable.  
       Dim i As Integer  
       ' Uses a For...Next loop to iterate through the operations to be  
       ' completed. In this case, five files are to be copied into memory,  
       ' so the loop will execute 5 times.  
       For i = 0 To 4  
          ' Insert code to copy a file  
          ProgressBar1.PerformStep()  
          ' Update the label to show that a file was read.  
          Label1.Text = "# of Files Read = " & ProgressBar1.Value.ToString  
       Next i  
    End Sub  
  
    ```  
  
    ```csharp  
    public void loadFiles()  
    {  
       // Sets the progress bar's minimum value to a number representing  
       // no operations complete -- in this case, no files read.  
       progressBar1.Minimum = 0;  
       // Sets the progress bar's maximum value to a number representing  
       // all operations complete -- in this case, all five files read.  
       progressBar1.Maximum = 5;  
       // Sets the Step property to amount to increase with each iteration.  
       // In this case, it will increase by one with every file read.  
       progressBar1.Step = 1;  
  
       // Uses a for loop to iterate through the operations to be  
       // completed. In this case, five files are to be copied into memory,  
       // so the loop will execute 5 times.  
       for (int i = 0; i <= 4; i++)  
       {  
          // Inserts code to copy a file  
          progressBar1.PerformStep();  
          // Updates the label to show that a file was read.  
          label1.Text = "# of Files Read = " + progressBar1.Value.ToString();  
       }  
    }  
    ```  
  
     È infine possibile aumentare il valore visualizzato da un indicatore di stato in modo che ogni aumento corrisponda a una quantità univoca.  Questo approccio è utile per tenere traccia di una serie di operazioni univoche, come la scrittura di file di dimensioni diverse su un disco rigido, o per misurare il progresso come percentuale del totale.  
  
### Per aumentare il valore dell'indicatore di stato in base a un valore dinamico  
  
1.  Impostare i valori <xref:System.Windows.Forms.ProgressBar.Minimum%2A> e <xref:System.Windows.Forms.ProgressBar.Maximum%2A> del controllo <xref:System.Windows.Forms.ProgressBar>.  
  
2.  Chiamare il metodo <xref:System.Windows.Forms.ProgressBar.Increment%2A> per modificare il valore visualizzato in base a un intero specificato.  
  
     Nell'esempio di codice seguente viene illustrato come calcolare lo spazio su disco utilizzato durante un'operazione di copia mediante un indicatore di stato.  
  
     Nell'esempio, man mano che ogni file viene scritto sul disco rigido, l'indicatore di stato e l'etichetta vengono aggiornati per riflettere la quantità di spazio su disco disponibile.  Per l'esempio è necessario che sul form siano presenti un controllo <xref:System.Windows.Forms.Label> e un controllo <xref:System.Windows.Forms.ProgressBar>.  
  
    ```vb  
    Public Sub ReadFiles()  
       ' Sets the progress bar's minimum value to a number   
       ' representing the hard disk space before the files are read in.  
       ' You will most likely have to set this using a system call.  
       ' NOTE: The code below is meant to be an example and  
       ' will not compile.  
       ProgressBar1.Minimum = AvailableDiskSpace()  
       ' Sets the progress bar's maximum value to a number   
       ' representing the total hard disk space.  
       ' You will most likely have to set this using a system call.  
       ' NOTE: The code below is meant to be an example   
       ' and will not compile.  
       ProgressBar1.Maximum = TotalDiskSpace()  
  
       ' Dimension a counter variable.  
       Dim i As Integer  
       ' Uses a For...Next loop to iterate through the operations to be  
       ' completed. In this case, five files are to be written to the disk,  
       ' so it will execute the loop 5 times.  
       For i = 1 To 5  
          ' Insert code to read a file into memory and update file size.  
          ' Increases the progress bar's value based on the size of   
          ' the file currently being written.  
          ProgressBar1.Increment(FileSize)  
          ' Updates the label to show available drive space.  
          Label1.Text = "Current Disk Space Used = " &_   
          ProgressBar1.Value.ToString()  
       Next i  
    End Sub  
  
    ```  
  
    ```csharp  
    public void readFiles()  
    {  
       // Sets the progress bar's minimum value to a number   
       // representing the hard disk space before the files are read in.  
       // You will most likely have to set this using a system call.  
       // NOTE: The code below is meant to be an example and   
       // will not compile.  
       progressBar1.Minimum = AvailableDiskSpace();  
       // Sets the progress bar's maximum value to a number   
       // representing the total hard disk space.  
       // You will most likely have to set this using a system call.  
       // NOTE: The code below is meant to be an example   
       // and will not compile.  
       progressBar1.Maximum = TotalDiskSpace();  
  
       // Uses a for loop to iterate through the operations to be  
       // completed. In this case, five files are to be written  
       // to the disk, so it will execute the loop 5 times.  
       for (int i = 1; i<= 5; i++)  
       {  
          // Insert code to read a file into memory and update file size.  
          // Increases the progress bar's value based on the size of   
          // the file currently being written.  
          progressBar1.Increment(FileSize);  
          // Updates the label to show available drive space.  
          label1.Text = "Current Disk Space Used = " + progressBar1.Value.ToString();  
       }  
    }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ProgressBar>   
 <xref:System.Windows.Forms.ToolStripProgressBar>   
 [Cenni preliminari sul controllo ProgressBar](../../../../docs/framework/winforms/controls/progressbar-control-overview-windows-forms.md)   
 [Controllo ProgressBar](../../../../docs/framework/winforms/controls/progressbar-control-windows-forms.md)