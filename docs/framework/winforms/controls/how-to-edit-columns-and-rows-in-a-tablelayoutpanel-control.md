---
title: "Procedura: modificare colonne e righe in un controllo TableLayoutPanel | Microsoft Docs"
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
  - "net.ComponentModel.StyleCollectionEditor"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "colonne [Windows Form], modifica"
  - "righe [Windows Form], modifica"
  - "TableLayoutPanel (controllo) [Windows Form], modifica"
ms.assetid: c367ed43-40dc-49eb-9e0f-ba70e83dfec0
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: modificare colonne e righe in un controllo TableLayoutPanel
Per modificare le righe e le colonne dei controlli è possibile utilizzare l'editor di raccolte del controllo <xref:System.Windows.Forms.TableLayoutPanel>, ossia la finestra di dialogo **Stili di riga e colonna**.  
  
> [!NOTE]
>  Per permettere a un controllo di inserire più righe o colonne, impostare le proprietà `RowSpan` e `ColumnSpan` sul controllo.  Per ulteriori informazioni, vedere [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando TableLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md).  
>   
>  Per allineare o estendere un controllo all'interno di una cella, utilizzare la proprietà <xref:System.Windows.Forms.Control.Anchor%2A> del controllo.  Per ulteriori informazioni, vedere [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando TableLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md).  
>   
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per modificare righe e colonne  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.TableLayoutPanel> dalla **Casella degli strumenti** al form.  
  
2.  Fare clic sull'icona dello smart tag del controllo <xref:System.Windows.Forms.TableLayoutPanel> \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\) e selezionare **Modifica righe e colonne** per aprire la finestra di dialogo **Stili di riga e colonna**.  È anche possibile fare clic con il pulsante destro del mouse sul controllo <xref:System.Windows.Forms.TableLayoutPanel> e selezionare **Modifica righe e colonne** dal menu di scelta rapida.  
  
3.  Per aggiungere o rimuovere le colonne, selezionare **Colonne** nella casella di riepilogo a discesa **Tipo di membro**.  
  
4.  Per aggiungere o rimuovere le righe, selezionare **Righe** nella casella di riepilogo a discesa **Tipo di membro**.  
  
5.  Fare clic sul pulsante **Aggiungi** per aggiungere una riga o una colonna all'elenco **Membro**.  
  
6.  Fare clic sul pulsante **Inserisci** per aggiungere una riga o una colonna prima della voce selezionata nell'elenco.  
  
7.  Se si sta aggiungendo una riga o una colonna, selezionare il **Tipo dimensione** per la nuova riga o colonna.  Per ulteriori informazioni, vedere <xref:System.Windows.Forms.SizeType>.  
  
8.  Per rimuovere una riga o una colonna, fare clic sul pulsante **Rimuovi** per eliminare la voce selezionata nell'elenco **Membro**.  
  
## Vedere anche  
 <xref:System.Windows.Forms.SizeType>   
 [Controllo TableLayoutPanel](../../../../docs/framework/winforms/controls/tablelayoutpanel-control-windows-forms.md)