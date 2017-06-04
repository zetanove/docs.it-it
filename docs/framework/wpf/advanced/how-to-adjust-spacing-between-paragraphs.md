---
title: "Procedura: regolare la spaziatura tra paragrafi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "documenti, regolazione della spaziatura tra paragrafi"
  - "paragrafi, spaziatura interna"
  - "spaziatura tra paragrafi"
ms.assetid: 7cd2f2ac-0e19-4587-bfb6-7f5b18c9536e
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: regolare la spaziatura tra paragrafi
In questo esempio viene illustrato come regolare o eliminare la spaziatura tra paragrafi nel contenuto in flusso.  
  
 Nel contenuto in flusso, lo spazio aggiuntivo che si trova tra i paragrafi è il risultato dei margini impostati per tali paragrafi. Quindi la spaziatura tra paragrafi può essere controllata regolando i margini degli stessi paragrafi.  Per eliminare completamente la spaziatura aggiuntiva tra due paragrafi, impostare i margini dei paragrafi su **0**.  Per ottenere una spaziatura uniforme tra i paragrafi di un intero <xref:System.Windows.Documents.FlowDocument>, applicare uno stile per impostare un valore di margine uniforme per tutti i paragrafi di <xref:System.Windows.Documents.FlowDocument>.  
  
 È importante notare che i margini di due paragrafi adiacenti saranno "compressi" nel margine più grande anziché raddoppiati.  Quindi, se due paragrafi adiacenti hanno rispettivamente margini di 20 e 40 pixel, la spaziatura risultante tra i paragrafi è di 40 pixel, il più grande dei valori dei due margini.  
  
## Esempio  
 Nell'esempio riportato di seguito viene applicato lo stile per impostare il margine di tutti gli elementi <xref:System.Windows.Documents.Paragraph> di <xref:System.Windows.Documents.FlowDocument> su **0**, eliminando effettivamente la spaziatura aggiuntiva tra i paragrafi di <xref:System.Windows.Documents.FlowDocument>.  
  
 [!code-xml[BlockSnippets#_ParagraphSpacingXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BlockSnippets/CSharp/Window1.xaml#_paragraphspacingxaml)]