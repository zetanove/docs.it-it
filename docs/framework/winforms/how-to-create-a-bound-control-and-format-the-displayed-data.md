---
title: "Procedura: creare un controllo con associazione e formattare i dati visualizzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli associati [Windows Form], creazione"
  - "controlli associati [Windows Form], formattazione di dati"
  - "dati [Windows Form], formattazione"
ms.assetid: d5a56228-899d-41d9-8af8-87b3f4ec2f94
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: creare un controllo con associazione e formattare i dati visualizzati
Con il data binding di Windows Form, è possibile formattare i dati visualizzati in un controllo con data binding mediante la **formattazione e binding avanzato** nella finestra di dialogo.  
  
> [!NOTE]
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/Esporta impostazioni** dal menu **Strumenti**.  Per altre informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per associare un controllo e formattare i dati visualizzati  
  
1.  Effettuare una connessione a un'origine dati.  
  
     Per altre informazioni, vedere [Connessione a un'origine dati](../../../docs/framework/data/adonet/connecting-to-a-data-source.md).  
  
2.  Nel form selezionare il controllo e aprire la finestra Proprietà.  
  
3.  Espandere la proprietà **\(DataBindings\)** e quindi nella casella **\(Avanzate\)** fare clic sul pulsante dei puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) per visualizzare la finestra di dialogo **Formattazione e associazione avanzata** con l'elenco completo delle proprietà per tale controllo.  
  
4.  Selezionare la proprietà da associare e fare clic sulla freccia **Binding**.  
  
     Verrà visualizzato un elenco di origini dati disponibili.  
  
5.  Espandere l'origine dati da associare fino a quando non vengono visualizzati i dati desiderati.  
  
     Se ad esempio si vuole associare il valore di una colonna in una tabella di set di dati, espandere il nome del set di dati, quindi espandere il nome della tabella per visualizzare i nomi delle colonne.  
  
6.  Fare clic sul nome dell'elemento a cui effettuare il binding.  
  
7.  Nella casella **Tipo formato** fare clic sul formato da applicare ai dati visualizzati nel controllo.  
  
     In ogni caso, è possibile specificare il valore visualizzato nel controllo se l'origine dati contiene <xref:System.DBNull>.  In caso contrario, le opzioni variano leggermente, a seconda del tipo di formato scelto.  La tabella seguente illustra i tipi di formato e le opzioni.  
  
    |Tipo di formato|Opzione di formattazione|  
    |---------------------|------------------------------|  
    |Nessuna formattazione|Nessuna opzione.|  
    |Numerico|Specificare il numero di posizioni decimali usando il controllo UpDown **Posizioni decimali**.|  
    |Valuta|Specificare il numero di posizioni decimali usando il controllo UpDown **Posizioni decimali**.|  
    |Data\/Ora|Selezionare la modalità di visualizzazione della data e dell'ora selezionando una delle opzioni nella casella di selezione **Tipo**.|  
    |Scientifico|Specificare il numero di posizioni decimali usando il controllo UpDown **Posizioni decimali**.|  
    |Personalizzato|Specificare una stringa di formato personalizzata.<br /><br /> Per altre informazioni, vedere [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md). **Note:**  Le stringhe di formato personalizzate non eseguono sempre correttamente il round trip tra l'origine dati e il controllo associato.  Gestire invece l'evento <xref:System.Windows.Forms.Binding.Parse> o <xref:System.Windows.Forms.Binding.Format> per il binding e applicare la formattazione personalizzata nel codice di gestione degli eventi.|  
  
8.  Fare clic su **OK** per chiudere la finestra di dialogo **Formattazione e associazione avanzata** e tornare alla finestra Proprietà.  
  
## Vedere anche  
 [Procedura: creare un controllo con associazione semplice in un Windows Form](../../../docs/framework/winforms/how-to-create-a-simple-bound-control-on-a-windows-form.md)   
 [User Input Validation in Windows Forms](../../../docs/framework/winforms/user-input-validation-in-windows-forms.md)   
 [Associazione ai dati di Windows Form](../../../docs/framework/winforms/windows-forms-data-binding.md)