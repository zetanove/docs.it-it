---
title: "Raccolte di schemi Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 89a75de8-dee8-45e2-a97f-254d7e62e7e1
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Raccolte di schemi Oracle
Il provider di dati Microsoft .NET Framework per Oracle, oltre alle raccolte di schemi comuni, supporta le seguenti raccolte di schemi specifici:  
  
-   Colonne  
  
-   Indexes  
  
-   IndexColumns  
  
-   Procedure  
  
-   Sequenze  
  
-   Synonyms  
  
-   Tabelle  
  
-   Utenti  
  
-   Visualizzazioni  
  
-   Funzioni  
  
-   Pacchetti  
  
-   PackageBodies  
  
-   Argomenti  
  
-   UniqueKeys  
  
-   PrimaryKeys  
  
-   ForeignKeys  
  
-   ForeignKeyColumns  
  
-   ProcedureParameters  
  
## Colonne  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario della tabella, della visualizzazione o del cluster.|  
|TABLE\_NAME|String|Nome della tabella, della visualizzazione o del cluster.|  
|COLUMN\_NAME|String|Nome della colonna.|  
|ID|Decimal|Numero di sequenza della colonna in base all'ordine in cui vengono create le colonne.|  
|DATATYPE|String|Tipo di dati della colonna.|  
|LENGTH|Decimal|Lunghezza della colonna in byte.|  
|PRECISION|Decimal|Precisione decimale per il tipo di dati NUMBER e precisione binaria per il tipo di dati FLOAT. Per tutti gli altri tipi di dati, il valore è null.|  
|SCALE|Decimal|Cifre a destra del separatore decimale in un numero.|  
|NULLABLE|String|Specifica se una colonna supporta i valori NULL.  Il valore è N se è presente un vincolo diverso da NULL sulla colonna o se la colonna fa parte di un vincolo PRIMARY KEY.|  
  
