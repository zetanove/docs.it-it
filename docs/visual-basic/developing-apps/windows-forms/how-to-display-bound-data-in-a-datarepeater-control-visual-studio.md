---
title: 'Procedura: visualizzare i dati associati in un controllo DataRepeater (Visual Studio) | Documenti di Microsoft'
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- DataRepeater, data-binding
- DataRepeater, displaying bound controls
ms.assetid: 56a15326-1334-4275-af4e-075cad79e6f7
caps.latest.revision: 11
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9bf8f2f5fcc4dfa2b29e368a4e26bf112e08149e
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-display-bound-data-in-a-datarepeater-control-visual-studio"></a>Procedura: visualizzare i dati associati in un controllo DataRepeater (Visual Studio)
L'utilizzo più comune del <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo consiste nel visualizzare i dati associati da un database o altra origine dati.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
 Oltre ai controlli associati, si desidera aggiungere altri controlli, ad esempio un'etichetta statica o un'immagine che viene ripetuta in ogni elemento di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Per ulteriori informazioni, vedere [procedura: visualizzare i controlli non associati in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md).  
  
 È inoltre possibile associare a un'origine dati in fase di esecuzione impostando la <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>proprietà `True` e l'assegnazione di un'origine dati per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DataSource%2A>proprietà.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DataSource%2A> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> In questo caso, è necessario gestire l'interazione con l'origine dati. Per ulteriori informazioni, vedere [modalità virtuale nel controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/virtual-mode-in-the-datarepeater-control-visual-studio.md).  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-data-bound-datarepeater"></a>Per creare un oggetto DataRepeater con associazione a dati  
  
1.  Trascinare un <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>da controllare il **Visual Basic Power Packs** nella scheda il **della casella degli strumenti** a un form o un controllo contenitore.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
2.  Trascinare i quadratini di ridimensionamento e la posizione di dimensioni e posizione del controllo.  
  
     Si noti che il controllo dispone di due aree rettangolari. L'area superiore è il *modello di elemento*; i controlli aggiunti al modello verranno ripetuti in ogni voce di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo in fase di esecuzione.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> L'area inferiore è il *viewport*, in cui verranno visualizzati gli elementi.  
  
     È anche possibile ridimensionare e posizionare il controllo o il modello di elemento modificando il **dimensioni** e **posizione** proprietà nella finestra Proprietà.  
  
3.  Scegliere **Mostra origini dati** dal menu **Dati**.  
  
    > [!NOTE]
    >  Se il **origini dati** finestra è vuota, aggiungere un'origine dati. Per ulteriori informazioni, vedere [aggiungere nuove origini dati](https://docs.microsoft.com/visualstudio/data-tools/add-new-data-sources).  
  
4.  Nel **origini dati** finestra, selezionare il nodo di primo livello per la tabella che contiene i dati che si desidera associare.  
  
5.  Modificare il tipo di visualizzazione della tabella da `Details` facendo `Details` nell'elenco a discesa del nodo della tabella.  
  
6.  Selezionare il nodo della tabella e trascinarlo nell'area del modello di elemento di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
     È possibile specificare tipi di controlli che vengono visualizzati per ogni campo. Per ulteriori informazioni, vedere [impostare il controllo da creare durante il trascinamento dalla finestra Origini dati](https://docs.microsoft.com/visualstudio/data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater></xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [Introduzione al controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [Procedura: visualizzazione controlli non associati in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)   
 [Procedura: creare un Form Master-Details mediante due controlli DataRepeater (Visual Studio)](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)   
 [Procedura: modificare l'aspetto di un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [Risoluzione dei problemi relativi al controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)
