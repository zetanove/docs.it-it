---
title: "Raccolte di schemi di SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c6403cc3-d78b-4f85-bab1-ada7a3446ec5
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Raccolte di schemi di SQL Server
Il provider di dati Microsoft .NET Framework per SQL Server, oltre alle raccolte di schemi comuni, supporta raccolte di schemi aggiuntivi.  Le raccolte di schemi variano leggermente in base alla versione di SQL Server usata.  Per determinare l'elenco delle raccolte di schemi supportati chiamare il metodo **GetSchema** senza argomenti oppure con il nome della raccolta di schemi "MetaDataCollections".  In questo modo verrà restituito un oggetto <xref:System.Data.DataTable> con un elenco delle raccolte di schemi supportati, il numero delle restrizioni supportate da ciascuna raccolta e il numero di parti identificatore usate.  
  
## Database  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|database\_name|String|Nome del database.|  
|Dbid|Int16|Identificatore del database.|  
|create\_date|DateTime|Data di creazione del database.|  
  
## Foreign Keys  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|constraint\_catalog|String|Catalogo a cui appartiene il vincolo.|  
|constraint\_schema|String|Schema contenente il vincolo.|  
|constraint\_name|String|Il nome.|  
|table\_catalog|String|Nome della tabella contenente il vincolo.|  
|table\_schema|String|Schema contenente la tabella.|  
|table\_name|String|Nome tabella|  
|constraint\_type|String|Tipo di vincolo.  È consentito solo il tipo "FOREIGN KEY".|  
|is\_deferrable|String|Specifica se il vincolo può essere rinviato.  Restituisce NO.|  
|initially\_deferred|String|Specifica se inizialmente il vincolo può essere rinviato.  Restituisce NO.|  
  
## Indexes  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|constraint\_catalog|String|Catalogo a cui appartiene l'indice.|  
|constraint\_schema|String|Schema contenente l'indice.|  
|constraint\_name|String|Nome dell'indice.|  
|table\_catalog|String|Nome della tabella a cui è associato l'indice.|  
|table\_schema|String|Schema contenente la tabella a cui è associato l'indice.|  
|table\_name|String|Nome della tabella.|  
  
### Indexes \(SQL Server 2008\)  
 A partire da .NET Framework versione 3.5 SP1 e SQL Server 2008, le colonne seguenti sono state aggiunte alla raccolta di schemi Indexes per supportare nuovi tipi di dati spaziali, filestream e colonne di tipo sparse.  Tali colonne non sono supportate nelle versioni precedenti di .NET Framework e di SQL Server.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|type\_desc|String|I valori del tipo di indice sono i seguenti:<br /><br /> -   HEAP<br />-   CLUSTERED<br />-   NONCLUSTERED<br />-   XML<br />-   SPATIAL|  
  
## IndexColumns  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|constraint\_catalog|String|Catalogo a cui appartiene l'indice.|  
|constraint\_schema|String|Schema contenente l'indice.|  
|constraint\_name|String|Nome dell'indice.|  
|table\_catalog|String|Nome della tabella a cui è associato l'indice.|  
|table\_schema|String|Schema contenente la tabella a cui è associato l'indice.|  
|table\_name|String|Nome della tabella.|  
|column\_name|String|Nome della colonna a cui è associato l'indice.|  
|ordinal\_position|Int32|Posizione ordinale della colonna.|  
|KeyType|UInt16|Tipo di oggetto.|  
  
## Procedure  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|specific\_catalog|String|Nome specifico del catalogo.|  
|specific\_schema|String|Il nome specifico dello schema.|  
|specific\_name|String|Nome specifico del catalogo.|  
|routine\_catalog|String|Il catalogo a cui appartiene la stored procedure.|  
|routine\_schema|String|Lo schema contenente la stored procedure.|  
|routine\_name|String|Il nome della stored procedure.|  
|routine\_type|String|Restituisce PROCEDURE per le stored procedure e FUNCTION per le funzioni.|  
|created|DateTime|L'ora in cui è stata creata la routine.|  
|last\_altered|DateTime|Data e ora dell'ultima modifica della routine.|  
  