## Indexes  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario dell'indice.|  
|INDEX\_NAME|String|Nome dell'indice.|  
|INDEX\_TYPE|String|Tipo di indice \(NORMAL, BITMAP, FUNCTION\-BASED NORMAL, FUNCTION\-BASED BITMAP o DOMAIN\).|  
|TABLE\_OWNER|String|Proprietario dell'oggetto indicizzato.|  
|TABLE\_NAME|String|Nome dell'oggetto indicizzato.|  
|TABLE\_TYPE|String|Tipo di oggetto indicizzato, ad esempio TABLE e CLUSTER.|  
|UNIQUENESS|String|Se l'indice è UNIQUE o NONUNIQUE.|  
|COMPRESSION|String|Se l'indice è ENABLED o DISABLED.|  
|PREFIX\_LENGTH|Decimal|Il numero di colonne nel prefisso della chiave compression.|  
|TABLESPACE\_NAME|String|Il nome dello spazio di tabella contenente l'indice.|  
|INI\_TRANS|Decimal|Il numero iniziale di transazioni.|  
|MAX\_TRANS|Decimal|Il numero massimo di transazioni.|  
|INITIAL\_EXTENT|Decimal|La dimensione dell'extent iniziale.|  
|NEXT\_EXTENT|Decimal|Dimensione degli extent successivi.|  
|MIN\_EXTENTS|Decimal|Numero minimo di extent consentito nel segmento.|  
|MAX\_EXTENTS|Decimal|Il numero massimo di extent consentito nel segmento.|  
|PCT\_INCREASE|Decimal|La percentuale di aumento della dimensione degli extent.|  
|PCT\_THRESHOLD|Decimal|La soglia percentuale di spazio dei blocchi consentita in base alla voce dell'indice.|  
|INCLUDE\_COLUMN|Decimal|L'identificatore colonna dell'ultima colonna da includere nell'indice \(non overflow\) della chiave primaria della tabella con indice.  Il mapping di questa colonna viene eseguito alla colonna COLUMN\_ID delle visualizzazioni del dizionario dei dati \*\_TAB\_COLUMNS.|  
|FREELISTS|Decimal|Il numero di elenchi di disponibilità di processi allocato al segmento.|  
|FREELIST\_GROUPS|Decimal|Il numero di elenchi di disponibilità di gruppi allocato al segmento.|  
|PCT\_FREE|Decimal|Percentuale minima di spazio disponibile in un blocco.|  
|LOGGING|String|Le informazioni sulla registrazione.|  
|BLEVEL|Decimal|Livello dell'albero B\*: profondità dell'indice dal blocco radice ai relativi blocchi foglia.  La profondità 0 indica che il blocco radice e il blocco foglia sono identici.|  
|LEAF\_BLOCKS|Decimal|Il numero di blocchi foglia nell'indice.|  
|DISTINCT\_KEYS|Decimal|Il numero di valori indicizzati distinti.  Per gli indici che impongono i vincoli UNIQUE e PRIMARY KEY, questo valore corrisponde al numero di righe nella tabella \(USER\_TABLES.NUM\_ROWS\).|  
|AVG\_LEAF\_BLOCKS\_PER\_KEY|Decimal|Il numero medio dei blocchi foglia in cui ciascun valore distinct dell'indice viene arrotondato al valore integer più vicino.  Per gli indici che impongono i vincoli UNIQUE e PRIMARY KEY, questo valore è sempre 1.|  
|AVG\_DATA\_BLOCKS\_PER\_KEY|Decimal|Il numero medio dei blocchi di dati nella tabella a cui fa riferimento un valore distinct dell'indice arrotondato al valore integer più vicino.  Questa statistica rappresenta il numero medio dei blocchi di dati contenenti righe in cui è presente un valore specificato per le colonne indicizzate.|  
|CLUSTERING\_FACTOR|Decimal|Indica il livello di ordine delle righe nella tabella in base ai valori dell'indice.|  
|STATO|String|Indica se un indice non partizionato è VALID o UNUSABLE.|  
|NUM\_ROWS|Decimal|Il numero di righe dell'indice.|  
|SAMPLE\_SIZE|Decimal|Dimensione dell'esempio usato per analizzare l'indice.|  
|LAST\_ANALYZED|DateTime|La data più recente in cui è stato analizzato l'indice.|  
|DEGREE|String|Il numero di thread per ogni istanza per l'analisi dell'indice.|  
|INSTANCES|String|Il numero di istanze in cui analizzare gli indici.|  
|PARTITIONED|String|Indica se l'indice è partizionato \(YES &#124; NO\).|  
|TEMPORARY|String|Indica se l'indice è in una tabella temporanea.|  
|GENERATED|String|Indica se il nome dell'indice è generato dal sistema \(Y&#124;N\).|  
|SECONDARY|String|Indica se l'indice è un oggetto secondario creato dal metodo ODCIIndexCreate di Oracle9i Data Cartridge \(Y&#124;N\).|  
|BUFFER\_POOL|String|Il nome del pool di buffer predefinito da usare per il blocchi dell'indice.|  
|USER\_STATS|String|Indica se le statistiche sono state immesse direttamente dall'utente.|  
|DURATION|String|Indica la durata di una tabella temporanea. 1\) SYS$SESSION: le righe vengono mantenute per la durata della sessione. 2\) SYS$TRANSACTION: le righe vengono eliminate dopo COMMIT. 3\) Null per una tabella permanente.|  
|PCT\_DIRECT\_ACCESS|Decimal|Indica la percentuale di righe con guess uguale a VALID per un indice secondario in una tabella con indice.|  
|ITYP\_OWNER|String|Indica il proprietario del tipo di indice per un indice di dominio.|  
|ITYP\_NAME|String|Indica il nome del tipo di indice per un indice di dominio.|  
|PARAMETERS|String|Indica la stringa del parametro per un indice di dominio.|  
|GLOBAL\_STATS|String|Per gli indici partizionati, indica se le statistiche sono state raccolte analizzando l'intero indice \(YES\) o se sono state valutate in base alle statistiche sulle partizioni e sottopartizioni dell'indice sottostanti \(NO\).|  
|DOMIDX\_STATUS|String|Riflette lo stato dell'indice di dominio.  NULL: l'indice specificato non è un indice di dominio.  VALID: l'indice è un indice di dominio valido.  IDXTYP\_INVLD: il tipo di indice dell'indice di dominio non è valido.|  
|DOMIDX\_OPSTATUS|String|Riflette lo stato di un'operazione eseguita su un indice di dominio. NULL: l'indice specificato non è un indice di dominio.  VALID: l'operazione è stata eseguita senza errori.  FAILED: si è verificato un errore e l'operazione non è stata eseguita correttamente.|  
|FUNCIDX\_STATUS|String|Indica lo stato di un indice basato sulla funzione. NULL: non si tratta di un indice basato sulla funzione. ENABLED: l'indice basato sulla funzione è abilitato. DISABLED: l'indice basato sulla funzione è disabilitato.|  
|JOIN\_INDEX|String|Indica se l'indice è un indice di join o meno.|  
  
