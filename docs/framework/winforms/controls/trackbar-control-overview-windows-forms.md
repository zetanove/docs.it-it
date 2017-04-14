---
title: "Cenni preliminari sul controllo TrackBar (Windows Form) | Microsoft Docs"
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
  - "TrackBar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "scorrimento (controlli), informazioni sui controlli a scorrimento"
  - "dispositivi di scorrimento, informazioni sui dispositivi di scorrimento"
  - "TrackBar (controllo) [Windows Form], informazioni sul controllo TrackBar"
ms.assetid: 95910ecb-8a4c-4776-89fa-206c89ed6973
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Cenni preliminari sul controllo TrackBar (Windows Form)
Il controllo <xref:System.Windows.Forms.TrackBar> di Windows Form, talvolta definito anche "dispositivo di scorrimento", viene utilizzato per lo spostamento all'interno di grandi quantità di informazioni o per modificare in modo visivo un'impostazione numerica.  Il controllo <xref:System.Windows.Forms.TrackBar> è costituito da due parti: la casella, ovvero la parte scorrevole, e i segni di graduazione.  La casella rappresenta la parte regolabile  e la posizione da essa occupata corrisponde alla proprietà <xref:System.Windows.Forms.TrackBar.Value%2A>.  I segni di graduazione costituiscono invece gli indicatori visivi disposti a intervalli regolari.  L'indicatore di avanzamento si sposta in base agli incrementi specificati dall'utente e può essere disposto orizzontalmente o verticalmente.  È possibile ad esempio utilizzare l'indicatore di avanzamento per controllare l'intermittenza del cursore o la velocità del mouse in un sistema.  
  
## Proprietà principali  
 Le proprietà principali del controllo <xref:System.Windows.Forms.TrackBar> sono <xref:System.Windows.Forms.TrackBar.Value%2A>, <xref:System.Windows.Forms.TrackBar.TickFrequency%2A>, <xref:System.Windows.Forms.TrackBar.Minimum%2A> e <xref:System.Windows.Forms.TrackBar.Maximum%2A>.  <xref:System.Windows.Forms.TrackBar.TickFrequency%2A> corrisponde alla spaziatura tra i segni di graduazione.  <xref:System.Windows.Forms.TrackBar.Minimum%2A> e <xref:System.Windows.Forms.TrackBar.Maximum%2A> corrispondono ai valori minimo e massimo rappresentabili sull'indicatore di avanzamento.  
  
 Altre due proprietà importanti sono costituite da <xref:System.Windows.Forms.TrackBar.SmallChange%2A> e <xref:System.Windows.Forms.TrackBar.LargeChange%2A>.  Il valore della proprietà <xref:System.Windows.Forms.TrackBar.SmallChange%2A> corrisponde al numero di posizioni di cui viene spostata la casella in seguito alla pressione dei tasti freccia DESTRA e freccia SINISTRA.  Il valore della proprietà <xref:System.Windows.Forms.TrackBar.LargeChange%2A> corrisponde al numero di posizioni di cui viene spostata la casella in seguito alla pressione dei tasti PGSU e PGGIÙ o a un clic del mouse sull'indicatore di avanzamento ai lati della casella.  
  
## Vedere anche  
 <xref:System.Windows.Forms.TrackBar>   
 [Controllo TrackBar](../../../../docs/framework/winforms/controls/trackbar-control-windows-forms.md)