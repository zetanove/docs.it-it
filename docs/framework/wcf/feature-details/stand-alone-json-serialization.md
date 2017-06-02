---
title: "Serializzazione JSON autonoma | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 312bd7b2-1300-4b12-801e-ebe742bd2287
caps.latest.revision: 32
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 32
---
# Serializzazione JSON autonoma
JSON \(JavaScript Object Notation\) è un formato dati progettato specificatamente per essere utilizzato dal codice JavaScript in esecuzione su pagine Web all'interno del browser.JSON è il formato dati predefinito utilizzato dai servizi ASP.NET AJAX creati in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
 Questo formato può essere utilizzato durante la creazione di servizi AJAX senza effettuare l'integrazione con ASP.NET: in questo caso, il formato predefinito è XML, ma è anche possibile scegliere JSON.  
  
 Infine, se è necessario disporre del supporto JSON ma non si sta creando un servizio AJAX, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> consente di serializzare direttamente oggetti di tipo .NET in dati JSON e di deserializzare tali dati in istanze di tipi .NET.Per una descrizione della procedura, vedere [Procedura: serializzare e deserializzare dati JSON](../../../../docs/framework/wcf/feature-details/how-to-serialize-and-deserialize-json-data.md).  
  
 Tranne rare eccezioni, quando si lavora con JSON sono supportati gli stessi tipi .NET supportati da <xref:System.Runtime.Serialization.DataContractSerializer>.Per un elenco dei tipi supportati, vedere [Tipi supportati dal serializzatore dei contratti dati](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md).L'elenco include la maggior parte dei tipi primitivi e dei tipi di matrice e di raccolta, nonché i tipi complessi che utilizzano <xref:System.Runtime.Serialization.DataContractAttribute> e <xref:System.Runtime.Serialization.DataMemberAttribute>.  
  
## Mapping di tipi .NET a tipi JSON  
 Nella tabella seguente viene illustrata la corrispondenza tra i tipi .NET e i tipi JSON\/JavaScript quando di questi è stato eseguito il mapping mediante le procedure di serializzazione e deserializzazione.  
  
