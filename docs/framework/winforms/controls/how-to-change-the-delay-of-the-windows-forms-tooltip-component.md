---
title: "Procedura: modificare il ritardo del componente ToolTip di Windows Form | Microsoft Docs"
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
  - "esempi [Windows Form], descrizioni comandi"
  - "ToolTip (componente) [Windows Form], valori di ritardo"
  - "descrizioni comandi [Windows Form], valori di ritardo"
ms.assetid: 08979ba7-dd84-477b-ab17-8d06e759be99
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: modificare il ritardo del componente ToolTip di Windows Form
Per un componente <xref:System.Windows.Forms.ToolTip> di Windows Form è possibile impostare più valori di ritardo.  Per tutte le proprietà, l'unità di misura è costituita dal millisecondo.  La proprietà <xref:System.Windows.Forms.ToolTip.InitialDelay%2A> determina l'intervallo di tempo che intercorre tra il posizionamento del mouse sul controllo associato e la visualizzazione della stringa di descrizione comandi.  Attraverso la proprietà <xref:System.Windows.Forms.ToolTip.ReshowDelay%2A> viene impostato il numero di millisecondi necessario perché vengano visualizzate le stringhe di descrizione comandi successive quando il mouse viene spostato da un controllo associato a una descrizione comandi a un altro.  La proprietà <xref:System.Windows.Forms.ToolTip.AutoPopDelay%2A> determina la durata della visualizzazione della stringa di descrizione comandi.  Questi valori possono essere impostati singolarmente oppure mediante l'impostazione del valore della proprietà <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>; le altre proprietà di ritardo verranno impostate in base al valore assegnato alla proprietà <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>.  Quando, ad esempio, <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> è impostato su un valore N, <xref:System.Windows.Forms.ToolTip.InitialDelay%2A> verrà impostato su N, <xref:System.Windows.Forms.ToolTip.ReshowDelay%2A> sul valore di <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> diviso per cinque \(oppure N\/5\) e <xref:System.Windows.Forms.ToolTip.AutoPopDelay%2A> su un valore ottenuto moltiplicando per cinque volte il valore della proprietà <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> \(o 5N\).  
  
### Per impostare il ritardo  
  
1.  Impostare le proprietà riportate di seguito come illustrato nell'esempio.  
  
    ```vb  
    ToolTip1.InitialDelay = 500  
    ToolTip1.ReshowDelay = 100  
    ToolTip1.AutoPopDelay = 5000  
  
    ```  
  
    ```csharp  
    ToolTip1.InitialDelay = 500;  
    ToolTip1.ReshowDelay = 100;  
    ToolTip1.AutoPopDelay = 5000;  
  
    ```  
  
    ```cpp  
    toolTip1->InitialDelay = 500;  
    toolTip1->ReshowDelay = 100;  
    toolTip1->AutoPopDelay = 5000;  
    ```  
  
## Vedere anche  
 [Cenni preliminari sul componente ToolTip](../../../../docs/framework/winforms/controls/tooltip-component-overview-windows-forms.md)   
 [Procedura: impostare le descrizioni comandi per i controlli in un Windows Form in fase di progettazione](../../../../docs/framework/winforms/controls/how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)   
 [Componente ToolTip](../../../../docs/framework/winforms/controls/tooltip-component-windows-forms.md)