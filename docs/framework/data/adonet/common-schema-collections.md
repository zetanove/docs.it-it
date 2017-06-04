---
title: "Raccolte di schemi comuni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 50127ced-2ac8-4d7a-9cd1-5c98c655ff03
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Raccolte di schemi comuni
Le raccolte di schemi comuni sono le raccolte di schemi implementati da ciascun provider gestito .NET Framework.  È possibile eseguire una query in un provider gestito .NET Framework per determinare l'elenco delle raccolte di schemi supportati chiamando il metodo **GetSchema** senza argomenti oppure con il nome della raccolta di schemi "MetaDataCollections".  In questo modo verrà restituito un oggetto <xref:System.Data.DataTable> con un elenco delle raccolte di schemi supportati, il numero delle restrizioni supportate da ciascuna raccolta e il numero di parti identificatore usate.  Tutte le colonne richieste vengono descritte in queste raccolte.  I provider hanno la possibilità di aggiungere colonne, se necessario.  Ad esempio, `SqlClient` e `OracleClient` aggiungono ParameterName alla raccolta delle restrizioni.  
  
 Se un provider non è in grado di determinare il valore di una colonna richiesta, verrà restituito null.  
  
 Per altre informazioni sull'utilizzo dei metodi **GetSchema**, vedere [GetSchema e raccolte di schemi](../../../../docs/framework/data/adonet/getschema-and-schema-collections.md).  
  
## MetaDataCollections  
 In questa raccolta di schemi vengono riportate informazioni su tutte le raccolte di schemi supportate dal provider gestito .NET Framework attualmente usato per la connessione al database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|CollectionName|string|Il nome della raccolta da passare al metodo **GetSchema** per restituire la raccolta.|  
|NumberOfRestriction|int|Il numero di restrizioni che è possibile specificare per la raccolta.|  
|NumberOfIdentifierParts|int|Il numero di parti nel nome dell'oggetto di database\/identificatore composito.  Ad esempio, in SQL Server 3 corrisponde alle tabelle e 4 alle colonne.  In Oracle 2 corrisponde alle tabelle e 3 alle colonne.|  
  
## DataSourceInformation  
 La raccolta di schemi espone informazioni sull'origine dati a cui è connesso il provider gestito .NET Framework.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|CompositeIdentifierSeparatorPattern|string|L'espressione regolare che corrisponde ai separatori compositi in un identificatore composito.  Ad esempio, "\\." \(per SQL Server\) o "@&#124;\\." \(per Oracle\).<br /><br /> Un identificatore composito viene generalmente usato come nome di oggetto di database, ad esempio: pubs.dbo.authors o pubs@dbo.authors.<br /><br /> Per SQL Server, usare l'espressione regolare "\\.".  Per OracleClient, usare "@&#124;\\.".<br /><br /> Per ODBC, usare Catalog\_name\_seperator.<br /><br /> Per OLE DB, usare DBLITERAL\_CATALOG\_SEPARATOR o DBLITERAL\_SCHEMA\_SEPARATOR.|  