|Tipi .NET|JSON\/JavaScript|Note|  
|---------------|----------------------|----------|  
|Tutti i tipi numerici, ad esempio <xref:System.Int32>, <xref:System.Decimal> o <xref:System.Double>|Numero|I valori speciali quali `Double.NaN`, `Double.PositiveInfinity` e `Double.NegativeInfinity` non sono supportati e determinano un tipo JSON non valido.|  
|<xref:System.Enum>|Number|Vedere "Enumerazioni e JSON" più avanti in questo argomento.|  
|<xref:System.Boolean>|Boolean|\-\-|  
|<xref:System.String>, <xref:System.Char>|String|\-\-|  
|<xref:System.Timespan>, <xref:System.Guid>, <xref:System.Uri>|String|Il formato di questi tipi in JSON è lo stesso che in XML \(fondamentalmente TimeSpan nel formato durata ISO 8601, GUID nel formato "12345678\-ABCD\-ABCD\-ABCD\-1234567890AB" e URI nella sua forma di stringa naturale, ad esempio "http:\/\/www.example.com"\)Per informazioni dettagliate, vedere [Riferimento allo schema del contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md).|  
|<xref:System.Xml.XmlQualifiedName>|Stringa|Il formato è "nome:spazio dei nomi" \(tutto ciò che si trova prima del primo segno di due punti è il nome\).Il nome o lo spazio dei nomi potrebbero non essere presenti.Se non esiste alcuno spazio dei nomi, è possibile omettere anche i due punti.|  
|<xref:System.Array> di tipo . <xref:System.Byte>|Matrice di numeri|Ogni numero rappresenta il valore di un byte.|  
|<xref:System.Datetime>|DateTime o String|Vedere Date\/Ore e JSON più avanti in questo argomento.|  
|<xref:System.DatetimeOffset>|Tipo complesso|Vedere Date\/Ore e JSON più avanti in questo argomento.|  
|Tipi XML e ADO.NET \(<xref:System.Xml.XmlElement>,<br /><br /> <xref:System.Xml.Linq.XElement>.Matrici di <xref:System.Xml.XmlNode>,<br /><br /> <xref:System.Runtime.Serialization.ISerializable>,<br /><br /> <xref:System.Data.DataSet>\).|String|Vedere la sezione relativa ai tipi XML e a JSON in questo argomento.|  
|<xref:System.DBNull>|Tipo complesso vuoto|\-\-|  
|Raccolte, dizionari e matrici|Matrice|Vedere la sezione relativa alle raccolte, ai dizionari e alle matrici in questo argomento.|  
|Tipi complessi \(con applicazione dell'attributo <xref:System.Runtime.Serialization.DataContractAttribute> o <xref:System.SerializableAttribute>\)|Tipo complesso|I membri dati diventano membri del tipo complesso JavaScript.|  
|Tipi complessi che implementano l'interfaccia <xref:System.Runtime.Serialization.ISerializable>|Tipo complesso|Come altri tipi complessi ma alcuni tipi <xref:System.Runtime.Serialization.ISerializable> non sono supportati. Vedere la parte relativa al supporto per ISerializable nella sezione Informazioni avanzate di questo argomento.|  
|Valore `Null` per qualsiasi tipo.|Null|Anche i tipi nullable sono supportati e mappati a JSON, così come i tipi non\-nullable.|  
  
### Enumerazioni e JSON  
 In JSON, i valori membro dell'enumerazione vengono trattati come numeri, a differenza di quanto accade nei contratti dati, nei quali questi vengono inclusi come nomi dei membri.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sul trattamento dei contratti dati, vedere [Tipi di enumerazioni nei contratti dati](../../../../docs/framework/wcf/feature-details/enumeration-types-in-data-contracts.md).  
  
-   Con `public enum Color {red, green, blue, yellow, pink}`, ad esempio, la serializzazione di `yellow` produce il numero 3 e non la stringa "yellow".  
  
-   Tutti i membri `enum` sono serializzabili.Gli attributi <xref:System.Runtime.Serialization.EnumMemberAttribute> e <xref:System.NonSerializedAttribute>, se utilizzati, vengono ignorati.  
  
-   È possibile deserializzare un valore `enum` non esistente: ad esempio, il valore 87 può essere deserializzato nell'enumerazione Color precedente anche se non è stato definito un nome di colore corrispondente.  
  
-   Un `enum` di flag non è speciale e viene trattato come qualsiasi altro `enum`.  
  
### Date\/Ore e JSON  
 Il formato JSON non supporta direttamente le date e le ore.Tuttavia, queste vengono comunemente utilizzate e in ASP.NET AJAX è disponibile un supporto speciale per tali tipi.Quando si utilizzano i proxy ASP.NET AJAX, il tipo <xref:System.DateTime> in .NET corrisponde perfettamente al tipo `DateTime` in JavaScript.  
  
-   Quando non si utilizza ASP.NET, un tipo <xref:System.DateTime> viene rappresentato in JSON come una stringa con formato speciale descritta nella sezione Informazioni avanzate di questo argomento.  
  
-   <xref:System.DateTimeOffset> è rappresentato in JSON come tipo complesso: {"DateTime":dateTime,"OffsetMinutes":offsetMinutes}.Il membro `offsetMinutes` rappresenta la differenza tra l'ora locale e l'ora di Greenwich \(GMT\), nota anche come ora UTC \(Coordinated Universal Time\), associata all'ubicazione dell'evento di interesse.Il membro `dateTime` rappresenta il momento in cui si è verificato l'evento di interesse \(anche in questo caso diventa `DateTime` in JavaScript se è in uso ASP.NET AJAX oppure una stringa in caso contrario\).Al momento della serializzazione, il membro `dateTime` viene sempre serializzato in GMT.Pertanto, nella descrizione dell'ora 03.00 di New York, il membro `dateTime` conterrà il componente temporale 08.00, mentre i `offsetMinutes` saranno 300 \(meno 300 minuti o 5 ore rispetto a GMT\).  
  
    > [!NOTE]
    >  Quando gli oggetti <xref:System.DateTime> e <xref:System.DateTimeOffset> vengono serializzati in JSON, conservano solo le informazioni con una precisione espressa in millisecondi.I sottomultipli di millisecondi \(micro\/nanosecondi\) vanno persi durante la serializzazione.  
  
### Tipi XML e JSON  
 I tipi XML diventano stringhe JSON.  
  
-   Se, ad esempio, un membro dati "q" di tipo XElement contiene \<abc\/\>, la stringa JSON è {"q":"\<abc\/\>"}.  
  
-   Alcune regole speciali determinano la modalità di incapsulamento dell'XML. Per ulteriori informazioni vedere la sezione Informazioni avanzate più avanti in questo argomento.  
  
-   Se si sta utilizzando ASP.NET AJAX e, al posto di stringhe in JavaScript, si desidera utilizzare DOM XML, impostare la proprietà <xref:System.ServiceModel.Web.WebGetAttribute.ResponseFormat%2A> su XML nell'oggetto <xref:System.ServiceModel.Web.WebGetAttribute> o la proprietà <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A> su XML nell'oggetto <xref:System.ServiceModel.Web.WebInvokeAttribute>.  
  
### Raccolte, dizionari e matrici  
 In JSON, tutti e le raccolte, tutti i dizionari e le matrici vengono rappresentati come matrici.  
  
-   Qualsiasi personalizzazione che utilizza <xref:System.Runtime.Serialization.CollectionDataContractAttribute> viene ignorata nella rappresentazione JSON.  
  
-   I dizionari non sono un modo per lavorare direttamente con JSON.In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], Dictionary\<string,object\> potrebbe non essere supportato come quando si lavora con altre tecnologie JSON.Se, ad esempio, "abc" viene mappato a "xyz" e "def" viene mappato a 42 in un dizionario, la rappresentazione JSON non può essere {"abc":"xyz","def":42}, ma sarà \[{"Key":"abc","Value":"xyz"},{"Key":"def","Value":42}\].  
  
