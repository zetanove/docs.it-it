---
title: "Procedura: creare un controllo di Windows Form che visualizzi lo stato di avanzamento | Microsoft Docs"
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
  - "controlli [Windows Form], creazione"
  - "controlli [Windows Form], analisi dello stato di avanzamento"
  - "FlashTrackBar (controllo personalizzato)"
  - "avanzamento, visualizzazione [Windows Form]"
ms.assetid: 24c5a2e3-058c-4b8d-a217-c06e6a130c2f
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: creare un controllo di Windows Form che visualizzi lo stato di avanzamento
Nell'esempio di codice riportato di seguito viene illustrato un controllo personalizzato, denominato `FlashTrackBar`, che può essere utilizzato per visualizzare il livello o lo stato di avanzamento di un'applicazione.  Il controllo utilizza una sfumatura per rappresentare visivamente l'avanzamento.  
  
 Nel controllo `FlashTrackBar` vengono illustrati i concetti seguenti:  
  
-   Definizione di proprietà personalizzate.  
  
-   Definizione di eventi personalizzati.  \(`FlashTrackBar` definisce l'evento `ValueChanged`\).  
  
-   Esecuzione dell'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A> per fornire la logica necessaria per la progettazione del controllo.  
  
-   Calcolo dell'area disponibile per disegnare il controllo mediante la proprietà <xref:System.Windows.Forms.Control.ClientRectangle%2A>.  `FlashTrackBar` esegue tale operazione nel metodo `OptimizedInvalidate`.  
  
-   Implementazione della serializzazione o della persistenza per una proprietà quando viene modificata in Progettazione Windows Form.  `FlashTrackBar` definisce i metodi `ShouldSerializeStartColor` e `ShouldSerializeEndColor` per la serializzazione delle proprietà `StartColor` e `EndColor`.  
  
 Nella tabella riportata di seguito sono illustrate le proprietà personalizzate definite da `FlashTrackBar`.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|`AllowUserEdit`|Indica se l'utente può modificare il valore del controllo FlashTrackBar selezionandolo e trascinandolo.|  
|`EndColor`|Specifica il colore finale della barra di avanzamento.|  
|`DarkenBy`|Specifica di quanto scurire lo sfondo rispetto alla sfumatura in primo piano.|  
|`Max`|Specifica il valore massimo della barra di avanzamento.|  
|`Min`|Specifica il valore minimo della barra di avanzamento.|  
|`StartColor`|Specifica il colore iniziale della sfumatura.|  
|`ShowPercentage`|Indica se visualizzare una percentuale sulla sfumatura.|  
|`ShowValue`|Indica se visualizzare il valore corrente sulla sfumatura.|  
|`ShowGradient`|Indica se sulla barra di avanzamento deve essere visualizzata una sfumatura di colore che indica il valore corrente.|  
|-   `Value`|Specifica il valore corrente della barra di avanzamento.|  
  
 Nella tabella riportata di seguito sono illustrati i membri aggiuntivi definiti da `FlashTrackBar:` l'evento proprietà modificata e il metodo che genera tale evento.  
  
|Membro|Descrizione|  
|------------|-----------------|  
|`ValueChanged`|L'evento che viene generato quando la proprietà `Value` della barra di avanzamento viene modificata.|  
|`OnValueChanged`|Il metodo che genera l'evento `ValueChanged`.|  
  
> [!NOTE]
>  `FlashTrackBar` utilizza la classe <xref:System.EventArgs> per i dati dell'evento e <xref:System.EventHandler> come delegato dell'evento.  
  
 Per gestire gli eventi *NomeEvento* corrispondenti, il controllo `FlashTrackBar` esegue l'override dei seguenti metodi ereditati da <xref:System.Windows.Forms.Control?displayProperty=fullName>:  
  
-   <xref:System.Windows.Forms.Control.OnPaint%2A>  
  
-   <xref:System.Windows.Forms.Control.OnMouseDown%2A>  
  
-   <xref:System.Windows.Forms.Control.OnMouseMove%2A>  
  
-   <xref:System.Windows.Forms.Control.OnMouseUp%2A>  
  
-   <xref:System.Windows.Forms.Control.OnResize%2A>  
  
 Per gestire gli eventi di proprietà modificata corrispondenti, il controllo `FlashTrackBar` esegue l'override dei seguenti metodi ereditati da <xref:System.Windows.Forms.Control?displayProperty=fullName>:  
  
-   <xref:System.Windows.Forms.Control.OnBackColorChanged%2A>  
  
-   <xref:System.Windows.Forms.Control.OnBackgroundImageChanged%2A>  
  
-   <xref:System.Windows.Forms.Control.OnTextChanged%2A>  
  
## Esempio  
 Il controllo `FlashTrackBar` definisce due editor di tipi con interfaccia utente, `FlashTrackBarValueEditor` e `FlashTrackBarDarkenByEditor`, riportati nei seguenti listati di codice.  La classe `HostApp` utilizza il controllo `FlashTrackBar` su un Windows Form.  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#1)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#1)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBarDarkenByEditor.cs#10)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBarDarkenByEditor.vb#10)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBarValueEditor.cs#20)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBarValueEditor.vb#20)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/HostApp.cs#30)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/HostApp.vb#30)]  
  
## Vedere anche  
 [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md)   
 [Nozioni fondamentali sullo sviluppo di controlli Windows Form](../../../../docs/framework/winforms/controls/windows-forms-control-development-basics.md)