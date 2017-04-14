---
title: "Linee guida relative alla serializzazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "serializzazione binaria, linee guida"
  - "serializzazione, linee guida"
ms.assetid: ebbeddff-179d-443f-bf08-9c373199a73a
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Linee guida relative alla serializzazione
In questo documento vengono elencate le linee guida da tenere presenti quando si progetta un'API da serializzare.  
  
 In .NET Framework sono disponibili tre tecnologie di serializzazione principali ottimizzate per vari scenari di serializzazione.Nella tabella seguente vengono elencate tali tecnologie e vengono indicati i principali tipi .NET Framework correlati.  
  
|Tecnologia|Classi rilevanti|Note|  
|----------------|----------------------|----------|  
|Serializzazione dei contratti dati|<xref:System.Runtime.Serialization.DataContractAttribute><br /><br /> <xref:System.Runtime.Serialization.DataMemberAttribute><br /><br /> <xref:System.Runtime.Serialization.DataContractSerializer><br /><br /> <xref:System.Runtime.Serialization.NetDataContractSerializer><br /><br /> <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer><br /><br /> <xref:System.Runtime.Serialization.ISerializable>|Persistenza generale<br /><br /> Servizi Web<br /><br /> JSON|  
|Serializzazione XML|<xref:System.Xml.Serialization.XmlSerializer>|Formato XML <br />con controllo completo|  
|Serializzazione di runtime \(binaria e SOAP\)|<xref:System.SerializableAttribute><br /><br /> <xref:System.Runtime.Serialization.ISerializable><br /><br /> <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter><br /><br /> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>|Servizi remoti .NET|  
  
 Quando si progettano nuovi tipi, è necessario determinare le eventuali tecnologie che devono essere supportate da tali tipi.Le linee guida seguenti descrivono come effettuare la scelta e come fornire tale supporto.È importante tenere presente che queste linee guida non hanno lo scopo di indicare la tecnologia di serializzazione da utilizzare nell'implementazione dell'applicazione o della libreriapoiché non sono correlate direttamente alla progettazione dell'API e pertanto esulano dall'ambito di questo argomento.  
  
## Linee guida  
  
-   Prendere in seria considerazione la serializzazione quando si progettano nuovi tipi.  
  
     La serializzazione è un aspetto importante della progettazione per qualsiasi tipo poiché è possibile che i programmi debbano rendere persistenti o trasmettere istanze del tipo.  
  
### Scelta della tecnologia di serializzazione corretta da supportare  
 Un tipo specifico può supportare nessuna, una o più tecnologie di serializzazione.  
  
-   Considerare il supporto della *serializzazione dei contratti dati* se è necessario rendere persistenti o utilizzare in servizi Web istanze del tipo.  
  
-   Considerare il supporto della *serializzazione XML* al posto di o in aggiunta alla serializzazione del contratto dati se è necessario disporre di maggiore controllo sul formato XML creato quando il tipo viene serializzato.  
  
     Questo aspetto può essere necessario in alcuni scenari di interoperabilità in cui è necessario utilizzare un costrutto XML non supportato dalla serializzazione dei contratti dati, ad esempio per creare attributi XML.  
  
-   Considerare il supporto della *serializzazione di runtime* se è necessario utilizzare istanze del tipo all'esterno dei servizi remoti .NET.  
  
-   Evitare il supporto della serializzazione runtime o XML per motivi di persistenza generalee dare la preferenza alla serializzazione dei contratti dati.  
  