-   Se si desidera lavorare direttamente con JSON \(accedendo alle chiavi e ai valori in modo dinamico, senza definire preliminarmente un contratto rigido\), sono disponibili diverse opzioni:  
  
    -   Utilizzo dell'esempio [Serializzazione JSON con tipizzazione debole \(AJAX\)](../../../../docs/framework/wcf/samples/weakly-typed-json-serialization-sample.md).  
  
    -   Utilizzo dell'interfaccia <xref:System.Runtime.Serialization.ISerializable> e dei costruttori di deserializzazione. Questi due meccanismi consentono di accedere alle coppie chiave\/valore di JSON rispettivamente durante la serializzazione e la deserializzazione, ma non funzionano in scenari di trust parziale.  
  
    -   Utilizzo di [Mapping tra JSON e XML](../../../../docs/framework/wcf/feature-details/mapping-between-json-and-xml.md) al posto di un serializzatore.  
  
    -   Nel contesto della serializzazione, *Polimorfismo* si riferisce alla capacità di serializzare un tipo derivato nei casi in cui è previsto un tipo di base.Quando vengono utilizzate raccolte in modo polimorfico \(ad esempio quando si assegna una raccolta a un elemento <xref:System.Object>\), esistono regole speciali specifiche per JSON.Questo argomento viene trattato in modo approfondito nella sezione Informazioni avanzate più avanti in questo argomento.  
  
## Ulteriori informazioni  
  
### Ordine dei membri dati  
 L'ordine dei membri dati non è importante quando si utilizza JSON.In particolare, anche se è impostato <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>, è comunque possibile deserializzare i dati JSON in qualsiasi ordine.  
  
### Tipi JSON  
 Il tipo JSON non deve necessariamente corrispondere alla tabella precedente durante la deserializzazione.Ad esempio, un `Int` normalmente viene mappato a un numero JSON, ma può anche essere deserializzato da una stringa JSON, se questa contiene un numero valido.Ovvero, sia {"q": 42} che {"q": "42"} sono validi se esiste un membro dati `Int` chiamato "q".  
  
