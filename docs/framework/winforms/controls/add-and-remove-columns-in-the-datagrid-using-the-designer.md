---
title: "Procedura: aggiungere e rimuovere colonne nel controllo DataGridView di Windows Form utilizzando Progettazione Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vs.DataGridViewAddColumnDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "DataGridView (controllo) [Windows Form], aggiunta di colonne"
  - "DataGridView (controllo) [Windows Form], rimozione di colonne"
ms.assetid: 9e709f35-0a8c-4e7e-b4c4-bacb7a834077
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: aggiungere e rimuovere colonne nel controllo DataGridView di Windows Form utilizzando Progettazione Windows Form
Per poter visualizzare i dati è necessario che nel controllo <xref:System.Windows.Forms.DataGridView> di Windows Form siano presenti delle colonne.  Se si intende inserire i dati nel controllo manualmente, anche le colonne devono essere aggiunte personalmente.  In alternativa, è possibile associare il controllo a un'origine dati che genera e popola le colonne automaticamente.  Se l'origine dati contiene più colonne rispetto a quelle da visualizzare, è possibile rimuovere le colonne non desiderate.  
  
 Nelle seguenti procedure è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.DataGridView>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per aggiungere una colonna utilizzando la finestra di progettazione  
  
1.  Scegliere il glifo dello smart tag \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\) nell'angolo superiore destro del controllo <xref:System.Windows.Forms.DataGridView> e quindi selezionare **Aggiungi colonna**.  
  
2.  Nella finestra di dialogo **Aggiungi colonna**, scegliere l'opzione **Colonna associata ai dati** e selezionare una colonna dall'origine dati o scegliere l'opzione **Colonna non associata** e definire la colonna utilizzando gli appositi campi.  
  
3.  Fare clic sul pulsante **Aggiungi** per aggiungere la colonna che viene visualizzata nella finestra di progettazione se le colonne esistenti non occupano già l'area di visualizzazione del controllo.  
  
    > [!NOTE]
    >  È possibile modificare le proprietà della colonna nella finestra di dialogo **Modifica colonne** disponibile nello smart tag del controllo.  
  
### Per rimuovere una colonna utilizzando la finestra di progettazione  
  
1.  Scegliere **Modifica colonne** dallo smart tag del controllo.  
  
2.  Selezionare una colonna dall'elenco **Colonne selezionate**.  
  
3.  Fare clic sul pulsante **Rimuovi** per eliminare la colonna dalla finestra di progettazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)