## Procedure Parameters  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|specific\_catalog|String|Nome del catalogo della routine per cui viene specificato questo parametro.|  
|specific\_schema|String|Lo schema contenente la routine a cui appartiene questo parametro.|  
|specific\_name|String|Il nome della routine contenente questo parametro.|  
|ordinal\_position|Int16|Posizione ordinale del parametro iniziando da 1.  Per il valore restituito di una routine, è uguale a 0.|  
|parameter\_mode|String|Restituisce IN se è un parametro di input, OUT se è un parametro di output e INOUT se è un parametro di input\/output.|  
|is\_result|String|Restituisce YES se indica il risultato di una routine che è una funzione.  In caso contrario, restituisce NO.|  
|as\_locator|String|Restituisce YES se dichiarato come indicatore di posizione.  In caso contrario, restituisce NO.|  
|parameter\_name|String|Nome del parametro.  Restituisce NULL se corrisponde al valore restituito di una funzione.|  
|data\_type|String|Il tipo di dati fornito dal sistema.|  
|character\_maximum\_length|Int32|La lunghezza massima in caratteri per il tipo di dati carattere o binario.  Per altri tipi di parametro, restituisce NULL.|  
|character\_octet\_length|Int32|La lunghezza massima in byte per il tipo di dati carattere o binario.  Per altri tipi di parametro, restituisce NULL.|  
|collation\_catalog|String|Il nome del catalogo per le regole di confronto del parametro.  Se non è di tipo carattere, restituisce NULL.|  
|collation\_schema|String|Restituisce sempre NULL.|  
|collation\_name|String|Nome delle regole di confronto del parametro.  Se non è di tipo carattere, restituisce NULL.|  
|character\_set\_catalog|String|Il nome del catalogo del set di caratteri del parametro.  Se non è di tipo carattere, restituisce NULL.|  
|character\_set\_schema|String|Restituisce sempre NULL.|  
|character\_set\_name|String|Nome del set di caratteri del parametro.  Se non è di tipo carattere, restituisce NULL.|  
|numeric\_precision|Byte|La precisione dei dati numerici approssimativi, dei dati numerici esatti, dei dati di tipo integer o dei dati di tipo valuta.  Per altri tipi di parametro, restituisce NULL.|  
|numeric\_precision\_radix|Int16|La radice della precisione dei dati numerici approssimativi, dei dati numerici esatti, dei dati di tipo integer o dei dati di tipo valuta.  Per altri tipi di parametro, restituisce NULL.|  
|numeric\_scale|Int32|La scala dei dati numerici approssimativi, dei dati numerici esatti, dei dati di tipo integer o dei dati di tipo valuta.  Per altri tipi di parametro, restituisce NULL.|  
|datetime\_precision|Int16|La precisione in secondi frazionari se il tipo di parametro è datetime oppure smalldatetime.  Per altri tipi di parametro, restituisce NULL.|  
|interval\_type|String|NULL.  Riservato per un utilizzo futuro da parte di SQL Server.|  
|interval\_precision|Int16|NULL.  Riservato per un utilizzo futuro da parte di SQL Server.|  
  
## Tabelle  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|table\_catalog|String|Catalogo della tabella.|  
|table\_schema|String|Schema contenente la tabella.|  
|table\_name|String|Nome della tabella.|  
|table\_type|String|Tipo di tabella.  Può essere VIEW o BASE TABLE.|  
  