### Polimorfismo  
 Per serializzazione polimorfa si intende la capacità di serializzare un tipo derivato nei casi in cui è previsto un tipo di base.Tale operazione è supportata per la serializzazione JSON mediante [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], allo stesso modo in cui è supportata la serializzazione XML.Ad esempio, è possibile serializzare `MyDerivedType` quando è previsto `MyBaseType`, oppure serializzare `Int` quando è previsto un `Object`.  
  
 Le informazioni sul tipo potrebbero andare perdute durante la deserializzazione di un tipo derivato nei casi in cui è previsto un tipo di base, a meno che non si stia deserializzando un tipo complesso.Se, ad esempio, viene serializzato <xref:System.Uri> quando è previsto <xref:System.Object>, il risultato sarà una stringa JSON.Se la stringa viene deserializzata di nuovo in <xref:System.Object> viene restituito un elemento <xref:System.String> .NET.Il deserializzatore non è a conoscenza del fatto che la stringa era inizialmente di tipo <xref:System.Uri>.In genere, quando è previsto un elemento <xref:System.Object>, tutte le stringhe JSON vengono deserializzate come stringhe .NET, mentre tutte le matrici JSON utilizzate per serializzare i dizionari, le matrici e le raccolte .NET vengono deserializzati come elementi <xref:System.Array> .NET di tipo <xref:System.Object>, indipendentemente da quale fosse il tipo originario.Un booleano JSON viene mappato a un elemento <xref:System.Boolean> .NET.Tuttavia, quando è previsto un elemento <xref:System.Object>, i numeri JSON vengono deserializzati automaticamente come <xref:System.Int32>, <xref:System.Decimal> o <xref:System.Double> .NET, a seconda del tipo più appropriato.  
  
 In caso di deserializzazione in un tipo di interfaccia, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> deserializza come se il tipo dichiarato fosse un oggetto.  
  
 Quando si lavora con i propri tipi derivati e di base, è generalmente necessario utilizzare <xref:System.Runtime.Serialization.KnownTypeAttribute>, <xref:System.ServiceModel.ServiceKnownTypeAttribute> o un meccanismo equivalente.Ad esempio, se il valore restituito di un'operazione è `Animal` e questa effettivamente restituisce un'istanza di `Cat` \(derivata da `Animal`\), è necessario applicare <xref:System.Runtime.Serialization.KnownTypeAttribute> al tipo `Animal` oppure applicare <xref:System.ServiceModel.ServiceKnownTypeAttribute> all'operazione, specificando il tipo `Cat` in questi attributi.Per ulteriori informazioni, vedere [Tipi conosciuti di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md).  
  
 Per dettagli sul funzionamento della serializzazione polimorfica e una discussione su alcune delle restrizioni che è necessario rispettare durante il suo utilizzo, vedere la sezione Informazioni avanzate più avanti in questo argomento.  
  
### Controllo delle versioni  
 Le funzionalità di controllo delle versioni dei contratti dati, inclusa l'interfaccia <xref:System.Runtime.Serialization.IExtensibleDataObject> sono pienamente supportate in JSON.Inoltre, nella maggior parte di casi è possibile deserializzare un tipo in un formato \(ad esempio XML\) e quindi serializzarlo in un altro formato \(ad esempio JSON\), conservando comunque i dati in un elemento <xref:System.Runtime.Serialization.IExtensibleDataObject>.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Contratti dati compatibili con versioni successive](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md).Poiché JSON non è ordinato, le informazioni relative all'ordine andranno perse.Inoltre, JSON non supporta più coppie chiave\/valore con lo stesso nome di chiave.Infine, tutte le operazioni su <xref:System.Runtime.Serialization.IExtensibleDataObject> sono intrinsecamente polimorfiche. ovvero i relativi tipi derivati sono assegnati a <xref:System.Object>, il tipo di base per tutti i tipi.  
  
