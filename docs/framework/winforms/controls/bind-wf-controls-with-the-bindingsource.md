---
title: "Procedura: associare controlli Windows Form al componente BindingSource utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "BindingSource (componente) [Windows Form], associazione di controlli"
  - "controlli [Windows Form], associazione"
  - "associazione dati, BindingSource (componente)"
ms.assetid: 391ae170-de5c-40f8-8233-91cb2ee4683a
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: associare controlli Windows Form al componente BindingSource utilizzando la finestra di progettazione
Dopo aver aggiunto controlli al form e determinato l'interfaccia utente desiderata per l'applicazione, è possibile associare i controlli a un'origine dati affinché, in fase di esecuzione, gli utenti siano in grado di modificare e salvare i dati correlati all'applicazione.  
  
 L'associazione di un controllo o di una serie di controlli in Windows Form è un'operazione di semplice esecuzione se si utilizza il controllo <xref:System.Windows.Forms.BindingSource>, che funge da ponte tra i controlli di un form e l'origine dati.  
  
 È possibile associare ai dati uno o più controlli. Nella procedura riportata di seguito un controllo <xref:System.Windows.Forms.TextBox> viene associato a un'origine dati.  
  
 Per completare la procedura si presuppone che si esegua l'associazione a un'origine dati derivata da un database.  Per ulteriori informazioni sulla creazione di origini dati da altri archivi di dati, vedere [Cenni preliminari sulle origini dati](../Topic/Add%20new%20data%20sources.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per associare un controllo in fase di progettazione  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.TextBox> sul form.  
  
2.  Nella finestra **Proprietà**:  
  
    1.  Espandere il nodo **\(DataBindings\)**.  
  
    2.  Fare clic sulla freccia posta accanto alla proprietà <xref:System.Windows.Forms.TextBox.Text%2A>.  
  
         Verrà aperto l'editor di tipi dell'interfaccia utente **DataSource**.  
  
         Se un'origine dati è stata già configurata per il progetto o il form, verrà visualizzata.  
  
3.  Fare clic su **Aggiungi origine dati progetto** per eseguire la connessione con i dati e creare un'origine dati.  
  
4.  Nella pagina iniziale della **Configurazione guidata origine dati** scegliere **Avanti**.  
  
5.  Nella pagina **Seleziona un tipo di origine dati** selezionare **Database**.  
  
6.  Nella pagina **Seleziona connessione dati** selezionare una connessione dati dall'elenco di connessioni disponibili.  Se la connessione dati desiderata non è disponibile, selezionare **Nuova connessione** per creare una nuova connessione dati.  
  
7.  Selezionare **Sì, salva la connessione con nome** per salvare la stringa di connessione nel file di configurazione dell'applicazione.  
  
8.  Selezionare gli oggetti di database da inserire nell'applicazione.  A tal fine selezionare un campo di una tabella che si desidera venga visualizzato dalla classe <xref:System.Windows.Forms.TextBox>.  
  
9. Se lo si desidera, sostituire il nome del DataSet predefinito.  
  
10. Fare clic su **Fine**.  
  
11. Nella finestra **Proprietà** fare nuovamente clic sulla freccia accanto alla proprietà <xref:System.Windows.Forms.TextBox.Text%2A>.  Nell'editor di tipi dell'interfaccia utente **DataSource** selezionare il nome del campo al quale associare la classe <xref:System.Windows.Forms.TextBox>.  
  
     L'editor di tipi dell'interfaccia utente **DataSource** verrà chiuso e il DataSet, il componente <xref:System.Windows.Forms.BindingSource> e l'adattatore di tabelle specifici della connessione dati verranno aggiunti al form.  
  
## Vedere anche  
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.Windows.Forms.BindingNavigator>   
 [Cenni preliminari sulle origini dati](../Topic/Add%20new%20data%20sources.md)   
 [Origini dati \(finestra\)](../Topic/Data%20Sources%20Window.md)