---
title: "How to: Print a Windows Form | Microsoft Docs"
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
  - "Windows Forms, printing"
  - "printing [Windows Forms]"
  - "printing a form"
  - "printing [Windows Forms, printing a form"
ms.assetid: c8dff5f8-f56a-4c07-ae31-64643b31f8fc
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Print a Windows Form
Durante il processo di sviluppo in genere si desidera stampare una copia del Windows Form.  Nell'esempio di codice riportato di seguito viene illustrato come stampare una copia del form corrente mediante il metodo <xref:System.Drawing.Graphics.CopyFromScreen%2A>.  
  
## Esempio  
 [!code-csharp[System.Drawing.Graphics.CopyFromScreen#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Graphics.CopyFromScreen/CS/Form1.cs#1)]
 [!code-vb[System.Drawing.Graphics.CopyFromScreen#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Graphics.CopyFromScreen/VB/Form1.vb#1)]  
  
## Compilazione del codice  
 Si tratta di un esempio di cdice completo contenente un metodo `Main`.  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Non si dispone dell'autorizzazione per accedere alla stampante.  
  
-   Non è installata alcuna stampante.  
  
## Sicurezza di .NET Framework  
 Per eseguire questo esempio di codice, è necessario disporre dell'autorizzazione per l'accesso alla stampante utilizzata con il computer.  
  
## Vedere anche  
 <xref:System.Drawing.Printing.PrintDocument>   
 [Procedura: eseguire il rendering delle immagini con GDI\+](../../../../docs/framework/winforms/advanced/how-to-render-images-with-gdi.md)   
 [How to: Print Graphics in Windows Forms](../../../../docs/framework/winforms/advanced/how-to-print-graphics-in-windows-forms.md)