---
title: "How to: Create a Master/Detail Form by Using Two DataRepeater Controls (Visual Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, master/detail tables"
ms.assetid: eec43ae3-05d8-45a1-8d41-3803c6359dbe
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Create a Master/Detail Form by Using Two DataRepeater Controls (Visual Studio)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È possibile visualizzare dati correlati utilizzando due o più controlli <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> per creare un form Master\-Details.  Ad esempio, potrebbe necessario visualizzare un elenco di clienti in un oggetto <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> e, quando l'utente seleziona un cliente, visualizzare un elenco degli ordini relativi a tale cliente in un secondo oggetto <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
 Per visualizzare dati correlati è possibile trascinare gli elementi dettaglio che condividono lo stesso nodo della tabella master dalla finestra **Origini dati** a un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  Se, ad esempio, si dispone di un'origine dati in cui sono presenti una tabella Customers e una tabella correlata Orders, è possibile visualizzare entrambe le tabelle come nodi di livello principale nella visualizzazione ad albero all'interno della finestra **Origini dati**.  Espandere il nodo Customers in modo che sia possibile vedere le colonne.  Si noti che l'ultima colonna dell'elenco è costituita da un nodo espandibile che rappresenta la tabella Orders.  Il nodo indica gli ordini relativi a un cliente.  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### Per visualizzare dati correlati in due controlli DataRepeater  
  
1.  Trascinare due controlli <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> dalla scheda **Visual Basic Power Pack 1.1** della **Casella degli strumenti** a un form o un controllo contenitore.  
  
2.  Trascinare i quadratini di ridimensionamento e di posizionamento per impostare le dimensioni dei controlli e posizionarli l'uno accanto all'altro.  
  
3.  Scegliere **Mostra origini dati** dal menu **Dati**.  
  
    > [!NOTE]
    >  Se la finestra **Origini dati** è vuota, aggiungervi un'origine dati.  Per ulteriori informazioni, vedere la classe [Cenni preliminari sulle origini dati](/visual-studio/data-tools/add-new-data-sources).  
  
4.  Nella finestra **Origini dati**, selezionare il nodo di primo livello della tabella master.  
  
5.  Impostare su Dettagli il tipo di visualizzazione degli elementi della tabella master facendo clic su **Dettagli** nell'elenco a discesa del nodo della tabella.  
  
6.  Trascinare il nodo della tabella master sull'area del modello di elemento del primo controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
7.  Espandere il nodo della tabella master e selezionare il nodo dettaglio per la tabella correlata.  
  
8.  Impostare su Dettagli il tipo di visualizzazione degli elementi della tabella dettaglio facendo clic su **Dettagli** nell'elenco a discesa del nodo della tabella.  
  
9. Selezionare tale nodo della tabella e trascinarlo sull'area del modello di elemento del secondo controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [Introduction to the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [How to: Display Bound Data in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [Procedura: visualizzare dati correlati in un'applicazione Windows Form](../Topic/How%20to:%20Display%20Related%20Data%20in%20a%20Windows%20Forms%20Application.md)   
 [How to: Change the Appearance of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [Troubleshooting the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)