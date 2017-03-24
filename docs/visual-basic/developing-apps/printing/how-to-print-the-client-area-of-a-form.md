---
title: "Procedura: stampare l&#39;area client di un form (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "area client, stampa"
ms.assetid: c06c9c0e-bc07-48cd-9596-e29a2ff96236
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Procedura: stampare l&#39;area client di un form (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> consente di stampare rapidamente un'immagine di un form senza usare un componente <xref:System.Drawing.Printing.PrintDocument>. La procedura seguente illustra come stampare solo l'area client di un form, senza la barra del titolo, i bordi e le barre di scorrimento.  
  
 I controlli PowerPacks non sono più inclusi in Visual Studio, ma è possibile scaricarli dall'[Area download](http://www.microsoft.com/en-us/download/details.aspx?id=25169).  
  
### Per stampare l'area client di un form  
  
1.  Nella **casella degli strumenti** fare clic sulla scheda **Visual Basic PowerPacks** e quindi trascinare il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> nel form.  
  
     Il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> viene aggiunto alla barra dei componenti.  
  
2.  Nella finestra **Proprietà** impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> su <xref:System.Drawing.Printing.PrintAction>.  
  
3.  Aggiungere il codice seguente nel gestore eventi appropriato \(ad esempio, nel gestore eventi `Click` per un controllo `Button` **Print**\).  
  
    ```  
    PrintForm1.Print(Me, PowerPacks.Printing.PrintForm.PrintOption.ClientAreaOnly)  
    ```  
  
    > [!NOTE]
    >  In alcuni sistemi operativi il testo o la grafica disegnati mediante i metodi <xref:System.Drawing.Graphics> potrebbero non essere stampati correttamente. In questo caso, usare il metodo di stampa compatibile: `PrintForm1.Print(Me, PowerPacks.Printing.PrintForm.PrintOption CompatibleModeClientAreaOnly).`  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>   
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>   
 [PrintForm Component](../../../visual-basic/developing-apps/printing/printform-component.md)   
 [Procedura: stampare aree client e non client di un form](../../../visual-basic/developing-apps/printing/how-to-print-client-and-non-client-areas-of-a-form.md)   
 [Procedura: stampare un form scorrevole](../../../visual-basic/developing-apps/printing/how-to-print-a-scrollable-form.md)