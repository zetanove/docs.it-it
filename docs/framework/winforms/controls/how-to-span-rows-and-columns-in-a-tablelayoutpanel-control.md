---
title: "Procedura: inserire righe e colonne in un controllo TableLayoutPanel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "net.ComponentModel.StyleCollectionEditor.TLP.SpanRowsColumns"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "celle, unione"
  - "colonne [Windows Form], span"
  - "unione di celle"
  - "righe [Windows Form], span"
  - "TableLayoutPanel (controllo) [Windows Form], espansione di righe e colonne"
ms.assetid: a8a2fdd3-a848-48b0-a4cd-4e85ebded87e
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: inserire righe e colonne in un controllo TableLayoutPanel
In un controllo <xref:System.Windows.Forms.TableLayoutPanel>, è possibile inserire righe e colonne adiacenti tramite i controlli.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per inserire colonne e righe  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.TableLayoutPanel> dalla **Casella degli strumenti** al form.  
  
2.  Trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** nella cella superiore sinistra del controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
3.  Impostare la proprietà **ColumnSpan** del controllo <xref:System.Windows.Forms.Button> su 2.  Il controllo <xref:System.Windows.Forms.Button> inserisce la prima e la seconda colonna.  
  
4.  Impostare la proprietà **RowSpan** del controllo <xref:System.Windows.Forms.Button> su 2.  Il controllo <xref:System.Windows.Forms.Button> inserisce la prima e la seconda riga.  
  
5.  Impostare la proprietà **ColumnSpan** del controllo <xref:System.Windows.Forms.Button> su 1.  Il controllo <xref:System.Windows.Forms.Button> si sposta nella prima colonna e inserisce la prima e la seconda riga.  
  
## Vedere anche  
 [Controllo TableLayoutPanel](../../../../docs/framework/winforms/controls/tablelayoutpanel-control-windows-forms.md)