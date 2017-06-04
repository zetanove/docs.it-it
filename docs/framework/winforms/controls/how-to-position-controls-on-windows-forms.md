---
title: "Procedura: posizionare i controlli in Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Location"
  - "Location.Y"
  - "Location.X"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli [Windows Form]"
  - "controlli [Windows Form], spostamento"
  - "controlli [Windows Form], posizionamento"
  - "guide di allineamento"
ms.assetid: 4693977e-34a4-4f19-8221-68c3120c2b2b
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: posizionare i controlli in Windows Form
Per posizionare i controlli, utilizzare Progettazione Windows Form o specificare la proprietà <xref:System.Windows.Forms.Control.Location%2A>.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per posizionare un controllo nell'area di progettazione di Progettazione Windows Form  
  
-   Trascinare il controllo nella posizione desiderata con il mouse.  
  
    > [!NOTE]
    >  Selezionare il controllo e spostarlo con i tasti di direzione per posizionarlo più accuratamente.  Un ulteriore supporto per il posizionamento accurato dei controlli nel form è fornito dalle *guide di allineamento*.  Per ulteriori informazioni, vedere [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando guide di allineamento](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md).  
  
### Per posizionare un controllo utilizzando la finestra Proprietà  
  
1.  Fare clic sul controllo che si desidera posizionare.  
  
2.  Nella finestra **Proprietà** digitare i valori per la proprietà <xref:System.Windows.Forms.Control.Location%2A>, separati da una virgola, per posizionare il controllo nel relativo contenitore.  
  
     Il primo numero \(X\) rappresenta la distanza dal bordo sinistro del contenitore, il secondo numero \(Y\) rappresenta la distanza dal bordo superiore dell'area del contenitore, misurata in pixel.  
  
    > [!NOTE]
    >  È possibile espandere la proprietà <xref:System.Windows.Forms.Control.Location%2A> per inserire i valori **X** e **Y** singolarmente.  
  
### Per posizionare un controllo a livello di codice  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.Control.Location%2A> del controllo su <xref:System.Drawing.Point>.  
  
    ```vb  
    Button1.Location = New Point(100, 100)  
    ```  
  
    ```csharp  
    button1.Location = new Point(100, 100);  
    ```  
  
    ```cpp  
    button1->Location = Point(100, 100);  
    ```  
  
2.  Modificare la coordinata X della posizione del controllo utilizzando la sottoproprietà <xref:System.Windows.Forms.Control.Left%2A>.  
  
    ```vb  
    Button1.Left = 300  
    ```  
  
    ```csharp  
    button1.Left = 300;  
    ```  
  
    ```cpp  
    button1->Left = 300;  
    ```  
  
### Per incrementare la posizione di un controllo a livello di codice  
  
1.  Impostare la sottoproprietà <xref:System.Windows.Forms.Control.Left%2A> per incrementare la coordinata X del controllo.  
  
    ```vb  
    Button1.Left += 200  
    ```  
  
    ```csharp  
    button1.Left += 200;  
    ```  
  
    ```cpp  
    button1->Left += 200;  
    ```  
  
    > [!NOTE]
    >  Utilizzare la proprietà <xref:System.Windows.Forms.Control.Location%2A> per impostare contemporaneamente le posizioni X e Y di un controllo.  Per impostare una posizione singolarmente, utilizzare la sottoproprietà <xref:System.Windows.Forms.Control.Left%2A> \(**X**\) o <xref:System.Windows.Forms.Control.Top%2A> \(**Y**\) del controllo.  Non tentare di impostare implicitamente le coordinate X e Y della struttura <xref:System.Drawing.Point> che rappresenta la posizione del pulsante, poiché tale struttura contiene una copia delle coordinate del pulsante.  
  
## Vedere anche  
 [Controlli per Windows Form](../../../../docs/framework/winforms/controls/index.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando guide di allineamento](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando TableLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando FlowLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)   
 [Disposizione di controlli in Windows Form](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [Impostazione delle etichette di singoli controlli Windows Form e creazione dei relativi tasti di scelta rapida](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [Controlli Windows Form per funzione](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)   
 [How to: Set the Screen Location of Windows Forms](http://msdn.microsoft.com/it-it/cb023ab7-dea7-4284-9aa6-8c03c59b60c6)