## IndexColumns  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|INDEX\_OWNER|String|Proprietario dell'indice.|  
|INDEX\_NAME|String|Nome dell'indice.|  
|TABLE\_OWNER|String|Proprietario della tabella o del cluster.|  
|TABLE\_NAME|String|Nome della tabella o del cluster.|  
|COLUMN\_NAME|String|Nome della colonna o attributo della colonna del tipo oggetto.|  
|COLUMN\_POSITION|Decimal|La posizione della colonna o dell'attributo all'interno dell'indice.|  
|COLUMN\_LENGTH|Decimal|La lunghezza indicizzata della colonna.|  
|CHAR\_LENGTH|Decimal|La lunghezza massima dei punti di codice della colonna.|  
|DESCEND|String|Indica se la colonna è ordinata in ordine decrescente.|  
  
## Procedure  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario dell'oggetto.|  
|OBJECT\_NAME|String|Nome dell'oggetto.|  
|SUBOBJECT\_NAME|String|Nome del sottoggetto, ad esempio una partizione.|  
|OBJECT\_ID|Decimal|Il numero dell'oggetto dizionario dell'oggetto.|  
|DATA\_OBJECT\_ID|Decimal|Numero dell'oggetto dizionario del segmento contenente l'oggetto.|  
|LAST\_DDL\_TIME|DateTime|Il timestamp per l'ultima modifica dell'oggetto, risultante da un comando DDL \(Database Definition Language\), incluse le concessioni e le revoche.|  
|TIMESTAMP|String|Il timestamp per la specifica dell'oggetto \(dati di tipo carattere\).|  
|STATO|String|Lo stato dell'oggetto \(VALID, INVALID o N\/A\).|  
|TEMPORARY|String|Indica se l'oggetto è temporaneo \(la sessione corrente è in grado di visualizzare solo i dati inseriti nell'oggetto stesso\).|  
|GENERATED|String|Indica se il nome dell'oggetto è stato generato dal sistema.  \(Y &#124; N\).|  
|SECONDARY|String|Indica se questo è un oggetto secondario creato dal metodo ODCIIndexCreate di Oracle9i Data Cartridge \(Y &#124; N\).|  
|CREATED|DateTime|Data di creazione dell'oggetto.|  
  
## Sequenze  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|SEQUENCE\_OWNER|String|Nome del proprietario della sequenza.|  
|SEQUENCE\_NAME|String|Il nome della sequenza.|  
|MIN\_VALUE|Decimal|Valore minimo della sequenza.|  
|MAX\_VALUE|Decimal|Valore massimo della sequenza.|  
|INCREMENT\_BY|Decimal|Il valore dell'incremento della sequenza.|  
|CYCLE\_FLAG|String|Indica se la sequenza è prossima al raggiungimento del limite.|  
|ORDER\_FLAG|String|Indica se i numeri di sequenza sono generati in ordine.|  
|CACHE\_SIZE|Decimal|Il numero dei numeri di sequenza da memorizzare nella cache.|  
|LAST\_NUMBER|Decimal|L'ultimo numero di sequenza scritto sul disco.  Se per una sequenza viene usata la memorizzazione nella cache, il numero scritto sul disco corrisponde all'ultimo numero inserito nella cache delle sequenze.  È probabile che questo numero sia maggiore dell'ultimo numero di sequenza usato.|  
  
## Synonyms  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario del sinonimo.|  
|SYNONYM\_NAME|String|Nome del sinonimo.|  
|TABLE\_OWNER|String|Proprietario dell'oggetto a cui fa riferimento il sinonimo.|  
|TABLE\_NAME|String|Il nome dell'oggetto a cui fa riferimento il sinonimo.|  
|DB\_LINK|String|Nome del collegamento al database a cui viene fatto riferimento, se presente.|  
  
## Tabelle  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario della tabella.|  
|TABLE\_NAME|String|Nome della tabella.|  
|TYPE|String|Tipo di tabella.|  
  
## Utenti  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|NAME|String|Nome dell'utente.|  
|ID|Decimal|Numero ID dell'utente.|  
|CREATEDATE|DateTime|Data di creazione dell'utente.|  
  
## Visualizzazioni  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario della visualizzazione.|  
|VIEW\_NAME|String|Nome della visualizzazione.|  
|TEXT\_LENGTH|Decimal|Lunghezza del testo della visualizzazione.|  
|TEXT|String|Testo della visualizzazione.|  
|TYPE\_TEXT\_LENGTH|Decimal|Lunghezza della clausola di tipo della visualizzazione tipizzata.|  
|TYPE\_TEXT|String|La clausola di tipo della visualizzazione tipizzata.|  
|OID\_TEXT\_LENGTH|Decimal|La lunghezza della clausola con l'identificatore di oggetto \(OID, Object IDentifier\) della visualizzazione tipizzata.|  
|OID\_TEXT|String|La clausola con l'identificatore di oggetto \(OID, Object IDentifier\) della visualizzazione tipizzata.|  
|VIEW\_TYPE\_OWNER|String|Il proprietario del tipo di visualizzazione, se questa è tipizzata.|  
|VIEW\_TYPE|String|Tipo di visualizzazione, se questa è tipizzata.|  
|SUPERVIEW\_NAME|String|Nome della superview.|  
  
## Funzioni  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario dell'oggetto.|  
|OBJECT\_NAME|String|Nome dell'oggetto.|  
|SUBOBJECT\_NAME|String|Nome del sottoggetto, ad esempio una partizione.|  
|OBJECT\_ID|Decimal|Il numero dell'oggetto dizionario dell'oggetto.|  
|DATA\_OBJECT\_ID|Decimal|Numero dell'oggetto dizionario del segmento contenente l'oggetto.|  
|OBJECT\_TYPE|String|Il tipo di oggetto.|  
|CREATED|DateTime|Data di creazione dell'oggetto.|  
|LAST\_DDL\_TIME|DateTime|Il timestamp per l'ultima modifica dell'oggetto, risultante da un comando DDL \(Database Definition Language\), incluse le concessioni e le revoche.|  
|TIMESTAMP|String|Il timestamp per la specifica dell'oggetto \(dati di tipo carattere\).|  
|STATO|String|Lo stato dell'oggetto \(VALID, INVALID o N\/A\).|  
|TEMPORARY|String|Indica se l'oggetto è temporaneo \(la sessione corrente è in grado di visualizzare solo i dati inseriti nell'oggetto stesso\).|  
|GENERATED|String|Indica se il nome dell'oggetto è stato generato dal sistema.  \(Y &#124; N\).|  
|SECONDARY|String|Indica se questo è un oggetto secondario creato dal metodo ODCIIndexCreate di Oracle9i Data Cartridge \(Y &#124; N\).|  
  
## Pacchetti  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario dell'oggetto.|  
|OBJECT\_NAME|String|Nome dell'oggetto.|  
|SUBOBJECT\_NAME|String|Nome del sottoggetto, ad esempio una partizione.|  
|OBJECT\_ID|Decimal|Il numero dell'oggetto dizionario dell'oggetto.|  
|DATA\_OBJECT\_ID|Decimal|Numero dell'oggetto dizionario del segmento contenente l'oggetto.|  
|LAST\_DDL\_TIME|DateTime|Il timestamp per l'ultima modifica dell'oggetto, risultante da un comando DDL \(Database Definition Language\), incluse le concessioni e le revoche.|  
|TIMESTAMP|String|Il timestamp per la specifica dell'oggetto \(dati di tipo carattere\).|  
|STATO|String|Lo stato dell'oggetto \(VALID, INVALID o N\/A\).|  
|TEMPORARY|String|Indica se l'oggetto è temporaneo \(la sessione corrente è in grado di visualizzare solo i dati inseriti nell'oggetto stesso\).|  
|GENERATED|String|Indica se il nome dell'oggetto è stato generato dal sistema.  \(Y &#124; N\).|  
|SECONDARY|String|Indica se questo è un oggetto secondario creato dal metodo ODCIIndexCreate di Oracle9i Data Cartridge \(Y &#124; N\).|  
|CREATED|DateTime|Data di creazione dell'oggetto.|  
  
## PackageBodies  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario dell'oggetto.|  
|OBJECT\_NAME|String|Nome dell'oggetto.|  
|SUBOBJECT\_NAME|String|Nome del sottoggetto, ad esempio una partizione.|  
|OBJECT\_ID|Decimal|Il numero dell'oggetto dizionario dell'oggetto.|  
|DATA\_OBJECT\_ID|Decimal|Numero dell'oggetto dizionario del segmento contenente l'oggetto.|  
|LAST\_DDL\_TIME|DateTime|Il timestamp per l'ultima modifica dell'oggetto, risultante da un comando DDL \(Database Definition Language\), incluse le concessioni e le revoche.|  
|TIMESTAMP|String|Il timestamp per la specifica dell'oggetto \(dati di tipo carattere\).|  
|STATO|String|Lo stato dell'oggetto \(VALID, INVALID o N\/A\).|  
|TEMPORARY|String|Indica se l'oggetto è temporaneo \(la sessione corrente è in grado di visualizzare solo i dati inseriti nell'oggetto stesso\).|  
|GENERATED|String|Indica se il nome dell'oggetto è stato generato dal sistema.  \(Y &#124; N\).|  
|SECONDARY|String|Indica se questo è un oggetto secondario creato dal metodo ODCIIndexCreate di Oracle9i Data Cartridge \(Y &#124; N\).|  
|CREATED|DateTime|Data di creazione dell'oggetto.|  
  
## Argomenti  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Nome del proprietario dell'oggetto.|  
|PACKAGE\_NAME|String|Il nome del package.|  
|OBJECT\_NAME|String|Nome della routine o funzione.|  
|ARGUMENT\_NAME|String|Il nome dell'argomento.|  
|POSITION|Decimal|Posizione nell'elenco degli argomenti o NULL per il valore restituito di una funzione.|  
|SEQUENCE|Decimal|La sequenza di argomenti, inclusi tutti i livelli di annidamento.|  
|DEFAULT\_VALUE|String|Valore predefinito dell'argomento.|  
|DEFAULT\_LENGTH|Decimal|La lunghezza del valore predefinito dell'argomento.|  
|IN\_OUT|String|La direzione dell'argomento \(IN, OUT o IN\/OUT\).|  
|DATA\_LENGTH|Decimal|Lunghezza della colonna in byte.|  
|DATA\_PRECISION|Decimal|La lunghezza in cifre decimali \(NUMBER\) o bit \(FLOAT\).|  
|DATA\_SCALE|Decimal|Cifre a destra del separatore decimale in un numero.|  
|DATA\_TYPE|String|Tipo di dati dell'argomento.|  
  
## UniqueKeys  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario della definizione del vincolo.|  
|CONSTRAINT\_NAME|String|Il nome della definizione del vincolo.|  
|TABLE\_NAME|String|Il nome associato alla tabella \(o visualizzazione\) con la definizione del vincolo.|  
|SEARCH\_CONDITION|String|Il testo della condizione di ricerca per un vincolo CHECK.|  
|R\_OWNER|String|Il proprietario della tabella a cui viene fatto riferimento in un vincolo referenziale.|  
|R\_CONSTRAINT\_NAME|String|Il nome della definizione del vincolo UNIQUE per la tabella a cui viene fatto riferimento.|  
|DELETE\_RULE|String|La regola di eliminazione per un vincolo referenziale \(CASCADE o NO ACTION\).|  
|STATO|String|Lo stato di attivazione del vincolo \(ENABLED o DISABLED\).|  
|DEFERRABLE|String|Specifica se il vincolo può essere rinviato.|  
|VALIDATED|String|Indica se tutti i dati sono conformi al vincolo \(VALIDATED o NOT VALIDATED\).|  
|GENERATED|String|Indica se il nome del vincolo è generato dall'utente o dal sistema.|  
|BAD|String|Il valore YES indica che nel vincolo un secolo è specificato in modo ambiguo.  Per evitare errori provocati da tale ambiguità, scrivere nuovamente il vincolo usando la funzione TO\_DATE con un anno di quattro cifre.|  
|RELY|String|Indica se è applicato un vincolo ENABLED.|  
|LAST\_CHANGE|DateTime|Indica l'ultima abilitazione o disabilitazione del vincolo.|  
|INDEX\_OWNER|String|Nome dell'utente proprietario dell'indice.|  
|INDEX\_NAME|String|Nome dell'indice.|  
  
## PrimaryKeys  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario della definizione del vincolo.|  
|CONSTRAINT\_NAME|String|Il nome della definizione del vincolo.|  
|TABLE\_NAME|String|Il nome associato alla tabella \(o visualizzazione\) con la definizione del vincolo.|  
|SEARCH\_CONDITION|String|Il testo della condizione di ricerca per un vincolo CHECK.|  
|R\_OWNER|String|Il proprietario della tabella a cui viene fatto riferimento in un vincolo referenziale.|  
|R\_CONSTRAINT\_NAME|String|Il nome della definizione del vincolo UNIQUE per la tabella a cui viene fatto riferimento.|  
|DELETE\_RULE|String|La regola di eliminazione per un vincolo referenziale \(CASCADE o NO ACTION\).|  
|STATO|String|Lo stato di attivazione del vincolo \(ENABLED o DISABLED\).|  
|DEFERRABLE|String|Specifica se il vincolo può essere rinviato.|  
|VALIDATED|String|Indica se tutti i dati sono conformi al vincolo \(VALIDATED o NOT VALIDATED\).|  
|GENERATED|String|Indica se il nome del vincolo è generato dall'utente o dal sistema.|  
|BAD|String|Il valore YES indica che nel vincolo un secolo è specificato in modo ambiguo.  Per evitare errori provocati da tale ambiguità, scrivere nuovamente il vincolo usando la funzione TO\_DATE con un anno di quattro cifre.|  
|RELY|String|Indica se è applicato un vincolo ENABLED.|  
|LAST\_CHANGE|DateTime|Indica l'ultima abilitazione o disabilitazione del vincolo.|  
|INDEX\_OWNER|String|Nome dell'utente proprietario dell'indice.|  
|INDEX\_NAME|String|Nome dell'indice.|  
  
## ForeignKeys  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|PRIMARY\_KEY\_CONSTRAINT\_NAME|String|Il nome della definizione del vincolo.|  
|PRIMARY\_KEY\_OWNER|String|Proprietario della definizione del vincolo.|  
|PRIMARY\_KEY\_TABLE\_NAME|String|Il nome associato alla tabella \(o visualizzazione\) con la definizione del vincolo.|  
|FOREIGN\_KEY\_OWNER|String|Proprietario della definizione del vincolo.|  
|FOREIGN\_KEY\_CONSTRAINT\_NAME|String|Il nome della definizione del vincolo.|  
|FOREIGN\_KEY\_TABLE\_NAME|String|Il nome associato alla tabella \(o visualizzazione\) con la definizione del vincolo.|  
|SEARCH\_CONDITION|String|Il testo della condizione di ricerca per un vincolo CHECK.|  
|R\_OWNER|String|Il proprietario della tabella a cui viene fatto riferimento in un vincolo referenziale.|  
|R\_CONSTRAINT\_NAME|String|Il nome della definizione del vincolo UNIQUE per la tabella a cui viene fatto riferimento.|  
|DELETE\_RULE|String|La regola di eliminazione per un vincolo referenziale \(CASCADE o NO ACTION\).|  
|STATO|String|Lo stato di attivazione del vincolo \(ENABLED o DISABLED\).|  
|VALIDATED|String|Indica se tutti i dati sono conformi al vincolo \(VALIDATED o NOT VALIDATED\).|  
|GENERATED|String|Indica se il nome del vincolo è generato dall'utente o dal sistema.|  
|RELY|String|Indica se è applicato un vincolo ENABLED.|  
|LAST\_CHANGE|DateTime|Indica l'ultima abilitazione o disabilitazione del vincolo.|  
|INDEX\_OWNER|String|Nome dell'utente proprietario dell'indice.|  
|INDEX\_NAME|String|Nome dell'indice.|  
  
## ForeignKeyColumns  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario della definizione del vincolo.|  
|CONSTRAINT\_NAME|String|Il nome della definizione del vincolo.|  
|TABLE\_NAME|String|Il nome della tabella con la definizione del vincolo.|  
|COLUMN\_NAME|String|Il nome della colonna o dell'attributo della colonna del tipo oggetto specificata nella definizione del vincolo.|  
|POSITION|Decimal|Posizione originale della colonna o dell'attributo nella definizione dell'oggetto.|  
  
## ProcedureParameters  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|------------------|-----------------|  
|OWNER|String|Proprietario dell'oggetto.|  
|OBJECT\_NAME|String|Nome della routine o funzione.|  
|PACKAGE\_NAME|String|Nome della routine o funzione.|  
|OBJECT\_ID|Decimal|Il numero di oggetto dell'oggetto.|  
|OVERLOAD|String|Identificatore univoco dell'overload.|  
|ARGUMENT\_NAME|String|Il nome dell'argomento.|  
|POSITION|Decimal|Posizione nell'elenco degli argomenti o NULL per il valore restituito di una funzione.|  
|SEQUENCE|Decimal|La sequenza di argomenti, inclusi tutti i livelli di annidamento.|  
|DATA\_LEVEL|Decimal|Il livello di annidamento dell'argomento per i tipi composti.|  
|DATA\_TYPE|String|Tipo di dati dell'argomento.|  
|DEFAULT\_VALUE|String|Valore predefinito dell'argomento.|  
|DEFAULT\_LENGTH|Decimal|La lunghezza del valore predefinito dell'argomento.|  
|IN\_OUT|String|La direzione dell'argomento \(IN, OUT o IN\/OUT\).|  
|DATA\_LENGTH|Decimal|La lunghezza della colonna in byte.|  
|DATA\_PRECISION|Decimal|La lunghezza in cifre decimali \(NUMBER\) o bit \(FLOAT\).|  
|DATA\_SCALE|Decimal|Le cifre a destra della virgola decimale in un numero.|  
|RADIX|Decimal|La base di un argomento per un numero.|  
|CHARACTER\_SET\_NAME|String|Il nome del set di caratteri per l'argomento.|  
|TYPE\_OWNER|String|Il proprietario del tipo dell'argomento.|  
|TYPE\_NAME|String|Nome del tipo dell'argomento.  Se il tipo è un tipo locale di package, ovvero se è dichiarato in una specifica di package, in questa colonna verrà visualizzato il nome del package.|  
|TYPE\_SUBNAME|String|È rilevante solo per i tipi locali di package.  Viene visualizzato il nome del tipo che è dichiarato nel package identificato nella colonna TYPE\_NAME.|  
|TYPE\_LINK|String|È rilevante solo per i tipi locali di package quando il package identificato nella colonna TYPE\_NAME è un package remoto.  In questa colonna viene visualizzato il collegamento al database usato per fare riferimento al package remoto.|  
|PLS\_TYPE|String|Per argomenti numerici, il nome del tipo PL\/SQL dell'argomento.  In caso contrario, il valore è NULL.|  
|CHAR\_LENGTH|Decimal|Il limite dei caratteri per i dati di tipo stringa.|  
|CHAR\_USED|String|Indica se il limite di byte \(B\) o il limite di caratteri \(C\) è ufficiale per la stringa.|  
  
## Vedere anche  
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)