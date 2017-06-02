---
title: "Serialization1 | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: bebb27ac-9712-4196-9931-de19fc04dbac
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
---
# Serializzazione
La serializzazione è il processo di conversione di un oggetto in un formato che può essere facilmente mantenuto o trasportato. Ad esempio, è possibile serializzare un oggetto, trasferirlo via Internet tramite HTTP e la deserializzazione, il computer di destinazione.  
  
 .NET Framework sono disponibili tre tecnologie di serializzazione principali ottimizzate per vari scenari di serializzazione. Nella tabella seguente sono elencate queste tecnologie e i principali tipi di .NET Framework relativi a tali tecnologie.  
  
|**Nome tecnologia**|**Tipi principali**|**Scenari**|  
|-------------------------|-------------------------|-----------------|  
|**Serializzazione del contratto dati**|<xref:System.Runtime.Serialization.DataContractAttribute> <br /> <xref:System.Runtime.Serialization.DataMemberAttribute> <br /> <xref:System.Runtime.Serialization.DataContractSerializer> <br /> <xref:System.Runtime.Serialization.NetDataContractSerializer> <br /> <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> <br /> <xref:System.Runtime.Serialization.ISerializable>|Persistenza generale<br />servizi Web<br />JSON|  
|**Serializzazione XML**|<xref:System.Xml.Serialization.XmlSerializer>|Formato XML con il pieno controllo sulla forma del codice XML|  
|**Serializzazione di runtime \(binaria e SOAP\)**|<xref:System.SerializableAttribute> <br /> <xref:System.Runtime.Serialization.ISerializable> <br /> <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> <br /> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>|Servizi remoti .NET|  
  
 **✓ si** basti pensare a serializzazione quando si progettano nuovi tipi.  
  
## Scelta della tecnologia di serializzazione corretta per il supporto  
 **✓ PROVARE** supporto di serializzazione del contratto dati se le istanze del tipo potrebbe essere necessario rendere persistenti o utilizzare i servizi Web.  
  
 **✓ PROVARE** se è necessario un maggiore controllo sul formato XML che viene generato quando viene serializzato il tipo di supporto della serializzazione XML anziché o oltre a serializzazione del contratto dati.  
  
 Ciò potrebbe essere necessario in alcuni scenari in cui è necessario usare un file XML costruire l'interoperabilità che non è supportato dalla serializzazione del contratto dati, ad esempio, per creare attributi XML.  
  
 **✓ PROVARE** che supporta la serializzazione di Runtime se le istanze del tipo necessario attraversare i limiti di .NET Remoting.  
  
 **X evitare** supporto solo per motivi di persistenza generale di serializzazione di Runtime o la serializzazione XML. Invece serializzazione del contratto dati.  
  
## Supporto serializzazione del contratto dati  
 I tipi supportino la serializzazione del contratto dati applicando il <xref:System.Runtime.Serialization.DataContractAttribute> per il tipo e il <xref:System.Runtime.Serialization.DataMemberAttribute> ai membri \(campi e proprietà\) del tipo.  
  
 **✓ PROVARE** contrassegnare i membri di dati pubblico del tipo se il tipo può essere utilizzato in attendibilità parziale.  
  
 In attendibilità totale, serializzatori dei contratti dati possono serializzare e deserializzare tipi non pubblici e membri, ma solo i membri pubblici possono essere serializzati e deserializzati in attendibilità parziale.  
  
 **✓ si** implementare un getter e setter su tutte le proprietà che dispongono di <xref:System.Runtime.Serialization.DataMemberAttribute>. Serializzatori dei contratti dati richiedono entrambi il metodo Get e set per il tipo possa essere considerato serializzabile. \(In .NET Framework 3.5 SP1, alcune proprietà di raccolta è può essere solo get.\) Se il tipo non verranno usato in attendibilità parziale, una o entrambe le funzioni di accesso di proprietà può essere non pubblici.  
  
 **✓ PROVARE** utilizzando i callback di serializzazione per l'inizializzazione di istanze deserializzate.  
  
 I costruttori non vengono chiamati quando gli oggetti sono deserializzati. \(Sono presenti eccezioni alla regola. I costruttori di raccolte contrassegnati con <xref:System.Runtime.Serialization.CollectionDataContractAttribute> chiamato durante la deserializzazione.\) Pertanto, qualsiasi logica eseguita durante la costruzione normale deve essere implementata come uno dei callback di serializzazione.  
  
 `OnDeserializedAttribute` è l'attributo di callback più comunemente utilizzato. Gli altri attributi della famiglia di prodotti sono <xref:System.Runtime.Serialization.OnDeserializingAttribute>,  <xref:System.Runtime.Serialization.OnSerializingAttribute>, e <xref:System.Runtime.Serialization.OnSerializedAttribute>. Possono essere utilizzati per contrassegnare callback eseguiti prima della deserializzazione, prima della serializzazione e, infine, dopo la serializzazione, rispettivamente.  
  
 **✓ PROVARE** utilizzando il <xref:System.Runtime.Serialization.KnownTypeAttribute> per indicare tipi concreti che devono essere utilizzati quando si deserializza un oggetto grafico complesso.  
  
 **✓ si** prendere in considerazione di compatibilità durante la creazione o modifica dei tipi serializzabili.  
  
 Tenere presente che i flussi serializzati di versioni future del tipo può essere deserializzati nella versione corrente del tipo e viceversa.  
  
 Assicurarsi di comprendere che i membri dati, anche privati e interni, non possono modificare i relativi nomi, tipi o anche l'ordine nelle versioni future del tipo a meno che non particolare attenzione a mantenere il contratto utilizzando parametri espliciti per gli attributi di contratto dati.  
  
 Quando si apportano modifiche ai tipi serializzabili, testare la compatibilità della serializzazione. Tenta di deserializzare la nuova versione in una versione precedente e viceversa.  
  
 **✓ PROVARE** implementazione <xref:System.Runtime.Serialization.IExtensibleDataObject> per consentire sequenze di andata e ritorno tra versioni diverse del tipo.  
  
 L'interfaccia consente al serializzatore di verificare che venga perso alcun dato durante round trip. Il <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A?displayProperty=fullName> proprietà viene utilizzata per archiviare i dati della versione futura del tipo che è sconosciuto alla versione corrente e pertanto non può contenere membri dei propri dati. Quando la versione corrente viene successivamente serializzata e deserializzata in una versione futura, i dati aggiuntivi saranno inoltre disponibili nel flusso serializzato.  
  