## Colonne  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|table\_catalog|String|Catalogo della tabella.|  
|table\_schema|String|Schema contenente la tabella.|  
|table\_name|String|Nome della tabella.|  
|column\_name|String|Nome della colonna.|  
|ordinal\_position|Int16|Numero di identificazione della colonna.|  
|column\_default|String|Il valore predefinito della colonna.|  
|is\_nullable|String|Supporto di valori Null della colonna.  Se la colonna supporta i valori NULL, restituisce YES.  In caso contrario, restituisce NO.|  
|data\_type|String|Il tipo di dati fornito dal sistema.|  
|character\_maximum\_length|Int32 – Sql8, Int16 – Sql7|La lunghezza massima in caratteri per i tipi di dati binario e carattere o per i tipi di dati testo e immagine.  Per altri tipi di dati, viene restituito NULL.|  
|character\_octet\_length|Int32 – SQL8, Int16 – Sql7|La lunghezza massima in byte per i tipi di dati binario e carattere o per i tipi di dati testo e immagine.  Per altri tipi di dati, viene restituito NULL.|  
|numeric\_precision|Unsigned Byte|La precisione dei dati numerici approssimativi, dei dati numerici esatti, dei dati di tipo integer o dei dati di tipo valuta.  Per altri tipi di dati, viene restituito NULL.|  
|numeric\_precision\_radix|Int16|La radice della precisione dei dati numerici approssimativi, dei dati numerici esatti, dei dati di tipo integer o dei dati di tipo valuta.  Per altri tipi di dati, viene restituito NULL.|  
|numeric\_scale|Int32|La scala dei dati numerici approssimativi, dei dati numerici esatti, dei dati di tipo integer o dei dati di tipo valuta.  Per altri tipi di dati, viene restituito NULL.|  
|datetime\_precision|Int16|Il codice Subtype per datetime e per i tipi di dati dell'intervallo di SQL\-92.  Per altri tipi di dati, viene restituito NULL.|  
|character\_set\_catalog|String|Se la colonna presenta un tipo di dati carattere o testo, viene restituito master, che indica il database in cui è posizionato il set di caratteri.  Per altri tipi di dati, viene restituito NULL.|  
|character\_set\_schema|String|Restituisce sempre NULL.|  
|character\_set\_name|String|Se la colonna presenta un tipo di dati carattere o testo, viene restituito il nome univoco del set di caratteri.  Per altri tipi di dati, viene restituito NULL.|  
|collation\_catalog|String|Se la colonna presenta un tipo di dati carattere o testo, viene restituito master, che indica il database in cui sono definite le regole di confronto.  In caso contrario, il valore di questa colonna è NULL.|  
  
### Columns \(SQL Server 2008\)  
 A partire da .NET Framework versione 3.5 SP1 e SQL Server 2008, le colonne seguenti sono state aggiunte alla raccolta di schemi Columns per supportare nuovi tipi di dati spaziali, filestream e colonne di tipo sparse.  Tali colonne non sono supportate nelle versioni precedenti di .NET Framework e di SQL Server.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|IS\_FILESTREAM|String|YES in caso di colonna con attributo FILESTREAM.<br /><br /> NO se la colonna non dispone dell'attributo FILESTREAM.|  
|IS\_SPARSE|String|YES in caso di colonna di tipo sparse.<br /><br /> NO se la colonna non è di tipo sparse.|  
|IS\_COLUMN\_SET|String|YES in caso di colonna del set di colonne.<br /><br /> NO se la colonna non fa parte del set di colonne.|  
  
### AllColumns \(SQL Server 2008\)  
 A partire da .NET Framework versione 3.5 SP1 e SQL Server 2008, è stata aggiunta la raccolta di schemi AllColumns per supportare colonne di tipo sparse.  AllColumns non è supportato nelle versioni precedenti di .NET Framework e di SQL Server.  
  
 AllColumns dispone delle stesse restrizioni e dello schema DataTable risultante della raccolta di schemi Columns,  l'unica differenza è costituita dal fatto che AllColumns include colonne del set di colonne che non sono incluse nella raccolta di schemi Columns.  Nella tabella seguente vengono descritte queste colonne.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|table\_catalog|String|Catalogo della tabella.|  
