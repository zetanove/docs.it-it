---
title: "Procedura: impostare punti di tabulazione nel testo disegnato | Microsoft Docs"
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
  - "schede, testo disegnato"
  - "testo, disegno con punti di tabulazione"
ms.assetid: 64878f98-39ba-4303-b63f-0859ab682eeb
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: impostare punti di tabulazione nel testo disegnato
È possibile impostare i punti di tabulazione nel testo chiamando il metodo <xref:System.Drawing.StringFormat.SetTabStops%2A> di un oggetto <xref:System.Drawing.StringFormat> e quindi passando l'oggetto <xref:System.Drawing.StringFormat> al metodo <xref:System.Drawing.Graphics.DrawString%2A> della classe <xref:System.Drawing.Graphics>.  
  
> [!NOTE]
>  L'oggetto <xref:System.Windows.Forms.TextRenderer?displayProperty=fullName> non supporta l'aggiunta di punti di tabulazione al testo disegnato, sebbene sia possibile espandere i punti di tabulazione esistenti utilizzando il flag <xref:System.Windows.Forms.TextFormatFlags?displayProperty=fullName>.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono impostati i punti di tabulazione sui valori 150, 250 e 350.  Viene poi visualizzato un elenco tabulato di nomi e risultati di esami.  
  
 Nell'illustrazione che segue si mostra il testo tabulato.  
  
 ![Testo caratteri](../../../../docs/framework/winforms/advanced/media/fontstext4.png "fontstext4")  
  
 Nel codice seguente vengono passati due argomenti al metodo <xref:System.Drawing.StringFormat.SetTabStops%2A>.  Il secondo argomento è una matrice che contiene offset di tabulazione.  Il primo argomento passato a <xref:System.Drawing.StringFormat.SetTabStops%2A> è 0, che indica che il primo offset nella matrice viene misurato dalla posizione 0, ovvero il margine sinistro del rettangolo di delimitazione.  
  
 [!code-csharp[System.Drawing.FontsAndText#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.FontsAndText#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#41)]  
  
## Compilazione del codice  
  
-   L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Utilizzo di tipi di carattere e testo](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)   
 [Procedura: creare testo con GDI](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)