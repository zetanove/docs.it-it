---
title: "Tipi di raccolta nei contratti dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "tipi di raccolta [WCF], contratti dati"
  - "contratti dati [WCF], tipi di raccolta"
  - "tipi di raccolta [WCF]"
ms.assetid: 9b45b28e-0a82-4ea3-8c33-ec0094aff9d5
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Tipi di raccolta nei contratti dati
Una *raccolta* costituisce un elenco di elementi di un certo tipo. In [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] tali elenchi possono essere rappresentati mediante matrici o una varietà di altri tipi \(elenco generico, <xref:System.ComponentModel.BindingList%601> generico, <xref:System.Collections.Specialized.StringCollection> o <xref:System.Collections.ArrayList>\). Una raccolta, ad esempio, può contenere un elenco di indirizzi per un determinato cliente. Queste raccolte vengono denominate *raccolte di elenchi*, indipendentemente dal tipo effettivo.  
  
 Esiste una forma speciale di raccolta che rappresenta un'associazione tra un elemento \(la "chiave"\) e un altro elemento \(il "valore"\). In [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] questa raccolta è rappresentata da tipi quali <xref:System.Collections.Hashtable> e il dizionario generico. Una raccolta di associazioni, ad esempio, può eseguire il mapping di una città \(la "chiave"\) alla relativa popolazione \(il "valore"\) Queste raccolte vengono denominate *raccolte di dizionario*, indipendentemente dal tipo effettivo.  
  
 Le raccolte ricevono un trattamento speciale nel modello del contratto dati.  
  
 I tipi che implementano l'interfaccia <xref:System.Collections.IEnumerable>, tra cui matrici e raccolte generiche, vengono riconosciuti come raccolte. Di questi, i tipi che implementano l'interfaccia <xref:System.Collections.IDictionary> o l'interfaccia <xref:System.Collections.Generic.IDictionary%602> generica sono raccolte di dizionario mentre tutti gli altri sono raccolte di elenco.  
  
 Nelle sezioni seguenti vengono descritti dettagliatamente gli ulteriori requisiti relativi ai tipi di raccolte, ad esempio la presenza di un metodo denominato `Add` e di un costruttore predefinito. La presenza di questi requisiti garantisce che i tipi di raccolta possano essere serializzati e deserializzati e implica inoltre che alcune raccolte non sono supportate direttamente, ad esempio l'oggetto <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> generico \(perché non dispone di un costruttore predefinito\). Per informazioni su come evitare queste restrizioni, tuttavia, vedere la sezione "Utilizzo di tipi di interfacce di raccolta e raccolte di sola lettura" più avanti in questo argomento.  
  
 I tipi contenuti nelle raccolte devono essere tipi di contratto dati o devono poter essere serializzati in altro modo.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Tipi supportati dal serializzatore dei contratti dati](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] distinzione tra raccolta valida e raccolta non valida, nonché sulla modalità di serializzazione delle raccolte, vedere le informazioni sulla serializzazione delle raccolte nella sezione "Regole avanzate di inserimento in raccolte" di questo argomento.  
  
