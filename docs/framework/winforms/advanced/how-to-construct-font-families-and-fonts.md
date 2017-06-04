---
title: "Procedura: creare caratteri e gruppi di caratteri | Microsoft Docs"
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
  - "famiglie di caratteri, creazione"
  - "tipi di carattere, creazione"
ms.assetid: d3a4a223-9492-4b54-9afd-db1c31c3cefd
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: creare caratteri e gruppi di caratteri
In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] i caratteri con lo stesso carattere tipografico ma stili diversi sono riuniti in famiglie di caratteri.  Il gruppo di caratteri Arial, ad esempio, contiene i caratteri che seguono:  
  
-   Arial normale  
  
-   Arial grassetto  
  
-   Arial corsivo  
  
-   Arial grassetto corsivo  
  
 In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] vengono utilizzati quattro stili per creare i gruppi: normale, grassetto, corsivo e grassetto corsivo.  Aggettivi come *narrow* e *rounded* non sono considerati stili bensì parti del nome del gruppo.  Il carattere Arial Narrow, ad esempio, è un gruppo di caratteri con i membri che seguono:  
  
-   Arial Narrow normale  
  
-   Arial Narrow grassetto  
  
-   Arial Narrow corsivo  
  
-   Arial Narrow grassetto corsivo  
  
 Prima di poter disegnare testo con [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)], è necessario costruire un oggetto <xref:System.Drawing.FontFamily> e un oggetto <xref:System.Drawing.Font>.  L'oggetto <xref:System.Drawing.FontFamily> consente di specificare il carattere tipografico, ad esempio Arial, mentre l'oggetto <xref:System.Drawing.Font> consente di specificare dimensione, stile e unità.  
  
## Esempio  
 Nell'esempio riportato di seguito viene creato un carattere Arial di stile normale con una dimensione di 16 pixel.  Nel codice seguente il primo argomento passato al costruttore <xref:System.Drawing.Font.%23ctor%2A> è l'oggetto <xref:System.Drawing.FontFamily>.  Con il secondo argomento viene specificata la dimensione del carattere, misurata nelle unità specificate con il quarto argomento.  Il terzo argomento consente di identificare lo stile.  
  
 <xref:System.Drawing.GraphicsUnit> è un membro dell'enumerazione <xref:System.Drawing.GraphicsUnit> e <xref:System.Drawing.FontStyle> è un membro dell'enumerazione <xref:System.Drawing.FontStyle>.  
  
 [!code-csharp[System.Drawing.FontsAndText#61](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#61)]
 [!code-vb[System.Drawing.FontsAndText#61](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#61)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e` un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Utilizzo di tipi di carattere e testo](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)