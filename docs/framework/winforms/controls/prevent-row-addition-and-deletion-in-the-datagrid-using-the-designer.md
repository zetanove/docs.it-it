---
title: "Procedura: impedire l&#39;aggiunta e l&#39;eliminazione di righe nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "DataGridView (controllo) [Windows Form], blocco dell'aggiunta o dell'eliminazione di righe"
ms.assetid: a17722bd-9400-41e6-8dcc-c9c151f0a749
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: impedire l&#39;aggiunta e l&#39;eliminazione di righe nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione
Talvolta potrebbe essere necessario impedire agli utenti di inserire nuove righe di dati o eliminare le righe esistenti nel controllo <xref:System.Windows.Forms.DataGridView>.  Le nuove righe vengono inserite nella riga speciale per i nuovi record in fondo al controllo.  Quando si disabilita l'aggiunta delle righe, la riga per i nuovi record non è visualizzata.  È possibile rendere l'intero controllo di sola lettura disabilitando l'eliminazione delle righe e la modifica delle celle.  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.DataGridView>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per impedire l'aggiunta e l'eliminazione delle righe  
  
-   Scegliere il glifo dello smart tag \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\) nell'angolo superiore destro del controllo <xref:System.Windows.Forms.DataGridView> e deselezionare quindi le caselle di controllo **Attiva aggiunta** e **Attiva eliminazione**.  
  
    > [!NOTE]
    >  Per rendere l'intero controllo di sola lettura, deselezionare anche la casella di controllo **Attiva modifica**.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A?displayProperty=fullName>   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)