|DataSourceProductName|string|Il nome del prodotto a cui ha avuto accesso il provider, come "Oracle" o "SQLServer".|  
|DataSourceProductVersion|string|Indica la versione del prodotto a cui ha avuto accesso il provider, nel formato nativo delle origini dati e non in formato Microsoft.<br /><br /> In alcuni casi DataSourceProductVersion e DataSourceProductVersionNormalized corrisponderanno allo stesso valore.  Nel caso di OLE DB e ODBC risulteranno sempre uguali poiché sono mappati alla stessa chiamata di funzione nell'API nativo sottostante.|  
|DataSourceProductVersionNormalized|string|Una versione normalizzata per l'origine dati, che è possibile confrontare con `String.Compare()`.  Il formato è lo stesso in tutte le versioni del provider per evitare che la versione 10 venga elencata tra la versione 1 e la versione 2.<br /><br /> Ad esempio, il provider Oracle usa il formato "nn.  nn.  nn.  nn.  nn" per la versione normalizzata. Ciò fa sì che da un'origine dati Oracle 8i venga restituito il valore "08.01.07.04.01".  SQL Server usa il formato "nn.  nn.  nnnn" tipico di Microsoft.<br /><br /> In alcuni casi DataSourceProductVersion e DataSourceProductVersionNormalized corrisponderanno allo stesso valore.  Nel caso di OLE DB e ODBC risulteranno sempre uguali poiché sono mappati alla stessa chiamata di funzione nell'API nativo sottostante.|  
|GroupByBehavior|<xref:System.Data.Common.GroupByBehavior>|Specifica il rapporto tra le colonne nella clausola GROUP BY e le colonne non aggregate nell'elenco di selezione.|  
|IdentifierPattern|string|Un'espressione regolare che corrisponde a un identificatore e dispone di un valore di corrispondenza dell'identificatore.  Ad esempio "\[A\-Za\-z0\-9\_\#$\]".|  
|IdentifierCase|<xref:System.Data.Common.IdentifierCase>|Indica se per gli identificatori non delimitati viene eseguita la distinzione tra maiuscole e minuscole.|  
|OrderByColumnsInSelect|bool|Specifica se le colonne nella clausola ORDER BY devono essere presenti nell'elenco di selezione.  Il valore true indica che le colonne devono risultare nell'elenco di selezione, mentre il valore false indica che non è necessario.|  
|ParameterMarkerFormat|string|Una stringa di formato che rappresenta la modalità di formattazione di un parametro.<br /><br /> Se i parametri denominati sono supportati dall'origine dati, il primo segnalibro di questa stringa deve trovarsi nella posizione in cui verrà formattato il nome del parametro.<br /><br /> Se ad esempio l'origine dati prevede che i parametri vengano denominati e presentino il prefisso ":", il risultato sarà ":{0}".  Quando si esegue la formattazione con il nome di parametro "p1" la stringa risultante sarà ":p1".<br /><br /> Se l'origine dati prevede che i parametri presentino il prefisso ‘@’ che tuttavia è già incluso nel nome, il risultato sarà ‘{0}’, mentre il risultato della formattazione di un parametro denominato "@p1" sarà "@p1".<br /><br /> Per le origini dati che non prevedono parametri denominati, bensì l'uso del carattere ‘?’, la stringa di formato può essere specificata come ‘?’, in modo da ignorare il nome del parametro.  Per OLE DB viene restituito‘?’.|  
|ParameterMarkerPattern|string|Un'espressione regolare che corrisponde al marcatore di parametro.  Avrà un valore corrispondente per il nome del parametro, se disponibile.<br /><br /> Se ad esempio i parametri denominati sono supportati con un carattere "@" principale incluso nel nome del parametro, il risultato sarà: "\(@\[A\-Za\-z0\-9\_$\#\]\*\)".<br /><br /> Se tuttavia i parametri denominati sono supportati con un carattere ":" principale non incluso nel nome del parametro, il risultato sarà: ":\(\[A\-Za\-z0\-9\_$\#\]\*\)".<br /><br /> Se l'origine dati non supporta i parametri nominati, il risultato sarà "?".|  
|ParameterNameMaxLength|int|La lunghezza massima del nome del parametro in caratteri.  In Visual Studio si presuppone che se i nomi di parametri sono supportati, il valore minimo per la lunghezza massima corrisponderà a 30 caratteri.<br /><br /> Se l'origine dati non supporta i parametri denominati, questa proprietà restituisce zero.|  
|ParameterNamePattern|string|Un'espressione regolare che corrisponde ai nomi di parametro validi.  Origini dati diverse hanno regole diverse per i caratteri che è possibile usare con i nomi di parametro.<br /><br /> In Visual Studio si presuppone che se sono supportati i nomi di parametro, i caratteri "\\p{Lu}\\p{Ll}\\p{Lt}\\p{Lm}\\p{Lo}\\p{Nl}\\p{Nd}" rappresentano il set di caratteri minimo supportato, valido per i nomi di parametro.|  
|QuotedIdentifierPattern|string|Un'espressione regolare che corrisponde a un identificatore delimitato e dispone di un valore di corrispondenza dell'identificatore senza virgolette.  Se ad esempio l'origine dati ha usato le virgolette doppie per identificare gli identificatori delimitati, il risultato sarà: "\(\(\[^\\"\]&#124;\\"\\"\)\*\)".|  
|QuotedIdentifierCase|<xref:System.Data.Common.IdentifierCase>|Indica se per gli identificatori delimitati viene eseguita la distinzione tra maiuscole e minuscole.|  
|StatementSeparatorPattern|string|Un'espressione regolare che corrisponde al separatore di istruzione.|  
|StringLiteralPattern|string|Un'espressione regolare che corrisponde a una stringa letterale e dispone di un valore di corrispondenza del valore letterale.  Se ad esempio l'origine dati ha usato le virgolette singole per identificare le stringhe, il risultato sarà: "\('\(\[^'\]&#124;''\)\*'\)"'.|  
|SupportedJoinOperators|<xref:System.Data.Common.SupportedJoinOperators>|Specifica i tipi di istruzioni join di SQL supportati dall'origine dati.|  
  
