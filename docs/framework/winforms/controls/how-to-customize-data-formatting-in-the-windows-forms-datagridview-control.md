---
title: "Procedura: formattare dati personalizzati in un controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "celle, modifica dei colori nel controllo DataGridView [Windows Form]"
  - "colori, modifica nel controllo DataGridView [Windows Form]"
  - "dati [Windows Form], formattazione nel controllo DataGridView"
  - "griglie dei dati, formattazione di dati"
  - "DataGridView (controllo) [Windows Form], personalizzazione delle celle"
  - "DataGridView (controllo) [Windows Form], stili della cella"
  - "DataGridView (controllo) [Windows Form], modifica dei colori delle celle"
  - "DataGridView (controllo) [Windows Form], formattazione di dati"
  - "DataGridView (controllo) [Windows Form], sostituzione dei valori delle celle per la visualizzazione"
  - "Windows Form, modifica dei colori delle celle DataGridView"
ms.assetid: a6e72c70-ce18-425f-828d-d57be6f96ab6
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Procedura: formattare dati personalizzati in un controllo DataGridView di Windows Form
Nell'esempio di codice seguente viene illustrato come implementare un gestore per l'evento <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=fullName> che modifica la visualizzazione delle celle a seconda delle colonne e dei valori.  
  
 Le celle nella colonna `Balance` che contengono numeri negativi hanno uno sfondo rosso.  È anche possibile formattare le celle come valuta per visualizzare le parentesi intorno ai valori negativi.  Per altre informazioni, vedere [Procedura: formattare i dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-format-data-in-the-windows-forms-datagridview-control.md)  
  
 Nelle celle della colonna `Priority` vengono visualizzate delle immagini invece dei valori delle celle testuali corrispondenti.  La proprietà <xref:System.Windows.Forms.ConvertEventArgs.Value%2A> della classe <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs> viene usata sia per ottenere il valore della cella testuale che per impostare il valore di visualizzazione dell'immagine corrispondente.  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.DataGridViewCustomizeDataFormatting#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCustomizeDataFormatting/cs/customFormatting.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewCustomizeDataFormatting#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCustomizeDataFormatting/vb/customFormatting.vb#00)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System, System.Drawing e System.Windows.Forms.  
  
-   Le immagini <xref:System.Drawing.Bitmap> denominate `highPri.bmp`, `mediumPri.bmp` e `lowPri.bmp` risiedono nella stessa directory del file eseguibile.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 <xref:System.Drawing.Bitmap>   
 [Visualizzazione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [Procedura: formattare i dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-format-data-in-the-windows-forms-datagridview-control.md)   
 [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [Formattazione di dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/data-formatting-in-the-windows-forms-datagridview-control.md)