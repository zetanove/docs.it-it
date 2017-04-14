---
title: "Origini dati supportate da Windows Form | Microsoft Docs"
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
  - "matrici [Windows Form]"
  - "raccolte [Windows Form], associazione a"
  - "dati [Windows Form], provider di dati"
  - "provider di dati [Windows Form]"
  - "origini dati [Windows Form]"
  - "DataColumn (classe)"
  - "DataSet (classe), associazione e Windows Form"
  - "DataTable (classe), associazione e Windows Form"
  - "DataView (classe), associazione e Windows Form"
  - "DataViewManager (classe), associazione e Windows Form"
  - "provider OLE DB, Windows Form"
  - "Windows Form, associazione dati"
  - "Windows Form, dati di origine"
ms.assetid: 3d2c43f6-462b-4d35-9c86-13e9afe012e1
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Origini dati supportate da Windows Form
Tradizionalmente, l'associazione dati è utilizzata all'interno delle applicazioni per utilizzare i dati archiviati in un database.  Con l'associazione dati di Windows Form è possibile invece accedere ai dati contenuti sia in database che in altre strutture, quali matrici e raccolte, a condizione che vengano soddisfatti determinati requisiti minimi.  
  
## Strutture con cui stabilire un'associazione  
 In Windows Form è possibile stabilire associazioni con un'ampia gamma di strutture, dagli oggetti semplici \(associazione semplice\) agli elenchi complessi, come ad esempio le tabelle dati ADO.NET \(associazione complessa\).  Nel caso dell'associazione semplice, Windows Form supporta l'associazione alle proprietà pubbliche nell'oggetto semplice.  In genere, per l'associazione basata su elenchi di Windows Form è necessario che l'oggetto supporti l'interfaccia <xref:System.Collections.IList> o l'interfaccia <xref:System.ComponentModel.IListSource>.  Inoltre, se si stabilisce un'associazione mediante un componente <xref:System.Windows.Forms.BindingSource> è possibile stabilire un'associazione a un oggetto che supporta l'interfaccia <xref:System.Collections.IEnumerable>.  Per ulteriori informazioni sulle interfacce correlate all'associazione dati, vedere [Interfacce correlate all'associazione dati](../../../docs/framework/winforms/interfaces-related-to-data-binding.md).  
  
 Nell'elenco riportato di seguito sono descritte le strutture con cui è possibile stabilire un'associazione in Windows Form.  
  
 <xref:System.Windows.Forms.BindingSource>  
 <xref:System.Windows.Forms.BindingSource> è l'origine dati Windows Form più comune e agisce come proxy tra un'origine dati e i controlli Windows Form.  Il criterio di utilizzo generale di <xref:System.Windows.Forms.BindingSource> consiste nell'associare i controlli alla classe <xref:System.Windows.Forms.BindingSource> e nell'associare la classe <xref:System.Windows.Forms.BindingSource> all'origine dati, ad esempio a una tabella dati ADO.NET o a un oggetto business.  La classe <xref:System.Windows.Forms.BindingSource> fornisce servizi che attivano e migliorano il livello di supporto dell'associazione dati.  I controlli Windows Form basati su elenchi, come <xref:System.Windows.Forms.DataGridView> e <xref:System.Windows.Forms.ComboBox>, ad esempio, non supportano in maniera diretta l'associazione a origini dati <xref:System.Collections.IEnumerable>, tuttavia è possibile dare vita a questo scenario creando un'associazione mediante una classe <xref:System.Windows.Forms.BindingSource>.  In questo caso, la classe <xref:System.Windows.Forms.BindingSource> convertirà l'origine dati in un'interfaccia <xref:System.Collections.IList>.  
  
 Oggetti semplici  
 Windows Form supporta l'associazione dati delle proprietà dei controlli con le proprietà pubbliche nell'istanza di un oggetto tramite il tipo <xref:System.Windows.Forms.Binding>.  Windows Form inoltre supporta l'associazione di controlli basati su elenchi, come ad esempio <xref:System.Windows.Forms.ListControl>, con un'istanza di un oggetto quando viene utilizzata la classe <xref:System.Windows.Forms.BindingSource>.  
  
 Matrice o raccolta  
 Per agire come origine dati, un elenco deve implementare l'interfaccia <xref:System.Collections.IList>. Un esempio è costituito da una matrice che rappresenta un'istanza della classe <xref:System.Array>.  Per ulteriori informazioni sulle matrici, vedere [How to: Create an Array of Objects \(Visual Basic\)](http://msdn.microsoft.com/it-it/6b64e069-0387-400c-9081-3bdc581020c3).  
  
 In generale, è necessario utilizzare la classe <xref:System.ComponentModel.BindingList%601> quando si creano elenchi di oggetti per l'associazione dati.  <xref:System.ComponentModel.BindingList%601> è una versione generica dell'interfaccia <xref:System.ComponentModel.IBindingList>.  L'interfaccia <xref:System.ComponentModel.IBindingList> estende l'interfaccia <xref:System.Collections.IList> aggiungendo proprietà, metodi ed eventi necessari per l'associazione dati bidirezionale.  
  
 <xref:System.Collections.IEnumerable>  
 I controlli Windows Form possono essere associati a origini dati che supportano solo l'interfaccia <xref:System.Collections.IEnumerable> se l'associazione avviene tramite un componente <xref:System.Windows.Forms.BindingSource>.  
  
 Oggetti dati [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]  
 In [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] sono disponibili diverse strutture di dati con cui è possibile stabilire l'associazione.  Ciascuna presenta caratteristiche di complessità differente.  
  
-   <xref:System.Data.DataColumn>.  Una classe <xref:System.Data.DataColumn> rappresenta il blocco predefinito fondamentale di una classe <xref:System.Data.DataTable>, poiché una tabella è costituita da un certo numero di colonne.  Ogni classe <xref:System.Data.DataColumn> dispone di una proprietà <xref:System.Data.DataColumn.DataType%2A> che determina il tipo di dati contenuti nelle colonne, ad esempio i componenti di un'automobile in una tabella in cui vengono descritte auto.  È possibile eseguire un'associazione semplice di un controllo, ad esempio la proprietà <xref:System.Windows.Forms.Control.Text%2A> di un controllo <xref:System.Windows.Forms.TextBox>, a una colonna all'interno di una tabella dati.  
  
-   <xref:System.Data.DataTable>.  Una classe <xref:System.Data.DataTable> è la rappresentazione di una tabella con righe e colonne in [!INCLUDE[vstecado](../../../includes/vstecado-md.md)].  Una tabella dati contiene due raccolte: <xref:System.Data.DataColumn>, che rappresenta le colonne di dati di una determinata tabella e con cui viene determinato il tipo di dati che possono essere inseriti in tale tabella, e <xref:System.Data.DataRow>, che rappresenta le righe di dati di una tabella.  È possibile eseguire l'associazione complessa di un controllo alle informazioni contenute in una tabella dati, ad esempio associando il controllo <xref:System.Windows.Forms.DataGridView> a una tabella dati.  Quando si esegue l'associazione a una classe <xref:System.Data.DataTable>, si effettua in realtà un'associazione alla visualizzazione predefinita della tabella.  
  
-   <xref:System.Data.DataView>.  Una classe <xref:System.Data.DataView> rappresenta una visualizzazione personalizzata di un'unica tabella dati che può essere ordinata o filtrata.  Una visualizzazione dati è lo snapshot dei dati utilizzato dai controlli con associazione complessa.  È possibile eseguire un'associazione semplice o complessa ai dati all'interno di una visualizzazione dati, ma è opportuno tenere presente che in questo modo viene eseguita un'associazione a un'immagine fissa dei dati e non a un'origine dati che viene aggiornata.  
  
-   <xref:System.Data.DataSet>.  Una classe <xref:System.Data.DataSet> rappresenta una raccolta di tabelle, relazioni e vincoli dei dati di un database.  È possibile eseguire un'associazione semplice o complessa ai dati all'interno di un oggetto DataSet, ma è necessario tenere presente che in questo modo viene eseguita un'associazione alla classe <xref:System.Data.DataViewManager> predefinita di <xref:System.Data.DataSet>, come illustrato al punto successivo.  
  
-   <xref:System.Data.DataViewManager>.  Una classe <xref:System.Data.DataViewManager> rappresenta una visualizzazione personalizzata dell'intero <xref:System.Data.DataSet>, analoga alla classe <xref:System.Data.DataView> ma contenente relazioni.  Con una raccolta <xref:System.Data.DataViewManager.DataViewSettings%2A> è possibile impostare filtri predefiniti e ordinare opzioni per qualsiasi visualizzazione predisposta da <xref:System.Data.DataViewManager> per una determinata tabella.  
  
## Vedere anche  
 [Notifica delle modifiche nell'associazione dati dei Windows Form](../../../docs/framework/winforms/change-notification-in-windows-forms-data-binding.md)   
 [Associazione dati e Windows Form](../../../docs/framework/winforms/data-binding-and-windows-forms.md)   
 [Associazione ai dati di Windows Form](../../../docs/framework/winforms/windows-forms-data-binding.md)