|table\_schema|String|Schema contenente la tabella.|  
|table\_name|String|Nome della tabella.|  
|column\_name|String|Nome della colonna.|  
|ordinal\_position|Int16|Numero di identificazione della colonna.|  
|column\_default|String|Il valore predefinito della colonna.|  
|is\_nullable|String|Supporto di valori Null della colonna.  Se la colonna supporta i valori NULL, restituisce YES.  In caso contrario, restituisce NO.|  
|data\_type|String|Il tipo di dati fornito dal sistema.|  
|character\_maximum\_length|Int32|La lunghezza massima in caratteri per i tipi di dati binario e carattere o per i tipi di dati testo e immagine.  Per altri tipi di dati, viene restituito NULL.|  
|character\_octet\_length|Int32|La lunghezza massima in byte per i tipi di dati binario e carattere o per i tipi di dati testo e immagine.  Per altri tipi di dati, viene restituito NULL.|  
|numeric\_precision|Unsigned Byte|La precisione dei dati numerici approssimativi, dei dati numerici esatti, dei dati di tipo integer o dei dati di tipo valuta.  Per altri tipi di dati, viene restituito NULL.|  
|numeric\_precision\_radix|Int16|La radice della precisione dei dati numerici approssimativi, dei dati numerici esatti, dei dati di tipo integer o dei dati di tipo valuta.  Per altri tipi di dati, viene restituito NULL.|  
|numeric\_scale|Int32|La scala dei dati numerici approssimativi, dei dati numerici esatti, dei dati di tipo integer o dei dati di tipo valuta.  Per altri tipi di dati, viene restituito NULL.|  
|datetime\_precision|Int16|Il codice Subtype per datetime e per i tipi di dati dell'intervallo di SQL\-92.  Per altri tipi di dati, viene restituito NULL.|  
|character\_set\_catalog|String|Se la colonna presenta un tipo di dati carattere o testo, viene restituito master, che indica il database in cui è posizionato il set di caratteri.  Per altri tipi di dati, viene restituito NULL.|  
|character\_set\_schema|String|Restituisce sempre NULL.|  
|character\_set\_name|String|Se la colonna presenta un tipo di dati carattere o testo, viene restituito il nome univoco del set di caratteri.  Per altri tipi di dati, viene restituito NULL.|  
|collation\_catalog|String|Se la colonna presenta un tipo di dati carattere o testo, viene restituito master, che indica il database in cui sono definite le regole di confronto.  In caso contrario, il valore di questa colonna è NULL.|  
|IS\_FILESTREAM|String|YES in caso di colonna con attributo FILESTREAM.<br /><br /> NO se la colonna non dispone dell'attributo FILESTREAM.|  
|IS\_SPARSE|String|YES in caso di colonna di tipo sparse.<br /><br /> NO se la colonna non è di tipo sparse.|  
|IS\_COLUMN\_SET|String|YES in caso di colonna del set di colonne.<br /><br /> NO se la colonna non fa parte del set di colonne.|  
  
### ColumnSetColumns \(SQL Server 2008\)  
 A partire da .NET Framework versione 3.5 SP1 e SQL Server 2008, è stata aggiunta la raccolta di schemi ColumnSetColumns per supportare colonne di tipo sparse.  ColumnSetColumns non è supportato nelle versioni precedenti di .NET Framework e di SQL Server.  La raccolta di schemi ColumnSetColumns restituisce lo schema per tutte le colonne di un set di colonne.  Nella tabella seguente vengono descritte queste colonne.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|table\_catalog|String|Catalogo della tabella.|  
