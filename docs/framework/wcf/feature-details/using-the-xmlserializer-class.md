---
title: "Utilizzo della classe XmlSerializer | Microsoft Docs"
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
  - "XmlSerializer [WCF], uso"
ms.assetid: c680602d-39d3-44f1-bf22-8e6654ad5069
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# Utilizzo della classe XmlSerializer
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] può usare due diverse tecnologie di serializzazione per trasformare i dati dell'applicazione in XML trasmesso tra client e servizi, un processo definito serializzazione.  
  
## DataContractSerializer come impostazione predefinita  
 Per impostazione predefinita, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] usa la classe <xref:System.Runtime.Serialization.DataContractSerializer> per serializzare i tipi di dati. Questo serializzatore supporta i tipi seguenti:  
  
-   Tipi primitivi \(ad esempio, integer, stringhe e matrici di byte\), nonché alcuni tipi speciali, ad esempio <xref:System.Xml.XmlElement> e <xref:System.DateTime>, che vengono trattati come primitivi.  
  
-   Tipi di contratti dati \(tipi contrassegnati con l'attributo <xref:System.Runtime.Serialization.DataContractAttribute>\).  
  
-   Tipi contrassegnati con l'attributo <xref:System.SerializableAttribute>, inclusi i tipi che implementano l'interfaccia <xref:System.Runtime.Serialization.ISerializable>.  
  
-   Tipi che implementano l'interfaccia <xref:System.Xml.Serialization.IXmlSerializable>.  
  
-   Molti tipi di raccolte comuni, inclusi molti tipi di raccolte generiche.  
  
 Molti tipi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] rientrano in una delle ultime due categorie e pertanto sono serializzabili. Anche le matrici di tipi serializzabili sono serializzabili. Per un elenco completo, vedere [Specifica del trasferimento di dati nei contratti di servizio](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md).  
  
 <xref:System.Runtime.Serialization.DataContractSerializer>, usato con i tipi di contratto dati, rappresenta il modo consigliato per scrivere nuovi servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md).  
  
## Quando usare la classe XmlSerializer  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta anche la classe <xref:System.Xml.Serialization.XmlSerializer>. La classe <xref:System.Xml.Serialization.XmlSerializer> non è univoca per [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. È lo stesso motore di serializzazione usato dai servizi Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]. La classe <xref:System.Xml.Serialization.XmlSerializer> supporta un set di tipi molto più ristretto rispetto alla classe <xref:System.Runtime.Serialization.DataContractSerializer>, ma garantisce un controllo maggiore sul contenuto XML risultante e un supporto maggiore dello standard XSD \(XML Schema Definition Language\). Inoltre, non richiede attributi dichiarativi sui tipi serializzabili.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'argomento relativo alla serializzazione XML nella documentazione di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]. La classe <xref:System.Xml.Serialization.XmlSerializer> non supporta i tipi di contratto dati.  
  
 Se si usa Svcutil.exe o la funzionalità **Aggiungi riferimento al servizio** in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] per generare codice client per un servizio di terze parti o per accedere a un schema di terze parti, viene selezionato automaticamente un serializzatore appropriato. Se lo schema non è compatibile con <xref:System.Runtime.Serialization.DataContractSerializer>, viene selezionato <xref:System.Xml.Serialization.XmlSerializer>.  
  
## Passaggio manuale a XmlSerializer  
 In alcuni casi può essere necessario passare manualmente a <xref:System.Xml.Serialization.XmlSerializer>. Ciò si verifica, ad esempio, nei casi seguenti:  
  
-   Quando si esegue la migrazione di un'applicazione dai servizi Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], può essere necessario riusare i tipi compatibili con <xref:System.Xml.Serialization.XmlSerializer> esistenti anziché creare nuovi tipi di contratto dati.  
  
-   Se è importante controllare in modo accurato il contenuto XML presente nei messaggi ma non è disponibile un documento WSDL \(Web Services Description Language\), ad esempio, quando si crea un servizio con tipi che devono conformarsi a uno specifico schema standardizzato pubblicato che non è compatibile con DataContractSerializer.  
  
