---
title: "Importazione dello schema per generare classi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF, importazione ed esportazione di schemi"
  - "Classe XsdDataContractImporter"
ms.assetid: b9170583-8c34-43bd-97bb-6c0c8dddeee0
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Importazione dello schema per generare classi
Per generare classi da schemi che possono essere usati con [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], utilizzare il <xref:System.Runtime.Serialization.XsdDataContractImporter> (classe). In questo argomento viene descritto il processo e le relative varianti.  
  
## <a name="the-import-process"></a>Processo di importazione  
 Il processo di importazione dello schema inizia con un <xref:System.Xml.Schema.XmlSchemaSet> e produce un <xref:System.CodeDom.CodeCompileUnit>.  
  
 La classe `XmlSchemaSet` fa parte del modello di oggetti dello schema di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] che rappresenta un set di documenti dello schema XSD (XML Schema Definition Language). Per creare un `XmlSchemaSet` oggetto da un set di documenti XSD, deserializzare ogni documento in un <xref:System.Xml.Schema.XmlSchema> oggetto (tramite il <xref:System.Xml.Serialization.XmlSerializer>) e aggiungere questi oggetti in un nuovo `XmlSchemaSet`.  
  
 La classe `CodeCompileUnit` fa parte del CodeDOM (Code Document Object Model) di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] che rappresenta il codice [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] in modo astratto. Per generare il codice effettivo da un `CodeCompileUnit`, usare una sottoclasse del <xref:System.CodeDom.Compiler.CodeDomProvider> classe, ad esempio il <xref:Microsoft.CSharp.CSharpCodeProvider> o <xref:Microsoft.VisualBasic.VBCodeProvider> (classe).  
  
#### <a name="to-import-a-schema"></a>Per importare uno schema  
  
1.  Creare un'istanza di <xref:System.Runtime.Serialization.XsdDataContractImporter>.  
  
2.  Facoltativo. Passare `CodeCompileUnit` nel costruttore. I tipi generati durante l'importazione dello schema vengono aggiunti a questa istanza di `CodeCompileUnit` anziché iniziare con un'istanza `CodeCompileUnit` vuota.  
  
3.  Facoltativo. Chiamare uno del <xref:System.Runtime.Serialization.XsdDataContractImporter.CanImport%2A> metodi. Il metodo determina se lo schema specificato è un schema del contratto dati valido e può essere importato. Il metodo `CanImport` presenta gli stessi overload di `Import` (il passaggio successivo).  
  
4.  Chiamare uno degli overload `Import` metodi, ad esempio, il <xref:System.Runtime.Serialization.XsdDataContractImporter.Import%28System.Xml.Schema.XmlSchemaSet%29> metodo.  
  
     L'overload più semplice accetta una classe `XmlSchemaSet` e importa tutti i tipi, incluso quelli anonimi, presenti in tale set di schemi. Altri overload consentono di specificare il tipo XSD o un elenco di tipi da importare (sotto forma di un <xref:System.Xml.XmlQualifiedName> o una raccolta di `XmlQualifiedName` oggetti). In questo caso, vengono importati solo i tipi specificati. Un overload accetta un <xref:System.Xml.Schema.XmlSchemaElement> che importa un elemento specifico fuori il `XmlSchemaSet`, insieme al tipo associato (se è anonimo o No). Questo overload restituisce una classe `XmlQualifiedName` che rappresenta il nome del contratto dati del tipo generato per questo elemento.  
  
     Più chiamate al metodo `Import` determinano l'aggiunta di più elementi alla stessa classe `CodeCompileUnit`. Se esiste già un tipo in `CodeCompileUnit`, non ne viene generato un altro. È consigliabile chiamare più volte `Import` sullo stesso `XsdDataContractImporter` anziché usare più oggetti `XsdDataContractImporter`. Questa procedura è consigliata per evitare la generazione di tipi duplicati.  
  
    > [!NOTE]
    >  Se si verifica un errore durante l'importazione, lo stato della classe `CodeCompileUnit` sarà imprevedibile. Se si usa una classe `CodeCompileUnit` da un'importazione non riuscita, è possibile esporre il sistema a vulnerabilità della protezione.  
  
