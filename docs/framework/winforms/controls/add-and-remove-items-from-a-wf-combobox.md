---
title: "Procedura: aggiungere e rimuovere elementi da un controllo ComboBox, ListBox o CheckedListBox Windows Form | Microsoft Docs"
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
  - "CheckedListBox (controllo) [Windows Form], aggiunta e rimozione di elementi"
  - "caselle combinate, aggiunta di elementi"
  - "caselle combinate, rimozione di elementi"
  - "ComboBox (controllo) [Windows Form], aggiunta e rimozione di elementi"
  - "caselle di riepilogo, aggiunta di elementi"
  - "caselle di riepilogo, rimozione di elementi"
  - "ListBox (controllo) [Windows Form], aggiunta e rimozione di elementi"
ms.assetid: 7224c8d2-4118-443e-ae1e-d7c17d1e69ee
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: aggiungere e rimuovere elementi da un controllo ComboBox, ListBox o CheckedListBox Windows Form
È possibile aggiungere elementi a una casella combinata, a una casella di riepilogo o a una casella di riepilogo selezionata in diversi modi perché tali controlli possono essere associati a diverse origini dati.  Tuttavia il metodo più semplice, descritto di seguito, non supporta l'associazione dati.  Gli elementi visualizzati sono costituiti in genere da stringhe, ma può essere utilizzato qualsiasi oggetto.  Il testo visualizzato nel controllo costituisce il valore restituito dal metodo `ToString`  dell'oggetto.  
  
### Per aggiungere elementi  
  
1.  Aggiungere la stringa o l'oggetto all'elenco utilizzando il metodo `Add` della classe `ObjectCollection`.  Alla raccolta viene fatto riferimento utilizzando la proprietà`Items` :  
  
    ```vb  
    ComboBox1.Items.Add("Tokyo")  
  
    ```  
  
    ```csharp  
    comboBox1.Items.Add("Tokyo");  
  
    ```  
  
    ```cpp  
    comboBox1->Items->Add("Tokyo");  
    ```  
  
     \-oppure\-  
  
2.  Inserire la stringa o l'oggetto nel punto desiderato all'interno dell'elenco utilizzando il metodo`Insert` :  
  
    ```vb  
    CheckedListBox1.Items.Insert(0, "Copenhagen")  
  
    ```  
  
    ```csharp  
    checkedListBox1.Items.Insert(0, "Copenhagen");  
  
    ```  
  
    ```cpp  
    checkedListBox1->Items->Insert(0, "Copenhagen");  
    ```  
  
     \-oppure\-  
  
3.  Assegnare un'intera matrice alla raccolta `Items` :  
  
    ```vb  
    Dim ItemObject(9) As System.Object  
    Dim i As Integer  
       For i = 0 To 9  
       ItemObject(i) = "Item" & i  
    Next i  
    ListBox1.Items.AddRange(ItemObject)  
  
    ```  
  
    ```csharp  
    System.Object[] ItemObject = new System.Object[10];  
    for (int i = 0; i <= 9; i++)  
    {  
       ItemObject[i] = "Item" + i;  
    }  
    listBox1.Items.AddRange(ItemObject);  
  
    ```  
  
    ```cpp  
    Array<System::Object^>^ ItemObject = gcnew Array<System::Object^>(10);  
    for (int i = 0; i <= 9; i++)  
    {  
       ItemObject[i] = String::Concat("Item", i.ToString());  
    }  
    listBox1->Items->AddRange(ItemObject);  
    ```  
  
### Per rimuovere un elemento  
  
1.  Chiamare il metodo`Remove` o`RemoveAt` per eliminare gli elementi.  
  
     `Remove` presenta un argomento che specifica l'elemento da rimuovere.`RemoveAt` rimuove l'elemento con il numero di indice specificato.  
  
    ```vb  
    ' To remove item with index 0:  
    ComboBox1.Items.RemoveAt(0)  
    ' To remove currently selected item:  
    ComboBox1.Items.Remove(ComboBox1.SelectedItem)  
    ' To remove "Tokyo" item:  
    ComboBox1.Items.Remove("Tokyo")  
  
    ```  
  
    ```csharp  
    // To remove item with index 0:  
    comboBox1.Items.RemoveAt(0);  
    // To remove currently selected item:  
    comboBox1.Items.Remove(comboBox1.SelectedItem);  
    // To remove "Tokyo" item:  
    comboBox1.Items.Remove("Tokyo");  
  
    ```  
  
    ```cpp  
    // To remove item with index 0:  
    comboBox1->Items->RemoveAt(0);  
    // To remove currently selected item:  
    comboBox1->Items->Remove(comboBox1->SelectedItem);  
    // To remove "Tokyo" item:  
    comboBox1->Items->Remove("Tokyo");  
    ```  
  
### Per rimuovere tutti gli elementi  
  
1.  Chiamare il metodo `Clear` per rimuovere tutti gli elementi dalla raccolta:  
  
    ```vb  
    ListBox1.Items.Clear()  
  
    ```  
  
    ```csharp  
    listBox1.Items.Clear();  
  
    ```  
  
    ```cpp  
    listBox1->Items->Clear();  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ComboBox>   
 <xref:System.Windows.Forms.ListBox>   
 <xref:System.Windows.Forms.CheckedListBox>   
 [Procedura: ordinare il contenuto di un controllo ComboBox, ListBox o CheckedListBox Windows Form](../../../../docs/framework/winforms/controls/sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)   
 [Quando utilizzare un controllo ComboBox Windows Form anziché un controllo ListBox](../../../../docs/framework/winforms/controls/when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)   
 [Controlli Windows Form usati per elencare opzioni](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)