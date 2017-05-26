---
title: 'Procedura: creare un Form Master-Details mediante due controlli DataRepeater (Visual Studio) | Documenti di Microsoft'
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- DataRepeater, master/detail tables
ms.assetid: eec43ae3-05d8-45a1-8d41-3803c6359dbe
caps.latest.revision: 7
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
ms.openlocfilehash: 23789bb11cab17b50928651e1dc00d5d59640c0f
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-masterdetail-form-by-using-two-datarepeater-controls-visual-studio"></a>Procedura: creare un form Master-Details mediante due controlli DataRepeater (Visual Studio)
È possibile visualizzare dati correlati utilizzando due o più <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controlli per creare un form master-details.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Potrebbe ad esempio, si desidera visualizzare un elenco di clienti in uno <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>e quando l'utente seleziona un cliente, visualizzare un elenco di ordini del cliente in un secondo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
 È possibile visualizzare dati correlati mediante il trascinamento degli elementi di dettaglio che condividono lo stesso nodo tabella master dal **origini dati** finestra un <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Ad esempio, se si dispone di un'origine dati che dispone di una tabella Customers e una tabella correlata Orders, noterete entrambe le tabelle come nodi di primo livello nella visualizzazione struttura ad albero di **origini dati** finestra. Espandere il nodo di clienti in modo che è possibile visualizzare le colonne. Si noti che l'ultima colonna nell'elenco è un nodo che rappresenta la tabella Orders. Questo nodo rappresenta gli ordini correlati per un cliente.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-display-related-data-in-two-datarepeater-controls"></a>Per visualizzare dati correlati in due controlli DataRepeater  
  
1.  Trascinare due <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>dei controlli di **Visual Basic Power Packs** nella scheda il **della casella degli strumenti** a un form o un controllo contenitore.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
2.  Trascinare i quadratini di ridimensionamento e la posizione per le dimensioni dei controlli e posizionarli side-by-side.  
  
3.  Scegliere **Mostra origini dati** dal menu **Dati**.  
  
    > [!NOTE]
    >  Se il **origini dati** finestra è vuota, aggiungere un'origine dati. Per ulteriori informazioni, vedere [aggiungere nuove origini dati](https://docs.microsoft.com/visualstudio/data-tools/add-new-data-sources).  
  
4.  Nel **origini dati** finestra, selezionare il nodo di primo livello per la tabella master.  
  
5.  Modificare il tipo di visualizzazione della tabella master per i dettagli, fare clic su **dettagli** nell'elenco a discesa del nodo della tabella.  
  
6.  Trascinare il nodo della tabella master sull'area del modello di elemento del primo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
7.  Espandere il nodo della tabella master e selezionare il nodo dettaglio per la tabella correlata.  
  
8.  Modificare il tipo di visualizzazione della tabella dettagli per i dettagli, fare clic su **dettagli** nell'elenco a discesa del nodo della tabella.  
  
9. Selezionare il nodo della tabella e trascinarlo nell'area del modello di elemento della seconda <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater></xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [Introduzione al controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [Procedura: visualizzare i dati associati in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [Procedura: visualizzare correlati i dati in un Windows Form dell'applicazione](http://msdn.microsoft.com/library/60b1f1ec-6257-42ab-83f0-06d54ed364fd)   
 [Procedura: modificare l'aspetto di un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [Risoluzione dei problemi relativi al controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)
