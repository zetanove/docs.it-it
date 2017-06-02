---
title: "Cenni preliminari sul controllo ListView (Windows Form) | Microsoft Docs"
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
  - "ListView"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "visualizzazioni elenco"
  - "elenchi"
  - "ListView (controllo) [Windows Form], informazioni sul controllo ListView"
ms.assetid: c9ef56c1-3bb1-4101-9f4e-e95e720f2756
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Cenni preliminari sul controllo ListView (Windows Form)
Il controllo <xref:System.Windows.Forms.ListView> di Windows Form consente di visualizzare un elenco di elementi con icone.  È possibile utilizzare una visualizzazione elenco per creare un'interfaccia utente simile al riquadro destro di Esplora risorse.  Il controllo dispone di quattro modalità di visualizzazione: LargeIcon, SmallIcon, List e Details.  
  
## Attività disponibili con il controllo ListView  
  
> [!NOTE]
>  Un'ulteriore modalità di visualizzazione, Tile, è disponibile solo in Windows XP e Windows Server 2003.  Per ulteriori informazioni, vedere [Procedura: abilitare la visualizzazione affiancata in un controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-enable-tile-view-in-a-windows-forms-listview-control.md).  
  
 La modalità LargeIcon visualizza icone grandi accanto al testo dell'elemento; gli elementi sono disposti in più colonne se le dimensioni del controllo lo consentono.  La modalità SmallIcon si differenzia unicamente per il fatto che le icone visualizzate sono piccole.  La modalità List visualizza icone piccole in un'unica colonna.  La modalità Details visualizza gli elementi in più colonne.  Per informazioni dettagliate, vedere [Procedura: aggiungere colonne al controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md).  La modalità di visualizzazione è determinata dalla proprietà <xref:System.Windows.Forms.ListView.View%2A>.  In tutte le modalità è possibile visualizzare le immagini dagli elenchi immagini.  Per informazioni dettagliate, vedere [Procedura: visualizzare icone per il controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md).  
  
 Nella tabella seguente sono elencati alcuni dei membri <xref:System.Windows.Forms.ListView> e le visualizzazioni in cui sono validi.  
  
|Membro ListView|Visualizzazione|  
|---------------------|---------------------|  
|Proprietà <xref:System.Windows.Forms.ListView.Alignment%2A>|<xref:System.Windows.Forms.View> o <xref:System.Windows.Forms.View>|  
|Proprietà <xref:System.Windows.Forms.ListView.AutoArrange%2A>|<xref:System.Windows.Forms.View> o <xref:System.Windows.Forms.View>|  
|Metodo <xref:System.Windows.Forms.ListView.AutoResizeColumn%2A>|<xref:System.Windows.Forms.View>|  
|Proprietà <xref:System.Windows.Forms.ListView.Columns%2A>|<xref:System.Windows.Forms.View> o <xref:System.Windows.Forms.View>|  
|Evento <xref:System.Windows.Forms.ListView.DrawSubItem>|<xref:System.Windows.Forms.View>|  
|Metodo <xref:System.Windows.Forms.ListView.FindItemWithText%2A>|<xref:System.Windows.Forms.View>, <xref:System.Windows.Forms.View> o <xref:System.Windows.Forms.View>|  
|Metodo <xref:System.Windows.Forms.ListView.FindNearestItem%2A>|<xref:System.Windows.Forms.View> o <xref:System.Windows.Forms.View>|  
|Metodo <xref:System.Windows.Forms.ListView.GetItemAt%2A>|<xref:System.Windows.Forms.View> o <xref:System.Windows.Forms.View>|  
|Proprietà <xref:System.Windows.Forms.ListView.Groups%2A>|Tutte le visualizzazioni ad eccezione di <xref:System.Windows.Forms.View>|  
|Proprietà <xref:System.Windows.Forms.ListView.HeaderStyle%2A>|<xref:System.Windows.Forms.View>.|  
|Proprietà <xref:System.Windows.Forms.ListView.InsertionMark%2A>|<xref:System.Windows.Forms.View>, <xref:System.Windows.Forms.View> o <xref:System.Windows.Forms.View>|  
  
 La proprietà fondamentale del controllo <xref:System.Windows.Forms.ListView> è <xref:System.Windows.Forms.ListView.Items%2A>, che contiene gli elementi visualizzati dal controllo.  La proprietà <xref:System.Windows.Forms.ListView.SelectedItems%2A> contiene una raccolta degli elementi attualmente selezionati nel controllo.  L'utente può selezionare più elementi, ad esempio per trascinarli contemporaneamente in un altro controllo, se la proprietà <xref:System.Windows.Forms.ListView.MultiSelect%2A> è impostata su `true`.  Il controllo <xref:System.Windows.Forms.ListView> può visualizzare caselle di controllo accanto agli elementi se la proprietà <xref:System.Windows.Forms.ListView.CheckBoxes%2A> è impostata su `true`.  
  
 La proprietà <xref:System.Windows.Forms.ListView.Activation%2A> determina il tipo di operazione da effettuare per attivare un elemento nell'elenco: le opzioni sono <xref:System.Windows.Forms.ItemActivation>, <xref:System.Windows.Forms.ItemActivation> e <xref:System.Windows.Forms.ItemActivation>.  Per l'attivazione di <xref:System.Windows.Forms.ItemActivation> è necessario fare clic sull'elemento per attivarlo.  Per l'attivazione di <xref:System.Windows.Forms.ItemActivation> è necessario fare doppio clic sull'elemento per attivarlo; con un solo clic viene modificato il colore del testo dell'elemento.  Per l'attivazione di <xref:System.Windows.Forms.ItemActivation> è necessario fare doppio clic sull'elemento per attivarlo, ma non viene modificato l'aspetto dell'elemento.  
  
 Il controllo <xref:System.Windows.Forms.ListView> supporta anche gli stili visivi e le altre funzionalità disponibili sulla piattaforma Windows XP, tra cui il raggruppamento, la visualizzazione affiancata e i segni di inserimento.  Per ulteriori informazioni, vedere [Windows XP Features and Windows Forms Controls](http://msdn.microsoft.com/it-it/bc7fab94-fce9-4bf1-a8ad-a5837c91c3c0).  
  
## Vedere anche  
 <xref:System.Windows.Forms.ListView>   
 [Controllo ListView](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)   
 [Procedura: aggiungere e rimuovere elementi tramite il controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)   
 [Procedura: aggiungere colonne al controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)   
 [Procedura: visualizzare icone per il controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md)   
 [Procedura: visualizzare elementi secondari nelle colonne con il controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)   
 [Procedura: selezionare un elemento nel controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-select-an-item-in-the-windows-forms-listview-control.md)   
 [Procedura: raggruppare elementi in un controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-group-items-in-a-windows-forms-listview-control.md)   
 [Procedura: visualizzare un segno di inserimento in un controllo ListView per Windows Form](../../../../docs/framework/winforms/controls/how-to-display-an-insertion-mark-in-a-windows-forms-listview-control.md)   
 [Procedura: aggiungere funzionalità di ricerca a un controllo ListView](../../../../docs/framework/winforms/controls/how-to-add-search-capabilities-to-a-listview-control.md)   
 [Procedura: aggiungere informazioni personalizzate a un controllo TreeView o ListView \(Windows Form\)](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)   
 [Procedura: creare un'interfaccia utente a più riquadri con Windows Form](../../../../docs/framework/winforms/controls/how-to-create-a-multipane-user-interface-with-windows-forms.md)