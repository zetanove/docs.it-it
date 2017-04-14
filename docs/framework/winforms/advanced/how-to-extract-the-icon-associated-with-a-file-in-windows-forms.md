---
title: "Procedura: estrarre l&#39;icona associata a un file in Windows Form | Microsoft Docs"
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
  - "visualizzazione di un nome file e dell'icona del relativo tipo di file in un controllo ListView [Windows Form]"
  - "estrazione delle icone associate a un tipo di file [Windows Form]"
  - "estensione di file (icone) [Windows Form], visualizzazione in un controllo ListView"
ms.assetid: 88e2ad8b-c34f-415a-84f2-dad756b5c928
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: estrarre l&#39;icona associata a un file in Windows Form
Molti file includono icone incorporate che forniscono una rappresentazione visiva del tipo di file associato.  Ad esempio, i documenti di Microsoft Word contengono un'icona che li identifica come tali.  Quando si visualizzano i file in un controllo elenco o tabella, è possibile decidere di visualizzare l'icona che rappresenta il tipo di file accanto a ogni nome di file.  A tale scopo, utilizzare il metodo <xref:System.Drawing.Icon.ExtractAssociatedIcon%2A>.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come estrarre l'icona associata a un file e visualizzare il nome file e l'icona associata in un controllo <xref:System.Windows.Forms.ListView>.  
  
 [!code-csharp[System.Drawing.Icon.ExtractAssociatedIconEx#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Icon.ExtractAssociatedIconEx/CS/Form1.cs#1)]
 [!code-vb[System.Drawing.Icon.ExtractAssociatedIconEx#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Icon.ExtractAssociatedIconEx/VB/Form1.vb#1)]  
  
## Compilazione del codice  
 Per compilare l'esempio:  
  
-   Incollare il codice precedente in Windows Form e chiamare il metodo `ExtractAssociatedIconExample` dal costruttore del form o il metodo di gestione degli eventi <xref:System.Windows.Forms.Form.Load>.  
  
     Sarà necessario assicurarsi che il form importi lo spazio dei nomi <xref:System.IO>.  
  
## Vedere anche  
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [Controllo ListView](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)