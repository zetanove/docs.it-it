---
title: "How to: Add Data to the Clipboard | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Clipboard, copying data to"
  - "data [Windows Forms], copying to Clipboard"
ms.assetid: 25152454-0e78-40a9-8a9e-a2a5a274e517
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# How to: Add Data to the Clipboard
La classe <xref:System.Windows.Forms.Clipboard> fornisce i metodi che consentono di interagire con la funzionalità Appunti del sistema operativo Windows.  Molte applicazioni utilizzano gli Appunti come repository temporaneo per i dati.  Negli elaboratori di testi, ad esempio, gli Appunti vengono utilizzati durante le operazioni di taglia e incolla.  Gli Appunti sono utili anche per trasferire i dati da un'applicazione a un'altra.  
  
 Quando si aggiungono dati agli Appunti, è possibile indicarne il formato in modo che i dati possano essere utilizzati da altre applicazioni che supportano tale formato.  È anche possibile aggiungere dati agli Appunti in più formati diversi per aumentare il numero delle altre applicazioni che possono utilizzare i dati.  
  
 Un formato degli Appunti è costituito da una stringa che identifica il formato, in modo che un'applicazione che utilizza tale formato possa recuperare i dati associati.  La classe <xref:System.Windows.Forms.DataFormats> fornisce nomi di formato predefiniti che l'utente può impiegare.  È anche possibile utilizzare nomi di formato personalizzati oppure utilizzare un tipo di oggetto come formato.  
  
 Per aggiungere dati agli Appunti in uno o più formati, utilizzare il metodo <xref:System.Windows.Forms.Clipboard.SetDataObject%2A>.  A questo metodo è possibile passare un qualsiasi oggetto ma, per poter aggiungere dati in più formati, è necessario innanzitutto aggiungere i dati a un oggetto distinto appositamente progettato per gestire più formati.  In genere, i dati verranno aggiunti alla classe <xref:System.Windows.Forms.DataObject>, ma è possibile utilizzare qualsiasi tipo che implementi l'interfaccia <xref:System.Windows.Forms.IDataObject>.  
  
 In [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] è possibile aggiungere dati direttamente agli Appunti utilizzando nuovi metodi progettati per semplificare le attività di base relative agli Appunti.  Questi metodi devono essere utilizzati quando si gestiscono dati in un singolo formato comune, ad esempio testo.  
  
> [!NOTE]
>  Tutte le applicazioni basate su Windows condividono gli Appunti.  Di conseguenza, quando si passa a un'altra applicazione, è possibile che il contenuto degli Appunti venga modificato.  
>   
>  La classe <xref:System.Windows.Forms.Clipboard> può essere utilizzata solo in thread impostati sulla modalità apartment a thread singolo \(STA, Single\-Threaded Apartment\).  Per utilizzare questa classe, verificare che il metodo `Main` sia contrassegnato con l'attributo <xref:System.STAThreadAttribute>.  
>   
>  Per essere inserito negli Appunti, è necessario che un oggetto sia serializzabile.  Per rendere un tipo serializzabile, contrassegnarlo con l'attributo <xref:System.SerializableAttribute>.  Se si passa un oggetto non serializzabile a un metodo degli Appunti, il metodo non riuscirà ma non verranno generate eccezioni.  Per ulteriori informazioni sulla serializzazione, vedere <xref:System.Runtime.Serialization>.  
  
### Per aggiungere dati agli Appunti in un singolo formato comune  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.Clipboard.SetAudio%2A>, il metodo <xref:System.Windows.Forms.Clipboard.SetFileDropList%2A>, il metodo <xref:System.Windows.Forms.Clipboard.SetImage%2A> o il metodo <xref:System.Windows.Forms.Clipboard.SetText%2A>.  Questi metodi sono disponibili solo in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)].  
  
     [!code-csharp[System.Windows.Forms.Clipboard#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#2)]
     [!code-vb[System.Windows.Forms.Clipboard#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#2)]  
  
### Per aggiungere dati agli Appunti in un formato personalizzato  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.Clipboard.SetData%2A> con un nome di formato personalizzato.  Questo metodo è disponibile solo in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)].  
  
     È anche possibile utilizzare nomi di formati predefiniti con il metodo <xref:System.Windows.Forms.Clipboard.SetData%2A>.  Per ulteriori informazioni, vedere <xref:System.Windows.Forms.DataFormats>.  
  
     [!code-csharp[System.Windows.Forms.Clipboard#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#3)]
     [!code-vb[System.Windows.Forms.Clipboard#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#3)]  
    [!code-csharp[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]  
  
### Per aggiungere dati agli Appunti in più formati  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.Clipboard.SetDataObject%2A> e passare una classe <xref:System.Windows.Forms.DataObject> contenente i dati.  Questo metodo deve essere utilizzato per aggiungere dati agli Appunti nelle versioni precedenti a [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)].  
  
     [!code-csharp[System.Windows.Forms.Clipboard#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#4)]
     [!code-vb[System.Windows.Forms.Clipboard#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#4)]  
    [!code-csharp[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]  
  
## Vedere anche  
 [Drag\-and\-Drop Operations and Clipboard Support](../../../../docs/framework/winforms/advanced/drag-and-drop-operations-and-clipboard-support.md)   
 [How to: Retrieve Data from the Clipboard](../../../../docs/framework/winforms/advanced/how-to-retrieve-data-from-the-clipboard.md)