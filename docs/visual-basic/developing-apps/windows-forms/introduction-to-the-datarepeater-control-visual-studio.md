---
title: Introduzione al controllo DataRepeater (Visual Studio) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- repeating data
- DataRepeater, overview
- DataRepeater
ms.assetid: 78a52a1d-65f0-4ecb-97ff-53bc114300c5
caps.latest.revision: 8
author: stevehoag
ms.author: shoag
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 86078426494caabefc6bbfb036037007e830e1cb
ms.lasthandoff: 03/13/2017

---
# <a name="introduction-to-the-datarepeater-control-visual-studio"></a>Introduzione al controllo DataRepeater (Visual Studio)
Visual Basic Power Packs <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo è un contenitore scorrevole per ripetuti controlli che visualizzano dati, ad esempio, le righe in una tabella di database.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> E può essere utilizzato come alternativa per il <xref:System.Windows.Forms.DataGridView>controllare quando è necessario maggiore controllo sul layout dei dati.</xref:System.Windows.Forms.DataGridView> Il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>"ripete" un gruppo di controlli correlati mediante la creazione di più istanze in una visualizzazione a scorrimento.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Ciò consente agli utenti di visualizzare più record contemporaneamente.  
  
## <a name="overview"></a>Panoramica  
 In fase di progettazione di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo è costituito da due sezioni.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> La sezione esterna è di *viewport*, in cui i dati di scorrimento verranno visualizzati in fase di esecuzione. La sezione (superiore) interna, nota come il *modello di elemento*, è in cui vengono posizionati i controlli che verranno ripetuti in fase di esecuzione, in genere un controllo per ogni campo nell'origine dati. Le proprietà e i controlli nel modello di elemento vengono incapsulati nel <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>proprietà.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>  
  
 In fase di esecuzione di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>viene copiato un virtuale <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>oggetto utilizzato per visualizzare i dati quando si scorre ogni record nella visualizzazione.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> È possibile personalizzare la visualizzazione dei singoli record di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>evento, ad esempio, evidenziando un campo in base al valore in esso contenuti.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> Per ulteriori informazioni, vedere [procedura: modificare l'aspetto di un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md).  
  
 L'utilizzo più comune per un <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo consiste nel visualizzare i dati da una tabella di database o altra origine dati associata.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Oltre a [!INCLUDE[vstecado](../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)] oggetti dati, il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo può eseguire l'associazione a qualsiasi classe che implementa il <xref:System.Collections.IList>interfaccia (incluse le matrici), qualsiasi classe che implementa il <xref:System.ComponentModel.IListSource>interfaccia, qualsiasi classe che implementa il <xref:System.ComponentModel.IBindingList>interfaccia o qualsiasi classe che implementa il <xref:System.ComponentModel.IBindingListView>interfaccia.</xref:System.ComponentModel.IBindingListView> </xref:System.ComponentModel.IBindingList> </xref:System.ComponentModel.IListSource> </xref:System.Collections.IList> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
### <a name="data-binding"></a>Data binding  
 In genere, eseguire l'associazione dati, trascinare i campi dal **origini dati** finestra il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Per ulteriori informazioni, vedere [procedura: visualizzare i dati associati in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md).  
  
 Quando si lavora con grandi quantità di dati, è possibile impostare il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>proprietà `True` per visualizzare un subset di dati disponibili.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> Modalità virtuale richiede l'implementazione di una cache di dati da cui il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>è popolato, ed è necessario controllare tutte le interazioni con la cache dei dati in fase di esecuzione.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Per ulteriori informazioni, vedere [modalità virtuale nel controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/virtual-mode-in-the-datarepeater-control-visual-studio.md).  
  
 È inoltre possibile visualizzare i controlli non associati in un <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Ad esempio, è possibile visualizzare un'immagine che viene ripetuta per ogni elemento. Per ulteriori informazioni, vedere [procedura: visualizzare i controlli non associati in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md).  
  
### <a name="events"></a>Eventi  
 Gli eventi più importanti per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo sono di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>evento, viene generato quando vengono scorsi nuovi elementi nella vista, e <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged>evento, viene generato quando viene selezionato un elemento.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> È possibile utilizzare il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>evento per modificare l'aspetto dell'elemento.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> Ad esempio, è possibile evidenziare i valori negativi. Utilizzare il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged>evento per accedere ai valori dei controlli quando si seleziona un elemento.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged>  
  
 Il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo espone tutti gli eventi di controllo standard nell'Editor di codice.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Tuttavia, alcuni degli eventi non devono essere utilizzati. Tastiera e mouse, ad esempio gli eventi `KeyDown`, `Click`, e `MouseDown` non verrà generato in fase di esecuzione perché il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo stesso non ha mai lo stato attivo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
 Il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>non espone gli eventi in fase di progettazione perché viene creato solo in fase di esecuzione.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> Se si desidera gestire gli eventi di tastiera e mouse, è possibile aggiungere un <xref:System.Windows.Forms.Panel>controllo il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>in fase di progettazione e quindi gestire gli eventi per <xref:System.Windows.Forms.Panel>.</xref:System.Windows.Forms.Panel> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> </xref:System.Windows.Forms.Panel> Per ulteriori informazioni, vedere [risoluzione dei problemi relativi al controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md).  
  
### <a name="customizations"></a>Personalizzazioni  
 Esistono molti modi per personalizzare l'aspetto e comportamento del <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllare, entrambi in fase di esecuzione e in fase di progettazione.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Proprietà possono essere impostate per modificare i colori, nascondere o modificare le intestazioni degli elementi, modificare l'orientamento da verticale a orizzontale e molto altro ancora. Per ulteriori informazioni, vedere [procedura: modificare l'aspetto di un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md), [procedura: visualizzare le intestazioni degli elementi in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-display-item-headers-in-a-datarepeater-control-visual-studio.md), e [procedura: modificare il Layout di un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-layout-of-a-datarepeater-control-visual-studio.md).  
  
 Si noti che alcune proprietà sono valide per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo stesso, mentre altre sono valide solo per i tipi <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Assicurarsi di avere la sezione corretta del controllo selezionato prima di impostare le proprietà. Per ulteriori informazioni, vedere [procedura: modificare l'aspetto di un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md).  
  
 Altre personalizzazioni includono la possibilità di aggiungere o eliminare record di controllo, l'aggiunta di funzionalità di ricerca e visualizzazione dei dati correlati in un formato master e dettaglio. Per ulteriori informazioni, vedere [procedura: disabilitare l'aggiunta e l'eliminazione di elementi DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio.md), [procedura: dati di ricerca in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/how-to-search-data-in-a-datarepeater-control-visual-studio.md), e [procedura: creare un Form Master-Details per mediante due controlli DataRepeater (Visual Studio)](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/datarepeater-control-visual-studio.md)   
 [Procedura dettagliata: Visualizzazione dei dati in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio.md)   
 [Risoluzione dei problemi relativi al controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)
