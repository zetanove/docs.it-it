---
title: "Procedura: compilare una finestra di dialogo standard dell&#39;interfaccia utente utilizzando l&#39;elemento Grid | Microsoft Docs"
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
  - "finestre di dialogo, creazione"
  - "Grid (controllo), creazione, finestra di dialogo"
ms.assetid: d6ac3d51-844b-4d29-96d8-81a696a7b960
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: compilare una finestra di dialogo standard dell&#39;interfaccia utente utilizzando l&#39;elemento Grid
In questo esempio viene illustrato come creare una finestra di dialogo standard dell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] utilizzando l'elemento <xref:System.Windows.Controls.Grid>.  
  
## Esempio  
 Nell'esempio seguente viene creata una finestra di dialogo simile alla finestra di dialogo **Esegui** del sistema operativo [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)].  
  
 Viene creato un elemento <xref:System.Windows.Controls.Grid> e vengono utilizzate le classi <xref:System.Windows.Controls.ColumnDefinition> e <xref:System.Windows.Controls.RowDefinition> per definire cinque colonne e quattro righe.  
  
 Viene quindi aggiunto e posizionato un oggetto <xref:System.Windows.Controls.Image>, `RunIcon.png`, per rappresentare l'immagine disponibile nella finestra di dialogo.  L'immagine viene posizionata nella prima colonna e nella prima riga dell'elemento <xref:System.Windows.Controls.Grid>, ossia nell'angolo superiore sinistro.  
  
 In seguito, viene aggiunto un elemento <xref:System.Windows.Controls.TextBlock> alla prima colonna, che si estende sulle colonne rimanenti della prima riga.  Viene aggiunto un secondo elemento <xref:System.Windows.Controls.TextBlock> alla seconda riga della prima colonna, per rappresentare la casella di testo **Apri**.  Viene quindi aggiunto un oggetto <xref:System.Windows.Controls.TextBlock>, che rappresenta l'area di immissione dati.  
  
 Nell'esempio, infine, vengono aggiunti tre elementi <xref:System.Windows.Controls.Button> alla riga finale, che rappresentano gli eventi **OK**, **Annulla** e **Sfoglia**.  
  
 [!code-csharp[GridRunDialog#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridRunDialog/CSharp/window1.xaml.cs#1)]
 [!code-vb[GridRunDialog#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GridRunDialog/VisualBasic/grid_vb.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Grid>   
 <xref:System.Windows.GridUnitType>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/grid-how-to-topics.md)