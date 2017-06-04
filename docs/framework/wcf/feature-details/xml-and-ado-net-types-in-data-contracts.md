---
title: "Tipi XML e ADO.NET nei contratti dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c2ce8461-3c15-4c41-8c81-1cb78f5b59a6
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Tipi XML e ADO.NET nei contratti dati
Il modello di contratto dati [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] supporta alcuni tipi che rappresentano direttamente il formato XML.  Quando questi tipi vengono serializzati in XML, il serializzatore scrive il contenuto XML di questi tipi senza ulteriore elaborazione.  I tipi supportati sono <xref:System.Xml.XmlElement>, matrici di <xref:System.Xml.XmlNode> \(ma non il tipo `XmlNode` stesso\) e tipi che implementano <xref:System.Xml.Serialization.IXmlSerializable>.  I tipi <xref:System.Data.DataSet> e <xref:System.Data.DataTable>, nonché i dataset tipizzati, vengono comunemente usati nella programmazione dei database.  Questi tipi implementano l'interfaccia `IXmlSerializable` e sono pertanto serializzabili nel modello del contratto dati.  Alcune considerazioni speciali per questi tipi sono elencate alla fine di questo argomento.  
  
## Tipi XML  
  
### Elemento XML  
 Il tipo `XmlElement` viene serializzato usando il contenuto XML.  Si usi ad esempio il tipo seguente.  
  
 [!code-csharp[DataContractAttribute#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/datacontractattribute/cs/overview.cs#4)]
 [!code-vb[DataContractAttribute#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datacontractattribute/vb/overview.vb#4)]  
  
 Questo tipo viene serializzato in XML come segue:  
  
```  
<MyDataContract xmlns="http://schemas.contoso.com">  
    <myDataMember>  
        <myElement xmlns="" myAttribute="myValue">  
            myContents  
        </myElement>  
    </myDataMember>  
</MyDataContract>  
```  
  
 Si noti che è ancora presente un elemento `<myDataMember>` membro dati del wrapper.  Non è possibile rimuovere questo elemento dal modello del contratto dati.  I serializzatori che gestiscono questo modello \(<xref:System.Runtime.Serialization.DataContractSerializer> e <xref:System.Runtime.Serialization.NetDataContractSerializer>\) possono generare attributi speciali in questo elemento wrapper.  Tali attributi includono l'attributo "nil" standard dell'istanza di XML Schema \(consentendo a `XmlElement` di essere `null`\) e l'attributo "type" \(consentendo l'uso di `XmlElement` in modo polimorfico\).  Inoltre, gli attributi XML seguenti sono specifici di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]: "Id", "Ref", "Type" e "Assembly".  Questi attributi possono essere generati per supportare l'uso di `XmlElement` con la modalità di mantenimento dell'oggetto grafico abilitata o con <xref:System.Runtime.Serialization.NetDataContractSerializer>.  \([!INCLUDE[crabout](../../../../includes/crabout-md.md)]lla modalità di mantenimento dell'oggetto grafico, vedere [Serializzazione e deserializzazione](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md)\).  
  
 Le matrici o raccolte di `XmlElement` sono consentite e sono gestite come qualsiasi altra matrice o raccolta.  Ovvero, è presente un elemento wrapper per l'intera raccolta e un elemento wrapper separato \(simile a `<myDataMember>``XmlElement nell'esempio precedente) per ogni`  della matrice.  
  
 Durante la deserializzazione, viene creato un `XmlElement` dal deserializzatore per il file XML in ingresso.  Dal deserializzatore viene fornito un elemento <xref:System.Xml.XmlDocument> padre valido.  
  
 Verificare che il frammento XML che viene deserializzato in un `XmlElement` definisca tutti i prefissi usati e non si basi su definizioni di prefissi degli elementi predecessori.  Questo aspetto è importante solo quando si adopera `DataContractSerializer` per usare il file XML da un'origine diversa \(non `DataContractSerializer`\).  
  
 Se usato con `DataContractSerializer`, `XmlElement` può essere assegnato in modo polimorfico, ma solo a un membro dati di tipo <xref:System.Object>.  Sebbene implementi <xref:System.Collections.IEnumerable>, `XmlElement` non può essere usato come tipo di raccolta e non può essere assegnato a un membro dati <xref:System.Collections.IEnumerable>.  In modo analogo alle assegnazioni polimorfiche, `DataContractSerializer` genera il nome del contratto dati nel file XML risultante, in questo caso è "XmlElement" nello spazio dei nomi "http:\/\/schemas.datacontract.org\/2004\/07\/System.Xml".  
  
 Con `NetDataContractSerializer`, è supportata qualsiasi assegnazione polimorfica valida di `XmlElement` \(`Object` o `IEnumerable`\).  
  
 Non tentare di usare uno dei serializzatori con i tipi derivati da `XmlElement`, indipendentemente dal fatto che siano stati assegnati in modo polimorfico o meno.  
  
### Matrice di XmlNode  
 L'uso di matrici di <xref:System.Xml.XmlNode> è molto simile all'uso di `XmlElement`.  Tuttavia, la scelta di usare matrici di `XmlNode` garantisce una maggiore flessibilità rispetto all'uso di `XmlElement`.  È possibile scrivere più elementi nell'elemento wrapper del membro dati  E’ possibile inserire al suo interno un contenuto diverso dagli elementi, ad esempio commenti XML.  Infine, è inoltre possibile inserire attributi nell'elemento wrapper del membro dati.  Tutte queste operazioni possono essere realizzate popolando la matrice di `XmlNode` con classi derivate specifiche di `XmlNode`, ad esempio <xref:System.Xml.XmlAttribute>, `XmlElement` o <xref:System.Xml.XmlComment>.  Si usi ad esempio il tipo seguente.  
  
 [!code-csharp[DataContractAttribute#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/datacontractattribute/cs/overview.cs#5)]
 [!code-vb[DataContractAttribute#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datacontractattribute/vb/overview.vb#5)]  
  
 Quando viene serializzato, l'XML risultante è simile al codice seguente.  
  
```  
<MyDataContract xmlns="http://schemas.contoso.com">  
  <myDataMember myAttribute="myValue">  
     <!--myComment-->  
     <myElement xmlns="" myAttribute="myValue">  
 myContents  
     </myElement>  
     <myElement xmlns="" myAttribute="myValue">  
       myContents  
     </myElement>  
  </myDataMember>  
</MyDataContract>  
```  
  
 Si noti che l'elemento wrapper del membro dati `<myDataMember>` contiene un attributo, un commento e due elementi.  Sono le quattro istanze di `XmlNode` serializzate.  
  
 Non è possibile serializzare una matrice di `XmlNode` che causa un XML non valido.  Ad esempio, una matrice di due istanze di `XmlNode` di cui la prima è un `XmlElement` e la seconda è un <xref:System.Xml.XmlAttribute> non è valida poiché questa sequenza non corrisponde ad alcuna istanza XML valida \(non è possibile allegare un attributo\).  
  
 Durante la deserializzazione di una matrice di `XmlNode`, i nodi vengono creati e popolati con informazioni derivate dal file XML in ingresso.  Dal deserializzatore viene fornito un elemento <xref:System.Xml.XmlDocument> padre valido.  Tutti i nodi vengono deserializzati, includendo qualsiasi attributo sull'elemento wrapper del membro dati, ma escludendo gli attributi posizionati dai serializzatori [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \(ad esempio gli attributi usati per indicare l'assegnazione polimorfica\).  La necessità di definire tutti i prefissi degli spazi dei nomi nel frammento XML si applica alla deserializzazione delle matrici di `XmlNode` e alla deserializzazione di `XmlElement`.  
  
 Se si usano serializzatori per i quali è attivato il mantenimento dell'oggetto grafico, l'uguaglianza degli oggetti viene mantenuta solo a livello delle matrici di `XmlNode` e non per le singole istanze di `XmlNode`.  
  
 Non tentare di serializzare una matrice di `XmlNode` se uno o più nodi è impostato su `null`.  L'intero membro matrice può essere `null`, ma non i singoli `XmlNode` contenuti nella matrice.  Se l'intero membro matrice è Null, l'elemento wrapper del membro dati contiene un attributo speciale che indica che è Null.  Durante la deserializzazione, anche l'intero membro matrice diviene Null.  
  
 Solo le matrici normali di `XmlNode` vengono trattate in modo speciale dal serializzatore.  I membri dati dichiarati come altri tipi di raccolta contenenti `XmlNode` o i membri dati dichiarati come matrici di tipi derivati da `XmlNode` non vengono trattati in modo speciale.  Pertanto, in genere non sono serializzabili a meno che soddisfino anche uno degli altri criteri di serializzazione.  
  
 Sono consentite matrici o raccolte di matrici di `XmlNode`.  E’ presente un elemento wrapper per l'intera raccolta e un elemento wrapper separato \(simile a `<myDataMember>``XmlNode nell'esempio precedente) per ogni matrice di`  nella matrice esterna o nella raccolta.  
  
 Se si popola un membro dati di tipo <xref:System.Array> di `Object` o `Array` di `IEnumerable` con le istanze di `XmlNode`, il membro dati non viene trattato come una `Array` di istanze di `XmlNode`.  Ogni membro della matrice viene serializzato separatamente.  
  
 Se si usano con `DataContractSerializer`, le matrici di `XmlNode` possono essere assegnate in modo polimorfico, ma solo a un membro dati di tipo `Object`.  Sebbene implementi `IEnumerable`, una matrice di `XmlNode` non può essere usata come tipo di raccolta e non può essere assegnata a un membro dati `IEnumerable`.  In modo analogo alle assegnazioni polimorfiche, `DataContractSerializer` genera il nome del contratto dati nel file XML risultante, in questo caso è "ArrayOfXmlNode" nello spazio dei nomi "http:\/\/schemas.datacontract.org\/2004\/07\/System.Xml".  Se usata con la classe Net`DataContractSerializer`, qualsiasi assegnazione valida di una matrice di `XmlNode` è supportata.  
  
### Considerazioni sugli schemi  
 Per dettagli sul mapping dello schema dei tipi XML, vedere [Riferimento allo schema del contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md).  Questa sezione fornisce un riepilogo dei punti importanti.  
  
 Un membro dati di tipo `XmlElement` viene mappato a un elemento definito usando il tipo anonimo seguente.  
  
```  
<xsd:complexType>  
   <xsd:sequence>  
      <xsd:any minOccurs="0" processContents="lax" />  
   </xsd:sequence>  
</xsd:complexType>  
```  
  
 Un membro dati di tipo matrice di `XmlNode` viene mappato a un elemento definito usando il tipo anonimo seguente.  
  
```  
<xsd:complexType mixed="true">  
   <xsd:sequence>  
      <xsd:any minOccurs="0" maxOccurs="unbounded" processContents="lax" />  
   </xsd:sequence>  
   <xsd:anyAttribute/>  
</xsd:complexType>  
```  
  
## Tipi che implementano l'interfaccia IXmlSerializable  
 I tipi che implementano l'interfaccia `IXmlSerializable` sono completamente supportati da `DataContractSerializer`.  L'attributo <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> deve essere applicato sempre a questi tipi per controllarne lo schema.  
  
 Esistono tre varietà di tipi che implementano `IXmlSerializable`: i tipi che rappresentano contenuto arbitrario, i tipi che rappresentano un singolo elemento e i tipi <xref:System.Data.DataSet> legacy.  
  
-   I tipi di contenuto usano un metodo del provider dello schema specificato dall'attributo `XmlSchemaProviderAttribute`.  Il metodo non restituisce `null` e la proprietà <xref:System.Xml.Serialization.XmlSchemaProviderAttribute.IsAny%2A> dell'attributo mantiene il valore predefinito `false`.  Si tratta dell'utilizzo più comune di tipi `IXmlSerializable`.  
  
-   I tipi di elemento vengono usati quando un tipo `IXmlSerializable` deve controllare il nome del relativo elemento radice.  Per contrassegnare un tipo come tipo di elemento, impostare la proprietà <xref:System.Xml.Serialization.XmlSchemaProviderAttribute.IsAny%2A> dell'attributo <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> su `true` o fare in modo che il metodo del provider dello schema restituisca Null.  Il metodo del provider dello schema è facoltativo per i tipi di elemento; è infatti possibile specificare Null anziché il nome del metodo in `XmlSchemaProviderAttribute`.  Tuttavia, se `IsAny` è `true` ed è specificato un metodo del provider dello schema, il metodo deve restituire Null.  
  
-   I tipi <xref:System.Data.DataSet> legacy sono tipi `IXmlSerializable` non contrassegnati con l'attributo `XmlSchemaProviderAttribute`,  che si basano sul metodo <xref:System.Xml.Serialization.IXmlSerializable.GetSchema%2A> per la generazione dello schema.  Questo modello è usato per il tipo `DataSet` e le relative classi derivate del dataset tipizzato nelle versioni precedenti di .NET Framework, ma ora è obsoleto ed è supportato solo per elementi legacy.  Non è consigliabile basarsi su questo modello, bensì applicare sempre `XmlSchemaProviderAttribute` ai tipi `IXmlSerializable`.  
  
### Tipi di contenuto IXmlSerializable  
 Quando si serializza un membro dati di un tipo che implementa `IXmlSerializable` e il tipo di contenuto rispecchia la definizione precedente, il serializzatore scrive l'elemento wrapper per il membro dati e passa il controllo al metodo <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A>.  L'implementazione <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> può scrivere qualsiasi elemento XML e può anche aggiungere attributi all'elemento wrapper.  Quando l'operazione `WriteXml` è stata completata, il serializzatore chiude l'elemento.  
  
 Quando si deserializza un membro dati di un tipo che implementa `IXmlSerializable` e il tipo di contenuto rispecchia la definizione precedente, il deserializzatore posiziona il lettore XML sull'elemento wrapper per il membro dati e passa il controllo al metodo <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A>.  Il metodo deve leggere l'elemento intero, inclusi i tag di inizio e fine.  Verificare che il codice `ReadXml` gestisca l'eventualità che l'elemento sia vuoto.  Inoltre, l'implementazione `ReadXml` non deve basarsi sull'uso di un nome specifico per l'elemento wrapper,  poiché il nome viene scelto dal serializzatore e quindi può variare.  
  
 È consentito assegnare tipi di contenuto `IXmlSerializable` in modo polimorfico, ad esempio, ai membri dati di tipo <xref:System.Object>.  È inoltre consentito che le istanze del tipo siano Null.  Infine, è possibile usare tipi `IXmlSerializable` con il mantenimento dell'oggetto grafico abilitato e con <xref:System.Runtime.Serialization.NetDataContractSerializer>.  Tutte queste funzionalità richiedono che il serializzatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] inserisca determinati attributi nell'elemento wrapper \("nil" e "type" nello spazio dei nomi dell'istanza di XML Schema e "Id", "Ref", "Type" e "Assembly" in uno spazio dei nomi specifico per [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\).  
  
#### Attributi da ignorare quando si implementa ReadXml  
 Prima di passare il controllo al codice `ReadXml`, il deserializzatore esamina l'elemento XML, rileva questi attributi XML speciali e interviene su di essi.  Ad esempio, se "nil" è `true`, un valore Null viene deserializzato e `ReadXml` non viene chiamato.  Se viene rilevato il polimorfismo, il contenuto dell'elemento viene deserializzato come se si trattasse di un tipo diverso.  L'implementazione di `ReadXml` del tipo assegnato in modo polimorfico viene chiamata.  In ogni caso, un'implementazione `ReadXml` deve ignorare questi attributi speciali poiché vengono gestiti dal deserializzatore.  
  
### Considerazioni sullo schema per i tipi di contenuto IXmlSerializable  
 Se si esporta lo schema per un tipo di contenuto `IXmlSerializable`, viene chiamato il metodo del provider dello schema.  Al metodo del provider dello schema viene passata una classe <xref:System.Xml.Schema.XmlSchemaSet>.  Il metodo può aggiungere qualsiasi schema valido al set di schemi.  Il set di schemi contiene lo schema già conosciuto al momento dell'esportazione dello schema.  Quando il metodo del provider dello schema deve aggiungere un elemento al set di schemi, deve determinare se esiste una classe <xref:System.Xml.Schema.XmlSchema> con lo spazio dei nomi appropriato nel set.  In tal caso, il metodo del provider dello schema deve aggiungere il nuovo elemento alla classe `XmlSchema` esistente.  In caso contrario, deve creare una nuova istanza di `XmlSchema`.  Questo è importante se vengono usate matrici di tipi `IXmlSerializable`.  Ad esempio, se un tipo `IXmlSerializable` viene esportato come tipo "A" nello spazio dei nomi "B", è possibile che quando il metodo del provider dello schema viene chiamato il set di schemi contenga già lo schema per "B" che contiene il tipo "ArrayOfA".  
  
 Oltre ad aggiungere i tipi nella classe <xref:System.Xml.Schema.XmlSchemaSet>, il metodo del provider dello schema per i tipi di contenuto deve restituire un valore diverso da Null.  Può restituire un oggetto <xref:System.Xml.XmlQualifiedName> che specifica il nome del tipo di schema da usare per il tipo `IXmlSerializable` specificato.  Questo nome completo serve anche come nome e spazio dei nomi del contratto dati per il tipo.  È consentito restituire un tipo che non esiste nel set di schemi quando il metodo del provider di schema viene restituito.  Tuttavia, in genere al momento dell'esportazione di tutti i tipi correlati \(il metodo <xref:System.Runtime.Serialization.XsdDataContractExporter.Export%2A> viene chiamato per tutti i tipi attinenti su <xref:System.Runtime.Serialization.XsdDataContractExporter> e si accede alla proprietà <xref:System.Runtime.Serialization.XsdDataContractExporter.Schemas%2A>\) il tipo esiste già nel set di schemi.  L'accesso alla proprietà `Schemas` prima che tutte le chiamate `Export` attinenti siano state effettuate può generare un'eccezione <xref:System.Xml.Schema.XmlSchemaException>.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sul processo di esportazione, vedere [Esportazione di schemi dalle classi](../../../../docs/framework/wcf/feature-details/exporting-schemas-from-classes.md).  
  
 Il metodo del provider dello schema può restituire anche l'oggetto <xref:System.Xml.Schema.XmlSchemaType> da usare.  Il tipo può o meno essere anonimo.  Se è anonimo, lo schema per il tipo `IXmlSerializable` viene esportato come tipo anonimo ogni volta che il tipo `IXmlSerializable` viene usato come membro dati.  Il tipo `IXmlSerializable` ha ancora un nome e uno spazio dei nomi del contratto dati  \(determinato come descritto in [Nomi di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-names.md) con l'eccezione che l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> non può essere usato per personalizzare il nome\). Se non è anonimo, deve essere uno dei tipi in `XmlSchemaSet`.  Questo caso è equivalente alla restituzione del `XmlQualifiedName` del tipo.  
  
 Inoltre, viene esportata una dichiarazione di elemento globale per il tipo.  Se al tipo non è applicato l'attributo <xref:System.Xml.Serialization.XmlRootAttribute>, l'elemento ha lo stesso nome e spazio dei nomi del contratto dati e la proprietà "nillable" sarà True.  L'unica eccezione a questo comportamento è costituito dallo spazio dei nomi dello schema \("http:\/\/www.w3.org\/2001\/XMLSchema"\), ovvero se il contratto dati del tipo è incluso in questo spazio dei nomi, l'elemento globale corrispondente si trova nello spazio dei nomi vuoto perché non è consentito aggiungere elementi nuovi allo spazio dei nomi dello schema.  Se al tipo è applicato l'attributo `XmlRootAttribute`, la dichiarazione di elemento globale viene esportata usando le proprietà <xref:System.Xml.Serialization.XmlRootAttribute.ElementName%2A>, <xref:System.Xml.Serialization.XmlRootAttribute.Namespace%2A> e <xref:System.Xml.Serialization.XmlRootAttribute.IsNullable%2A>.  L'impostazione predefinita quando è applicato l'attributo `XmlRootAttribute` è costituita dal nome del contratto dati, da un spazio dei nomi vuoto e da un valore "nillable" impostato su True.  
  
 Le stesse regole della dichiarazione di elemento globale si applicano ai tipi di dataset legacy.  Si noti che `XmlRootAttribute` non può eseguire l'override delle dichiarazioni di elemento globale aggiunte tramite codice personalizzato o aggiunte a `XmlSchemaSet` usando il metodo del provider dello schema o tramite `GetSchema` per i tipi di dataset legacy.  
  
### Tipi di elemento IXmlSerializable  
 I tipi di elemento `IXmlSerializable` hanno la proprietà `IsAny` impostata su `true` o il relativo metodo del provider dello schema restituisce `null`.  
  
 La serializzazione e deserializzazione di un tipo di elemento è molto simile alla serializzazione e deserializzazione di un tipo di contenuto.  Esistono tuttavia alcune importanti differenze:  
  
-   Si presuppone che l'implementazione `WriteXml` scriva un solo elemento \(che può ovviamente contenere più elementi figlio\).  Non deve scrivere attributi all'esterno di questo singolo elemento, più elementi di pari livello o contenuto misto.  L'elemento può essere vuoto.  
  
-   L'implementazione `ReadXml` non deve leggere l'elemento wrapper,  bensì deve leggere l'unico elemento prodotto da `WriteXml`.  
  
-   Quando si serializza regolarmente un tipo di elemento \(ad esempio, come un membro dati in un contratto dati\), il serializzatore restituisce un elemento wrapper prima di chiamare `WriteXml`, come per i tipi di contenuto.  Tuttavia, quando si serializza un tipo di elemento al primo livello, il serializzatore in genere non restituisce un elemento wrapper per l'elemento scritto da `WriteXml`, a meno che un nome e uno spazio dei nomi principali vengano specificati in modo esplicito durante la creazione del serializzatore nei costruttori `DataContractSerializer` o `NetDataContractSerializer`.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Serializzazione e deserializzazione](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md).  
  
-   Quando si serializza un tipo di elemento al primo livello senza specificare il nome e lo spazio dei nomi principali in fase di creazione, i metodi <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteStartObject%2A> e <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteEndObject%2A> essenzialmente non eseguono alcuna operazione e il metodo <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteObjectContent%2A> chiama `WriteXml`.  In questo caso, l'oggetto serializzato non può essere Null e non può essere assegnato in modo polimorfico.  Inoltre, il mantenimento dell'oggetto grafico non può essere abilitato e `NetDataContractSerializer` non può essere usato.  
  
-   Quando si deserializza un tipo di elemento al primo livello senza specificare il nome e lo spazio dei nomi radice in fase di costruzione, il metodo <xref:System.Runtime.Serialization.XmlObjectSerializer.IsStartObject%2A> restituisce `true` se riesce a trovare l'inizio di qualsiasi elemento.  <xref:System.Runtime.Serialization.XmlObjectSerializer.ReadObject%2A> con il parametro `verifyObjectName` impostato su `true` si comporta allo stesso modo di `IsStartObject` prima di leggere effettivamente l'oggetto.  `ReadObject` passa quindi il controllo al metodo `ReadXml`.  
  
 Lo schema esportato per i tipi di elemento è lo stesso del tipo `XmlElement`, come illustrato in una sezione precedente, con l'eccezione che il metodo del provider dello schema può aggiungere qualsiasi altro schema a <xref:System.Xml.Schema.XmlSchemaSet> come con i tipi di contenuto.  L'uso dell'attributo `XmlRootAttribute` con i tipi di elemento non è consentito e le dichiarazioni di elemento globale non vengono mai generate per questi tipi.  
  
### Differenze rispetto a XmlSerializer  
 L'interfaccia `IXmlSerializable` e gli attributi `XmlSchemaProviderAttribute` e `XmlRootAttribute` vengono riconosciuti anche da <xref:System.Xml.Serialization.XmlSerializer>.  Tuttavia, esistono alcune differenze nel modo in cui questi elementi vengono gestiti nel modello del contratto dati.  Le differenze più importanti sono riepilogate di seguito:  
  
-   Il metodo del provider dello schema deve essere pubblico per poter essere usato in `XmlSerializer`, ma non deve essere pubblico per poter essere usato nel modello del contratto dati.  
  
-   Il metodo del provider dello schema viene chiamato quando `IsAny` è True nel modello del contratto dati, ma non con `XmlSerializer`.  
  
-   Quando l'attributo `XmlRootAttribute` non è presente per contenuto o i tipi di dataset legacy, `XmlSerializer` esporta una dichiarazione di elemento globale nello spazio dei nomi vuoto.  Nel modello del contratto dati, lo spazio dei nomi usato è in genere lo spazio dei nomi del contratto dati, come descritto in precedenza.  
  
 Tenere presenti queste differenze durante la creazione di tipi che vengono usati con entrambe le tecnologie di serializzazione.  
  
### Importazione dello schema IXmlSerializable  
 Quando si importa uno schema generato dai tipi `IXmlSerializable`, si verificano alcuni possibili scenari:  
  
-   Lo schema generato può essere uno schema valido del contratto dati, come descritto in [Riferimento allo schema del contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md).  In questo caso, lo schema può essere importato normalmente e vengono generati tipi del contratto dati normali.  
  
-   Lo schema generato può non essere uno schema valido del contratto dati.  Ad esempio, il metodo del provider dello schema può generare lo schema coinvolgendo gli attributi XML che non sono supportati nel modello del contratto dati.  In questo caso, è possibile importare lo schema come tipi `IXmlSerializable`.  Questa modalità di importazione non è attiva per impostazione predefinita ma può essere abilitata facilmente, ad esempio, con l'opzione della riga di comando `/importXmlTypes` in [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  Questo aspetto viene descritto in dettaglio in [Importazione dello schema per generare classi](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md).  Si noti che è necessario interagire direttamente con XML per le istanze del tipo.  Si può anche scegliere di usare una tecnologia di serializzazione diversa che supporti una gamma più ampia di schemi \(vedere l'argomento relativo all'uso di `XmlSerializer`\).  
  
-   Può essere necessario riusare i tipi `IXmlSerializable` esistenti nel proxy anziché generare tipi nuovi.  In questo caso, è possibile usare la funzionalità dei tipi a cui è stato fatto riferimento descritta nell'argomento relativo all'importazione dello schema per generare i tipi per indicare il tipo da riusare.  Questa procedura corrisponde all'uso dell'opzione `/reference` in svcutil.exe, che specifica l'assembly contenente i tipi da riusare.  
  
## Rappresentazione di contenuto XML arbitrario nei contratti dati  
 `XmlElement`, la matrice di `XmlNode` e i tipi `IXmlSerializable` consentono di inserire contenuto XML arbitrario nel modello del contratto dati.  `DataContractSerializer` e `NetDataContractSerializer` passano questo contenuto XML al writer XML in uso, senza interferire nel processo.  Tuttavia, i writer XML possono applicare alcune restrizioni sul contenuto XML che scrivono.  Di seguito sono riportati alcuni esempi importanti:  
  
-   I writer XML in genere non consentono una dichiarazione del documento XML \(ad esempio \<?xml version\=’1.0’ ?\>\) mentre è in corso la scrittura di un altro documento.  Non è possibile serializzare un documento XML completo come un elemento `Array` del membro dati `XmlNode`.  Per questo scopo, è necessario rimuovere la dichiarazione del documento o usare uno schema di codifica personalizzato per rappresentarlo.  
  
-   Tutti i writer XML forniti con [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] rifiutano le istruzioni di elaborazione XML \(\<?  … ?\>\) e definizioni del tipo di documento \(\<\!  … \>\), poiché non sono consentite nei messaggi SOAP.  Anche in questo caso è possibile usare un meccanismo di codifica personalizzato per evitare questa restrizione.  Se è necessario includere questi elementi nel contenuto XML risultante, è possibile scrivere un codificatore personalizzato che usi i writer XML che li supportano.  
  
-   Quando si implementa `WriteXml`, evitare di chiamare il metodo <xref:System.Xml.XmlWriter.WriteRaw%2A> sul writer XML.  Poiché in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene usata una varietà di codifiche XML \(inclusa la codifica binaria\), è molto difficile o impossibile usare `WriteRaw` in modo che il risultato sia usabile in qualsiasi codifica.  
  
-   Quando si implementa `WriteXml`, evitare di usare i metodi <xref:System.Xml.XmlWriter.WriteEntityRef%2A> e <xref:System.Xml.XmlWriter.WriteNmToken%2A> che sono non supportati dai writer XML forniti con [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Uso di dataset, dataset tipizzati e DataTable  
 L'uso di questi tipi è supportato pienamente nel modello del contratto dati.  Quando si usano questi tipi, è opportuno considerare i punti seguenti:  
  
-   Lo schema per questi tipi \(in particolare <xref:System.Data.DataSet> e le relative classi derivate tipizzate\) non può interagire con alcune piattaforme diverse da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] o può determinare scarsa usabilità se usato con queste piattaforme.  Inoltre, l'uso del tipo `DataSet` può avere implicazioni sulle prestazioni.  Può infine rendere più difficile il controllo della versione dell'applicazione in futuro.  È consigliabile usare tipi di contratto dati definiti in modo esplicito al posto dei tipi `DataSet` nei contratti.  
  
-   Quando si importa lo schema `DataSet` o `DataTable`, è importante fare riferimento a questi tipi.  Con l'utilità strumento da riga di comando svcutil.exe, è possibile eseguire questa operazione passando il nome dell'assembly System.Data.dll all'opzione `/reference`.  Se si importa lo schema del dataset tipizzato, è necessario fare riferimento al tipo del dataset tipizzato.  Con svcutil.exe, passare il percorso dell'assembly del set di dati tipizzato all'opzione `/reference`.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]i riferimenti ai tipi, vedere [Importazione dello schema per generare classi](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md).  
  
 Il supporto per i dataset tipizzati nel modello del contratto dati è limitato.  I dataset tipizzati possono essere serializzati e deserializzati e possono esportare il proprio schema.  Tuttavia, l’importazione dello schema del contratto dati non è in grado di generare nuovi tipi di dataset tipizzati dallo schema, in quanto può solo riusare quelli esistenti.  E’ possibile far riferimento a un dataset tipizzato esistente usando l’opzione `/r` in Svcutil.exe.  Se si tenta di usare Svcutil.exe senza l’opzione `/r` in un servizio che usa un dataset tipizzato, viene automaticamente selezionato un serializzatore alternativo \(XmlSerializer\).  Se è necessario usare il DataContractSerializer e generare dataset dallo schema, è possibile usare la seguente procedura: generare i tipi di dataset tipizzati \(usando lo strumento Xsd.exe con l’opzione `/d` nel servizio\), compilare i tipi, quindi farvi riferimento usando l’opzione `/r` in Svcutil.exe.  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Xml.Serialization.IXmlSerializable>   
 [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)   
 [Tipi supportati dal serializzatore dei contratti dati](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)