## DataTypes  
 La raccolta di schemi espone informazioni sui tipi di dati supportati dal database al quale è connesso il provider gestito .NET Framework.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|TypeName|string|Il nome del tipo di dati specifico del provider.|  
|ProviderDbType|int|Il tipo di valore specifico del provider da usare quando si specifica un tipo di parametro.  Ad esempio, SqlDbType.Money o OracleType.Blob.|  
|ColumnSize|long|La lunghezza di una colonna o di un parametro non numerico fa riferimento alla lunghezza massima o definita per questo tipo dal provider.<br /><br /> Per i dati di tipo carattere, rappresenta la lunghezza massima o definita in unità, definita dall'origine dati.  In Oracle è possibile specificare una lunghezza, quindi la dimensione della memoria effettiva per determinati tipi di dati carattere.  Ciò consente di definire solo la lunghezza in unità per Oracle.<br /><br /> Per i tipi di dati data\-ora, rappresenta la lunghezza della rappresentazione stringa \(se si suppone la massima precisione consentita del componente in frazioni di secondo\).<br /><br /> Se il tipo di dati è numerico, rappresenta il limite superiore sulla massima precisione del tipo di dati.|  
|CreateFormat|string|Stringa di formato che indica come aggiungere la colonna a un'istruzione di definizione dei dati, come CREATE TABLE.  Ciascun elemento nella matrice CreateParameter deve essere rappresentato da un "marcatore di parametro" nella stringa di formato.<br /><br /> Ad esempio, per il tipo di dati SQL DECIMAL sono necessarie una precisione e una scala.  In questo caso, la stringa di formato risulterà "DECIMAL\({0},{1}\)".|  
|CreateParameters|string|I parametri di creazione da specificare durante la creazione di una colonna di questo tipo di dati.  Ciascun parametro di creazione viene elencato nella stringa, separato da una virgola nell'ordine in cui deve essere fornito.<br /><br /> Ad esempio, per il tipo di dati SQL DECIMAL sono necessarie una precisione e una scala.  In questo caso, i parametri di creazione devono contenere la stringa "precision, scale".<br /><br /> In un comando di testo per creare una colonna DECIMAL con una precisione di 10 e una scala di 2, il valore della colonna CreateFormat può essere DECIMAL\({0},{1}\)" e la specifica completa del tipo sarà DECIMAL\(10,2\).|  
|Tipo di dati|string|Il nome del tipo di dati .NET Framework.|  
|IsAutoincrementable|bool|true—I valori di questo tipo di dati possono essere a incremento automatico.<br /><br /> false—I valori di questo tipo di dati possono non essere a incremento automatico.<br /><br /> Notare che anche se una colonna di questo tipo di dati può essere a incremento automatico, non significa che tutte le colonne di questo tipo lo siano.|  
|IsBestMatch|bool|true—Il tipo di dati è la corrispondenza più appropriata tra tutti i tipi di dati nell'archivio e il tipo di dati .NET Framework indicato dal valore nella colonna DataType.<br /><br /> false—Il tipo di dati non rappresenta la corrispondenza più appropriata.<br /><br /> Per ciascun set di righe in cui il valore della colonna DataType è lo stesso, la colonna IsBestMatch è impostata su true in una sola riga.|  
|IsCaseSensitive|bool|true—Il tipo di dati è di tipo carattere e viene fatta distinzione tra maiuscole e minuscole.<br /><br /> false—Il tipo di dati è di tipo carattere e viene fatta distinzione tra maiuscole e minuscole.|  
|IsFixedLength|bool|true—Le colonne di questo tipo di dati create dal DDL \(Data Definition Language\) saranno di lunghezza fissa.<br /><br /> false—Le colonne di questo tipo di dati create dal DDL saranno di lunghezza variabile.<br /><br /> DBNull.Value—Non è noto se il provider eseguirà il mapping del campo con una colonna di lunghezza fissa o di lunghezza variabile.|  
|IsFixedPrecisionScale|bool|true—Il tipo di dati dispone di una precisione e una scala fisse.<br /><br /> false—Il tipo di dati non dispone di una precisione e una scala fisse.|  
|IsLong|bool|true—Il tipo di dati contiene dati molto lunghi. La definizione dei dati molto lunghi è specifica del provider.<br /><br /> false—Il tipo di dati non contiene dati molto lunghi.|  
|IsNullable|bool|true—Il tipo di dati ammette valori null.<br /><br /> false—Il tipo di dati non ammette valori null.<br /><br /> DBNull.Value—Non è noto se il tipo di dati ammette valori null.|  
|IsSearchable|bool|true—Il tipo di dati può essere usato in una clausola WHERE con qualsiasi operatore ad eccezione del predicato LIKE.<br /><br /> false—Il tipo di dati non può essere usato in una clausola WHERE con qualsiasi operatore ad eccezione del predicato LIKE.|  
|IsSearchableWithLike|bool|true—Il tipo di dati può essere usato con il predicato LIKE<br /><br /> false—Il tipo di dati non può essere usato con il predicato LIKE.|  
|IsUnsigned|bool|true—Il tipo di dati è unsigned.<br /><br /> false—Il tipo di dati è signed.<br /><br /> DBNull.Value—Non applicabile al tipo di dati.|  
|MaximumScale|short|Se l'indicatore di tipo è numerico, corrisponde al numero massimo di cifre consentito a destra del separatore decimale.  Altrimenti sarà DBNull.Value.|  
|MinimumScale|short|Se l'indicatore di tipo è numerico, corrisponde al numero minimo di cifre consentito a destra del separatore decimale.  Altrimenti sarà DBNull.Value.|  
|IsConcurrencyType|bool|true – Il tipo di dati viene aggiornato dal database ogni volta che la riga viene modificata e il valore della colonna è diverso da tutti i valori precedenti<br /><br /> false – Il tipo di dati non viene aggiornato dal database ogni volta che viene modificata la riga<br /><br /> DBNull.Value – il database non supporta questo tipo di dati|  
|IsLiteralsSupported|bool|true – Il tipo di dati può essere espresso come valore letterale<br /><br /> false – Il tipo di dati non può essere espresso come valore letterale|  
|LiteralPrefix|string|Il prefisso applicato a un dato valore letterale.|  
|LitteralSuffix|string|Il suffisso applicato a un dato valore letterale.|  
|NativeDataType|String|NativeDataType è una colonna specifica di OLE DB per l'esposizione del tipo di dati OLE DB.|  
  
## Restrizioni  
 La raccolta di schemi espone informazioni sulle restrizioni supportate dal provider gestito .NET Framework usato per la connessione al database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|CollectionName|string|Il nome della raccolta a cui sono applicate queste restrizioni.|  
|RestrictionName|string|Il nome della restrizione nella raccolta.|  
|RestrictionDefault|string|Ignorato.|  
|RestrictionNumber|int|La posizione effettiva nelle restrizioni delle raccolte in cui rientra questa particolare restrizione.|  
  
## ReservedWords  
 La raccolta di schemi espone informazioni sulle parole riservate dal database al quale è connesso il provider gestito .NET Framework.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|ReservedWords|string|Le parole riservate specifiche del provider.|  
  
## Vedere anche  
 [Recupero di informazioni sullo schema di database](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)   
 [GetSchema e raccolte di schemi](../../../../docs/framework/data/adonet/getschema-and-schema-collections.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)