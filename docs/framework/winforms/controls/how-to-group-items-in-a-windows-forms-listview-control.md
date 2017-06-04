---
title: "Procedura: raggruppare elementi in un controllo ListView Windows Form | Microsoft Docs"
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
  - "raggruppamento"
  - "gruppi"
  - "gruppi, in controlli Windows Form"
  - "visualizzazioni elenco, raggruppamento di elementi"
  - "elenchi, raggruppamento di elementi"
  - "ListView (controllo) [Windows Form], raggruppamento di elementi"
ms.assetid: 610416a1-8da4-436c-af19-5f19e654769b
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: raggruppare elementi in un controllo ListView Windows Form
La funzionalità di raggruppamento del controllo <xref:System.Windows.Forms.ListView> consente di visualizzare insiemi correlati di elementi in gruppi.  Questi gruppi sono separati sullo schermo da intestazioni di gruppo orizzontali che includono il titolo dei gruppi.  È possibile utilizzare i gruppi <xref:System.Windows.Forms.ListView> per semplificare lo spostamento in elenchi contenenti numerose voci raggruppando gli elementi in ordine alfabetico, per data o in base a qualsiasi altro raggruppamento logico.  Nell'immagine riportata di seguito sono illustrati alcuni elementi raggruppati.  
  
 ![Gruppi ListView](../../../../docs/framework/winforms/controls/media/listviewgroups.gif "ListViewGroups")  
Elementi raggruppati ListView  
  
 Per consentire il raggruppamento è necessario prima creare uno o più gruppi, nella finestra di progettazione oppure a livello di codice.  Una volta definito un gruppo, è possibile assegnare elementi <xref:System.Windows.Forms.ListView> ai gruppi.  A livello di codice è possibile anche spostare gli elementi da un gruppo a un altro.  
  
> [!NOTE]
>  I gruppi <xref:System.Windows.Forms.ListView> sono disponibili solo in [!INCLUDE[WinXpFamily](../../../../includes/winxpfamily-md.md)] quando il metodo <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName> viene chiamato dall'applicazione.  Nei sistemi operativi di versioni precedenti, qualsiasi codice relativo ai gruppi non ha alcun effetto e non verranno visualizzati gruppi.  Per ulteriori informazioni, vedere <xref:System.Windows.Forms.ListView.Groups%2A?displayProperty=fullName>.  
  
### Per aggiungere i gruppi  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.ListViewGroupCollection.Add%2A> della raccolta <xref:System.Windows.Forms.ListView.Groups%2A>.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#21)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#21)]  
  
### Per rimuovere i gruppi  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.ListViewGroupCollection.RemoveAt%2A> o <xref:System.Windows.Forms.ListViewGroupCollection.Clear%2A> della raccolta <xref:System.Windows.Forms.ListView.Groups%2A>.  
  
     Il metodo <xref:System.Windows.Forms.ListViewGroupCollection.RemoveAt%2A> consente di rimuovere un singolo gruppo, mentre il metodo <xref:System.Windows.Forms.ListViewGroupCollection.Clear%2A> consente di rimuovere tutti gli elementi dell'elenco.  
  
    > [!NOTE]
    >  Con la rimozione di un gruppo non vengono rimossi gli elementi contenuti in tale gruppo.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#22)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#22)]  
  
### Per assegnare elementi ai gruppi o spostare elementi tra i gruppi  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.ListViewItem.Group%2A?displayProperty=fullName> di singoli elementi.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#23)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#23)]  
  
## Vedere anche  
 <xref:System.Windows.Forms.ListView>   
 <xref:System.Windows.Forms.ListView.Groups%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ListViewGroup>   
 [Controllo ListView](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)   
 [Cenni preliminari sul controllo ListView](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)   
 [Windows XP Features and Windows Forms Controls](http://msdn.microsoft.com/it-it/bc7fab94-fce9-4bf1-a8ad-a5837c91c3c0)   
 [Procedura: aggiungere e rimuovere elementi tramite il controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)