|table\_schema|String|Schema contenente la tabella.|  
|table\_name|String|Nome della tabella.|  
|column\_name|String|Nome della colonna.|  
|ordinal\_position|Int16|Numero di identificazione della colonna.|  
|column\_default|String|Il valore predefinito della colonna.|  
|is\_nullable|String|Supporto di valori Null della colonna.  Se la colonna supporta i valori NULL, restituisce YES.  In caso contrario, restituisce NO.|  
|data\_type|String|Il tipo di dati fornito dal sistema.|  
|character\_maximum\_length|Int32|La lunghezza massima in caratteri per i tipi di dati binario e carattere o per i tipi di dati testo e immagine.  Per altri tipi di dati, viene restituito NULL.|  
|character\_octet\_length|Int32|La lunghezza massima in byte per i tipi di dati binario e carattere o per i tipi di dati testo e immagine.  Per altri tipi di dati, viene restituito NULL.|  
|numeric\_precision|Unsigned Byte|La precisione dei dati numerici approssimativi, dei dati numerici esatti, dei dati di tipo integer o dei dati di tipo valuta.  Per altri tipi di dati, viene restituito NULL.|  
|numeric\_precision\_radix|Int16|La radice della precisione dei dati numerici approssimativi, dei dati numerici esatti, dei dati di tipo integer o dei dati di tipo valuta.  Per altri tipi di dati, viene restituito NULL.|  
|numeric\_scale|Int32|La scala dei dati numerici approssimativi, dei dati numerici esatti, dei dati di tipo integer o dei dati di tipo valuta.  Per altri tipi di dati, viene restituito NULL.|  
|datetime\_precision|Int16|Il codice Subtype per datetime e per i tipi di dati dell'intervallo di SQL\-92.  Per altri tipi di dati, viene restituito NULL.|  
|character\_set\_catalog|String|Se la colonna presenta un tipo di dati carattere o testo, viene restituito master, che indica il database in cui è posizionato il set di caratteri.  Per altri tipi di dati, viene restituito NULL.|  
|character\_set\_schema|String|Restituisce sempre NULL.|  
|character\_set\_name|String|Se la colonna presenta un tipo di dati carattere o testo, viene restituito il nome univoco del set di caratteri.  Per altri tipi di dati, viene restituito NULL.|  
|collation\_catalog|String|Se la colonna presenta un tipo di dati carattere o testo, viene restituito master, che indica il database in cui sono definite le regole di confronto.  In caso contrario, il valore di questa colonna è NULL.|  
|IS\_FILESTREAM|String|YES in caso di colonna con attributo FILESTREAM.<br /><br /> NO se la colonna non dispone dell'attributo FILESTREAM.|  
|IS\_SPARSE|String|YES in caso di colonna di tipo sparse.<br /><br /> NO se la colonna non è di tipo sparse.|  
|IS\_COLUMN\_SET|String|YES in caso di colonna del set di colonne.<br /><br /> NO se la colonna non fa parte del set di colonne.|  
  
## Utenti  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|uid|Int16|Identificatore utente univoco nel database.  1 corrisponde al proprietario del database.|  
|name|String|Il nome utente o il nome del gruppo, univoco nel database.|  
|createdate|DateTime|La data in cui è stato aggiunto l'account.|  
|updatedate|DateTime|Data dell'ultima modifica dell'account.|  
  
## Visualizzazioni  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|table\_catalog|String|Catalogo della visualizzazione.|  
|table\_schema|String|Schema contenente la visualizzazione.|  
|table\_name|String|Nome della visualizzazione.|  
|check\_option|String|Tipo di WITH CHECK OPTION.  Se la visualizzazione originale è stata creata usando WITH CHECK OPTION, il tipo è CASCADE.  In caso contrario, viene restituito NONE.|  
|is\_updatable|String|Specifica se la visualizzazione può essere aggiornata.  Restituisce sempre NO.|  
  
## ViewColumns  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|view\_catalog|String|Catalogo della visualizzazione.|  
|view\_schema|String|Schema contenente la visualizzazione.|  
|view\_name|String|Nome della visualizzazione.|  
|table\_catalog|String|Catalogo della tabella associata a questa visualizzazione.|  
|table\_schema|String|Il catalogo della tabella associata a questa visualizzazione.|  
|table\_name|String|Il nome della tabella associata alla visualizzazione.  Tabella di base.|  
|column\_name|String|Nome della colonna.|  
  
## UserDefinedTypes  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|assembly\_name|String|Nome del file dell'assembly.|  
|UDT\_name|String|Il nome della classe per l'assembly.|  
|version\_major|Oggetto|Il numero di versione principale.|  
|version\_minor|Oggetto|Numero di versione secondario.|  
|version\_build|Oggetto|Numero di build.|  
|version\_revision|Oggetto|Numero di revisione.|  
|Culture\_info|Oggetto|Informazioni sulle impostazioni cultura associate all'UDT.|  
|Public\_key|Oggetto|La chiave pubblica usata dall'assembly.|  
|Is\_fixed\_length|Boolean|Specifica se la lunghezza del tipo è sempre uguale a max\_length.|  
|max\_length|Int16|La lunghezza massima del tipo in byte.|  
|permission\_set\_desc|String|Il nome descrittivo del set di autorizzazioni o del livello di sicurezza dell'assembly.|  
|create\_date|DateTime|La data di creazione o di registrazione dell'assembly.|  
  
## Vedere anche  
 [Recupero di informazioni sullo schema di database](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)