---
title: "Procedura: aggiungere un controllo a un oggetto TabPage | Microsoft Docs"
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
  - "controlli delle schede, ordine di tabulazione"
  - "schede, aggiunta di controlli"
  - "TabPage (controllo)"
ms.assetid: b092532e-7346-469f-b9a1-897f9bea4fb7
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: aggiungere un controllo a un oggetto TabPage
È possibile utilizzare il controllo <xref:System.Windows.Forms.TabControl> Windows Form per visualizzare altri controlli in modo organizzato.  Nella procedura seguente viene illustrato come aggiungere un pulsante nella prima scheda.  Per informazioni sull'aggiunta di un'icona alla parte dell'etichetta di una pagina della scheda, vedere [Procedura: modificare l'aspetto del controllo TabControl Windows Form](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md).  
  
### Per aggiungere un controllo a livello di codice  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.Control.ControlCollection.Add%2A> della raccolta restituita dalla proprietà <xref:System.Windows.Forms.Control.Controls%2A> di <xref:System.Windows.Forms.TabPage>:  
  
     [!code-cpp[TabPageControlCollectionHowToAdd#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/tabpagecontrolcollectionhowtoadd/cpp/add.cpp#1)]
     [!code-csharp[TabPageControlCollectionHowToAdd#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/tabpagecontrolcollectionhowtoadd/cs/add.cs#1)]
     [!code-vb[TabPageControlCollectionHowToAdd#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/tabpagecontrolcollectionhowtoadd/vb/add.vb#1)]  
  
## Vedere anche  
 [Controllo TabControl](../../../../docs/framework/winforms/controls/tabcontrol-control-windows-forms.md)   
 [Cenni preliminari sul controllo TabControl](../../../../docs/framework/winforms/controls/tabcontrol-control-overview-windows-forms.md)   
 [Procedura: modificare l'aspetto del controllo TabControl Windows Form](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md)   
 [Procedura: disabilitare le schede](../../../../docs/framework/winforms/controls/how-to-disable-tab-pages.md)   
 [Procedura: aggiungere e rimuovere schede tramite il controllo TabControl Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol.md)