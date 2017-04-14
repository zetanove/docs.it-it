---
title: "Procedura: aggiungere funzionalit&#224; di ricerca a un controllo ListView | Microsoft Docs"
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
  - "visualizzazioni elenco, abilitazione della ricerca"
  - "elenchi, abilitazione della ricerca"
  - "ListView (controllo) [Windows Form], aggiunta di funzionalità di ricerca"
  - "ricerca, aggiunta di funzionalità di ricerca al controllo ListView"
ms.assetid: 557782d9-b705-4bab-b496-9938afddac82
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: aggiungere funzionalit&#224; di ricerca a un controllo ListView
Quando si utilizza un elenco di elementi di grandi dimensioni in un controllo <xref:System.Windows.Forms.ListView>, spesso è necessario fornire all'utente funzionalità di ricerca.  Il controllo <xref:System.Windows.Forms.ListView> offre tali funzionalità in due modi diversi, mediante corrispondenza del testo e mediante ricerca della posizione.  
  
 Il metodo <xref:System.Windows.Forms.ListView.FindItemWithText%2A> consente di eseguire una ricerca di testo in un controllo <xref:System.Windows.Forms.ListView> in visualizzazione elenco o dettagli, in base a una stringa di ricerca e a indici di inizio e fine facoltativi.  Il metodo <xref:System.Windows.Forms.ListView.FindNearestItem%2A>, invece, consente di trovare un elemento in un controllo <xref:System.Windows.Forms.ListView> in visualizzazione a icone o affiancata, in base a un insieme di coordinate x e y e a una direzione di ricerca.  
  
### Per trovare un elemento utilizzando del testo  
  
1.  Creare un controllo <xref:System.Windows.Forms.ListView> con la proprietà <xref:System.Windows.Forms.ListView.View%2A> impostata su <xref:System.Windows.Forms.View> o <xref:System.Windows.Forms.View>, quindi compilare il controllo <xref:System.Windows.Forms.ListView> con elementi.  
  
2.  Chiamare il metodo <xref:System.Windows.Forms.ListView.FindItemWithText%2A>, passando il testo dell'elemento che si desidera trovare.  
  
3.  Nell'esempio di codice riportato di seguito viene illustrato come creare un controllo <xref:System.Windows.Forms.ListView> base, compilarlo con elementi e utilizzare testo immesso dall'utente per trovare un elemento nell'elenco.  
  
 [!code-cpp[System.Windows.Forms.ListViewFindItems#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/cpp/form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.ListViewFindItems#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.ListViewFindItems#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/VB/form1.vb#1)]  
  
### Per trovare un elemento utilizzando le coordinate x e y  
  
1.  Creare un controllo <xref:System.Windows.Forms.ListView> con la proprietà <xref:System.Windows.Forms.View> impostata su <xref:System.Windows.Forms.View> o <xref:System.Windows.Forms.View>, quindi compilare il controllo <xref:System.Windows.Forms.ListView> con elementi.  
  
2.  Chiamare il metodo <xref:System.Windows.Forms.ListView.FindNearestItem%2A>, passando le coordinate x e y desiderate e la direzione in cui eseguire la ricerca.  
  
3.  Nell'esempio di codice riportato di seguito viene illustrato come creare un controllo <xref:System.Windows.Forms.ListView> base con visualizzazione a icone, compilarlo con elementi e acquisire l'evento <xref:System.Windows.Forms.Control.MouseDown> per trovare l'elemento in alto più vicino.  
  
 [!code-cpp[System.Windows.Forms.ListViewFindItems#2](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/cpp/form1.cpp#2)]
 [!code-csharp[System.Windows.Forms.ListViewFindItems#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/CS/form1.cs#2)]
 [!code-vb[System.Windows.Forms.ListViewFindItems#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewFindItems/VB/form1.vb#2)]  
  
## Vedere anche  
 <xref:System.Windows.Forms.ListView>   
 <xref:System.Windows.Forms.ListView.FindItemWithText%2A>   
 <xref:System.Windows.Forms.ListView.FindNearestItem%2A>   
 [Controllo ListView](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)   
 [Cenni preliminari sul controllo ListView](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)   
 [Procedura: aggiungere e rimuovere elementi tramite il controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)