## Supporto della serializzazione XML  
 Serializzazione del contratto dati è il principale \(impostazione predefinita\) la tecnologia di serializzazione in .NET Framework, ma sono disponibili scenari di serializzazione che non supporta la serializzazione del contratto dati. Ad esempio, non offre tuttavia il controllo completo sulla forma del codice XML creato o utilizzato dal serializzatore. Se è necessario un controllo così accurato, la serializzazione XML da utilizzare, ed è necessario progettare i tipi per supportare questa tecnologia di serializzazione.  
  
 **X evitare** la progettazione di tipi in modo specifico per la serializzazione XML, a meno che non esista un motivo molto sicuro per controllare la forma del codice XML generato. Questa tecnologia di serializzazione è stata sostituita da serializzazione del contratto dati illustrati nella sezione precedente.  
  
 **✓ PROVARE** che implementa il <xref:System.Xml.Serialization.IXmlSerializable> interfaccia se si desidera un maggiore controllo sulla forma del codice XML serializzato rispetto a quello offerto applicando gli attributi di serializzazione XML. Due metodi dell'interfaccia, <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> e <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A>, consentono di controllare completamente il flusso XML serializzato. È inoltre possibile controllare lo schema XML generato per il tipo applicando il `XmlSchemaProviderAttribute`.  
  
## Supporto della serializzazione di Runtime  
 Serializzazione di runtime è una tecnologia utilizzata da .NET Remoting. Se si ritiene che i tipi verranno trasportati utilizzando i servizi remoti .NET, è necessario assicurarsi che supportano la serializzazione di Runtime.  
  
 Il supporto di base per la serializzazione di Runtime può essere fornito applicando il <xref:System.SerializableAttribute>, e scenari più avanzati prevedono l'implementazione di un semplice modello di Runtime serializzabile \(implementa <xref:System.Runtime.Serialization.ISerializable> e fornire il costruttore di serializzazione\).  
  
 **✓ PROVARE** che supportano la serializzazione di Runtime se verranno utilizzati i tipi con .NET Remoting. Ad esempio, il <xref:System.AddIn?displayProperty=fullName> dello spazio dei nomi viene utilizzato .NET Remoting e pertanto tutti i tipi scambiati tra `System.AddIn` componenti aggiuntivi necessari per supportare la serializzazione di Runtime.  
  
 **✓ PROVARE** che implementa il modello di Runtime serializzabile se si desidera che il controllo completo sul processo di serializzazione. Ad esempio, se si desidera trasformare i dati come ottiene serializzato o deserializzato.  
  
 Il modello è molto semplice. È sufficiente per implementare la <xref:System.Runtime.Serialization.ISerializable> l'interfaccia e fornire un costruttore speciale utilizzato quando l'oggetto viene deserializzato.  
  
 **✓ si** rendere il costruttore di serializzazione protetto e specificare due parametri digitati e denominati esattamente come illustrato nell'esempio di seguito.  
  
```  
[Serializable]  
public class Person : ISerializable {  
    protected Person(SerializationInfo info, StreamingContext context) {  
        ...  
    }  
}  
```  
  
 **✓ si** implementare il `ISerializable` membri in modo esplicito.  
  
 **✓ si** si applicano a una richiesta di collegamento <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> implementazione. Ciò garantisce che solo completamente attendibile principale e il serializzatore di Runtime dispongano dell'accesso al membro.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Linee guida di utilizzo](../../../docs/standard/design-guidelines/usage-guidelines.md)