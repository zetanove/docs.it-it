---
title: "Procedura: modificare il tipo di una colonna DataGridView di Windows Form utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "colonne [Windows Form], tipi"
  - "dati [Windows Form], visualizzazione"
  - "DataGridView (controllo) [Windows Form], modifica del tipo di colonna"
  - "Windows Form, colonne"
ms.assetid: 7f994d45-600d-4190-a187-35803214b40c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: modificare il tipo di una colonna DataGridView di Windows Form utilizzando la finestra di progettazione
Talvolta potrebbe risultare necessario cambiare il tipo per una colonna che è stata già aggiunta a un controllo <xref:System.Windows.Forms.DataGridView> di Windows Form.  Si potrebbe, ad esempio, voler cambiare i tipi di alcune colonne che vengono generate automaticamente quando si associa il controllo a un'origine dati.  Questa operazione si rivela utile quando la tabella visualizzata contiene colonne con chiavi esterne per le righe di una tabella correlata.  In questo caso, è possibile sostituire le colonne di caselle di testo che visualizzano le chiavi esterne con colonne di caselle combinate che visualizzano valori della tabella correlata più significativi.  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.DataGridView>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per cambiare il tipo di una colonna utilizzando la finestra di progettazione  
  
1.  Scegliere il glifo dello smart tag \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\) nell'angolo superiore destro del controllo <xref:System.Windows.Forms.DataGridView> e quindi selezionare **Modifica colonne**.  
  
2.  Selezionare una colonna dall'elenco **Colonne selezionate**.  
  
3.  Nella griglia **Proprietà colonne** impostare la proprietà `ColumnType` sul nuovo tipo di colonna.  
  
    > [!NOTE]
    >  `ColumnType` è una proprietà disponibile solo nella fase di progettazione indicante la classe che rappresenta il tipo di colonna  e non si tratta di una proprietà realmente definita in una classe di colonna.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewColumn>   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)