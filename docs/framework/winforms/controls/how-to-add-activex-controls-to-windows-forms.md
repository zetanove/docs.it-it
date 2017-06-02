---
title: "Procedura: aggiungere i controlli ActiveX a Windows Form | Microsoft Docs"
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
  - "controlli ActiveX [Windows Form], aggiunta"
  - "form, aggiunta di controlli ActiveX"
  - "controlli Windows Form, controlli ActiveX"
ms.assetid: 54a61e5b-555e-4887-b41e-6244fed271eb
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: aggiungere i controlli ActiveX a Windows Form
Nonostante Progettazione Windows Form sia ottimizzata per contenere controlli per Windows Form, è possibile inserire in un Windows Form anche controlli ActiveX.  
  
> [!CAUTION]
>  Esistono limitazioni relative alle prestazioni dei Windows Form nel caso in cui a essi vengano aggiunti controlli ActiveX.  
  
 Prima di aggiungere controlli ActiveX a un form, è necessario aggiungerli alla Casella degli strumenti.  Per ulteriori informazioni, vedere [Componenti COM, finestra di dialogo Personalizza Casella degli strumenti](http://msdn.microsoft.com/it-it/171333f3-f207-4e02-bbdc-17862556212c).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/Esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per aggiungere un controllo ActiveX al Windows Form  
  
-   Fare doppio clic sul controllo nella Casella degli strumenti.  
  
     In [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] tutti i riferimenti verranno aggiunti al controllo nel progetto.  Per ulteriori informazioni sugli elementi di cui tener conto durante l'utilizzo di controlli ActiveX in Windows Form, vedere [Considerazioni sull'inserimento di controlli ActiveX in Windows Form](../../../../docs/framework/winforms/controls/considerations-when-hosting-an-activex-control-on-a-windows-form.md).  
  
    > [!NOTE]
    >  L'Utilità di importazione di controlli ActiveX di Windows Form \(AxImp.exe\) crea argomenti di un tipo diverso da quanto previsto durante l'importazione di librerie a collegamento dinamico ActiveX.  Gli argomenti creati da AxImp.exe sono simili al seguente: `Invoke(object sender, DWebBrowserEvents2_ProgressChangeEvent e)`, al posto del previsto `Invoke(object sender, DWebBrowserEvents2_ProgressChangeEventArgs e)`.  Questa anomalia, tuttavia, non pregiudica il corretto funzionamento del codice.  Per informazioni dettagliate, vedere [Utilità di importazione di controlli ActiveX di Windows Form \(Aximp.exe\)](../../../../docs/framework/tools/aximp-exe-windows-forms-activex-control-importer.md).  
  
## Vedere anche  
 [Controlli per Windows Form](../../../../docs/framework/winforms/controls/index.md)   
 [Controls and Programmable Objects Compared in Various Languages and Libraries](http://msdn.microsoft.com/it-it/021f2a1b-8247-4348-a5ad-e1d9ab23004b)   
 [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)   
 [Disposizione di controlli in Windows Form](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [Impostazione delle etichette di singoli controlli Windows Form e creazione dei relativi tasti di scelta rapida](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [Controlli Windows Form per funzione](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)