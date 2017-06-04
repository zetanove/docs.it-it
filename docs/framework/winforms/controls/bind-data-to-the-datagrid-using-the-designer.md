---
title: "Procedura: associare dati al controllo DataGridView di Windows Form utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "origini dati, associazione a controlli Windows Form"
  - "DataGridView (controllo) [Windows Form], associazione dati"
  - "controlli Windows Form, associazione a un'origine dati"
ms.assetid: f4f46009-cec2-441b-8668-6b5af057558b
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# Procedura: associare dati al controllo DataGridView di Windows Form utilizzando la finestra di progettazione
È possibile utilizzare la finestra di progettazione per associare un controllo <xref:System.Windows.Forms.DataGridView> a origini dati di tipi diversi, ad esempio database, oggetti business o servizi Web.  Quando si associa il controllo a un'origine dati utilizzando la finestra di progettazione, il controllo viene automaticamente associato a un componente <xref:System.Windows.Forms.BindingSource> che rappresenta l'origine dati  e le colonne vengono generate automaticamente nel controllo in modo da soddisfare le informazioni dello schema fornite dall'origine.  
  
 Una volta generate le colonne, è possibile modificarle per soddisfare le proprie necessità.  Ad esempio, è possibile rimuovere o nascondere quelle che non si devono visualizzare, ridisporle o modificarne i tipi.  Per ulteriori informazioni sulla modifica delle colonne, vedere gli argomenti presenti nella sezione Vedere anche.  
  
 È anche possibile associare più controlli <xref:System.Windows.Forms.DataGridView> a tabelle correlate in modo da creare relazioni Master\-Details.  In questa configurazione, un controllo visualizza una tabella padre e l'altro controllo visualizza soltanto le specifiche righe di una tabella figlio che sono correlate alla riga corrente nella tabella padre.  Per ulteriori informazioni, vedere [Procedura: visualizzare dati correlati in un'applicazione Windows Form](../Topic/How%20to:%20Display%20Related%20Data%20in%20a%20Windows%20Forms%20Application.md).  
  
 Nella procedura riportata di seguito si presuppone l'esistenza di un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.DataGridView> o due controlli per creare una relazione Master\-Details.  Per informazioni sull'avvio di un progetto di questo tipo, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per associare il controllo a un'origine dati  
  
1.  Fare clic sul glifo dello smart tag \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\) nell'angolo superiore destro del controllo <xref:System.Windows.Forms.DataGridView>.  
  
2.  Fare clic sulla freccia a discesa dell'opzione **Scegli origine dati**.  
  
3.  Se il progetto non dispone di un'origine dati, fare clic su **Aggiungi origine dati progetto** e seguire i passaggi indicati dalla procedura guidata.  
  
     Per ulteriori informazioni, vedere [Configurazione guidata origine dati](../Topic/Data%20Source%20Configuration%20Wizard.md).  Nella finestra a discesa **Scegli origine dati** viene visualizzata la nuova origine dati.  Se la nuova origine dati contiene un solo membro, ad esempio una singola tabella di database, il controllo verrà associato automaticamente a tale membro.  Altrimenti, continuare con il passaggio successivo.  
  
4.  Se non è stato già fatto, espandere i nodi **Altre origini dati** e **Origini dati del progetto**, quindi selezionare l'origine dati da associare al controllo.  
  
5.  Se l'origine dati contiene più membri, ad esempio se è stato creato un <xref:System.Data.DataSet?displayProperty=fullName> contenente più tabelle, espandere l'origine dati e quindi selezionare il membro specifico da associare.  
  
6.  Per creare una relazione Master\-Details, nella finestra a discesa **Scegli origini dati** di un secondo controllo <xref:System.Windows.Forms.DataGridView> espandere il componente <xref:System.Windows.Forms.BindingSource> creato per la tabella padre, quindi selezionare la tabella figlio correlata dall'elenco visualizzato.  
  
    > [!NOTE]
    >  Se il progetto già contiene un'origine dati, per creare un form di dati è anche possibile utilizzare la finestra **Origini dati**.  Per ulteriori informazioni, vedere [Origini dati \(finestra\)](../Topic/Data%20Sources%20Window.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.Windows.Forms.DataGridView.DataMember%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.DataSource%2A?displayProperty=fullName>   
 [Procedura: connettersi ai dati di un database](../Topic/How%20to:%20Connect%20to%20Data%20in%20a%20Database.md)   
 [Procedura: aggiungere e rimuovere colonne nel controllo DataGridView di Windows Form utilizzando Progettazione Windows Form](../../../../docs/framework/winforms/controls/add-and-remove-columns-in-the-datagrid-using-the-designer.md)   
 [Procedura: modificare l'ordine delle colonne nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/change-the-order-of-columns-in-the-datagrid-using-the-designer.md)   
 [Procedura: modificare il tipo di una colonna DataGridView di Windows Form utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/change-the-type-of-a-wf-datagridview-column-using-the-designer.md)   
 [Procedura: bloccare le colonne nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/freeze-columns-in-the-datagrid-using-the-designer.md)   
 [Procedura: nascondere le colonne nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/hide-columns-in-the-datagrid-using-the-designer.md)   
 [Procedura: rendere le colonne di sola lettura nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/make-columns-read-only-in-the-datagrid-using-the-designer.md)   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)   
 [Origini dati \(finestra\)](../Topic/Data%20Sources%20Window.md)   
 [Procedura: visualizzare dati correlati in un'applicazione Windows Form](../Topic/How%20to:%20Display%20Related%20Data%20in%20a%20Windows%20Forms%20Application.md)