## JSON negli URL  
 Quando si utilizzano endpoint ASP.NET AJAX con il verbo HTTP GET \(utilizzando l'attributo <xref:System.ServiceModel.Web.WebGetAttribute>\), nell'URL della richiesta vengono visualizzati i parametri in arrivo anziché il corpo del messaggio.JSON è supportato anche nell'URL della richiesta, pertanto se è presente un'operazione che prende un `Int` chiamato "number" e un tipo complesso di `Person` chiamato "p", l'URL potrebbe assomigliare all'URL seguente:  
  
```  
http://example.com/myservice.svc/MyOperation?number=7&p={"name":"John","age":42}  
```  
  
 Se si utilizzano un controllo Script Manager ASP.NET AJAX e un proxy per chiamare il servizio, l'URL viene automaticamente generato dal proxy e non viene visualizzato.Non è possibile utilizzare JSON in URL su endpoint non ASP.NET AJAX.  
  
## Informazioni avanzate  
  
### Supporto per ISerializable  
  
#### Tipi ISerializable supportati e non supportati  
 In generale, i tipi che implementano l'interfaccia <xref:System.Runtime.Serialization.ISerializable> sono completamente supportati durante la serializzazione\/deserializzazione di JSON.Tuttavia, alcuni di questi tipi \(inclusi alcuni tipi .NET Framework\) vengono implementati in modo tale che gli aspetti specifici della serializzazione di JSON ne impediscono la corretta deserializzazione.  
  
-   Con <xref:System.Runtime.Serialization.ISerializable>, il tipo dei singoli membri dati non è noto in anticipo.Ciò causa una situazione polimorfica simile alla deserializzazione di tipi in un oggetto.Come già sottolineato, ciò potrebbe causare la perdita di informazioni sul tipo in JSON.Ad esempio, un tipo che serializza un `enum` nella sua implementazione di <xref:System.Runtime.Serialization.ISerializable> e tenta di effettuare la deserializzazione direttamente in un elemento `enum` \(senza cast adeguati\) non riesce poiché un `enum` viene serializzato utilizzando un numero in JSON mentre i numeri JSON eseguono la deserializzazione in tipi numerici incorporati .NET \(Int32 .NET, Decimal o Double\).Pertanto, l'informazione che il numero utilizzato era in precedenza un valore `enum` viene persa.  
  
-   Un tipo <xref:System.Runtime.Serialization.ISerializable> che dipende da un particolare ordine di deserializzazione nel relativo costruttore di deserializzazione potrebbe non riuscire a deserializzare alcuni dati JSON poiché la maggior parte dei serializzatori JSON non garantisce un ordine specifico.  
  
#### Tipi Factory  
 Mentre l'interfaccia <xref:System.Runtime.Serialization.IObjectReference> è generalmente supportata in JSON, i tipi che richiedono la funzionalità "tipo factory" \(che restituisce un'istanza di un tipo differente da <xref:System.Runtime.Serialization.IObjectReference.GetRealObject%28System.Runtime.Serialization.StreamingContext%29> rispetto al tipo che implementa l'interfaccia\) non sono supportati.  
  
### Formato di trasmissione DateTime  
 I valori <xref:System.DateTime> vengono visualizzati come stringhe JSON nella forma "\/Date\(700000\+0500\)\/", dove il primo numero \(700000 nell'esempio fornito\) è il numero di millisecondi nel fuso orario di GMT, orario solare \(non ora legale\) dalla mezzanotte del 1° gennaio 1970.Il numero può essere negativo per rappresentare momenti precedenti.La parte rappresentata da "\+0500" nell'esempio è facoltativa e indica che l'orario è di tipo <xref:System.DateTimeKind>, ossia dovrebbe essere convertito nel fuso orario locale durante la deserializzazione.Se assente, l'orario viene deserializzato come <xref:System.DateTimeKind>.Il numero effettivo \("0500" in questo esempio\) e il relative segno \(\+ o \-\) vengono ignorati.  
  
 Durante la serializzazione di <xref:System.DateTime>, gli orari <xref:System.DateTimeKind> e <xref:System.DateTimeKind> sono scritti con uno scostamento, mentre <xref:System.DateTimeKind> viene scritto senza alcuno scostamento.  
  
 Il codice JavaScript del client ASP.NET AJAX converte automaticamente tali stringhe in istanze `DateTime` JavaScript.Verranno convertite anche tutte le altre stringhe che presentano una forma simile e non sono di tipo <xref:System.DateTime> in .NET.  
  
 La conversione avviene solo se viene utilizzato il carattere di escape per "\/" \(ossia JSON appare "\\\/Date\(700000\+0500\)\\\/"\); per questa ragione, il codificatore JSON di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \(attivato mediante <xref:System.ServiceModel.WebHttpBinding>\) utilizza sempre il carattere di escape per  "\/".  
  
### XML nelle stringhe JSON  
  
#### XmlElement  
 <xref:System.Xml.XmlElement> viene serializzato così com'è, senza incapsulamento.Ad esempio, il membro dati "x" di tipo <xref:System.Xml.XmlElement> contenente \<abc\/\> viene rappresentato nel modo seguente.  
  
```  
{"x":"<abc/>"}  
```  
  
#### Matrici di XmlNode  
 Gli oggetti <xref:System.Array> di tipo <xref:System.Xml.XmlNode> vengono incapsulati in un elemento denominato ArrayOfXmlNode nello spazio dei nomi del contratto dati standard per il tipo.Se "x" è una matrice contenente il nodo attributo "N" nello spazio dei nomi "ns" che contiene "value" e un nodo elemento vuoto "M", la rappresentazione risulterà quella seguente:  
  
```  
{"x":"<ArrayOfXmlNode xmlns=\"http://schemas.datacontract.org/2004/07/System.Xml\" a:N=\"value\" xmlns:a=\"ns\"><M/></ArrayOfXmlNode>"}  
```  
  
 Gli attributi nello spazio dei nomi vuoto all'inizio della matrice XmlNode \(prima di altri elementi\) non sono supportati.  
  
#### Tipi IXmlSerializable inclusi XElement e DataSet  
 I tipi <xref:System.Runtime.Serialization.ISerializable> si suddividono in tipi contenuto, tipi DataSet e tipi elemento.Per le definizioni di questi tipi, vedere [Tipi XML e ADO.NET nei contratti dati](../../../../docs/framework/wcf/feature-details/xml-and-ado-net-types-in-data-contracts.md).  
  
 I tipi contenuto e DataSet vengono serializzati in modo simile agli oggetti <xref:System.Array> di <xref:System.Xml.XmlNode> descritti nella sezione precedente.Tali tipi vengono incapsulati in un elemento il cui nome e spazio dei nomi corrisponde al nome e allo spazio dei nomi del contratto dati del tipo in questione.  
  
 I tipi elemento come <xref:System.Xml.Linq.XElement> vengono serializzati così come sono, in modo analogo a <xref:System.Xml.XmlElement>, già descritto in questo argomento.  
  
### Polimorfismo  
  
#### Mantenimento delle informazioni sui tipi  
 Come già illustrato il polimorfismo è supportato in JSON. con alcune restrizioni.JavaScript è un linguaggio con tipizzazione debole e l'identità del tipo non rappresenta solitamente un problema.Tuttavia, quando si utilizza JSON per le comunicazioni tra un sistema fortemente tipizzato \(.NET\) e uno con tipizzazione debole \(JavaScript\), è utile mantenere l'identità del tipo.Ad esempio, i tipi con nomi di contratto dati "Square" e "Circle" derivano da un tipo con nome di contratto dati "Shape".Se "Circle" viene inviato da .NET a JavaScript e viene quindi restituito a un metodo .NET che prevede "Shape", è utile per .NET sapere che l'oggetto in questione è stato originariamente un "Circle"; in caso contrario, tutte le informazioni specifiche del tipo derivato \(ad esempio il membro dati "radium" su "Circle"\) potrebbero andare perdute.  
  
 Per mantenere l'identità del tipo, durante la serializzazione di tipi complessi in JSON può essere aggiunto un suggerimento; il deserializzatore riconosce tale suggerimento e agisce di conseguenza.Il suggerimento relativo ai tipi è rappresentato da una coppia chiave\/valore JSON dove il nome della chiave è "\_\_type" \(due caratteri di sottolineatura seguiti dalla parola "type"\).Il valore è rappresentato da una stringa JSON con forma "DataContractName:DataContractNamespace" \(tutto il testo che precede i due punti rappresenta il nome\).Facendo riferimento all'esempio precedente, "cerchio" può essere serializzato nel modo seguente.  
  
```  
{"__type":"Circle:http://example.com/myNamespace","x":50,"y":70,"radius":10}  
```  
  
 Il suggerimento relativo ai tipi è molto simile all'attributo `xsi:type` definito dallo standard delle istanze di schemi XML e utilizzato durante la serializzazione\/deserializzazione dell'XML.  
  
 I membri dati denominati "\_\_type" non sono consentiti a causa di un potenziale conflitto con il suggerimento relative al tipo.  
  
#### Riduzione delle dimensioni del suggerimento relativo al tip006F  
 Per ridurre le dimensioni dei messaggi JSON, il prefisso dello spazio dei nomi del contratto dati predefinito \(\) viene sostituito dal carattere "\#".Per rendere reversibile questa sostituzione, viene utilizzata una regola di escape: se il primo carattere nello spazio dei nomi è "\#" or "\\", verrà aggiunto un carattere "\\"\).Pertanto, se "Circle" è un tipo nello spazio dei nomi .NET "MyApp.Shapes", il relativo spazio dei nomi del contratto dati sarà http:\/\/schemas.datacontract.org\/2004\/07\/MyApp.Le forme e la rappresentazione JSON appaiono nel modo seguente.  
  
```  
{"__type":"Circle:#MyApp.Shapes","x":50,"y":70,"radius":10}  
```  
  
 Sia i nomi troncati \(\#MyApp.Shapes\) che quelli completi \(\) vengono riconosciuti durante la deserializzazione.  
  
#### Posizione del suggerimento relativo ai tipi negli oggetti JSON  
 Il suggerimento relativo ai tipi deve essere visualizzato innanzitutto nella rappresentazione JSON.Questo è il solo caso in cui l'ordine delle coppie chiave\/valore è importante nell'elaborazione di JSON.Di seguito viene riportato un esempio di modalità non valida per specificare un suggerimento relativo ai tipi.  
  
```  
{"x":50,"y":70,"radius":10,"__type":"Circle:#MyApp.Shapes"}  
```  
  
 Sia <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> utilizzato da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che le pagine del client ASP.NET AJAX inviano sempre il suggerimento relativo ai tipi per primo.  
  
#### I suggerimenti relativi al tipo si applicano solo ai tipi complessi  
 Non è possibile inviare un suggerimento relativo ai tipi a tipi non complessi.Ad esempio, se il tipo restituito da un'operazione è <xref:System.Object> ma viene restituito un Circle, la rappresentazione JSON può essere del tipo illustrato in precedenza e le informazioni sul tipo verranno mantenute.Tuttavia, se viene restituito l'URI, la rappresentazione JSON sarà una stringa e l'informazione che la stringa utilizzata per rappresentare l'URI viene persa.Ciò è valido non solo per i tipi primitivi ma anche per le raccolte e le matrici.  
  
#### Invio dei suggerimenti relativi al tipo  
 I suggerimenti relativi al tipo possono aumentare significativamente le dimensioni dei messaggi; un modo per limitare questa conseguenza è quello di utilizzare uno spazio dei nomi del contratto dati più breve, se possibile.Pertanto, le regole seguenti determinano quali suggerimenti relativi al tipo vengono inviati.  
  
-   Se si utilizza ASP.NET AJAX, laddove possibile i suggerimenti relativi al tipo vengono sempre inviati, anche se non esiste un'assegnazione di base\/derivata \(ad esempio, se un Circle è assegnato a un Circle\).Ciò è necessario per abilitare completamente il processo di chiamata da un ambiente JSON con tipizzazione debole a un ambiente .NET fortemente tipizzato, senza un imprevista perdita di informazioni.  
  
-   Se si utilizzano i servizi ASP.NET AJAX senza integrazione ASP.NET, i suggerimenti relativi al tipo vengono inviati solamente se esiste un'assegnazione di base\/derivata, ossia quando Circle viene assegnato a Shape o a <xref:System.Object>, ma non a Circle.Ciò garantisce che vengano fornite le informazioni minime necessarie per l'implementazione corretta di un client JavaScript, migliorando in tal modo le prestazioni, ma non offre alcuna protezione contro la perdita delle informazioni sui tipi nei client progettati in modo non corretto.Per impedire che si presenti tale problema sul client, evitare di utilizzare le assegnazioni di base\/derivate sul server.  
  
-   Se si utilizza il tipo <xref:System.Runtime.Serialization.DataContractSerializer>, il parametro di costruttore `alwaysEmitTypeInformation` consente di scegliere tra le due modalità precedenti, mentre l'impostazione predefinita è "`false`" \(i suggerimenti sul tipo vengono inviati solo se richiesto\).  
  
#### Nomi di membro dati duplicati  
 Le informazioni sul tipo derivato sono incluse nello stesso oggetto JSON delle informazioni sul tipo di base, in qualsiasi ordine.Ad esempio,  `Shape` può essere rappresentato nel modo seguente.  
  
```  
{"__type":"Shape:#MyApp.Shapes","x":50,"y":70}  
```  
  
 Circle, invece, potrebbe essere rappresentato nel modo seguente.  
  
```  
{"__type":"Circle:#MyApp.Shapes","x":50, "radius":10,"y":70}  
```  
  
 Se anche il tipo `Shape` di base contiene un membro dati denominato "`radius`", ciò potrebbe comportare una collisione sia durante la serializzazione \(poiché gli oggetti JSON non possono contenere nomi di chiave ripetuti\) che durante la deserializzazione \(poiché non è chiaro se "radius" si riferisce a `Shape.radius` o a `Circle.radius`\).Pertanto, mentre il concetto di "occultamento della proprietà" \(i membri dati con lo stesso nome sulle classi di base e derivate\) non viene generalmente consigliato nelle classi del contratto dati, non è assolutamente consentito nel caso di JSON.  
  
#### Polimorfismo e tipi IXmlSerializable  
 In base alle normali regole sui contratti dati, i tipi <xref:System.Xml.Serialization.IXmlSerializable> possono non essere assegnati in modo polimorfico l'uno all'altro come di norma a condizione che siano soddisfatti i requisiti dei tipi conosciuti.Tuttavia, la serializzazione di un tipo <xref:System.Xml.Serialization.IXmlSerializable> al posto di <xref:System.Object> causa la perdita di informazioni sul tipo poiché il risultato è una stringa JSON.  
  
#### Polimorfismo e determinati tipi di interfaccia  
 Non è consentito serializzare una raccolta di tipi o un tipo che implementa <xref:System.Xml.Serialization.IXmlSerializable> nei casi in cui è previsto un tipo non di raccolta diverso da <xref:System.Xml.Serialization.IXmlSerializable> \(ad eccezione di <xref:System.Object>\).Ad esempio, un'interfaccia personalizzata denominata `IMyInterface` e un tipo `MyType` che implementano <xref:System.Collections.Generic.IEnumerable%601> di tipo `int` e `IMyInterface`.Non è consentito restituire `MyType` da un'operazione il cui tipo restituito è `IMyInterface`.Ciò è dovuto al fatto che `MyType` deve essere serializzato come matrice JSON e richiede un suggerimento relative al tipo; come illustrato in precedenza, però, non è possibile includere un suggerimento relativo ai tipi nelle matrici, ma solo nei tipi complessi.  
  
#### Tipi conosciuti e configurazione  
 Tutti i meccanismi relativi ai tipi conosciuti utilizzati dall'elemento <xref:System.Runtime.Serialization.DataContractSerializer> sono supportati anche da <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>.Entrambi i serializzatori leggono il medesimo elemento di configurazione, [\<dataContractSerializer\>](../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-of-system-runtime-serialization.md)[\<system.runtime.serialization\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-runtime-serialization.md), per individuare i tipi conosciuti aggiunti tramite un file di configurazione.  
  
#### Raccolte assegnate a un oggetto  
 Le raccolte assegnate a un oggetto vengono serializzate se implementano <xref:System.Collections.Generic.IEnumerable%601>: una matrice JSON le cui voci dispongono di un suggerimento relativo ai tipi, se si tratta di un tipo complesso.Ad esempio, un <xref:System.Collections.Generic.List%601> di tipo `Shape` assegnato a <xref:System.Object> appare nel modo seguente.  
  
```  
[{"__type":"Shape:#MyApp.Shapes","x":50,"y":70},  
{"__type":"Shape:#MyApp.Shapes","x":58,"y":73},  
{"__type":"Shape:#MyApp.Shapes","x":41,"y":32}]  
```  
  
 Se deserializzata di nuovo in <xref:System.Object>:  
  
-   `Shape` deve essere presente nell'elenco dei tipi conosciuti.Se <xref:System.Collections.Generic.List%601> di tipo `Shape` è presente tra i tipi conosciuti, non si produce alcun effetto.In questo caso, non è necessario aggiungere `Shape` ai tipi conosciuti durante la serializzazione, poiché l'operazione viene eseguita automaticamente.  
  
-   La raccolta viene deserializzata come un elemento <xref:System.Array> di tipo <xref:System.Object> contenente istanze di `Shape`.  
  
#### Raccolte derivate assegnate a raccolte di base  
 Se una raccolta derivata viene assegnata a una raccolta di base, verrà generalmente serializzata come se si trattasse di una raccolta di tipi di base.Tuttavia, se il tipo di elemento della raccolta derivata non può essere assegnato al tipo di elemento della raccolta di base, verrà generata un'eccezione.  
  
#### Suggerimenti relativi al tipo e dizionari  
 Se un dizionario viene assegnato a un elemento <xref:System.Object>, ciascuna voce Key e Value nel dizionario verrà trattata come se fosse assegnata a <xref:System.Object> e ottiene un suggerimento relativo ai tipi.  
  
 Durante la serializzazione dei tipi di dizionario, l'oggetto JSON che contiene i membri "Key" e "Value" non è interessato dall'impostazione `alwaysEmitTypeInformation` e includerà un suggerimento relativo ai tipi solo se le regole della raccolta precedente lo richiedono.  
  
### Nomi di chiave JSON validi  
 Il serializzatore XML codifica i nomi delle chiavi che non sono nomi XML validi.Ad esempio, il nome codificato di un membro dati con il nome "123" sarebbe "\_x0031\_\_x0032\_\_x0033\_", dal momento che "123" è un nome di elemento XML non valido \(poiché inizia con un numero\).Una situazione simile può presentarsi con alcuni set di caratteri internazioni non validi per i nomi XML.Per una spiegazione su questo effetto dell'XML sull'elaborazione JSON, vedere [Mapping tra JSON e XML](../../../../docs/framework/wcf/feature-details/mapping-between-json-and-xml.md).  
  
## Vedere anche  
 [Supporto per JSON e altri formati di trasferimento dati](../../../../docs/framework/wcf/feature-details/support-for-json-and-other-data-transfer-formats.md)