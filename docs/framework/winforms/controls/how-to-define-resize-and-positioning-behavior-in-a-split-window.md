---
title: "Procedura: definire il ridimensionamento e il posizionamento in una finestra divisa | Microsoft Docs"
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
  - "finestre divise, ridimensionamento"
  - "SplitContainer (controllo) [Windows Form], ridimensionamento"
  - "finestre con separatore, ridimensionamento"
ms.assetid: 9bf73f36-ed2d-4a02-b15a-0770eff4fdfa
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: definire il ridimensionamento e il posizionamento in una finestra divisa
I pannelli del controllo <xref:System.Windows.Forms.SplitContainer> possono essere facilmente ridimensionati e modificati dagli utenti.  È tuttavia possibile controllare la barra di divisione anche a livello di codice, determinandone la posizione e l'entità dello spostamento.  
  
 La proprietà <xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A> e le altre proprietà del controllo <xref:System.Windows.Forms.SplitContainer> consentono di controllare con precisione il comportamento dell'interfaccia utente, in modo da rispondere a esigenze specifiche.  Queste proprietà sono elencate nella tabella che segue.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|Proprietà <xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A>|Determina se la barra di divisione può essere spostata tramite mouse o tastiera.|  
|Proprietà <xref:System.Windows.Forms.SplitContainer.SplitterDistance%2A>|Determina la distanza in pixel dal bordo superiore o sinistro alla barra di divisione mobile.|  
|Proprietà <xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A>|Determina la distanza minima in pixel per cui la barra di divisione può essere spostata dall'utente.|  
  
 Nell'esempio che segue la proprietà <xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A> viene modificata in modo da creare un effetto di "aggancio della barra di divisione". Quando l'utente trascina la barra di divisione la posizione viene incrementata in unità di 10 pixel, anziché di 1 pixel come avviene per impostazione predefinita.  
  
### Per definire il comportamento di ridimensionamento del controllo SplitContainer  
  
1.  In una routine impostare la proprietà <xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A> sulle dimensioni desiderate, in modo da ottenere l'effetto di aggancio del separatore.  
  
     Nell'esempio di codice che segue, nell'ambito dell'evento <xref:System.Windows.Forms.Form.Load> del form la barra di divisione nel controllo <xref:System.Windows.Forms.SplitContainer> viene impostata in modo da spostarsi di 10 pixel alla volta quando la si trascina.  
  
    ```vb  
    Private Sub Form1_Load(ByVal sender As System.Object, _  
        ByVal e As System.EventArgs) Handles MyBase.Load  
        Dim splitSnapper as new SplitContainer()  
        splitSnapper.SplitterIncrement = 10  
        splitSnapper.Dock = DockStyle.Fill  
        splitSnapper.Parent = me  
    End Sub  
  
    ```  
  
    ```csharp  
    private void Form1_Load(System.Object sender, System.EventArgs e)  
    {  
        SplitContainer splitSnapper = new SplitContainer();  
        splitSnapper.SplitterIncrement = 10;  
        splitSnapper.Dock = DockStyle.Fill;  
        splitSnapper.Parent = this;  
    }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)]\) Inserire il codice che segue nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.Load += new System.EventHandler(this.Form1_Load);  
    ```  
  
     Se la barra di divisione viene spostata leggermente verso sinistra o verso destra, non si otterrà alcun effetto visibile. Se invece il puntatore del mouse si sposta di 10 pixel in direzione orizzontale, la barra di divisione verrà bloccata sulla nuova posizione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.SplitContainer>   
 <xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A>