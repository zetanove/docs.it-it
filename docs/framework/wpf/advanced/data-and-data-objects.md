---
title: "Dati e oggetti dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "trasferimento dati [WPF], trascinamento"
  - "DataFormats (classe) [WPF]"
  - "DataObject (classe) [WPF]"
ms.assetid: 5967d557-1867-420f-a524-ae3af78402da
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Dati e oggetti dati
I dati trasferiti durante un'operazione di trascinamento vengono archiviati in un oggetto dati.  Concettualmente, un oggetto dati è costituito da una o più delle coppie seguenti:  
  
-   Oggetto <xref:System.Object> contenente i dati effettivi.  
  
-   Un identificatore del formato dati corrispondente.  
  
 I dati stessi possono essere costituiti da qualsiasi elemento che possa essere rappresentato come un <xref:System.Object> di base.  Il formato dati corrispondente è una stringa o un <xref:System.Type> che fornisce indicazioni sul formato.  Gli oggetti dati supportano l'hosting di più coppie di dati\/formato dati; in questo modo, un singolo oggetto dati può fornire dati in più formati.  
  
<a name="Data_and_Data_Objects"></a>   
## Oggetti dati  
 Tutti gli oggetti dati devono implementare l'interfaccia <xref:System.Windows.IDataObject> che fornisce l'insieme standard di metodi seguente necessario per l'abilitazione e l'esecuzione del trasferimento dei dati.  
  
|Metodo|Riepilogo|  
|------------|---------------|  
|<xref:System.Windows.IDataObject.GetData%2A>|Recupera un oggetto dati in un formato dati specificato.|  
|<xref:System.Windows.IDataObject.GetDataPresent%2A>|Verifica se i dati sono disponibili o se possono essere convertiti in un formato specificato.|  
|<xref:System.Windows.IDataObject.GetFormats%2A>|Restituisce un elenco di formati in cui sono archiviati i dati di questo oggetto o in cui possono essere convertiti.|  
|<xref:System.Windows.IDataObject.SetData%2A>|Archivia i dati specificati in questo oggetto dati.|  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornisce un'implementazione di base di <xref:System.Windows.IDataObject> nella classe <xref:System.Windows.DataObject>.  La classe <xref:System.Windows.DataObject> predefinita è sufficiente per la maggior parte degli scenari di trasferimento dei dati.  
  
 Vi sono vari formati predefiniti, tra cui CSV, file, HTML, RTF, stringa, testo e audio.  Per informazioni sui formati dati predefiniti forniti con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere l'argomento di riferimento della classe <xref:System.Windows.DataFormats>.  
  
 Gli oggetti dati includono in genere una funzionalità per la conversione automatica dei dati archiviati in un formato in un altro formato durante l'estrazione.  Quando si eseguono query per conoscere i formati dati disponibili in un oggetto dati, i formati dati convertibili automaticamente possono essere filtrati da formati dati nativi chiamando il metodo <xref:System.Windows.DataObject.GetFormats%28System.Boolean%29> o <xref:System.Windows.DataObject.GetDataPresent%28System.String%2CSystem.Boolean%29> e impostando il parametro `autoConvert` su `false`.  Quando si aggiungono dati a un oggetto dati con il metodo <xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%2CSystem.Boolean%29>, auto\-la conversione automatica dei dati può essere impedita impostando il parametro `autoConvert` su `false`.  
  
<a name="Working_with_Data_Objects"></a>   
## Utilizzo di oggetti dati  
 In questa sezione vengono illustrate le tecniche comuni per la creazione e l'utilizzo di oggetti dati.  
  
### Creazione di nuovi oggetti dati  
 Tramite la classe <xref:System.Windows.DataObject> sono disponibili molti costruttori di overload che agevolano la compilazione di una nuova istanza di <xref:System.Windows.DataObject> con una coppia di singoli dati\/formato dati.  
  
 Nell'esempio di codice riportato di seguito viene creato un nuovo oggetto dati e viene utilizzato uno dei costruttori di overload <xref:System.Windows.DataObject.%23ctor%2A>\(<xref:System.Windows.DataObject.%23ctor%28System.String%2CSystem.Object%29>\) per inizializzare l'oggetto dati con una stringa e un formato dati specificato.  In questo caso, il formato dati è specificato da una stringa; la classe <xref:System.Windows.DataFormats> fornisce un insieme di stringhe di tipo predefinite.  La conversione automatica dei dati archiviati è consentita per impostazione predefinita.  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_typestring)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_typestring)]  
  
 Per ulteriori esempi di codice per la creazione di un oggetto dati, vedere [Creare un oggetto dati](../../../../docs/framework/wpf/advanced/how-to-create-a-data-object.md).  
  
