---
title: "Introduzione alla serializzazione XML | Microsoft Docs"
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
  - "DataSet (classe), serializzazione"
  - "ICollection (interfaccia), serializzazione"
  - "serializzazione, informazioni sulla serializzazione"
  - "XML (schema), serializzazione"
  - "serializzazione XML, informazioni sulla serializzazione XML"
  - "XmlSerializer (classe), serializzazione"
ms.assetid: 8c63200d-db63-4a03-a93d-21641623df62
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Introduzione alla serializzazione XML
La serializzazione è il processo di conversione di un oggetto in un formato che può essere agevolmente trasportato.Ad esempio, è possibile serializzare un oggetto e trasferirlo via Internet tramite protocollo HTTP tra un client e un server.Viceversa, la deserializzazione ricostruisce l'oggetto dal flusso.  
  
 La serializzazione XML serializza solo i campi pubblici e i valori di proprietà di un oggetto in un flusso XML.La serializzazione XML non include informazioni sul tipo.Se ad esempio si dispone di un oggetto **Book** che esiste nello spazio dei nomi **Library**, non c'è nessuna garanzia che venga deserializzato in un oggetto dello stesso tipo.  
  
> [!NOTE]
>  La serializzazione XML non converte metodi, indicizzatori o proprietà in sola lettura \(salvo le raccolte in sola lettura\).Per serializzare tutti i campi e le proprietà di un oggetto, pubblici e privati, utilizzare <xref:System.Runtime.Serialization.DataContractSerializer> invece della serializzazione XML.  
  
 La classe centrale nella serializzazione XML è la classe [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx) e i metodi più importanti in questa classe sono i metodi **Serialize** e **Deserialize**.La classe <xref:System.Xml.Serialization.XmlSerializer> crea file C\# e li compila in file dll per eseguire tale serializzazione.In .NET Framework 2.0, [Strumento per la generazione di serializzatori XML \(Sgen.exe\)](../../../docs/framework/serialization/xml-serializer-generator-tool-sgen-exe.md) è progettato per generare precedentemente tali assembly di serializzazione consentendone la distribuzione con l'applicazione e migliorando le prestazioni di avvio.Il flusso XML generato dalla classe **XmlSerializer** è conforme ai requisiti del World Wide Web Consortium \(www.w3.org\) relativi alla versione 1.0 di XSD \(XML Schema Definition\).Inoltre, i tipi di dati generati sono conformi al documento intitolato "XML Schema Part 2: Datatypes".  
  
 I dati negli oggetti sono descritti tramite costrutti del linguaggio di programmazione come classi, campi, proprietà, tipi primitivi, matrici, nonché XML incorporati sotto forma di oggetti **XmlElement** o **XmlAttribute**.È possibile creare le classi, annotate con attributi, o utilizzare lo strumento XML Schema Definition per generare le classi basate su uno schema XML esistente.  
  
 Se si dispone di uno schema XML, è possibile eseguire lo strumento XML Schema Definition per generare un set di classi fortemente tipizzate rispetto allo schema e annotate con attributi.Quando viene serializzata un'istanza di tale classe, l'XML generato è conforme allo schema XML.Con l'utilizzo di tale classe, è possibile effettuare la programmazione rispetto a un modello a oggetti facilmente modificato essendo certi che l'XML generato sia conforme allo schema XML.Si tratta di un'alternativa all'utilizzo di altre classi in .NET Framework, ad esempio le classi **XmlReader** e **XmlWriter**, per analizzare e scrivere un flusso XML.Per ulteriori informazioni, vedere [Documenti e dati XML](../../../docs/standard/data/xml/index.md).Queste classi consentono di analizzare qualsiasi flusso XML.Viceversa, utilizzare la classe **XmlSerializer** quando si prevede che il flusso XML sia conforme a uno schema XML noto.  
  
 Gli attributi controllano il flusso XML generato dalla classe **XmlSerializer**, consentendo di impostare lo spazio dei nomi XML, il nome dell'elemento, il nome di attributo e altri elementi del flusso XML.Per ulteriori informazioni su tali attributi e sulle loro modalità di controllo della serializzazione XML, vedere [Controllo della serializzazione XML mediante attributi](../../../docs/framework/serialization/controlling-xml-serialization-using-attributes.md).Per una tabella degli attributi utilizzati per controllare l'XML generato, vedere [Attributi per il controllo della serializzazione XML](../../../docs/framework/serialization/attributes-that-control-xml-serialization.md).  
  
 La classe **XmlSerializer** può serializzare ulteriormente un oggetto e può generare un flusso XML con codifica SOAP.L'elemento XML generato risulta conforme alla sezione 5 del documento "Simple Object Access Protocol \(SOAP\) 1.1" del World Wide Web Consortium. Per ulteriori informazioni su questo processo, vedere [Procedura: serializzare un oggetto come flusso XML con codifica SOAP](../../../docs/framework/serialization/how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md).Per una tabella degli attributi che controllano l'XML generato, vedere [Attributi per il controllo della serializzazione SOAP codificata](../../../docs/framework/serialization/attributes-that-control-encoded-soap-serialization.md).  
  
 La classe **XmlSerializer** genera i messaggi SOAP creati dai e passati ai servizi Web XML.Per controllare i messaggi SOAP, è possibile applicare attributi alle classi, ai valori restituiti, ai parametri e ai campi trovati in un file del servizio Web XML \(.asmx\).È possibile utilizzare entrambi gli attributi elencati in "Attributi per il controllo della serializzazione XML" e "Attributi per il controllo della serializzazione SOAP codificata", dal momento che un servizio Web XML può utilizzare sia lo stile SOAP letterale che quello codificato.Per ulteriori informazioni sull'utilizzo di tali attributi per il controllo dell'XML generato da un servizio Web XML, vedere [Serializzazione XML con Servizi Web XML](../../../docs/framework/serialization/xml-serialization-with-xml-web-services.md).Per ulteriori informazioni su SOAP e sui servizi Web XML, vedere [Customizing SOAP Messages](http://msdn.microsoft.com/it-it/1d777288-c0d9-4e6a-b638-f010da031952).  
  
## Considerazioni sulla sicurezza per le applicazioni XmlSerializer  
 Durante la creazione di un'applicazione che utilizza la classe **XmlSerializer**, tenere in considerazione i seguenti aspetti e le relative implicazioni:  
  
-   La classe **XmlSerializer** crea file C\# \(.cs\) e li compila in file dll nella directory denominata dalla variabile di ambiente TEMP; la serializzazione si verifica con tali file dll.  
  
    > [!NOTE]
    >  Questi assembly di serializzazione possono essere generati in anticipo ed essere firmati tramite lo strumento SGen.exe.Tale funzione non è disponibile per i server di servizi Web.In altre parole, è disponibile solo per l'utilizzo client e per la serializzazione manuale.  
  
     Il codice e le DLL sono vulnerabili a un processo dannoso al momento della creazione e della compilazione.Se si utilizza un computer su cui è in esecuzione Microsoft Windows NT 4.0 o versioni successive, è possibile che due o più utenti condividano la directory TEMP.La condivisione di una directory TEMP risulta pericolosa se i due account dispongono di privilegi di sicurezza diversi e se l'account con privilegi più elevati esegue un'applicazione utilizzando **XmlSerializer**.In tal caso, un utente può compromettere la sicurezza del computer sostituendo il file cs o dll compilato.Per ovviare a questo problema, accertarsi sempre che ciascun account del computer disponga del proprio profilo.Per impostazione predefinita, la variabile di ambiente TEMP fa riferimento a una directory diversa per ciascun account.  
  
-   Se un utente malintenzionato invia un flusso continuo di dati XML a un server Web \(un attacco di tipo Denial of Service\), **XmlSerializer** continua a elaborare i dati fino all'esaurimento delle risorse del computer.  
  
     Questo tipo di attacco può essere impedito se si utilizza un computer su cui è in esecuzione Internet Information Services \(IIS\) e l'applicazione è in esecuzione all'interno di IIS.IIS dispone di un modulo di verifica che non elabora i flussi maggiori di una determinata dimensione \(l'impostazione predefinita è 4 KB\).Se si crea un'applicazione che non utilizza IIS e che esegue la deserializzazione con **XmlSerializer**, è necessario implementare una modulo di verifica simile che impedisca un attacco Denial of Service.  
  
-   **XmlSerializer** serializza i dati ed esegue qualsiasi codice utilizzando qualsiasi tipo fornito.  
  
     Un oggetto non autorizzato può presentare una minaccia in due modi.L'oggetto può avere eseguito codice dannoso o può avere inserito codice dannoso nel file C\# creato da **XmlSerializer**.Nel primo caso, se un oggetto non autorizzato tenta di eseguire una procedura distruttiva, la sicurezza di accesso al codice consente di impedire eventuali danni.Nel secondo caso, esiste una possibilità teorica che un oggetto non autorizzato possa inserire in qualche modo del codice nel file C\# creato da **XmlSerializer**.Sebbene questo problema sia stato esaminato in modo approfondito e tale attacco è considerato improbabile, è necessario prendere la precauzione di non serializzare mai dati con un tipo ignoto e non attendibile.  
  
-   I dati sensibili serializzati potrebbero essere vulnerabili.  
  
     Successivamente alla serializzazione dei dati da parte di **XmlSerializer**, i dati possono essere archiviati come file XML o come altro archivio dati.Se l'archivio dati è disponibile per altri processi o è visibile su una Intranet o Internet, i dati possono essere rubati e utilizzati in modo dannoso.Ad esempio, se si crea un'applicazione che serializza ordini che includono numeri di carta di credito, i dati risultano essere estremamente riservati.Per evitare ciò, proteggere sempre l'archivio per i dati ed eseguire le operazioni per mantenerli privati.  
  
## Serializzazione di una classe semplice  
 Nell'esempio di codice riportato di seguito viene mostrata una classe di base con un campo pubblico.  
  
```vb  
Public Class OrderForm  
    Public OrderDate As DateTime  
End Class  
  
```  
  
```csharp  
public class OrderForm  
{  
    public DateTime OrderDate;  
}  
```  
  
 Quando un'istanza di questa classe viene serializzata, potrebbe assomigliare agli elementi seguenti.  
  
```  
<OrderForm>  
    <OrderDate>12/12/01</OrderDate>  
</OrderForm>  
```  
  
 Per ulteriori esempi di serializzazione, vedere [Esempi di serializzazione XML](../../../docs/framework/serialization/examples-of-xml-serialization.md).  
  
## Elementi che possono essere serializzati  
 I seguenti elementi possono essere serializzati utilizzando la classe **XmLSerializer**:  
  
-   Proprietà di lettura\/scrittura pubbliche e campi di classi pubbliche.  
  
-   Classi che implementano **ICollection** o **IEnumerable**.  
  
    > [!NOTE]
    >  Vengono serializzate solo le raccolte e non le proprietà pubbliche.  
  
-   Oggetti **XmlElement**.  
  
-   Oggetti **XmlNode**.  
  
-   Oggetti **DataSet**.  
  
 Per ulteriori informazioni sulla serializzazione o deserializzazione degli oggetti, vedere [Procedura: serializzare un oggetto](../../../docs/framework/serialization/how-to-serialize-an-object.md) e [Procedura: deserializzare un oggetto](../../../docs/framework/serialization/how-to-deserialize-an-object.md).  
  
## Vantaggi dell'utilizzo della serializzazione XML  
 La classe **XmlSerializer** fornisce il controllo completo e flessibile durante la serializzazione di un oggetto come XML.Se si sta creando un servizio Web XML, è possibile applicare attributi che controllano la serializzazione su classi e membri in modo da assicurare che l'output XML sia conforme a uno schema specifico.  
  
 Ad esempio, **XmlSerializer** consente di:  
  
-   Specificare se un campo o una proprietà devono essere codificati come attributo o elemento.  
  
-   Specificare un spazio dei nomi XML da utilizzare.  
  
-   Specificare il nome di un elemento o di un attributo se un nome di campo o proprietà non è appropriato.  
  
 Un altro vantaggio della serializzazione XML è che non si hanno vincoli sulle applicazioni in fase di sviluppo, finché il flusso XML generato sia conforme a uno schema specifico.Immaginare uno schema utilizzato per descrivere libri.Lo schema riporta un elemento titolo, autore, editore autore e numero ISBN.È possibile sviluppare un'applicazione che elabori i dati XML in qualsiasi modo desiderato, ad esempio, come un ordine di libri o come inventario di libri.In entrambi i casi, l'unico requisito è che il flusso XML sia conforme allo schema XSD \(XML Schema definition\) specificato.  
  
## Considerazioni sulla serializzazione XML  
 Di seguito sono riportati alcuni elementi da tenere in considerazione quando si utilizza la classe **XmlSerializer**:  
  
-   Lo strumento Sgen.exe è progettato espressamente per generare assembly di serializzazione per prestazioni ottimali.  
  
-   I dati serializzati contengono solo i dati stessi e la struttura delle classi.Le informazioni sull'identità e sull'assembly non sono incluse.  
  
-   È possibile serializzare solo le proprietà e i campi pubblici.Le proprietà devono disporre di funzioni di accesso pubbliche \(metodi get e set\).Se è necessario serializzare dati non pubblici, utilizzare la classe <xref:System.Runtime.Serialization.DataContractSerializer> anziché la serializzazione XML.  
  
-   Una classe deve disporre di un costruttore predefinito da serializzare tramite **XmlSerializer**.  
  
-   I metodi non possono essere serializzati.  
  
-   **XmlSerializer** può elaborare classi che implementano **IEnumerable** o **ICollection** in modo diverso, nel caso soddisfino determinati requisiti, come riportato di seguito.  
  
     Una classe che implementa **IEnumerable** deve implementare un metodo **Add** pubblico che accetta un solo parametro.Il parametro del metodo **Add** deve essere coerente \(polimorfico\) con il tipo restituito dalla proprietà **IEnumerator.Current** restituita dal metodo **GetEnumerator**.  
  
     Una classe che implementa **ICollection** oltre a **IEnumerable** \(come **CollectionBase**\) deve avere una proprietà indicizzata **Item** pubblica \(un indexer in C\#\) che accetta un valore integer e deve disporre di una proprietà **Count** pubblica di tipo **integer**.Il parametro passato al metodo **Add** deve essere dello stesso tipo di quello restituito dalla proprietà **Item** o una delle basi di tale tipo.  
  
     Per le classi che implementano **ICollection**, i valori da serializzare vengono recuperati dalla proprietà **Item** indicizzata piuttosto che dalla chiamata a **GetEnumerator**.Inoltre, proprietà e campi pubblici non vengono serializzati, fatta eccezione per i campi pubblici che restituiscono un'altra classe di raccolte \(una che implementa **ICollection**\).Per un esempio, vedere [Esempi di serializzazione XML](../../../docs/framework/serialization/examples-of-xml-serialization.md).  
  
## Mappatura del tipo di dati XSD  
 Il documento del World Wide Web Consortium \(www.w3.org\) intitolato "XML Schema Part 2: Datatypes" specifica i tipi di dati semplici consentiti in uno schema XSD \(XML Schema Definition\).Per molti di questi \(ad esempio, **int** e **decimal**\), esiste un tipo di dati corrispondente in .NET Framework.Tuttavia, alcuni tipi di dati XML non dispongono di un tipo di dati corrispondente in .NET Framework \(ad esempio, il tipo di dati **NMTOKEN**\).In tali casi, se si utilizza lo strumento XML Schema Definition \([Strumento XML Schema Definition \(Xsd.exe\)](../../../docs/framework/serialization/xml-schema-definition-tool-xsd-exe.md)\) per generare classi da uno schema, viene applicato un attributo appropriato a un membro di tipo stringa e la relativa proprietà **DataType** viene impostata sul nome del tipo di dati XML.Ad esempio, se uno schema contiene un elemento denominato "MyToken" con il tipo di dati XML **NMTOKEN**, la classe generata potrebbe contenere un membro come illustrato nell'esempio riportato di seguito.  
  
```vb  
<XmlElement(DataType:="NMTOKEN")> _  
Public MyToken As String  
  
```  
  
```csharp  
[XmlElement(DataType = "NMTOKEN")]  
public string MyToken;  
```  
  
 Analogamente, se si sta creando una classe che deve essere conforme a uno schema XML \(XSD\) specifico, è necessario applicare l'attributo appropriato e impostare la relativa proprietà **DataType** sul nome del tipo di dati XML desiderato.  
  
 Per un elenco completo dei mapping dei tipi, vedere la proprietà **DataType** per una delle seguenti classi di attributo:  
  
-   <xref:System.Xml.Serialization.SoapAttributeAttribute>  
  
-   <xref:System.Xml.Serialization.SoapElementAttribute>  
  
-   <xref:System.Xml.Serialization.XmlArrayItemAttribute>  
  
-   <xref:System.Xml.Serialization.XmlAttributeAttribute>  
  
-   <xref:System.Xml.Serialization.XmlElementAttribute>  
  
-   <xref:System.Xml.Serialization.XmlRootAttribute>  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)   
 [XMLSerializer.Serialize](frlrfSystemXmlSerializationXmlSerializerClassSerializeTopic)   
 [Serializzazione binaria](../../../docs/framework/serialization/binary-serialization.md)   
 [Serializzazione](../../../docs/framework/serialization/index.md)   
 [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx)   
 [FileStream](frlrfSystemIOFileStreamClassTopic)   
 [Esempi di serializzazione XML](../../../docs/framework/serialization/examples-of-xml-serialization.md)   
 [Procedura: serializzare un oggetto](../../../docs/framework/serialization/how-to-serialize-an-object.md)   
 [Procedura: deserializzare un oggetto](../../../docs/framework/serialization/how-to-deserialize-an-object.md)