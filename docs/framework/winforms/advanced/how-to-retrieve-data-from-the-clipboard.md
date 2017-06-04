---
title: "How to: Retrieve Data from the Clipboard | Microsoft Docs"
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
  - "pasting Clipboard data"
  - "Clipboard, retrieving data"
ms.assetid: 99612537-2c8a-449f-aab5-2b3b28d656e7
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# How to: Retrieve Data from the Clipboard
La classe <xref:System.Windows.Forms.Clipboard> fornisce i metodi che consentono di interagire con la funzionalità Appunti del sistema operativo Windows.  Molte applicazioni utilizzano gli Appunti come repository temporaneo per i dati.  Negli elaboratori di testi, ad esempio, gli Appunti vengono utilizzati durante le operazioni di taglia e incolla.  Gli Appunti sono anche utili per trasferire informazioni da un'applicazione a un'altra.  
  
 Alcune applicazioni memorizzano i dati negli Appunti in più formati per aumentare il numero delle altre applicazioni che possono utilizzare i dati.  Un formato degli Appunti è costituito da una stringa che identifica il formato.  Un'applicazione che utilizza tale formato può recuperare i dati associati contenuti negli Appunti.  La classe <xref:System.Windows.Forms.DataFormats> fornisce nomi di formato predefiniti che l'utente può impiegare.  Sarà anche possibile utilizzare nomi di formato personalizzati o utilizzare un tipo di oggetto come formato.  Per informazioni sull'aggiunta di dati agli Appunti a un progetto, vedere [How to: Add Data to the Clipboard](../../../../docs/framework/winforms/advanced/how-to-add-data-to-the-clipboard.md).  
  
 Per determinare se gli Appunti contengono dati in un determinato formato, utilizzare uno dei metodi `Contains`*Formato* oppure il metodo <xref:System.Windows.Forms.Clipboard.GetData%2A>.  Per recuperare dati dagli Appunti, utilizzare uno dei metodi `Get`*Formato* oppure il metodo <xref:System.Windows.Forms.Clipboard.GetData%2A>.  Questi metodi sono nuovi in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)].  
  
 Per accedere ai dati dagli Appunti utilizzando versioni precedenti di [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)], utilizzare il metodo <xref:System.Windows.Forms.Clipboard.GetDataObject%2A> e chiamare i metodi dell'interfaccia <xref:System.Windows.Forms.IDataObject> restituita.  Ad esempio, per determinare se un formato particolare è disponibile nell'oggetto restituito, chiamare il metodo <xref:System.Windows.Forms.IDataObject.GetDataPresent%2A>.  
  
> [!NOTE]
>  Tutte le applicazioni basate su Windows condividono gli Appunti.  Di conseguenza, quando si passa a un'altra applicazione, è possibile che il contenuto degli Appunti venga modificato.  
>   
>  La classe <xref:System.Windows.Forms.Clipboard> può essere utilizzata solo in thread impostati sulla modalità apartment a thread singolo \(STA, Single\-Threaded Apartment\).  Per utilizzare questa classe, assicurarsi che il metodo `Main` sia contrassegnato con l'attributo <xref:System.STAThreadAttribute>.  
  
### Per recuperare dati dagli Appunti in un formato singolo comune  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.Clipboard.GetAudioStream%2A>, il metodo <xref:System.Windows.Forms.Clipboard.GetFileDropList%2A>, il metodo <xref:System.Windows.Forms.Clipboard.GetImage%2A> o il metodo <xref:System.Windows.Forms.Clipboard.GetText%2A>.  È anche possibile utilizzare prima i metodi `Contains`*Formato* corrispondenti per verificare se i dati sono disponibili in un determinato formato.  Questi metodi sono disponibili solo in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)].  
  
     [!code-csharp[System.Windows.Forms.Clipboard#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#2)]
     [!code-vb[System.Windows.Forms.Clipboard#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#2)]  
  
### Per recuperare dati dagli Appunti in un formato personalizzato  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.Clipboard.GetData%2A> con un nome di formato personalizzato.  Questo metodo è disponibile solo in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)].  
  
     È anche possibile utilizzare nomi di formati predefiniti con il metodo <xref:System.Windows.Forms.Clipboard.SetData%2A>.  Per ulteriori informazioni, vedere <xref:System.Windows.Forms.DataFormats>.  
  
     [!code-csharp[System.Windows.Forms.Clipboard#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#3)]
     [!code-vb[System.Windows.Forms.Clipboard#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#3)]  
    [!code-csharp[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]  
  
### Per recuperare dati dagli Appunti in più formati  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.Clipboard.GetDataObject%2A>.  Questo metodo deve essere utilizzato per recuperare dati dagli Appunti nelle versioni precedenti a [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)].  
  
     [!code-csharp[System.Windows.Forms.Clipboard#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#4)]
     [!code-vb[System.Windows.Forms.Clipboard#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#4)]  
    [!code-csharp[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]  
  
## Vedere anche  
 [Drag\-and\-Drop Operations and Clipboard Support](../../../../docs/framework/winforms/advanced/drag-and-drop-operations-and-clipboard-support.md)   
 [How to: Add Data to the Clipboard](../../../../docs/framework/winforms/advanced/how-to-add-data-to-the-clipboard.md)