---
title: "Procedura: modificare l&#39;aspetto del controllo TabControl Windows Form | Microsoft Docs"
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
  - "pulsanti, visualizzazione di schede"
  - "icone, visualizzazione nelle schede"
  - "TabControl (controllo) [Windows Form], modifica dell'aspetto di pagine"
  - "schede, controllo dell'aspetto"
ms.assetid: 7c6cc443-ed62-4d26-b94d-b8913b44f773
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: modificare l&#39;aspetto del controllo TabControl Windows Form
L'aspetto delle schede in Windows Form può essere modificato mediante le proprietà degli oggetti <xref:System.Windows.Forms.TabControl> e <xref:System.Windows.Forms.TabPage> che costituiscono le singole schede nel controllo.  L'impostazione di queste proprietà consente di visualizzare immagini sulle schede, di visualizzare le schede in verticale anziché in orizzontale, di visualizzare più righe di schede e di attivare o disabilitare le schede a livello di codice.  
  
### Per visualizzare un'icona sull'etichetta di una scheda  
  
1.  Aggiungere un controllo <xref:System.Windows.Forms.ImageList> al form.  
  
2.  Aggiungere le immagini all'elenco di immagini.  
  
     Per ulteriori informazioni sugli elenchi di immagini, vedere [Componente ImageList](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md) e [Procedura: aggiungere o rimuovere immagini tramite il componente ImageList Windows Form](../../../../docs/framework/winforms/controls/how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md).  
  
3.  Impostare la proprietà <xref:System.Windows.Forms.TabControl.ImageList%2A> del controllo <xref:System.Windows.Forms.TabControl> sul controllo <xref:System.Windows.Forms.ImageList>.  
  
4.  Impostare la proprietà <xref:System.Windows.Forms.TabPage.ImageIndex%2A> dell'oggetto <xref:System.Windows.Forms.TabPage> sull'indice di un'immagine appropriata nell'elenco.  
  
### Per creare più righe di schede  
  
1.  Aggiungere il numero di pagine a schede desiderato.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.TabControl.Multiline%2A> del controllo <xref:System.Windows.Forms.TabControl> su `true`.  
  
3.  Se le schede non sono già visualizzate su più righe, impostare la proprietà <xref:System.Windows.Forms.Control.Width%2A> del controllo <xref:System.Windows.Forms.TabControl> in modo che sia inferiore alla larghezza di tutte le schede.  
  
### Per disporre le schede a lato del controllo  
  
-   Impostare la proprietà <xref:System.Windows.Forms.TabControl.Alignment%2A> del controllo <xref:System.Windows.Forms.TabControl> su <xref:System.Windows.Forms.TabAlignment> o <xref:System.Windows.Forms.TabAlignment>.  
  
### Per abilitare o disabilitare a livello di codice tutti i controlli in una scheda  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.TabPage.Enabled%2A> del controllo <xref:System.Windows.Forms.TabPage> su `true` o `false`.  
  
    ```vb  
    TabPage1.Enabled = False  
  
    ```  
  
    ```csharp  
    tabPage1.Enabled = false;  
  
    ```  
  
    ```cpp  
    tabPage1->Enabled = false;  
    ```  
  
### Per visualizzare le schede come pulsanti  
  
-   Impostare la proprietà <xref:System.Windows.Forms.TabControl.Appearance%2A> del controllo <xref:System.Windows.Forms.TabControl> su <xref:System.Windows.Forms.TabAppearance> o <xref:System.Windows.Forms.TabAppearance>.  
  
## Vedere anche  
 [Controllo TabControl](../../../../docs/framework/winforms/controls/tabcontrol-control-windows-forms.md)   
 [Cenni preliminari sul controllo TabControl](../../../../docs/framework/winforms/controls/tabcontrol-control-overview-windows-forms.md)   
 [Procedura: aggiungere un controllo a un oggetto TabPage](../../../../docs/framework/winforms/controls/how-to-add-a-control-to-a-tab-page.md)   
 [Procedura: disabilitare le schede](../../../../docs/framework/winforms/controls/how-to-disable-tab-pages.md)   
 [Procedura: aggiungere e rimuovere schede tramite il controllo TabControl Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol.md)