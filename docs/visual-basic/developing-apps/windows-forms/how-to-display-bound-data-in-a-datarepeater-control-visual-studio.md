---
title: "How to: Display Bound Data in a DataRepeater Control (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, data-binding"
  - "DataRepeater, displaying bound controls"
ms.assetid: 56a15326-1334-4275-af4e-075cad79e6f7
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# How to: Display Bound Data in a DataRepeater Control (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> viene generalmente utilizzato per visualizzare dati associati provenienti da database o da altre origini dati.  
  
 In aggiunta a controlli associati, è possibile aggiungere altri controlli, ad esempio un'etichetta statica o un'immagine ripetuta su ciascun elemento del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  Per ulteriori informazioni, vedere la classe [How to: Display Unbound Controls in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md).  
  
 È inoltre possibile eseguire un'associazione a un'origine dati in fase di esecuzione impostando la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> su `True` e assegnando un'origine dati alla proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DataSource%2A>.  In questo caso, sarà necessario gestire ogni interazione con l'origine dati.  Per ulteriori informazioni, vedere [Virtual Mode in the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/virtual-mode-in-the-datarepeater-control-visual-studio.md).  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### Per creare un oggetto DataRepeater con associazione a dati  
  
1.  Trascinare un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> dalla scheda **Visual Basic Power Pack 1.1** della **Casella degli strumenti** a un form o un controllo contenitore.  
  
2.  Trascinare i quadratini di ridimensionamento e di posizionamento per impostare le dimensioni e la posizione del controllo.  
  
     Si noti che il controllo dispone di due aree rettangolari.  L'area superiore è il *modello di elemento*. I controlli aggiunti al modello verranno ripetuti in fase di esecuzione in ciascun elemento del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  L'area inferiore è il *riquadro di visualizzazione*, dove gli elementi verranno visualizzati.  
  
     Per ridimensionare e posizionare il controllo o il modello di elemento è anche possibile modificare le proprietà **Size** e **Position** nella finestra Proprietà.  
  
3.  Scegliere **Mostra origini dati** dal menu **Dati**.  
  
    > [!NOTE]
    >  Se la finestra **Origini dati** è vuota, aggiungervi un'origine dati.  Per ulteriori informazioni, vedere la classe [Cenni preliminari sulle origini dati](/visual-studio/data-tools/add-new-data-sources).  
  
4.  Nella finestra **Origini dati**, selezionare il nodo di livello superiore relativo alla tabella contenente i dati da associare.  
  
5.  Impostare su `Details` il tipo di visualizzazione degli elementi della tabella facendo clic su `Details` nell'elenco a discesa del nodo della tabella.  
  
6.  Selezionare il nodo della tabella e trascinarlo sull'area del modello di elemento del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
     È possibile specificare quali tipi di controlli vengono visualizzati per ciascuno campo.  Per ulteriori informazioni, vedere [Impostare il controllo da creare durante il trascinamento dalla finestra Origini dati](/visual-studio/data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [Introduction to the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [How to: Display Unbound Controls in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)   
 [How to: Create a Master\/Detail Form by Using Two DataRepeater Controls](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)   
 [How to: Change the Appearance of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [Troubleshooting the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)