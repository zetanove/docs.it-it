---
title: "Procedura: stampare un form utilizzando il componente PrintForm (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "form, stampa"
ms.assetid: df963bf6-3ee1-49f4-8b2e-1d95d1beb0be
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Procedura: stampare un form utilizzando il componente PrintForm (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> consente di stampare rapidamente un'immagine di un form così come viene visualizzata sullo schermo senza usare un componente <xref:System.Drawing.Printing.PrintDocument>. Le procedure seguenti illustrano come stampare un form in una stampante, una finestra di anteprima di stampa e un file Encapsulated PostScript.  
  
 I controlli PowerPacks non sono più inclusi in Visual Studio, ma è possibile scaricarli dall'[Area download](http://www.microsoft.com/en-us/download/details.aspx?id=25169).  
  
### Per stampare un form sulla stampante predefinita  
  
1.  Nella **casella degli strumenti** fare clic sulla scheda **Visual Basic PowerPacks** e quindi trascinare il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> nel form.  
  
     Il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> viene aggiunto alla barra dei componenti.  
  
2.  Nella finestra **Proprietà** impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> su <xref:System.Drawing.Printing.PrintAction>.  
  
3.  Aggiungere il codice seguente nel gestore eventi appropriato \(ad esempio, nel gestore eventi `Click` per un controllo `Button` **Print**\).  
  
    ```  
    PrintForm1.Print()  
    ```  
  
### Per visualizzare un form in una finestra di anteprima di stampa  
  
1.  Nella **casella degli strumenti** fare clic sulla scheda **Visual Basic PowerPacks** e quindi trascinare il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> nel form.  
  
     Il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> viene aggiunto alla barra dei componenti.  
  
2.  Nella finestra **Proprietà** impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> su <xref:System.Drawing.Printing.PrintAction>.  
  
3.  Aggiungere il codice seguente nel gestore eventi appropriato \(ad esempio, nel gestore eventi `Click` per un controllo `Button` **Print**\).  
  
    ```  
    PrintForm1.Print()  
    ```  
  
### Per stampare un form in un file  
  
1.  Nella **casella degli strumenti** fare clic sulla scheda **Visual Basic PowerPacks** e quindi trascinare il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> nel form.  
  
     Il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> viene aggiunto alla barra dei componenti.  
  
2.  Nella finestra **Proprietà** impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> su <xref:System.Drawing.Printing.PrintAction>.  
  
3.  Facoltativamente, selezionare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintFileName%2A> e digitare il percorso completo e il nome del file di destinazione.  
  
     Se si salta questo passaggio, all'utente verrà richiesto di specificare un nome di file in fase di esecuzione.  
  
4.  Aggiungere il codice seguente nel gestore eventi appropriato \(ad esempio, nel gestore eventi `Click` per un controllo `Button` **Print**\).  
  
    ```  
    PrintForm1.Print()  
    ```  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>   
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintFileName%2A>   
 [Procedura: stampare l'area client di un form](../../../visual-basic/developing-apps/printing/how-to-print-the-client-area-of-a-form.md)   
 [Procedura: stampare aree client e non client di un form](../../../visual-basic/developing-apps/printing/how-to-print-client-and-non-client-areas-of-a-form.md)   
 [Procedura: stampare un form scorrevole](../../../visual-basic/developing-apps/printing/how-to-print-a-scrollable-form.md)   
 [PrintForm Component](../../../visual-basic/developing-apps/printing/printform-component.md)