#### Supporto della serializzazione dei contratti dati  
 Affinché i tipi supportino la serializzazione dei contratti dati, è necessario applicare l'elemento **DataContractAttribute** e l'elemento **DataMemberAttribute** ai membri \(campi e proprietà\) del tipo.  
  
 [!code-csharp[SerializationGuidelines#1](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#1)]
 [!code-vb[SerializationGuidelines#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#1)]  
  
1.  Contrassegnare i membri dati del tipo come pubblici se il tipo può essere utilizzato in condizioni di attendibilità parziale.In condizioni di attendibilità totale i serializzatori dei contratti dati possono serializzare e deserializzare anche tipi e membri non pubblici, mentre in condizioni di attendibilità parziale possono essere serializzati o deserializzati solo i membri pubblici.  
  
2.  Implementare un metodo Getter e Setter su tutte le proprietà che dispongono di un elemento Data\-MemberAttribute.Affinché il tipo possa essere considerato serializzabile, i serializzatori dei contratti dati richiedono entrambi i metodi.Se il tipo non verrà utilizzato in condizioni di attendibilità parziale, è possibile che una o entrambe le funzioni di accesso alle proprietà non siano pubbliche.  
  
     [!code-csharp[SerializationGuidelines#2](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#2)]
     [!code-vb[SerializationGuidelines#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#2)]  
  
3.  Utilizzare i callback di serializzazione per l'inizializzazione di istanze deserializzate.  
  
     Poiché i costruttori non vengono chiamati quando gli oggetti sono deserializzati,qualsiasi logica eseguita durante la costruzione normale deve essere implementata come uno dei *callback di serializzazione*.  
  
     [!code-csharp[SerializationGuidelines#3](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#3)]
     [!code-vb[SerializationGuidelines#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#3)]  
  
     L'oggetto <xref:System.Runtime.Serialization.OnDeserializedAttribute> è l'attributo di callback più comunemente utilizzato.Gli altri attributi della famiglia sono <xref:System.Runtime.Serialization.OnDeserializingAttribute>, <xref:System.Runtime.Serialization.OnSeralizingAttribute> e <xref:System.Runtime.Serialization.OnSerializedAttribute>.Tali attributi possono essere utilizzati rispettivamente per contrassegnare callback eseguiti prima della deserializzazione, prima della serializzazione e dopo la serializzazione.  
  
4.  Considerare l'utilizzo di <xref:System.Runtime.Serialization.KnownTypeAttribute> per indicare tipi concreti da utilizzare in caso di deserializzazione di un oggetto grafico complesso.  
  
     Se ad esempio un tipo di un membro dati deserializzato viene rappresentato da una classe astratta, sarà necessario specificare le informazioni sul *tipo noto* affinché il serializzatore sia in grado di decidere il tipo concreto per cui creare un'istanza e da assegnare al membro.Se il tipo noto non viene specificato tramite l'attributo, dovrà essere passato in modo esplicito al serializzatore, ad esempio passando tipi noti al costruttore relativo, o dovrà essere specificato nel file di configurazione.  
  
     [!code-csharp[SerializationGuidelines#4](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#4)]
     [!code-vb[SerializationGuidelines#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#4)]  
  
     Nei casi in cui l'elenco di tipi noti non sia conosciuto staticamente \(quando la classe **Person** è compilata\), l'elemento **KnownTypeAttribute** può puntare anche a un metodo che restituisce un elenco di tipi noti in fase di esecuzione.  
  
5.  Prendere in considerazione la compatibilità con le versioni precedenti e successive quando si creano o si modificano tipi serializzabili.  
  
     Tenere presente che i flussi serializzati di versioni future del tipo possono essere deserializzati nella versione corrente del tipo e viceversa.È importante comprendere che nelle versioni future del tipo non è possibile modificare il nome, il tipo o l'ordine dei membri dati, anche privati e interni, a meno che non si presti particolare attenzione a mantenere il contratto utilizzando parametri espliciti per gli attributi del contratto dati. Quando si apportano modifiche ai tipi serializzabili, testare la compatibilità della serializzazione,provando ad esempio a deserializzare la nuova versione in una versione precedente e viceversa.  
  
6.  Considerare l'implementazione dell'interfaccia <xref:System.Runtime.Serialization.IExtensibleDataObject> per consentire le sequenze di andata e ritorno tra versioni diverse del tipo.  
  
     L'interfaccia consente al serializzatore di verificare che durante le sequenze di andata e ritorno non venga perso alcun dato.Nella proprietà <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> vengono archiviati tutti i dati della versione futura del tipo non conosciuto nella versione corrente.Successivamente, quando la versione corrente viene serializzata e deserializzata in una versione futura, i dati aggiuntivi saranno disponibili nel flusso serializzato tramite il valore della proprietà **ExtensionData**.  
  
     [!code-csharp[SerializationGuidelines#5](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#5)]
     [!code-vb[SerializationGuidelines#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#5)]  
  
     Per ulteriori informazioni, vedere [Contratti dati compatibili con versioni successive](../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md).  
  
#### Supporto della serializzazione XML  
 La serializzazione dei contratti dati è la tecnologia di serializzazione principale e predefinita in .NET Framework, anche se non supporta tutti gli scenari di serializzazione,ad esempio non consente di controllare completamente la forma del codice XML creato o utilizzato dal serializzatore.Se è richiesto un controllo così accurato, è necessario utilizzare la *serializzazione XML* nonché progettare i tipi in modo che supportino questa tecnologia di serializzazione.  
  
1.  Evitare di progettare in maniera specifica i tipi per la serializzazione XML, a meno che non sia presente un motivo estremamente valido per controllare la forma del codice XML creato.Questa tecnologia è stata sostituita dalla serializzazione dei contratti dati descritta nella sezione precedente.  
  
     In altre parole, non applicare attributi dallo spazio dei nomi <xref:System.Runtime.Serialization> ai nuovi tipi, a meno che non si sia certi che il tipo verrà utilizzato con la serializzazione XML.Nell'esempio seguente viene illustrato come è possibile utilizzare **System.Xml.Serialization** per controllare la forma del codice XML creato.  
  
     [!code-csharp[SerializationGuidelines#6](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#6)]
     [!code-vb[SerializationGuidelines#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#6)]  
  
2.  Considerare l'implementazione dell'interfaccia <xref:System.Xml.Serialization.IXmlSerializable> se si desidera maggiore controllo sulla forma del codice XML serializzato rispetto a quello offerto applicando gli attributi della serializzazione XML.Per controllare completamente il flusso XML serializzato, è possibile utilizzare due metodi dell'interfaccia, ovvero <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> e <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A>.È inoltre possibile controllare l'XML Schema generato per il tipo applicando l'attributo <xref:System.Xml.Serialization.XmlSchemaProviderAttribute>.  
  
#### Supporto della serializzazione di runtime  
 La *serializzazione di runtime* è una tecnologia utilizzata dai servizi remoti .NET.Se si ritiene che i tipi verranno trasportati utilizzando i servizi remoti .NET, è necessario verificare che supportino la serializzazione di runtime.  
  
 Il supporto di base per la *serializzazione di runtime* può essere fornito applicando l'attributo <xref:System.SerializableAttribute> e scenari più avanzati prevedono l'implementazione di un semplice *modello di runtime serializzabile* \(implementazione di <xref:System.Runtime.Serialization.ISerializable> e specifica di un costruttore di serializzazione\).  
  
1.  Considerare il supporto della serializzazione di runtime se i tipi verranno utilizzati con i servizi remoti .NET.Lo spazio dei nomi <xref:System.AddIn>, ad esempio, utilizza i servizi remoti .NET e pertanto tutti i tipi scambiati tra i componenti aggiuntivi **System.AddIn** devono supportare la serializzazione di runtime.  
  
     [!code-csharp[SerializationGuidelines#7](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#7)]
     [!code-vb[SerializationGuidelines#7](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#7)]  
  
2.  Considerare l'implementazione del *modello di runtime serializzabile* se si desidera il controllo completo sul processo di serializzazione,ad esempio se si desidera trasformare i dati quando vengono serializzati o deserializzati.  
  
     Il modello è molto semplice.È sufficiente implementare l'interfaccia **ISerializable** e specificare un costruttore speciale utilizzato quando l'oggetto viene deserializzato.  
  
     [!code-csharp[SerializationGuidelines#8](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#8)]
     [!code-vb[SerializationGuidelines#8](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#8)]  
  
3.  Creare il costruttore di serializzazione in modo protetto e specificare due parametri digitati e denominati esattamente come indicato nell'esempio.  
  
     [!code-csharp[SerializationGuidelines#9](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#9)]
     [!code-vb[SerializationGuidelines#9](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#9)]  
  
4.  Implementare i membri ISerializable in modo protetto.  
  
     [!code-csharp[SerializationGuidelines#10](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#10)]
     [!code-vb[SerializationGuidelines#10](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#10)]  
  
5.  Applicare una richiesta di collegamento all'implementazione di **ISerializable.GetObjectData**per garantire che solo un nucleo completamente attendibile e il serializzatore di runtime dispongano dell'accesso al membro.  
  
     [!code-csharp[SerializationGuidelines#11](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#11)]
     [!code-vb[SerializationGuidelines#11](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#11)]  
  
## Vedere anche  
 [Uso di contratti dati](../../../docs/framework/wcf/feature-details/using-data-contracts.md)   
 [Serializzatore dei contratti dati](../../../docs/framework/wcf/feature-details/data-contract-serializer.md)   
 [Tipi supportati dal serializzatore dei contratti dati](../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)   
 [Serializzazione binaria](../../../docs/framework/serialization/binary-serialization.md)   
 [Remote Objects](http://msdn.microsoft.com/it-it/515686e6-0a8d-42f7-8188-73abede57c58)   
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)   
 [Security and Serialization](../../../docs/framework/misc/security-and-serialization.md)