### Archiviazione di dati in più formati  
 È possibile archiviare dati in più formati in un singolo oggetto dati.  L'utilizzo strategico di più formati dati all'interno di un singolo oggetto dati rende l'oggetto dati potenzialmente utilizzabile da molte più destinazioni di rilascio rispetto ai casi in cui è possibile rappresentare un solo formato dati.  In generale, un'origine del trascinamento non deve essere consapevole dei formati dati utilizzabili da potenziali destinazioni di rilascio.  
  
 Nell'esempio riportato di seguito viene illustrato come utilizzare il metodo <xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%29> per aggiungere dati a un oggetto dati in più formati.  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_storemultipleformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_storemultipleformats)]  
  
### Esecuzione di una query di un oggetto dati per i formati disponibili  
 Poiché un singolo oggetto dati può contenere un numero arbitrario di formati dati, gli oggetti dati consentono di recuperare un elenco di formati dati disponibili.  
  
 Nell'esempio di codice riportato di seguito viene utilizzato l'overload di <xref:System.Windows.DataObject.GetFormats%2A> per ottenere una matrice di stringhe contenente l'indicazione di tutti i formati dati disponibili in un oggetto dati \(nativo e a conversione automatica\).  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats)]  
  
 Per ulteriori esempi di codice per l'esecuzione di query di un oggetto dati per conoscere i formati dati disponibili, vedere [Elencare i formati di dati in un oggetto dati](../../../../docs/framework/wpf/advanced/how-to-list-the-data-formats-in-a-data-object.md).  Per esempi di query di un oggetto dati per stabilire la presenza di un determinato formato dati, vedere [Determinare se un formato di dati è presente in un oggetto dati](../../../../docs/framework/wpf/advanced/how-to-determine-if-a-data-format-is-present-in-a-data-object.md).  
  
### Recupero di dati da un oggetto dati  
 Il recupero di dati da un oggetto dati in un determinato formato richiede semplicemente la chiamata a uno dei metodi <xref:System.Windows.DataObject.GetData%2A> e l'indicazione del formato dati desiderato.  Uno dei metodi <xref:System.Windows.DataObject.GetDataPresent%2A> può essere utilizzato per determinare la presenza di un particolare formato dati.  <xref:System.Windows.DataObject.GetData%2A> restituisce i dati in <xref:System.Object>; a seconda del formato dati, è possibile eseguire il cast di questo oggetto a un contenitore specifico del tipo.  
  
 Nell'esempio di codice riportato di seguito viene utilizzato l'overload di <xref:System.Windows.DataObject.GetDataPresent%28System.String%29> per determinare la disponibilità di un determinato formato dati \(in modo nativo o tramite conversione automatica\).  Se il formato specificato è disponibile, nell'esempio vengono recuperati i dati utilizzando il metodo <xref:System.Windows.DataObject.GetData%28System.String%29>.  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getspecificdataformat)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getspecificdataformat)]  
  
 Per ulteriori esempi di codice per il recupero di dati da un oggetto dati, vedere [Recuperare dati in un formato dati particolare](../../../../docs/framework/wpf/advanced/how-to-retrieve-data-in-a-particular-data-format.md).  
  
### Rimozione di dati da un oggetto dati  
 Non è possibile rimuovere direttamente i dati da un oggetto dati.  Per rimuovere efficacemente i dati da un oggetto dati, seguire i passaggi riportati di seguito:  
  
1.  Creare un nuovo oggetto dati che dovrà contenere solo i dati che si desidera conservare.  
  
2.  "Copiare" i dati desiderati dall'oggetto dati precedente a quello nuovo.  Per copiare i dati, utilizzare uno dei metodi <xref:System.Windows.DataObject.GetData%2A> per recuperare un <xref:System.Object> che contiene i dati non elaborati, quindi utilizzare uno dei metodi <xref:System.Windows.DataObject.SetData%2A> per aggiungere i dati al nuovo oggetto dati.  
  
3.  Sostituire l'oggetto dati precedente con quello nuovo.  
  
> [!NOTE]
>  I metodi <xref:System.Windows.DataObject.SetData%2A> consentono unicamente di aggiungere dati a un oggetto dati, ma non di sostituirli, anche se i dati e il formato dati sono esattamente gli stessi della chiamata precedente.  Se si chiama due volte <xref:System.Windows.DataObject.SetData%2A> per gli stessi dati e formato dati, i dati e il formato dati saranno presenti due volte nell'oggetto dati.