-   Quando si creano servizi che seguono lo standard della codifica SOAP legacy.  
  
 In questi e altri casi è possibile passare manualmente alla classe <xref:System.Xml.Serialization.XmlSerializer> applicando l'attributo `XmlSerializerFormatAttribute` al servizio, come illustrato nel codice seguente.  
  
 [!code-csharp[c_XmlSerializer#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_xmlserializer/cs/source.cs#1)]
 [!code-vb[c_XmlSerializer#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_xmlserializer/vb/source.vb#1)]  
  
## Considerazioni sulla sicurezza  
  
> [!NOTE]
>  È importante fare attenzione quando si passa ai motori di serializzazione. Lo stesso tipo può essere serializzato in XML in modo diverso a seconda del serializzatore usato. Se si usa accidentalmente il serializzatore sbagliato, potrebbero essere diffuse informazioni dal tipo che non si aveva intenzione di diffondere.  
  
 Ad esempio, la classe <xref:System.Runtime.Serialization.DataContractSerializer> serializza solo membri contrassegnati con l'attributo <xref:System.Runtime.Serialization.DataMemberAttribute> quando si serializzano tipi di contratto dati. La classe <xref:System.Xml.Serialization.XmlSerializer> serializza qualsiasi membro pubblico. Vedere il tipo nel codice seguente.  
  
 [!code-csharp[c_XmlSerializer#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_xmlserializer/cs/source.cs#2)]
 [!code-vb[c_XmlSerializer#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_xmlserializer/vb/source.vb#2)]  
  
 Se il tipo viene usato inavvertitamente in un contratto di servizio in cui è selezionata la classe <xref:System.Xml.Serialization.XmlSerializer>, il membro `creditCardNumber` viene serializzato, operazione probabilmente non voluta.  
  
 Anche se la classe <xref:System.Runtime.Serialization.DataContractSerializer> è l'impostazione predefinita, è possibile selezionarla in modo esplicito per il servizio \(anche se questa operazione non è richiesta\) applicando l'attributo <xref:System.ServiceModel.DataContractFormatAttribute> al tipo di contratto di servizio.  
  
 Il serializzatore usato per il servizio è parte integrante del contratto e non può essere modificato selezionando un'associazione diversa o modificando le altre impostazioni di configurazione.  
  
 Altre importanti considerazioni di sicurezza riguardano la classe <xref:System.Xml.Serialization.XmlSerializer>. È innanzitutto consigliabile firmare qualsiasi applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che usa la classe <xref:System.Xml.Serialization.XmlSerializer> con una chiave a cui sia applicata una misura di protezione che impedisca la diffusione di informazioni. Questa indicazione è valida sia quando si esegue un passaggio manuale a <xref:System.Xml.Serialization.XmlSerializer> che quando si esegue un passaggio automatico \(mediante Svcutil.exe, Aggiungi riferimento al servizio o uno strumento simile\). Ciò è necessario in quanto il motore di serializzazione <xref:System.Xml.Serialization.XmlSerializer> supporta il caricamento di *assembly di serializzazione pregenerati* purché siano firmati con la stessa chiave dell'applicazione. Un'applicazione non firmata è priva di qualsiasi protezione rispetto alla possibilità che un assembly dannoso corrispondente al nome previsto dell'assembly di serializzazione pregenerato venga posizionato nella cartella dell'applicazione o nella Global Assembly Cache. L'autore di un attacco dovrà comunque ottenere l'accesso in scrittura a uno di questi due percorsi prima di tentare questa azione.  
  
 Un'altra minaccia che esiste quando si usa <xref:System.Xml.Serialization.XmlSerializer> riguarda l'accesso in scrittura alla cartella temporanea del sistema. Il motore di serializzazione <xref:System.Xml.Serialization.XmlSerializer> crea e usa *assembly di serializzazione* temporanei in questa cartella. È quindi necessario tenere presente che qualsiasi processo con accesso in scrittura alla cartella temporanea può sovrascrivere questi assembly di serializzazione con codice dannoso.  
  
## Regole per il supporto di XmlSerializer  
 Non è possibile applicare direttamente attributi compatibili con <xref:System.Xml.Serialization.XmlSerializer> ai parametri o ai valori restituiti dell'operazione del contratto. Tali attributi possono tuttavia essere applicati ai messaggi tipizzati \(parti del corpo del contratto di messaggio\), come illustrato nel codice seguente.  
  
 [!code-csharp[c_XmlSerializer#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_xmlserializer/cs/source.cs#3)]
 [!code-vb[c_XmlSerializer#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_xmlserializer/vb/source.vb#3)]  
  
 Se applicati ai membri del messaggio tipizzato, questi attributi eseguono l'override delle proprietà in conflitto negli attributi del messaggio tipizzato. Ad esempio, nel codice seguente `ElementName` esegue l'override di `Name`.  
  
 [!code-csharp[c_XmlSerializer#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_xmlserializer/cs/source.cs#4)]
 [!code-vb[c_XmlSerializer#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_xmlserializer/vb/source.vb#4)]  
  
 L'attributo <xref:System.ServiceModel.MessageHeaderArrayAttribute> non è supportato quando si usa <xref:System.Xml.Serialization.XmlSerializer>.  
  
> [!NOTE]
>  In questo caso, <xref:System.Xml.Serialization.XmlSerializer> genera la seguente eccezione, rilasciata prima di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]: "Un elemento dichiarato al livello principale di uno schema non può avere l'attributo `maxOccurs` \> 1. Fornire un elemento wrapper per "more" usando `XmlArray` o `XmlArrayItem` anziché `XmlElementAttribute`, oppure usando lo stile di parametro Wrapped".  
>   
>  Se si riceve tale eccezione, verificare se questa situazione è applicabile.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non supporta gli attributi <xref:System.Xml.Serialization.SoapIncludeAttribute> e <xref:System.Xml.Serialization.XmlIncludeAttribute> nei contratti di messaggio e di operazione, pertanto è necessario usare l'attributo <xref:System.Runtime.Serialization.KnownTypeAttribute>.  
  
## Tipi che implementano l'interfaccia IXmlSerializable  
 I tipi che implementano l'interfaccia `IXmlSerializable` sono completamente supportati da `DataContractSerializer`. L'attributo <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> deve essere applicato sempre a questi tipi per controllarne lo schema.  
  
> [!WARNING]
>  Se si serializzano dei tipi polimorfici è necessario applicare a tali tipi l'attributo <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> per assicurare che venga serializzato il tipo corretto.  
  
 Esistono tre varietà di tipi che implementano `IXmlSerializable`: i tipi che rappresentano contenuto arbitrario, i tipi che rappresentano un singolo elemento e i tipi <xref:System.Data.DataSet> legacy.  
  
-   I tipi di contenuto usano un metodo del provider dello schema specificato dall'attributo `XmlSchemaProviderAttribute`. Il metodo non restituisce `null` e la proprietà <xref:System.Xml.Serialization.XmlSchemaProviderAttribute.IsAny%2A> dell'attributo mantiene il valore predefinito `false`. Si tratta dell'utilizzo più comune di tipi `IXmlSerializable`.  
  
-   I tipi di elemento vengono usati quando un tipo `IXmlSerializable` deve controllare il nome del relativo elemento radice. Per contrassegnare un tipo come tipo di elemento, impostare la proprietà <xref:System.Xml.Serialization.XmlSchemaProviderAttribute.IsAny%2A> dell'attributo <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> su `true` o fare in modo che il metodo del provider dello schema restituisca `null`. Il metodo del provider dello schema è facoltativo per i tipi di elemento; è infatti possibile specificare `null` anziché il nome del metodo in `XmlSchemaProviderAttribute`. Tuttavia, se `IsAny` è `true` ed è specificato un metodo del provider dello schema, il metodo deve restituire `null`.  
  
-   I tipi <xref:System.Data.DataSet> legacy sono tipi `IXmlSerializable` non contrassegnati con l'attributo `XmlSchemaProviderAttribute`, che si basano sul metodo <xref:System.Xml.Serialization.IXmlSerializable.GetSchema%2A> per la generazione dello schema. Questo modello è usato per il tipo `DataSet` e le relative classi derivate del dataset tipizzato nelle versioni precedenti di .NET Framework, ma ora è obsoleto ed è supportato solo per elementi legacy. Non è consigliabile basarsi su questo modello, bensì applicare sempre `XmlSchemaProviderAttribute` ai tipi `IXmlSerializable`.  
  
### Tipi di contenuto IXmlSerializable  
 Quando si serializza un membro dati di un tipo che implementa `IXmlSerializable` e il tipo di contenuto rispecchia la definizione precedente, il serializzatore scrive l'elemento wrapper per il membro dati e passa il controllo al metodo <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A>. L'implementazione <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> può scrivere qualsiasi elemento XML e può anche aggiungere attributi all'elemento wrapper. Quando l'operazione `WriteXml` è stata completata, il serializzatore chiude l'elemento.  
  
 Quando si deserializza un membro dati di un tipo che implementa `IXmlSerializable` e il tipo di contenuto rispecchia la definizione precedente, il deserializzatore posiziona il lettore XML sull'elemento wrapper per il membro dati e passa il controllo al metodo <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A>. Il metodo deve leggere l'elemento intero, inclusi i tag di inizio e fine. Verificare che il codice `ReadXml` gestisca l'eventualità che l'elemento sia vuoto. Inoltre, l'implementazione `ReadXml` non deve basarsi sull'uso di un nome specifico per l'elemento wrapper, poiché il nome viene scelto dal serializzatore e quindi può variare.  
  
 È consentito assegnare tipi di contenuto `IXmlSerializable` in modo polimorfico, ad esempio, ai membri dati di tipo <xref:System.Object>. È inoltre consentito che le istanze del tipo siano Null. Infine, è possibile usare tipi `IXmlSerializable` con il mantenimento dell'oggetto grafico abilitato e con <xref:System.Runtime.Serialization.NetDataContractSerializer>. Tutte queste funzionalità richiedono che il serializzatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] inserisca determinati attributi nell'elemento wrapper \("nil" e "type" nello spazio dei nomi dell'istanza di XML Schema e "Id", "Ref", "Type" e "Assembly" in uno spazio dei nomi specifico per [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\).  
  
#### Attributi da ignorare quando si implementa ReadXml  
 Prima di passare il controllo al codice `ReadXml`, il deserializzatore esamina l'elemento XML, rileva questi attributi XML speciali e interviene su di essi. Ad esempio, se "nil" è `true`, un valore Null viene deserializzato e `ReadXml` non viene chiamato. Se viene rilevato il polimorfismo, il contenuto dell'elemento viene deserializzato come se si trattasse di un tipo diverso. L'implementazione di `ReadXml` del tipo assegnato in modo polimorfico viene chiamata. In ogni caso, un'implementazione `ReadXml` deve ignorare questi attributi speciali poiché vengono gestiti dal deserializzatore.  
  
### Considerazioni sullo schema per i tipi di contenuto IXmlSerializable  
 Se si esporta lo schema e un tipo di contenuto `IXmlSerializable`, viene chiamato il metodo del provider dello schema. Al metodo del provider dello schema viene passata una classe <xref:System.Xml.Schema.XmlSchemaSet>. Il metodo può aggiungere qualsiasi schema valido al set di schemi. Il set di schemi contiene lo schema già conosciuto al momento dell'esportazione dello schema. Quando il metodo del provider dello schema deve aggiungere un elemento al set di schemi, deve determinare se esiste una classe <xref:System.Xml.Schema.XmlSchema> con lo spazio dei nomi appropriato nel set. In tal caso, il metodo del provider dello schema deve aggiungere il nuovo elemento alla classe `XmlSchema` esistente. In caso contrario, deve creare una nuova istanza di `XmlSchema`. Questo è importante se vengono usate matrici di tipi `IXmlSerializable`. Ad esempio, se un tipo `IXmlSerializable` viene esportato come tipo "A" nello spazio dei nomi "B", è possibile che quando il metodo del provider dello schema viene chiamato il set di schemi contenga già lo schema per "B" che contiene il tipo "ArrayOfA".  
  
 Oltre ad aggiungere i tipi nella classe <xref:System.Xml.Schema.XmlSchemaSet>, il metodo del provider dello schema per i tipi di contenuto deve restituire un valore diverso da Null. Può restituire un oggetto <xref:System.Xml.XmlQualifiedName> che specifica il nome del tipo di schema da usare per il tipo `IXmlSerializable` specificato. Questo nome completo serve anche come nome e spazio dei nomi del contratto dati per il tipo. È consentito restituire un tipo che non esiste nel set di schemi quando il metodo del provider di schema viene restituito. Tuttavia, in genere al momento dell'esportazione di tutti i tipi correlati \(il metodo <xref:System.Runtime.Serialization.XsdDataContractExporter.Export%2A> viene chiamato per tutti i tipi attinenti su <xref:System.Runtime.Serialization.XsdDataContractExporter> e si accede alla proprietà <xref:System.Runtime.Serialization.XsdDataContractExporter.Schemas%2A>\) il tipo esiste già nel set di schemi. L'accesso alla proprietà `Schemas` prima che tutte le chiamate `Export` attinenti siano state effettuate può generare un'eccezione <xref:System.Xml.Schema.XmlSchemaException>.[!INCLUDE[crabout](../../../../includes/crabout-md.md)]l processo di esportazione, vedere [Esportazione di schemi dalle classi](../../../../docs/framework/wcf/feature-details/exporting-schemas-from-classes.md).  
  
 Il metodo del provider dello schema può restituire anche l'oggetto <xref:System.Xml.Schema.XmlSchemaType> da usare. Il tipo può o meno essere anonimo. Se è anonimo, lo schema per il tipo `IXmlSerializable` viene esportato come tipo anonimo ogni volta che il tipo `IXmlSerializable` viene usato come membro dati. Il tipo `IXmlSerializable` ha ancora un nome e uno spazio dei nomi del contratto dati Questo aspetto viene determinato in base a quanto descritto in [Nomi di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-names.md), ad eccezione del fatto che l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> non può essere usato per personalizzare il nome. Se non è anonimo, deve essere uno dei tipi in `XmlSchemaSet`. Questo caso è equivalente alla restituzione del `XmlQualifiedName` del tipo.  
  
 Inoltre, viene esportata una dichiarazione di elemento globale per il tipo. Se al tipo non è applicato l'attributo <xref:System.Xml.Serialization.XmlRootAttribute>, l'elemento ha lo stesso nome e spazio dei nomi del contratto dati e la proprietà "nillable" sarà `true`. L'unica eccezione a questo comportamento è costituito dallo spazio dei nomi dello schema \("http:\/\/www.w3.org\/2001\/XMLSchema"\), ovvero se il contratto dati del tipo è incluso in questo spazio dei nomi, l'elemento globale corrispondente si trova nello spazio dei nomi vuoto perché non è consentito aggiungere elementi nuovi allo spazio dei nomi dello schema. Se al tipo è applicato l'attributo `XmlRootAttribute`, la dichiarazione di elemento globale viene esportata usando le proprietà <xref:System.Xml.Serialization.XmlRootAttribute.ElementName%2A>, <xref:System.Xml.Serialization.XmlRootAttribute.Namespace%2A> e <xref:System.Xml.Serialization.XmlRootAttribute.IsNullable%2A>. L'impostazione predefinita quando è applicato l'attributo `XmlRootAttribute` è costituita dal nome del contratto dati, da un spazio dei nomi vuoto e da un valore "nillable" impostato su `true`.  
  
 Le stesse regole della dichiarazione di elemento globale si applicano ai tipi di dataset legacy. Si noti che `XmlRootAttribute` non può eseguire l'override delle dichiarazioni di elemento globale aggiunte tramite codice personalizzato o aggiunte a `XmlSchemaSet` usando il metodo del provider dello schema o tramite `GetSchema` per i tipi di dataset legacy.  
  
### Tipi di elemento IXmlSerializable  
 I tipi di elemento `IXmlSerializable` hanno la proprietà `IsAny` impostata su `true` o il relativo metodo del provider dello schema restituisce `null`.  
  
 La serializzazione e deserializzazione di un tipo di elemento è molto simile alla serializzazione e deserializzazione di un tipo di contenuto. Esistono tuttavia alcune importanti differenze:  
  
-   Si presuppone che l'implementazione `WriteXml` scriva un solo elemento \(che può ovviamente contenere più elementi figlio\). Non deve scrivere attributi all'esterno di questo singolo elemento, più elementi di pari livello o contenuto misto. L'elemento può essere vuoto.  
  
-   L'implementazione `ReadXml` non deve leggere l'elemento wrapper, bensì deve leggere l'unico elemento prodotto da `WriteXml`.  
  
-   Quando si serializza regolarmente un tipo di elemento \(ad esempio, come un membro dati in un contratto dati\), il serializzatore restituisce un elemento wrapper prima di chiamare `WriteXml`, come per i tipi di contenuto. Tuttavia, quando si serializza un tipo di elemento al primo livello, il serializzatore in genere non restituisce un elemento wrapper per l'elemento scritto da `WriteXml`, a meno che un nome e uno spazio dei nomi radice vengano specificati in modo esplicito durante la creazione del serializzatore nei costruttori `DataContractSerializer` o `NetDataContractSerializer`.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Serializzazione e deserializzazione](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md).  
  
-   Quando si serializza un tipo di elemento al primo livello senza specificare il nome e lo spazio dei nomi radice in fase di costruzione, i metodi <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteStartObject%2A> e <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteEndObject%2A> essenzialmente non eseguono alcuna operazione e il metodo <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteObjectContent%2A> chiama `WriteXml`. In questo caso, l'oggetto serializzato non può essere `null` e non può essere assegnato in modo polimorfico. Inoltre, il mantenimento dell'oggetto grafico non può essere abilitato e `NetDataContractSerializer` non può essere usato.  
  
-   Quando si deserializza un tipo di elemento al primo livello senza specificare il nome e lo spazio dei nomi radice in fase di costruzione, il metodo <xref:System.Runtime.Serialization.XmlObjectSerializer.IsStartObject%2A> restituisce `true` se riesce a trovare l'inizio di qualsiasi elemento.<xref:System.Runtime.Serialization.XmlObjectSerializer.ReadObject%2A> con il parametro `verifyObjectName` impostato su `true` si comporta allo stesso modo di `IsStartObject` prima di leggere effettivamente l'oggetto.`ReadObject` passa quindi il controllo al metodo `ReadXml`.  
  
 Lo schema esportato per i tipi di elemento è lo stesso del tipo `XmlElement`, come illustrato in una sezione precedente, con l'eccezione che il metodo del provider dello schema può aggiungere qualsiasi altro schema a <xref:System.Xml.Schema.XmlSchemaSet> come con i tipi di contenuto. L'uso dell'attributo `XmlRootAttribute` con i tipi di elemento non è consentito e le dichiarazioni di elemento globale non vengono mai generate per questi tipi.  
  
### Differenze rispetto a XmlSerializer  
 L'interfaccia `IXmlSerializable` e gli attributi `XmlSchemaProviderAttribute` e `XmlRootAttribute` vengono riconosciuti anche da <xref:System.Xml.Serialization.XmlSerializer>. Tuttavia, esistono alcune differenze nel modo in cui questi elementi vengono gestiti nel modello del contratto dati. Le differenze più importanti sono riepilogate nell'elenco seguente:  
  
-   Il metodo del provider dello schema deve essere pubblico per poter essere usato in `XmlSerializer`, ma non deve essere pubblico per poter essere usato nel modello del contratto dati.  
  
-   Il metodo del provider dello schema viene chiamato quando `IsAny` è `true` nel modello del contratto dati, ma non con `XmlSerializer`.  
  
-   Quando l'attributo `XmlRootAttribute` non è presente per contenuto o i tipi di dataset legacy, `XmlSerializer` esporta una dichiarazione di elemento globale nello spazio dei nomi vuoto. Nel modello del contratto dati, lo spazio dei nomi usato è in genere lo spazio dei nomi del contratto dati, come descritto in precedenza.  
  
 Tenere presenti queste differenze durante la creazione di tipi che vengono usati con entrambe le tecnologie di serializzazione.  
  
### Importazione dello schema IXmlSerializable  
 Quando si importa uno schema generato dai tipi `IXmlSerializable`, si verificano alcuni possibili scenari:  
  
-   Lo schema generato può essere uno schema valido del contratto dati, come descritto in [Riferimento allo schema del contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md). In questo caso, lo schema può essere importato normalmente e vengono generati tipi del contratto dati normali.  
  
-   Lo schema generato può non essere uno schema valido del contratto dati. Ad esempio, il metodo del provider dello schema può generare lo schema coinvolgendo gli attributi XML che non sono supportati nel modello del contratto dati. In questo caso, è possibile importare lo schema come tipi `IXmlSerializable`. Questa modalità di importazione non è attiva per impostazione predefinita, ma può essere abilitata facilmente, ad esempio con l'opzione della riga di comando `/importXmlTypes` in [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md). Questo aspetto viene descritto dettagliatamente in [Importazione dello schema per generare classi](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md). Si noti che è necessario interagire direttamente con XML per le istanze del tipo. Si può anche scegliere di usare una tecnologia di serializzazione diversa che supporti una gamma più ampia di schemi \(vedere l'argomento relativo all'uso di `XmlSerializer`\).  
  
-   Può essere necessario riusare i tipi `IXmlSerializable` esistenti nel proxy anziché generare tipi nuovi. In questo caso, è possibile usare la funzionalità dei tipi a cui è stato fatto riferimento descritta nell'argomento relativo all'importazione dello schema per generare i tipi per indicare il tipo da riusare. Questa procedura corrisponde all'uso dell'opzione `/reference` in svcutil.exe, che specifica l'assembly contenente i tipi da riutilizzare.  
  
### Comportamento legacy di XmlSerializer  
 In .NET Framework 4.0 e versioni precedenti, XmlSerializer generava assembly di serializzazione temporanei scrivendo codice C\# in un file. Il file veniva quindi compilato in un assembly.  Questo comportamento implicava alcune conseguenze indesiderate, ad esempio l'aumento del tempo di avvio del serializzatore. In .NET Framework 4.5 questo comportamento è stato modificato in modo da generare assembly senza richiedere l'uso del compilatore. Alcuni sviluppatori potrebbero voler visualizzare il codice C\# generato. È possibile specificare di usare questo comportamento legacy tramite la configurazione seguente:  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.xml.serialization>  
    <xmlSerializer tempFilesLocation='e:\temp\XmlSerializerBug' useLegacySerializerGeneration="true" />  
  </system.xml.serialization>  
  <system.diagnostics>  
    <switches>  
      <add name="XmlSerialization.Compilation" value="1" />  
    </switches>  
  </system.diagnostics>  
</configuration>  
  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.DataContractFormatAttribute>   
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Xml.Serialization.XmlSerializer>   
 <xref:System.ServiceModel.MessageHeaderArrayAttribute>   
 [Specifica del trasferimento di dati nei contratti di servizio](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)   
 [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)   
 [Procedura: migliorare il tempo di avvio di applicazioni client WCF utilizzando XmlSerializer](../../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)