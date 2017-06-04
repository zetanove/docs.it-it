---
title: "Procedura: rilevare gli elementi selezionati nel controllo CheckedListBox di Windows Form | Microsoft Docs"
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
  - "caselle di controllo, rilevamento stato selezionato"
  - "CheckedListBox (controllo) [Windows Form], rilevamento stato selezionato"
ms.assetid: 178b477d-27c9-489c-8914-44a9623a4d41
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: rilevare gli elementi selezionati nel controllo CheckedListBox di Windows Form
Per la presentazione di dati in un controllo <xref:System.Windows.Forms.CheckedListBox> di Windows Form è possibile scorrere la raccolta memorizzata nella proprietà <xref:System.Windows.Forms.CheckedListBox.CheckedItems%2A> o esaminare l'elenco utilizzando il metodo <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A> per rilevare gli elementi selezionati.  Il metodo <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A> accetta il numero di indice di un elemento come argomento e restituisce `true` o `false`.  Le proprietà <xref:System.Windows.Forms.ListBox.SelectedItems%2A> e <xref:System.Windows.Forms.ListBox.SelectedIndices%2A>, contrariamente a quanto si potrebbe pensare, non rilevano gli elementi selezionati, ma quelli evidenziati.  
  
### Per rilevare gli elementi selezionati in un controllo CheckedListBox  
  
1.  Scorrere la raccolta <xref:System.Windows.Forms.CheckedListBox.CheckedItems%2A> partendo da 0, trattandosi di una raccolta a base zero.  Si noti che il metodo fornirà il numero dell'elemento nell'elenco degli elementi selezionati, non nell'intero elenco.  Di conseguenza, se il primo elemento dell'elenco non è selezionato e il secondo sì, nel codice che segue verrà visualizzato un testo analogo a "Checked Item 1 \= MyListItem2".  
  
    ```vb  
    ' Determine if there are any items checked.  
    If CheckedListBox1.CheckedItems.Count <> 0 Then  
       ' If so, loop through all checked items and print results.  
       Dim x As Integer  
       Dim s As String = ""  
       For x = 0 To CheckedListBox1.CheckedItems.Count - 1  
          s = s & "Checked Item " & (x + 1).ToString & " = " & CheckedListBox1.CheckedItems(x).ToString & ControlChars.CrLf  
       Next x  
       MessageBox.Show(s)  
    End If  
  
    ```  
  
    ```csharp  
    // Determine if there are any items checked.  
    if(checkedListBox1.CheckedItems.Count != 0)  
    {  
       // If so, loop through all checked items and print results.  
       string s = "";  
       for(int x = 0; x <= checkedListBox1.CheckedItems.Count - 1 ; x++)  
       {  
          s = s + "Checked Item " + (x+1).ToString() + " = " + checkedListBox1.CheckedItems[x].ToString() + "\n";  
       }  
    MessageBox.Show (s);  
    }  
  
    ```  
  
    ```cpp  
    // Determine if there are any items checked.  
    if(checkedListBox1->CheckedItems->Count != 0)  
    {  
       // If so, loop through all checked items and print results.  
       String ^ s = "";  
       for(int x = 0; x <= checkedListBox1->CheckedItems->Count - 1; x++)  
       {  
          s = String::Concat(s, "Checked Item ", (x+1).ToString(),  
             " = ", checkedListBox1->CheckedItems[x]->ToString(),  
             "\n");  
       }  
       MessageBox::Show(s);  
    }  
    ```  
  
     \-oppure\-  
  
2.  Scorrere la raccolta <xref:System.Windows.Forms.CheckedListBox.Items%2A> partendo da 0, trattandosi di una raccolta a base zero, e chiamare il metodo <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A> per ogni elemento.  Tenere presente che questo metodo fornirà il numero dell'elemento nell'intero elenco. Di conseguenza, se il primo elemento dell'elenco non è selezionato e il secondo sì, verrà visualizzato un testo analogo a "Item 2 \= MyListItem2".  
  
    ```vb  
    Dim i As Integer  
    Dim s As String  
    s = "Checked Items:" & ControlChars.CrLf  
    For i = 0 To (CheckedListBox1.Items.Count - 1)  
       If CheckedListBox1.GetItemChecked(i) = True Then  
          s = s & "Item " & (i + 1).ToString & " = " & CheckedListBox1.Items(i).ToString & ControlChars.CrLf  
       End If  
    Next  
    MessageBox.Show(s)  
  
    ```  
  
    ```csharp  
    int i;  
    string s;   
    s = "Checked items:\n" ;  
    for (i = 0; i <= (checkedListBox1.Items.Count-1); i++)  
    {  
       if (checkedListBox1.GetItemChecked(i))  
       {  
          s = s + "Item " + (i+1).ToString() + " = " + checkedListBox1.Items[i].ToString() + "\n";  
       }  
    }  
    MessageBox.Show (s);  
  
    ```  
  
    ```cpp  
    int i;  
    String ^ s;   
    s = "Checked items:\n" ;  
    for (i = 0; i <= (checkedListBox1->Items->Count-1); i++)  
    {  
       if (checkedListBox1->GetItemChecked(i))  
       {  
          s = String::Concat(s, "Item ", (i+1).ToString(), " = ",  
             checkedListBox1->Item[i]->ToString(), "\n");  
       }  
    }  
    MessageBox::Show(s);  
    ```  
  
## Vedere anche  
 [Controlli Windows Form usati per elencare opzioni](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)