5.  Accesso di `CodeCompileUnit` tramite il <xref:System.Runtime.Serialization.XsdDataContractImporter.CodeCompileUnit%2A> proprietà.  
  
### <a name="import-options-customizing-the-generated-types"></a>Opzioni di importazione: personalizzazione dei tipi generati  
 È possibile impostare il <xref:System.Runtime.Serialization.XsdDataContractImporter.Options%2A> proprietà del <xref:System.Runtime.Serialization.XsdDataContractImporter> a un'istanza del <xref:System.Runtime.Serialization.ImportOptions> classe per controllare vari aspetti del processo di importazione. Alcune opzioni influenzano direttamente i tipi generati.  
  
#### <a name="controlling-the-access-level-generateinternal-or-the-internal-switch"></a>Controllo del livello di accesso (opzione GenerateInternal o /internal)  
 Corrisponde al **/ interno** attivata la [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  
  
 In genere, i tipi pubblici vengono generati dallo schema, con campi privati e proprietà dei membri dati pubblici corrispondenti. Per generare invece tipi interni, impostare il <xref:System.Runtime.Serialization.ImportOptions.GenerateInternal%2A> proprietà `true`.  
  
 Nell'esempio seguente viene illustrato uno schema trasformato in una classe quando il <xref:System.Runtime.Serialization.ImportOptions.GenerateInternal%2A> è impostata su`true.`  
  
 [!code-csharp[c_SchemaImportExport#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#2)]
 [!code-vb[c_SchemaImportExport#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#2)]  
  
#### <a name="controlling-namespaces-namespaces-or-the-namespace-switch"></a>Controllo degli spazi dei nomi (opzione Namespaces o /namespace)  
 Corrisponde al **/namespace** attivata di `Svcutil.exe` strumento.  
  
 In genere, vengono generati tipi generati dallo schema in [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] spazi dei nomi, con ogni spazio dei nomi XSD corrisponde a uno specifico [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] dello spazio dei nomi in base a un mapping descritto in [riferimento dello Schema del contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md). È possibile personalizzare questo mapping impostando la <xref:System.Runtime.Serialization.ImportOptions.Namespaces%2A> proprietà per un <xref:System.Collections.Generic.Dictionary%602>.\</TKey, TValue> Se uno specifico spazio dei nomi XSD viene rilevato nel dizionario, anche lo spazio dei nomi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] corrispondente viene prelevato dal dizionario.  
  
 Si consideri ad esempio lo schema seguente.  
  
 <!-- TODO: review snippet reference [!code[c_SchemaImportExport#10](../../../../samples/snippets/common/VS_Snippets_CFX/c_schemaimportexport/common/source.config#10)]  -->  
  
 Nell'esempio seguente viene usata la proprietà `Namespaces` per associare lo spazio dei nomi "http://schemas.contoso.com/carSchema" a "Contoso.Cars".  
  
 [!code-csharp[c_SchemaImportExport#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#8)]
 [!code-vb[c_SchemaImportExport#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#8)]  
  
#### <a name="adding-the-serializableattribute-generateserializable-or-the-serializable-switch"></a>Aggiunta di SerializableAttribute (opzione GenerateSerializable o /serializable)  
 Corrisponde al **/ serializzabile** attivata di `Svcutil.exe` strumento.  
  
 Talvolta è importante per i tipi generati dallo schema possano essere usati con [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] motori di serializzazione di runtime (ad esempio, il <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=fullName> e <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> classi). Questo aspetto è utile quando si usano tipi per i servizi remoti [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]. A tale scopo, è necessario applicare il <xref:System.SerializableAttribute> attributo tipi generati in aggiunta alle normali <xref:System.Runtime.Serialization.DataContractAttribute> attributo. L'attributo viene generato automaticamente se l'opzione di importazione `GenerateSerializable` è impostata su `true`.  
  
 Nell'esempio seguente viene illustrata la classe `Vehicle` generata con l'opzione di importazione `GenerateSerializable` impostata su `true`.  
  
 [!code-csharp[c_SchemaImportExport#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#4)]
 [!code-vb[c_SchemaImportExport#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#4)]  
  
#### <a name="adding-data-binding-support-enabledatabinding-or-the-enabledatabinding-switch"></a>Aggiunta del supporto dei data binding (opzione EnableDataBinding o /enableDataBinding)  
 Corrisponde al **/enableDataBinding** dello strumento Svcutil.exe.  
  
 In alcuni casi può essere necessario associare i tipi generati dallo schema ai componenti dell'interfaccia utente grafica in modo che qualsiasi aggiornamento alle istanze di questi tipi aggiorni automaticamente l'interfaccia utente. Il `XsdDataContractImporter` può generare tipi che implementano il <xref:System.ComponentModel.INotifyPropertyChanged> interfaccia in modo che qualsiasi modifica delle proprietà generi un evento. Se si generano tipi da utilizzare con un ambiente di programmazione dell'interfaccia utente client che supporta questa interfaccia (ad esempio [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)]), impostare il <xref:System.Runtime.Serialization.ImportOptions.EnableDataBinding%2A> proprietà `true` per abilitare questa funzionalità.  
  
 Nell'esempio seguente il `Vehicle` classe generata con il <xref:System.Runtime.Serialization.ImportOptions.EnableDataBinding%2A> impostato su `true`.  
  
 [!code-csharp[C_SchemaImportExport#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#5)]
 [!code-vb[C_SchemaImportExport#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#5)]  
  
### <a name="import-options-choosing-collection-types"></a>Opzioni di importazione: scelta dei tipi di raccolta  
 Due modelli speciali in XML rappresentano raccolte di elementi: elenchi di elementi e associazioni tra due elementi. Di seguito è riportato un esempio di un elenco di stringhe.  
  
 <!-- TODO: review snippet reference [!code[C_SchemaImportExport#11](../../../../samples/snippets/common/VS_Snippets_CFX/c_schemaimportexport/common/source.config#11)]  -->  
  
 Nell'esempio seguente viene mostrata un'associazione tra una stringa e un numero intero (`city name` e `population`).  
  
 <!-- TODO: review snippet reference [!code[C_SchemaImportExport#12](../../../../samples/snippets/common/VS_Snippets_CFX/c_schemaimportexport/common/source.config#12)]  -->  
  
> [!NOTE]
>  Qualsiasi associazione può essere considerata un elenco. Ad esempio, è possibile visualizzare l'associazione precedente come un elenco di oggetti `city` complessi che presentano due campi (un campo stringa e un campo numero intero). Entrambi i modelli sono rappresentati nello schema XSD. Non è possibile differenziare un elenco da un'associazione, pertanto tali modelli vengono sempre considerati come elenchi a meno che nello schema sia presente un'annotazione speciale, specifica di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. L'annotazione indica che un modello specifico rappresenta un'associazione. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Riferimento allo Schema del contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md).  
  
 In genere, un elenco viene importato come un contratto dati della raccolta che deriva da un elenco generico o come una matrice [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], a seconda che lo schema segua o meno il modello di denominazione standard per le raccolte. Questo è descritto in dettaglio in [tipi di raccolta nei contratti dati](../../../../docs/framework/wcf/feature-details/collection-types-in-data-contracts.md). Le associazioni normalmente vengono importate come un <xref:System.Collections.Generic.Dictionary%602> oppure un contratto dati della raccolta che deriva dall'oggetto dizionario.\</TKey, TValue> Si consideri ad esempio lo schema seguente.  
  
 <!-- TODO: review snippet reference [!code[c_SchemaImportExport#13](../../../../samples/snippets/common/VS_Snippets_CFX/c_schemaimportexport/common/source.config#13)]  -->  
  
 Questo schema viene importato come segue (vengono visualizzati i campi anziché le proprietà per migliorare la leggibilità).  
  
 [!code-csharp[c_SchemaImportExport#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#6)]
 [!code-vb[c_SchemaImportExport#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#6)]  
  
 È possibile personalizzare i tipi di raccolta generati per tali modelli di schema. Ad esempio, si desidera generare raccolte che derivano dal <xref:System.ComponentModel.BindingList%601> anziché il <xref:System.Collections.Generic.List%601> classe per associare il tipo a una casella di riepilogo e averlo aggiornato automaticamente quando cambia il contenuto della raccolta. A tale scopo, impostare il <xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A> proprietà di <xref:System.Runtime.Serialization.ImportOptions> classe a un elenco di tipi di raccolta da usare (successivamente indicati come tipi di riferimento). Quando si importa una raccolta, questo elenco di tipi di raccolta a cui si fa riferimento viene analizzato e la raccolta più corrispondente viene usata, se ne viene trovata una. Le associazioni vengono confrontate solo con tipi che implementano il tipo generico o non generica <xref:System.Collections.IDictionary> interfaccia, mentre gli elenchi vengono confrontati con qualsiasi tipo di raccolta supportato.  
  
 Ad esempio, se il <xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A> è impostata su un <xref:System.ComponentModel.BindingList%601>, `people` nell'esempio precedente viene generato come segue.  
  
 [!code-csharp[C_SchemaImportExport#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#7)]
 [!code-vb[C_SchemaImportExport#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#7)]  
  
 Un tipo generico chiuso è considerato la corrispondenza migliore, Ad esempio, se i tipi di `BindingList(Of Integer)` e <xref:System.Collections.ArrayList> vengono passati alla raccolta di tipi di riferimento, qualsiasi elenco di numeri interi trovato nello schema viene importato come un `BindingList(Of Integer)`. Qualsiasi altro elenco, ad esempio, un `List(Of String)`, viene importato come un `ArrayList`.  
  
 Se viene aggiunto un tipo che implementa l'interfaccia `IDictionary` generica alla raccolta di tipi a cui si fa riferimento, i relativi parametri del tipo devono essere completamente aperti o completamente chiusi.  
  
 Non è consentito l'uso di duplicati. Ad esempio, non è possibile aggiungere `List(Of Integer)` e `Collection(Of Integer)` ai tipi a cui si fa riferimento. Questa operazione renderebbe impossibile determinare quale elemento deve essere usato quando nello schema è presente un elenco di numeri interi. I duplicati verranno rilevati solo se nello schema esiste un tipo che espone il problema dei duplicati. Se ad esempio lo schema importato non contiene elenchi di numeri interi, è consentito avere sia `List(Of Integer)` che `Collection(Of Integer)` nella raccolta di tipi a cui si fa riferimento, ma nessuno dei due elementi eserciterà alcun effetto.  
  
 Il meccanismo dei tipi della raccolta a cui si fa riferimento funziona ugualmente per le raccolte di tipi complessi (incluse le raccolte di altre raccolte) e non solo per raccolte di primitivi.  
  
 Il `ReferencedCollectionTypes` proprietà corrisponde al **/collectionType** dello strumento SvcUtil.exe. Si noti che per fare riferimento a più tipi di raccolta, il **/collectionType** deve essere specificata più volte. Se il tipo non è presente in mscorlib. dll, l'assembly è necessario fare riferimento tramite il **/Reference** passare.  
  
#### <a name="import-options-referencing-existing-types"></a>Opzioni di importazione: riferimento ai tipi esistenti  
 A volte i tipi nello schema corrispondono ai tipi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] esistenti e non è necessario generare questi tipi da zero (questa sezione si applica solo ai tipi non di raccolta. Per i tipi di raccolta, vedere la sezione precedente).  
  
 Ad esempio, è possibile che si disponga di un contratto dati "Person" standard per tutta l'azienda che si desidera usare sempre quando si rappresenta una persona. Ogni volta che un servizio usa questo tipo e lo schema è presente nei metadati del servizio, è possibile riutilizzare il tipo `Person` esistente durante l'importazione di questo schema anziché generare un nuovo tipo per ogni servizio.  
  
 A tale scopo, passare un elenco di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] tipi che si desidera riutilizzare nella raccolta di <xref:System.Runtime.Serialization.ImportOptions.ReferencedTypes%2A> proprietà restituisce il <xref:System.Runtime.Serialization.ImportOptions> (classe). Se uno di questi tipi presenta un nome del contratto dati e un spazio dei nomi corrispondenti al nome e allo spazio dei nomi di un tipo di schema, viene eseguito un confronto strutturale. Se si stabilisce che i tipi hanno nomi e strutture corrispondenti, il tipo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] esistente viene riutilizzato anziché generare un nuovo tipo. Se corrisponde solo il nome ma non la struttura, viene generata un'eccezione. Si noti che non è consentito il controllo delle versioni quando si fa riferimento ai tipi (ad esempio, aggiungendo nuovi membri dati facoltativi). Le strutture devono corrispondere perfettamente.  
  
 È possibile aggiungere più tipi con lo stesso nome del contratto dati e lo stesso spazio dei nomi alla raccolta di tipi a cui si fa riferimento, fintanto che non vengono importati tipi dello schema con tale nome e spazio dei nomi. In questo modo è possibile aggiungere facilmente tutti i tipi di un assembly alla raccolta senza temere che vengano creati duplicati dei tipi che non sono presenti nello schema.  
  
 Il `ReferencedTypes` proprietà corrisponde al **/Reference** in alcune modalità di utilizzo dello strumento Svcutil.exe.  
  
> [!NOTE]
>  Quando si utilizza il Svcutil.exe o (in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)]) il **Aggiungi riferimento al servizio** viene fatto automaticamente riferimento strumenti, tutti i tipi in mscorlib. dll.  
  
#### <a name="import-options-importing-non-datacontract-schema-as-ixmlserializable-types"></a>Opzioni di importazione: importazione di schemi diversi dal contratto dati come tipi IXmlSerializable  
 Il <xref:System.Runtime.Serialization.XsdDataContractImporter> supporta un sottoinsieme limitato dello schema. Se sono presenti costrutti dello schema non supportati (ad esempio, attributi XML), il tentativo di importazione non riesce e viene generata un'eccezione. Tuttavia, l'impostazione di <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> proprietà `true` estende l'intervallo di schemi supportati. Se impostato su `true`, <xref:System.Runtime.Serialization.XsdDataContractImporter> genera tipi che implementano il <xref:System.Xml.Serialization.IXmlSerializable> interfaccia. In questo modo viene consentito l'accesso diretto alla rappresentazione XML di questi tipi.  
  
##### <a name="design-considerations"></a>Considerazioni di progettazione  
  
-   Può risultare difficile lavorare direttamente con la rappresentazione XML con tipizzazione debole, Si consiglia di utilizzare un motore di serializzazione alternativo, ad esempio il <xref:System.Xml.Serialization.XmlSerializer>, per lavorare con schemi non compatibili con i dati contratti in una modalità fortemente tipizzata. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Utilizzo della classe XmlSerializer](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md).  
  
-   Alcuni costrutti dello schema non possono essere importati tramite il <xref:System.Runtime.Serialization.XsdDataContractImporter> anche quando il <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> è impostata su `true`. Anche in questo caso, si consiglia di utilizzare il <xref:System.Xml.Serialization.XmlSerializer> in questi casi.  
  
-   I costrutti dello schema che sono supportati quando <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> è `true` o `false` sono descritti in [riferimento dello Schema del contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md).  
  
-   Per lo schema generato <xref:System.Xml.Serialization.IXmlSerializable> tipi non conservano la fedeltà quando vengono importati ed esportati. In altre parole, se si esporta lo schema dai tipi generati e lo si importa come classi, non si ottiene lo schema originale.  
  
 È possibile combinare il <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> con il <xref:System.ServiceModel.Description.ServiceContractGenerator.ReferencedTypes%2A> opzione descritta in precedenza. Per i tipi che devono essere generati come <xref:System.Xml.Serialization.IXmlSerializable> implementazioni, il controllo strutturale viene ignorato quando si utilizza il <xref:System.ServiceModel.Description.ServiceContractGenerator.ReferencedTypes%2A> funzionalità.  
  
 Il <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> opzione corrisponde al **/importXmlTypes** dello strumento Svcutil.exe.  
  
##### <a name="working-with-generated-ixmlserializable-types"></a>Utilizzo dei tipi IXmlSerializable generati  
 Generato `IXmlSerializable` tipi contengono un campo privato denominato "nodesField" che restituisce una matrice di <xref:System.Xml.XmlNode> oggetti. Quando si deserializza un'istanza di questo tipo, è possibile accedere ai dati XML direttamente tramite questo campo usando il modello DOM XML. Quando si serializza un'istanza di questo tipo, è possibile impostare questo campo sui dati XML desiderati e verrà serializzato.  
  
 Questa operazione viene eseguita tramite l'implementazione dell'interfaccia `IXmlSerializable`. Nell'oggetto generato `IXmlSerializable` tipo, il <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> implementazione chiama il <xref:System.Runtime.Serialization.XmlSerializableServices.ReadNodes%2A> metodo il <xref:System.Runtime.Serialization.XmlSerializableServices> (classe). Il metodo è un metodo helper che converte il codice XML fornito tramite un <xref:System.Xml.XmlReader> a una matrice di <xref:System.Xml.XmlNode> oggetti. Il <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> implementazione esegue l'operazione inversa e converte la matrice di `XmlNode` oggetti in una sequenza di <xref:System.Xml.XmlWriter> chiamate. Ciò avviene utilizzando il <xref:System.Runtime.Serialization.XmlSerializableServices.WriteNodes%2A> metodo.  
  
 È possibile eseguire il processo di esportazione dello schema sulle classi `IXmlSerializable` generate. Come illustrato in precedenza, non è possibile ottenere lo schema originale. Si otterrà invece il tipo XSD standard "anyType" che è un elemento jolly per qualsiasi tipo XSD.  
  
 Questa operazione viene eseguita applicando il <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> attributo generato `IXmlSerializable` classi e specificando un metodo che chiama il <xref:System.Runtime.Serialization.XmlSerializableServices.AddDefaultSchema%2A> per generare il tipo "anyType".  
  
> [!NOTE]
>  Il <xref:System.Runtime.Serialization.XmlSerializableServices> tipo esiste esclusivamente per supportare questa particolare funzionalità. Non è consigliabile usarlo per qualsiasi altro scopo.  
  
#### <a name="import-options-advanced-options"></a>Opzioni di importazione: opzioni avanzate  
 Di seguito sono elencate le opzioni importazione avanzate:  
  
-   <xref:System.Runtime.Serialization.ImportOptions.CodeProvider%2A> proprietà. Specificare il <xref:System.CodeDom.Compiler.CodeDomProvider> da utilizzare per generare il codice per le classi generate. Il meccanismo di importazione tenta di evitare le funzionalità che la <xref:System.CodeDom.Compiler.CodeDomProvider> non supporta. Ad esempio, il linguaggio di J# non supporta generics. Se si specifica il provider di codice j# in questa proprietà, nessuno tipo generico viene generato nell'utilità di importazione <xref:System.CodeDom.CodeCompileUnit>. Se il <xref:System.Runtime.Serialization.ImportOptions.CodeProvider%2A> non è impostata, il set completo di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] funzionalità viene utilizzato senza alcuna restrizione.  
  
-   <xref:System.Runtime.Serialization.ImportOptions.DataContractSurrogate%2A> proprietà. Un <xref:System.Runtime.Serialization.IDataContractSurrogate> implementazione può essere specificata con questa proprietà. Il <xref:System.Runtime.Serialization.IDataContractSurrogate> consente di personalizzare il processo di importazione. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Surrogati del contratto dati](../../../../docs/framework/wcf/extending/data-contract-surrogates.md). Per impostazione predefinita, non viene usato alcun surrogato.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Runtime.Serialization.XsdDataContractImporter>   
 <xref:System.Runtime.Serialization.XsdDataContractExporter>   
 <xref:System.Runtime.Serialization.ImportOptions>   
 [Riferimento allo Schema di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)   
 [Surrogati del contratto dati](../../../../docs/framework/wcf/extending/data-contract-surrogates.md)   
 [Esportazione e importazione dello schema](../../../../docs/framework/wcf/feature-details/schema-import-and-export.md)   
 [Esportazione di schemi dalle classi](../../../../docs/framework/wcf/feature-details/exporting-schemas-from-classes.md)   
 [Riferimento allo Schema di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)