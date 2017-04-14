---
title: "Procedura: accedere a elementi specifici di un controllo ComboBox, ListBox o CheckedListBox Windows Form | Microsoft Docs"
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
  - "CheckedListBox (controllo) [Windows Form], accesso a elementi"
  - "caselle combinate, accesso a elementi"
  - "ComboBox (controllo) [Windows Form], accesso a elementi"
  - "caselle di riepilogo, accesso a elementi"
  - "ListBox (controllo) [Windows Form], accesso a elementi"
  - "ListBox (controllo) [Windows Form], restituzione di informazioni sugli elementi"
ms.assetid: 1216742f-bcf9-4ff8-8a62-d7c9053c2b96
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: accedere a elementi specifici di un controllo ComboBox, ListBox o CheckedListBox Windows Form
L'accesso a elementi specifici di una casella combinata, di una casella di riepilogo o di una casella di riepilogo selezionata è un'attività di importanza fondamentale.  Consente infatti di stabilire a livello di codice il contenuto di un elenco in ogni singolo percorso.  
  
### Per accedere a un elemento specifico  
  
1.  Eseguire una query sulla raccolta`Items` utilizzando l'indice dell'elemento specifico:  
  
    ```vb  
    Private Function GetItemText(i As Integer) As String  
       ' Return the text of the item using the index:  
       Return ComboBox1.Items(i).ToString  
    End Function  
  
    ```  
  
    ```csharp  
    private string GetItemText(int i)  
    {  
       // Return the text of the item using the index:  
       return (comboBox1.Items[i].ToString());  
    }  
  
    ```  
  
    ```cpp  
    private:  
       String^ GetItemText(int i)  
       {  
          // Return the text of the item using the index:  
          return (comboBox1->Items->Item[i]->ToString());  
       }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ComboBox>   
 <xref:System.Windows.Forms.ListBox>   
 <xref:System.Windows.Forms.CheckedListBox>   
 [Controlli Windows Form usati per elencare opzioni](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)