## Raccolte intercambiabili  
 Si suppone che tutte le raccolte di elenco dello stesso tipo dispongano dello stesso contratto dati \(a meno che non vengano personalizzate con l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute>, come viene descritto più avanti in questo argomento\). Pertanto, ad esempio, i contratti dati seguenti sono equivalenti.  
  
 [!code-csharp[c_collection_types_in_data_contracts#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#0)]
 [!code-vb[c_collection_types_in_data_contracts#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#0)]  
  
 Entrambi i contratti dati generano XML simile al codice seguente.  
  
```  
<PurchaseOrder>  
    <customerName>...</customerName>  
    <items>  
        <Item>...</Item>  
        <Item>...</Item>  
        <Item>...</Item>  
        ...  
    </items>  
    <comments>  
        <string>...</string>  
        <string>...</string>  
        <string>...</string>  
        ...  
    </comments>  
</PurchaseOrder>  
```  
  
 L'intercambiabilità delle raccolte consente di utilizzare, ad esempio, un tipo di raccolta ottimizzato per le prestazioni nel server e un tipo di raccolta progettato per essere associato ai componenti dell'interfaccia utente nel client.  
  
 Come per le raccolte di elenco, si suppone che tutte le raccolte di dizionario con lo stesso tipo di chiave e valore dispongano dello stesso contratto dati \(a meno che non vengano personalizzate con l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute>\).  
  
 Ai fini dell'equivalenza delle raccolte vale solo il tipo di contratto dati, non i tipi .NET. Una raccolta Type1 è considerata equivalente a una raccolta Type2 se Type1 e Type2 presentano contratti dati equivalenti.  
  
 Si suppone che raccolte non generiche dispongano dello stesso contratto dati di raccolte generiche di tipo `Object`. Ad esempio, i contratti dati per <xref:System.Collections.ArrayList> e per un oggetto <xref:System.Collections.Generic.List%601> generico di `Object` sono uguali.  
  
## Utilizzo di tipi di interfacce di raccolta e raccolte di sola lettura  
 Anche per i tipi di interfaccia di raccolta \(<xref:System.Collections.IEnumerable>, <xref:System.Collections.IDictionary>, <xref:System.Collections.Generic.IDictionary%602> generico o interfacce che derivano da queste interfacce\) si suppone che dispongano di contratti dati di raccolta, equivalenti a contratti dati di raccolta per tipi di raccolta effettivi. È dunque possibile dichiarare il tipo serializzato come tipo di interfaccia di raccolta e i risultati sono gli stessi che verrebbero ottenuti se fosse utilizzato un tipo di raccolta effettivo. I contratti dati seguenti, ad esempio, sono equivalenti.  
  
 [!code-csharp[c_collection_types_in_data_contracts#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#1)]
 [!code-vb[c_collection_types_in_data_contracts#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#1)]  
  
 Durante la serializzazione, quando il tipo dichiarato è un'interfaccia, il tipo dell'istanza effettivo utilizzato può essere qualsiasi tipo che implementa quell'interfaccia. Le restrizioni discusse in precedenza \(la presenza di un costruttore predefinito e di un metodo `Add`\) non sono applicabili. È ad esempio possibile impostare indirizzi in Customer2 su un'istanza della classe <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> generica di Address, anche se non si può dichiarare direttamente un membro dati di tipo <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> generico.  
  
 Durante la deserializzazione, quando il tipo dichiarato è un'interfaccia, il motore di serializzazione sceglie un tipo che implementi l'interfaccia dichiarata e viene creata un'istanza del tipo. Il meccanismo dei tipi noti \(descritto in [Tipi conosciuti di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)\) non ha alcun effetto in questo caso. La scelta del tipo è incorporata in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Personalizzazione dei tipi di raccolta  
 È possibile personalizzare i tipi di raccolta utilizzando l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute>, che presenta molti utilizzi.  
  
 Si noti che la personalizzazione dei tipi di raccolta compromette l'intercambiabilità delle raccolte, pertanto si consiglia in genere di evitare l'applicazione di questo attributo quando possibile.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] questo problema, vedere la sezione "Regole avanzate di inserimento in raccolte" più avanti in questo argomento.  
  
### Denominazione del contratto dati della raccolta  
 Le regole per la denominazione dei tipi di raccolta sono simili a quelle per la denominazione dei tipi di contratto dati normali, come viene descritto in [Nomi di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-names.md), ad eccezione di alcune importanti differenze:  
  
-   Per personalizzare il nome viene utilizzato l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute> anziché l'attributo <xref:System.Runtime.Serialization.DataContractAttribute>. Anche l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute> dispone delle proprietà `Name` e `Namespace`.  
  
-   Quando l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute> non viene applicato, il nome e lo spazio dei nomi predefiniti per i tipi di raccolta dipendono dai nomi e dagli spazi dei nomi dei tipi contenuti nella raccolta. Non vengono influenzati dal nome e dallo spazio dei nomi del tipo di raccolta stesso. Per un esempio, vedere i tipi seguenti.  
  
    ```  
    public CustomerList1 : Collection<string> {}  
    public StringList1 : Collection<string> {}  
    ```  
  
 Il nome del contratto dati di entrambi i tipi è "ArrayOfstring" e non "CustomerList1" o "StringList1". Ciò significa che eseguendo la serializzazione di uno qualsiasi di questi tipi a livello di radice si ottiene codice XML simile al seguente:  
  
```  
<ArrayOfstring>  
    <string>...</string>  
    <string>...</string>  
    <string>...</string>  
    ...  
</ArrayOfstring>  
```  
  
 Questa regola di denominazione è stata scelta per avere la certezza che i tipi non personalizzati che rappresentano un elenco di stringhe abbiano lo stesso contratto dati e la stessa rappresentazione XML. In questo modo l'intercambiabilità delle raccolte è possibile. Nell'esempio CustomerList1 e StringList1 sono completamente intercambiabili.  
  
 Quando viene applicato l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute>, tuttavia, la raccolta diventa un contratto dati di una raccolta personalizzata, anche se nell'attributo non è impostata alcuna proprietà. Il nome e lo spazio dei nomi del contratto dati della raccolta dipendono quindi dal tipo di raccolta stesso. Per un esempio, vedere il tipo seguente.  
  
 [!code-csharp[c_collection_types_in_data_contracts#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#2)]
 [!code-vb[c_collection_types_in_data_contracts#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#2)]  
  
 Quando viene serializzato, l'XML risultante è simile al codice seguente.  
  
```  
<CustomerList2>  
    <string>...</string>  
    <string>...</string>  
    <string>...</string>  
    ...  
</CustomerList2>  
```  
  
 Si noti che questo codice non è più equivalente alla rappresentazione XML dei tipi non personalizzati.  
  
-   È quindi possibile utilizzare le proprietà `Name` e `Namespace` per personalizzare ulteriormente la denominazione. Fare riferimento alla classe seguente.  
  
     [!code-csharp[c_collection_types_in_data_contracts#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#3)]
     [!code-vb[c_collection_types_in_data_contracts#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#3)]  
  
 L'XML risultante è simile al codice seguente.  
  
```  
<cust_list>  
    <string>...</string>  
    <string>...</string>  
    <string>...</string>  
    ...  
</cust_list>  
```  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la sezione "Regole avanzate di inserimento in raccolte" più avanti in questo argomento.  
  
### Personalizzazione del nome dell'elemento ripetuto nelle raccolte di elenco  
 Le raccolte di elenco contengono voci ripetute. Normalmente ogni voce ripetuta è rappresentata come un elemento denominato secondo il nome del contratto dati del tipo contenuto nella raccolta.  
  
 Negli esempi `CustomerList`, le raccolte contengono stringhe. Poiché il nome del contratto dati per il tipo primitivo della stringa è "string", l'elemento ripetuto è "\<string\>".  
  
 Utilizzando la proprietà <xref:System.Runtime.Serialization.CollectionDataContractAttribute.ItemName%2A> nell'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute>, tuttavia, questo nome di elemento ripetuto può essere personalizzato. Per un esempio, vedere il tipo seguente.  
  
 [!code-csharp[c_collection_types_in_data_contracts#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#4)]
 [!code-vb[c_collection_types_in_data_contracts#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#4)]  
  
 L'XML risultante è simile al codice seguente.  
  
```  
<CustomerList4>  
    <customer>...</ customer>  
    <customer>...</customer>  
    <customer>...</customer>  
    ...  
</CustomerList4>  
```  
  
 Lo spazio dei nomi dell'elemento ripetuto è sempre uguale allo spazio dei nomi del contratto dati della raccolta, che può essere personalizzato tramite la proprietà `Namespace`, come descritto in precedenza.  
  
### Personalizzazione di raccolte di dizionario  
 Le raccolte di dizionario sono essenzialmente elenchi di voci, in cui ogni voce presenta una chiave seguita da un valore. Come per gli elenchi normali, è possibile modificare il nome di elemento corrispondente all'elemento ripetuto utilizzando la proprietà <xref:System.Runtime.Serialization.CollectionDataContractAttribute.ItemName%2A>.  
  
 È inoltre possibile modificare i nomi di elemento che rappresentano la chiave e il valore utilizzando le proprietà <xref:System.Runtime.Serialization.CollectionDataContractAttribute.KeyName%2A> e <xref:System.Runtime.Serialization.CollectionDataContractAttribute.ValueName%2A>. Gli spazi dei nomi di questi elementi sono gli stessi dello spazio dei nomi del contratto dati della raccolta.  
  
 Per un esempio, vedere il tipo seguente.  
  
 [!code-csharp[c_collection_types_in_data_contracts#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#5)]
 [!code-vb[c_collection_types_in_data_contracts#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#5)]  
  
 Quando viene serializzato, l'XML risultante è simile al codice seguente.  
  
```  
<CountriesOrRegionsWithCapitals>  
    <entry>  
        <countryorregion>USA</countryorregion>  
        <capital>Washington</capital>  
    </entry>  
    <entry>  
        <countryorregion>France</countryorregion>  
        <capital>Paris</capital>  
    </entry>  
    ...  
</CountriesOrRegionsWithCapitals>  
```  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] raccolte di dizionario, vedere la sezione "Regole avanzate di inserimento in raccolte" più avanti in questo argomento.  
  
## Raccolte e tipi noti  
 Non è necessario aggiungere tipi di raccolta a tipi noti quando vengono utilizzati polimorficamente in luogo di altre raccolte o di altre interfacce di raccolta. Se ad esempio si dichiara un membro dati di tipo <xref:System.Collections.IEnumerable> e lo si utilizza per inviare un'istanza di <xref:System.Collections.ArrayList>, non è necessario aggiungere <xref:System.Collections.ArrayList> a tipi noti.  
  
 Quando si utilizzano raccolte in modo polimorfico al posto di tipi diversi da raccolte, è necessario aggiungerli ai tipi noti. Ad esempio, se si dichiara un membro dati di tipo `Object` e lo si utilizza per inviare un'istanza di <xref:System.Collections.ArrayList>, aggiungere <xref:System.Collections.ArrayList> ai tipi noti.  
  
 Ciò non consente di serializzare eventuali raccolte equivalenti polimorficamente. Ad esempio, quando si aggiunge <xref:System.Collections.ArrayList> all'elenco di tipi noti nell'esempio precedente, non è consentito assegnare la classe `Array of Object`, anche se presenta un contratto dati equivalente. Il comportamento normale di tipi noti nel caso della serializzazione per tipi diversi da raccolte non è diverso, ma è particolarmente importante essere a conoscenza di tale funzionamento nel caso delle raccolte perché capita frequentemente che si equivalgano.  
  
 Durante la serializzazione solo un tipo può essere conosciuto in un determinato ambito per un contratto dati specificato e le raccolte equivalenti presentano tutti gli stessi contratti dati. Nell'esempio precedente, ciò significa che non è possibile aggiungere sia <xref:System.Collections.ArrayList> sia `Array of Object` ai tipi noti nello stesso ambito. Anche questo caso è equivalente al comportamento dei tipi noti per tipi diversi da raccolte ma è particolarmente importante esserne a conoscenza per quanto riguarda le raccolte.  
  
 È inoltre possibile che i tipi noti siano necessari come contenuto di raccolte. Se un elemento <xref:System.Collections.ArrayList>, ad esempio, contiene effettivamente istanze di `Type1` e `Type2`, entrambi questi tipi devono essere aggiunti ai tipi noti.  
  
 Nell'esempio seguente viene illustrato un oggetto grafico costruito correttamente in cui sono utilizzati raccolte e tipi noti. L'esempio è stato studiato appositamente in quanto in un'applicazione effettiva i membri dati seguenti non verrebbero normalmente definiti `Object` e quindi non si verificherebbero problemi di polimorfismo\/tipi noti.  
  
 [!code-csharp[c_collection_types_in_data_contracts#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#6)]
 [!code-vb[c_collection_types_in_data_contracts#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#6)]  
  
 In fase di deserializzazione, se il tipo dichiarato è un tipo di raccolta, ne viene creata un'istanza indipendentemente dal tipo effettivamente inviato. Se il tipo dichiarato è un'interfaccia di raccolta, il deserializzatore sceglie un tipo di cui creare un'istanza senza considerare i tipi noti.  
  
 In fase di deserializzazione, inoltre, se il tipo dichiarato non è un tipo di raccolta ma viene inviato un tipo di raccolta, dall'elenco dei tipi noti viene selezionato un tipo di raccolta corrispondente. In fase di deserializzazione è possibile aggiungere tipi di interfaccia di raccolta all'elenco di tipi noti. Anche in questo caso il motore di deserializzazione sceglie un tipo di cui creare un'istanza.  
  
## Raccolte e classe NetDataContractSerializer  
 Quando si utilizza la classe <xref:System.Runtime.Serialization.NetDataContractSerializer>, i tipi di raccolta non personalizzati \(senza l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute>\) che non sono matrici perdono il relativo significato speciale.  
  
 Tipi di raccolta non personalizzati contrassegnati con l'attributo <xref:System.SerializableAttribute> possono comunque essere serializzati dalla classe <xref:System.Runtime.Serialization.NetDataContractSerializer> secondo l'attributo <xref:System.SerializableAttribute> o le regole dell'interfaccia <xref:System.Runtime.Serialization.ISerializable>.  
  
 Tipi di raccolta personalizzati, interfacce di raccolta e matrici vengono comunque considerati raccolte, anche quando la classe <xref:System.Runtime.Serialization.NetDataContractSerializer> è in uso.  
  
## Raccolte e schema  
 Tutte le raccolte equivalenti presentano la stessa rappresentazione nello schema XSD \(XML Schema Definition Language\). Per questo motivo in genere non si ottiene, nel codice client generato, lo stesso tipo di raccolta del codice generato nel server. Il server, ad esempio, può utilizzare un contratto dati con <xref:System.Collections.Generic.List%601> generico del membro dati Integer ma nel codice client generato lo stesso membro dati può diventare una matrice di numeri interi.  
  
 Le raccolte di dizionario sono contrassegnate con un'annotazione dello schema specifica di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che indica che si tratta di dizionari. In caso contrario, non sarebbero distinguibili da semplici elenchi contenenti voci con una chiave e un valore. Per una descrizione più precisa del modo in cui le raccolte vengono rappresentate nello schema del contratto dati, vedere [Riferimento allo schema del contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md).  
  
 Per impostazione predefinita i tipi non vengono generati per raccolte non personalizzate nel codice importato. I membri dati di tipi di raccolta di elenco sono importati come matrici e i membri dati di tipi di raccolta di dizionario sono importati come dizionario generico.  
  
 Per le raccolte personalizzate, tuttavia, vengono generati tipi separati, contrassegnati con l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute>. \(il tipo di raccolta personalizzato contenuto nello schema è un tipo che non utilizza spazio dei nomi, nome, elemento ripetuto o nomi di elementi chiave\/valore predefiniti\). Si tratta di tipi vuoti che derivano da <xref:System.Collections.Generic.List%601> generico per i tipi di elenco e dal dizionario generico per i tipi di dizionario.  
  
 È ad esempio possibile che nel server siano presenti i tipi seguenti.  
  
 [!code-csharp[c_collection_types_in_data_contracts#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#7)]
 [!code-vb[c_collection_types_in_data_contracts#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#7)]  
  
 Quando lo schema viene esportato per poi essere nuovamente importato, il codice client generato è simile al seguente \(per facilità di lettura vengono mostrati i campi anziché le proprietà\):  
  
 [!code-csharp[c_collection_types_in_data_contracts#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#8)]
 [!code-vb[c_collection_types_in_data_contracts#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#8)]  
  
 È consigliabile utilizzare tipi diversi nel codice generato anziché i tipi predefiniti. È ad esempio opportuno utilizzare <xref:System.ComponentModel.BindingList%601> generico anziché matrici normali dei membri dati per semplificarne l'associazione ai componenti dell'interfaccia utente.  
  
 Per scegliere i tipi di raccolta da generare, durante l'importazione dello schema passare un elenco dei tipi di raccolta che si desidera utilizzare nella proprietà <xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A> dell'oggetto <xref:System.Runtime.Serialization.ImportOptions>. Questi tipi sono chiamati *tipi di raccolta a cui viene fatto riferimento*.  
  
 Quando si fa riferimento a tipi generici, deve trattarsi di generics completamente aperti o di generics completamente chiusi.  
  
> [!NOTE]
>  Quando si usa lo strumento Svcutil.exe, questo riferimento può essere eseguito usando l'opzione della riga di comando **\/collectionType** \(forma breve: **\/ct**\). È importante ricordare che è anche necessario specificare l'assembly per i tipi di raccolta a cui viene fatto riferimento usando l'opzione **\/reference** \(forma breve: **\/r**\). Se il tipo è generico, deve essere seguito da una virgoletta inversa e dal numero di parametri generici. La virgoletta inversa \(\`\) non deve essere confusa con il carattere della virgoletta singola \('\). È possibile specificare più tipi di raccolta a cui viene fatto riferimento usando l'opzione **\/collectionType** più di una volta.  
  
 Ad esempio, per fare in modo che tutti gli elenchi vengano importati come oggetto <xref:System.Collections.Generic.List%601> generico.  
  
```  
svcutil.exe MyService.wsdl MyServiceSchema.xsd /r:C:\full_path_to_system_dll\System.dll /ct:System.Collections.Generic.List`1  
  
```  
  
 Quando si importa una raccolta, l'elenco di tipi di raccolta a cui si fa riferimento viene analizzato e viene utilizzata la raccolta con la migliore corrispondenza trovata, come tipo di membro dati \(per le raccolte non personalizzate\) o come tipo di base per la derivazione \(per le raccolte personalizzate\). I dizionari vengono associati solo a dizionari mentre gli elenchi a elenchi.  
  
 Se ad esempio si aggiungono la classe <xref:System.ComponentModel.BindingList%601> generica e la classe <xref:System.Collections.Hashtable> all'elenco di tipi a cui viene fatto riferimento, il codice client generato per l'esempio precedente sarà simile al seguente:  
  
 [!code-csharp[c_collection_types_in_data_contracts#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#9)]
 [!code-vb[c_collection_types_in_data_contracts#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#9)]  
  
 È possibile specificare i tipi di interfaccia di raccolta nell'ambito dei tipi di raccolta a cui si fa riferimento, ma non è possibile specificare tipi di raccolta non validi \(ad esempio tipi senza il metodo `Add` o il costruttore pubblico\).  
  
 Un generico chiuso è considerato la corrispondenza migliore \(i tipi non generici sono considerati equivalenti ai generics chiusi di `Object`\). Se ad esempio i tipi <xref:System.Collections.Generic.List%601> generico di <xref:System.DateTime>, <xref:System.ComponentModel.BindingList%601> generico \(generico aperto\) e <xref:System.Collections.ArrayList> sono tipi di raccolta a cui viene fatto riferimento, viene generato il codice seguente:  
  
 [!code-csharp[c_collection_types_in_data_contracts#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#10)]
 [!code-vb[c_collection_types_in_data_contracts#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#10)]  
  
 Per le raccolte di elenchi, sono supportati solo i casi illustrati nella tabella seguente:  
  
|Tipo a cui viene fatto riferimento|Interfaccia implementata dal tipo a cui viene fatto riferimento|Esempio|Tipo trattato come:|  
|----------------------------------------|---------------------------------------------------------------------|-------------|-------------------------|  
|Non generico o generico chiuso \(qualsiasi numero di parametri\)|Non generico|`MyType : IList`<br /><br /> o<br /><br /> `MyType<T> : IList`<br /><br /> dove T\= `int`|Generico chiuso di `Object` \(ad esempio, `IList<object>`\)|  
|Non generico o generico chiuso \(qualsiasi numero di parametri che non corrispondono necessariamente al tipo di raccolta\)|Generico chiuso|`MyType : IList<string>`<br /><br /> o<br /><br /> `MyType<T> : IList<string>` dove T\=`int`|Generico chiuso \(ad esempio `IList<string>`\)|  
|Generico chiuso con qualsiasi numero di parametri|Generico aperto che utilizza qualsiasi parametro del tipo|`MyType<T,U,V> : IList<U>`<br /><br /> dove T\=`int`, U\=`string`, V\=`bool`|Generico chiuso \(ad esempio `IList<string>`\)|  
|Generico aperto con un parametro|Generico aperto che utilizza il parametro del tipo|`MyType<T> : IList<T>`, T è aperto|Generico aperto \(ad esempio `IList<T>`\)|  
  
 Se un tipo implementa più di un'interfaccia della raccolta di elenco, vengono applicate le restrizioni seguenti:  
  
-   Se il tipo implementa <xref:System.Collections.Generic.IEnumerable%601> generico \(o le interfacce derivate\) più volte per tipi diversi, non viene considerato un tipo di raccolta a cui fare riferimento valido e viene ignorato. Questa condizione è vera anche se alcune implementazioni non sono valide o utilizzano generics aperti. Un tipo che implementa <xref:System.Collections.Generic.IEnumerable%601> generico di `int` e <xref:System.Collections.Generic.IEnumerable%601> generico di T, ad esempio, non verrebbe mai utilizzato come raccolta a cui si fa riferimento di `int` o di qualsiasi altro tipo, indipendentemente dalla circostanza che il tipo abbia un metodo `Add` che accetta `int` o un metodo `Add` che accetta un parametro di tipo T o entrambi.  
  
-   Se il tipo implementa un'interfaccia di raccolta generica oltre a <xref:System.Collections.IList>, non viene mai utilizzato come tipo di raccolta a cui si fa riferimento, a meno che l'interfaccia di raccolta generica non sia una generica chiusa di tipo <xref:System.Object>.  
  
 Per le raccolte di dizionario, sono supportati solo i casi illustrati nella tabella seguente:  
  
|Tipo a cui viene fatto riferimento|Interfaccia implementata dal tipo a cui viene fatto riferimento|Esempio|Tipo trattato come|  
|----------------------------------------|---------------------------------------------------------------------|-------------|------------------------|  
|Non generico o generico chiuso \(qualsiasi numero di parametri\)|<xref:System.Collections.IDictionary>|`MyType : IDictionary`<br /><br /> o<br /><br /> `MyType<T> : IDictionary` dove T\=`int`|Generico chiuso `IDictionary<object,object>`|  
|Generico chiuso \(qualsiasi numero di parametri\)|<xref:System.Collections.Generic.IDictionary%602>, chiuso|`MyType<T> : IDictionary\<string, bool>` dove T\=`int`|Generico chiuso \(ad esempio `IDIctionary\<string,bool>`\)|  
|Generico chiuso \(qualsiasi numero di parametri\)|<xref:System.Collections.Generic.IDictionary%602> generico, la chiave o il valore è chiuso, l'altro è aperto e utilizza uno dei parametri del tipo|`MyType\<T,U,V> : IDictionary\<string,V>` dove T\=`int`, U\=`float`, V\=`bool`<br /><br /> o<br /><br /> `MyType<Z> : IDictionary\<Z,bool>` dove Z\=`string`|Generico chiuso \(ad esempio `IDictionary\<string,bool>`\)|  
|Generico chiuso \(qualsiasi numero di parametri\)|<xref:System.Collections.Generic.IDictionary%602> generico, chiave e valore sono aperti e ognuno utilizza uno dei parametri del tipo|`MyType\<T,U,V> : IDictionary\<V,U>` dove T\=`int`, U\=`bool`, V\=`string`|Generico chiuso \(ad esempio `IDictionary\<string,bool>`\)|  
|Generico aperto \(due parametri\)|<xref:System.Collections.Generic.IDictionary%602> generico, aperto, utilizza entrambi i parametri generici del tipo nell'ordine in cui sono visualizzati.|`MyType\<K,V> : IDictionary\<K,V>`, K e V entrambi aperti|Generico aperto \(ad esempio `IDictionary\<K,V>`\)|  
  
 Se il tipo implementa sia <xref:System.Collections.IDictionary> che <xref:System.Collections.Generic.IDictionary%602> generico, solo <xref:System.Collections.Generic.IDictionary%602> generico viene considerato.  
  
 Il riferimento a tipi generici parziali non è supportato.  
  
 I duplicati non sono consentiti, ad esempio non è possibile aggiungere l'oggetto <xref:System.Collections.Generic.List%601> generico di `Integer` e la raccolta generica di `Integer` a <xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A>, perché ciò renderebbe impossibile stabilire quale utilizzare quando nello schema viene trovato un elenco di valori integer. I duplicati vengono rilevati solo se nello schema esiste un tipo che espone il problema dei duplicati. Se ad esempio lo schema importato non contiene elenchi di numeri interi, è consentito disporre sia di <xref:System.Collections.Generic.List%601> generico di `Integer` che della raccolta generica di `Integer` nella proprietà <xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A>, ma nessuno esercita alcun effetto.  
  
## Regole avanzate di inserimento in raccolte  
  
### Serializzazione delle raccolte  
 Di seguito vengono elencate le regole per la serializzazione delle raccolte:  
  
-   La combinazione di tipi di raccolta \(con raccolte di raccolte\) è consentita. Le matrici di matrici vengono trattate come raccolte di raccolte. Le matrici multidimensionali non sono supportate.  
  
-   Matrici di byte e matrici di <xref:System.Xml.XmlNode> sono tipi speciali di matrici trattati come primitivi, non come raccolte. La serializzazione di una matrice di byte genera un singolo elemento XML contenente un blocco di dati con codifica Base64 anziché un elemento separato per ogni byte.[!INCLUDE[crabout](../../../../includes/crabout-md.md)]l modo in cui viene considerata una matrice di <xref:System.Xml.XmlNode>, vedere [Tipi XML e ADO.NET nei contratti dati](../../../../docs/framework/wcf/feature-details/xml-and-ado-net-types-in-data-contracts.md). Questi tipi speciali, naturalmente, possono fare parte delle raccolte: una matrice di matrice di byte sfocia in più elementi XML, ognuno dei quali contiene un blocco di dati con codifica Base64.  
  
-   Se l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> viene applicato a un tipo di raccolta, il tipo viene trattato come tipo di contratto dati normale, non come una raccolta.  
  
-   Se un tipo di raccolta implementa l'interfaccia <xref:System.Xml.Serialization.IXmlSerializable>, vengono applicate le regole seguenti, dato un tipo `myType:IList<string>, IXmlSerializable`:  
  
    -   Il tipo di dichiarato è `IList<string>`, il tipo è serializzato come elenco.  
  
    -   Il tipo di dichiarato è `myType`, ed è serializzato come `IXmlSerializable`.  
  
    -   Se il tipo dichiarato è `IXmlSerializable`, viene serializzato come `IXmlSerializable`, ma solo se si aggiunge `myType` all'elenco dei tipi noti.  
  
-   Le raccolte vengono serializzate e deserializzate tramite i metodi illustrati nella tabella seguente:  
  
|Il tipo di raccolta implementa|Metodo\/i chiamato\/i durante la serializzazione|Metodo\/i chiamato\/i durante la deserializzazione|  
|------------------------------------|------------------------------------------------------|--------------------------------------------------------|  
|<xref:System.Collections.Generic.IDictionary%602> generico|`get_Keys`, `get_Values`|Add generico|  
|<xref:System.Collections.IDictionary>|`get_Keys`, `get_Values`|`Add`|  
|<xref:System.Collections.Generic.IList%601> generico|Indicizzatore <xref:System.Collections.Generic.IList%601> generico|Add generico|  
|<xref:System.Collections.Generic.ICollection%601> generico|Enumerator|Add generico|  
|<xref:System.Collections.IList>|Indicizzatore <xref:System.Collections.IList>|`Add`|  
|<xref:System.Collections.Generic.IEnumerable%601> generico|`GetEnumerator`|Metodo non statico denominato `Add` che accetta un parametro del tipo appropriato \(il tipo del parametro generico o uno dei tipi di base\). È necessario che tale metodo esista affinché il serializzatore tratti un tipo di raccolta come raccolta sia durante la serializzazione che durante la deserializzazione.|  
|<xref:System.Collections.IEnumerable> \(e di conseguenza <xref:System.Collections.ICollection>, interfaccia derivata\)|`GetEnumerator`|Metodo non statico denominato `Add` che accetta un parametro di tipo `Object`. È necessario che tale metodo esista affinché il serializzatore tratti un tipo di raccolta come raccolta sia durante la serializzazione che durante la deserializzazione.|  
  
 Nella tabella precedente sono elencate le interfacce di raccolta in ordine decrescente di precedenza. Se un tipo implementa sia <xref:System.Collections.IList> che <xref:System.Collections.Generic.IEnumerable%601> generico, ad esempio, la raccolta viene serializzata e deserializzata secondo le regole di <xref:System.Collections.IList>:  
  
-   In fase di deserializzazione, tutte le raccolte vengono deserializzate creando innanzitutto un'istanza del tipo chiamando il costruttore predefinito, che deve essere presente affinché il serializzatore sia in grado di trattare un tipo di raccolta come raccolta durante la serializzazione e la deserializzazione.  
  
-   Se la stessa interfaccia di raccolta generica viene implementata più di una volta \(ad esempio se un tipo implementa sia <xref:System.Collections.Generic.ICollection%601> generica di `Integer` che <xref:System.Collections.Generic.ICollection%601> generica di <xref:System.String>\) e non viene trovata nessuna interfaccia con un livello di precedenza maggiore, la raccolta non viene trattata come raccolta valida.  
  
-   L'attributo <xref:System.SerializableAttribute> può essere applicato ai tipi di raccolta, i quali possono implementare l'interfaccia <xref:System.Runtime.Serialization.ISerializable>. Entrambi vengono ignorati. Se, tuttavia, il tipo non soddisfa pienamente i requisiti del tipo di raccolta \(ad esempio, manca il metodo `Add`\), il tipo non viene considerato un tipo di raccolta, di conseguenza per stabilire se il tipo può essere serializzato, vengono utilizzati l'attributo <xref:System.SerializableAttribute> e l'interfaccia <xref:System.Runtime.Serialization.ISerializable>.  
  
-   L'applicazione dell'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute> a una raccolta per personalizzarlo rimuove il meccanismo di fallback di <xref:System.SerializableAttribute> precedente. Se invece una raccolta personalizzata non soddisfa i requisiti del tipo di raccolta, viene generata un'eccezione <xref:System.Runtime.Serialization.InvalidDataContractException>. Poiché spesso la stringa dell'eccezione contiene informazioni che spiegano il motivo per il quale un determinato tipo non viene considerato una raccolta valida \(nessun metodo `Add`, nessun costruttore predefinito e così via\), risulta utile applicare l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute> a scopo di debug.  
  
### Denominazione di raccolte  
 Di seguito vengono elencate le regole di denominazione delle raccolte:  
  
-   Lo spazio dei nomi predefinito per tutti i contratti dati delle raccolte di dizionario, nonché per contratti dati delle raccolte di elenco contenenti tipi primitivi, è http:\/\/schemas.microsoft.com\/2003\/10\/Serialization\/Arrays, a meno che non venga sottoposto a override utilizzando Namespace. I tipi che eseguono il mapping a tipi XSD incorporati, nonché i tipi `char`, `Timespan` e `Guid`, vengono considerati primitivi a questo scopo.  
  
-   Lo spazio dei nomi predefinito per tipi di raccolta che contengono tipi non primitivi corrisponde allo spazio dei nomi del contratto dati del tipo contenuto nella raccolta, a meno che non venga eseguito l'override utilizzando Namespace.  
  
-   Il nome predefinito per i contratti dati delle raccolte di elenco, a meno che non venga sottoposto a override utilizzando Name, è la stringa "ArrayOf" associata al nome del contratto dati del tipo contenuto nella raccolta. Il nome del contratto dati per un elenco generico di numeri interi è, ad esempio, "ArrayOfint". È importante ricordare che il nome del contratto dati di `Object` è "anyType", quindi il nome del contratto dati di elenchi non generici come <xref:System.Collections.ArrayList> è "ArrayOfanyType".  
  
 Il nome predefinito per i contratti dati delle raccolte di dizionario, a meno che non venga sottoposto a override utilizzando `Name`, è la stringa "ArrayOfKeyValueOf" associata al nome del contratto dati del tipo di chiave seguito dal nome del contratto dati del tipo di valore. Il nome del contratto dati per un dizionario generico di stringa e numero intero, ad esempio, è "ArrayOfKeyValueOfstringint". Inoltre, se il tipo di chiave o il tipo di valore non sono tipi primitivi, un hash di spazio dei nomi degli spazi dei nomi del contratto dati dei tipi di chiave e valore viene aggiunto al nome.[!INCLUDE[crabout](../../../../includes/crabout-md.md)]gli hash di spazio dei nomi, vedere [Nomi di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-names.md).  
  
 Ogni contratto dati della raccolta di dizionario dispone di un contratto dati complementare che rappresenta una voce del dizionario. Il nome è lo stesso del contratto dati del dizionario, ad eccezione del prefisso "ArrayOf", e lo spazio dei nomi corrisponde a quello del contratto dati del dizionario. Per il contratto dati del dizionario "ArrayOfKeyValueOfstringint", ad esempio, il contratto dati "KeyValueofstringint" rappresenta una voce del dizionario. È possibile personalizzare il nome di questo contratto dati utilizzando la proprietà `ItemName`, come viene descritto nella prossima sezione.  
  
 Le regole di denominazione dei tipi generici, descritte in [Nomi di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-names.md), si applicano completamente ai tipi di raccolta, ovvero è possibile usare parentesi graffe all'interno di Name per indicare parametri di tipi generici. Tuttavia, i numeri tra parentesi graffe si riferiscono a parametri generici e non a tipi contenuti nella raccolta.  
  
## Personalizzazione di raccolte  
 Gli utilizzi seguenti dell'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute> non sono consentiti e generano un'eccezione <xref:System.Runtime.Serialization.InvalidDataContractException>:  
  
-   Applicare l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> a un tipo al quale è stato applicato l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute> oppure a uno dei tipi derivati.  
  
-   Applicare l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute> a un tipo che implementa l'interfaccia <xref:System.Xml.Serialization.IXmlSerializable>.  
  
-   Applicare l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute> a un tipo diverso da una raccolta.  
  
-   Tentare di impostare <xref:System.Runtime.Serialization.CollectionDataContractAttribute.KeyName%2A> o <xref:System.Runtime.Serialization.CollectionDataContractAttribute.ValueName%2A> su un attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute> applicato a un tipo diverso da un dizionario.  
  
### Regole del polimorfismo  
 Come indicato in precedenza, la personalizzazione delle raccolte mediante l'attributo <xref:System.Runtime.Serialization.CollectionDataContractAttribute> può interferire con l'intercambiabilità delle stesse. Due tipi di raccolta personalizzati possono essere considerati equivalenti solo se il nome, lo spazio dei nomi, il nome dell'elemento nonché il nome di chiave e valore \(se raccolte di dizionari\) corrispondono.  
  
 A causa delle personalizzazioni, è possibile utilizzare inavvertitamente il contratto dati di una raccolta laddove ne è previsto un altro. Questa evenienza deve essere evitata. Vedere i tipi seguenti.  
  
 [!code-csharp[c_collection_types_in_data_contracts#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#11)]
 [!code-vb[c_collection_types_in_data_contracts#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#11)]  
  
 In questo caso, un'istanza di `Marks1` può essere assegnata a `testMarks`.`Marks2`, tuttavia, non deve essere utilizzato poiché il relativo contratto dati non viene considerato equivalente al contratto dati `IList<int>`. Il nome del contratto dati è "Marks2" e non "ArrayOfint" e il nome dell'elemento ripetuto è "\<mark\>" e non "\<int\>".  
  
 Per l'assegnazione polimorfica delle raccolte vengono applicate le regole riportate nella tabella seguente:  
  
|Tipo dichiarato|Assegnazione di una raccolta non personalizzata|Assegnazione di una raccolta personalizzata|  
|---------------------|-----------------------------------------------------|-------------------------------------------------|  
|Oggetto|Il nome del contratto è serializzato.|Il nome del contratto è serializzato.<br /><br /> Viene utilizzata la personalizzazione.|  
|Interfaccia di raccolta|Il nome del contratto non è serializzato.|Il nome del contratto non è serializzato.<br /><br /> La personalizzazione non viene utilizzata.\*|  
|Raccolta non personalizzata|Il nome del contratto non è serializzato.|Il nome del contratto è serializzato.<br /><br /> Viene utilizzata la personalizzazione.\*\*|  
|Raccolta personalizzata|Il nome del contratto è serializzato. La personalizzazione non viene utilizzata.\*\*|Il nome del contratto è serializzato.<br /><br /> Viene utilizzata la personalizzazione del tipo assegnato.\*\*|  
  
 \*Con la classe <xref:System.Runtime.Serialization.NetDataContractSerializer>, in questo caso viene utilizzata la personalizzazione. La classe <xref:System.Runtime.Serialization.NetDataContractSerializer> serializza inoltre il nome effettivo del tipo in questo caso, quindi la deserializzazione viene eseguita in base alle previsioni.  
  
 \*\*Questi casi determinano istanze non valide per lo schema, quindi devono essere evitati.  
  
 Nei casi in cui il nome del contratto è serializzato, il tipo di raccolta assegnato deve risultare nell'elenco dei tipi noti. È anche vero il contrario: nei casi in cui il nome non è serializzato, l'aggiunta del tipo all'elenco dei tipi noti non è necessaria.  
  
 Una matrice di un tipo derivato può essere assegnata a una matrice di un tipo di base. In questo caso il nome del contratto per il tipo derivato viene serializzato per ogni elemento ripetuto. Se ad esempio un tipo `Book` deriva dal tipo `LibraryItem`, è possibile assegnare una matrice di `Book` a una matrice di `LibraryItem`. Quanto esposto sopra non vale per altri tipi di raccolta. Ad esempio, non è possibile assegnare un oggetto `Generic List of Book` a un oggetto `Generic List of LibraryItem`. È tuttavia possibile assegnare un `Generic List of LibraryItem` contenente istanze di `Book`. In entrambi i casi, matrice e non matrice, `Book` deve essere presente nell'elenco dei tipi noti.  
  
## Raccolte e conservazione dei riferimenti all'oggetto  
 Quando un serializzatore opera in una modalità che consente di preservare i riferimenti all'oggetto, la conservazione dei riferimenti all'oggetto si applica anche alle raccolte. In particolare, l'identità dell'oggetto viene conservata sia per raccolte intere che per elementi singoli contenuti nelle raccolte. Per i dizionari, l'identità dell'oggetto viene conservata sia per oggetti coppia di chiave e valore che per oggetti chiave e valore singoli.  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.CollectionDataContractAttribute>