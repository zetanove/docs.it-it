---
title: "Procedura: stampare un form scorrevole (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "intero form, stampa"
  - "form scorrevole, stampa"
ms.assetid: 1196e1cf-b77f-4928-a3e4-85b51ba3787d
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Procedura: stampare un form scorrevole (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> consente di stampare rapidamente un'immagine di un form senza usare un componente <xref:System.Drawing.Printing.PrintDocument>. Per impostazione predefinita, viene stampata solo la parte visibile del form. Se un utente ha ridimensionato il form in fase di esecuzione, l'immagine potrebbe non essere stampata come previsto. La procedura seguente illustra come stampare l'intera area client di un form scorrevole, anche se il form è stato ridimensionato.  
  
 I controlli PowerPacks non sono più inclusi in Visual Studio, ma è possibile scaricarli dall'[Area download](http://www.microsoft.com/en-us/download/details.aspx?id=25169).  
  
### Per stampare l'intera area client di un form scorrevole  
  
1.  Nella **casella degli strumenti** fare clic sulla scheda **Visual Basic PowerPacks** e quindi trascinare il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> nel form.  
  
     Il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> verrà aggiunto alla barra dei componenti.  
  
2.  Nella finestra **Proprietà** impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> su <xref:System.Drawing.Printing.PrintAction>.  
  
3.  Aggiungere il codice seguente nel gestore eventi appropriato \(ad esempio nel gestore eventi `Click` per un controllo **Print**`Button`\).  
  
    ```  
    PrintForm1.Print(Me, PowerPacks.Printing.PrintForm.PrintOption.Scrollable)  
    ```  
  
    > [!NOTE]
    >  In alcuni sistemi operativi il testo o la grafica disegnati mediante i metodi <xref:System.Drawing.Graphics> potrebbero non essere stampati correttamente. In questo caso, non sarà possibile eseguire la stampa con il parametro `Scrollable`.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>   
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>   
 [PrintForm Component](../../../visual-basic/developing-apps/printing/printform-component.md)   
 [Procedura: stampare l'area client di un form](../../../visual-basic/developing-apps/printing/how-to-print-the-client-area-of-a-form.md)   
 [Procedura: stampare aree client e non client di un form](../../../visual-basic/developing-apps/printing/how-to-print-client-and-non-client-areas-of-a-form.md)