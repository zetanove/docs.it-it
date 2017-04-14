---
title: "SqlMetal.exe (strumento per la generazione del codice) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
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
helpviewer_keywords: 
  - "SQLMetal [LINQ to SQL]"
  - "generazione di codice (strumento)"
  - "SQLMetal.exe"
  - "LINQ to SQL, serializzazione"
  - "LINQ to SQL, file DBML"
  - "LINQ to SQL, SQLMetal"
ms.assetid: 819e5a96-7646-4fdb-b14b-fe31221b0614
caps.latest.revision: 43
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 43
---
# SqlMetal.exe (strumento per la generazione del codice)
Lo strumento da riga di comando SqlMetal genera codice e mapping per il componente [!INCLUDE[vbtecdlinq](../../../includes/vbtecdlinq-md.md)] di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Mediante l'applicazione delle opzioni riportate più avanti in questo argomento è possibile usare SqlMetal per eseguire diverse operazioni, fra cui:  
  
-   A partire da un database, generare codice sorgente e attributi di mapping oppure un file di mapping.  
  
-   A partire da un database, generare un file .dbml \(Database Markup Language\) intermedio da personalizzare.  
  
-   A partire da un file .dbml, generare codice e attributi di mapping oppure un file di mapping.  
  
 Viene installato automaticamente con Visual Studio. Per impostazione predefinita, il file si trova in `drive`:\\Programmi\\Microsoft SDKs\\Windows\\v`n.nn`\\bin. Se non si installa Visual Studio, è possibile ottenere il file SQLMetal anche scaricando [Windows SDK](http://go.microsoft.com/fwlink/?LinkId=142225).  
  
> [!NOTE]
>  Gli sviluppatori che usano Visual Studio possono usare anche [!INCLUDE[vs_ordesigner_long](../../../includes/vs-ordesigner-long-md.md)] per generare classi di entità. Quando si usano database di grandi dimensioni, l'approccio basato sulla riga di comando rappresenta la scelta più adeguata. In quanto strumento da riga di comando, SqlMetal può essere usato in un processo di compilazione.  
  
 Per eseguire lo strumento, usare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7. Per altre informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md). Al prompt dei comandi digitare quanto segue:  
  
## Sintassi  
  
```  
sqlmetal [options] [<input file>]  
```  
  
## Opzioni  
 Per visualizzare l'elenco di opzioni più aggiornato, digitare `sqlmetal /?` al prompt dei comandi dal percorso di installazione.  
  
 **Opzioni di connessione**  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/server:** *\<nome\>*|Specifica il nome del server di database.|  
|**\/database:** *\<nome\>*|Specifica il catalogo del database contenuto nel server.|  
|**\/user:** *\<nome\>*|Specifica l'ID utente di accesso. Valore predefinito: autenticazione di Windows.|  
|**\/password:** *\<password\>*|Specifica la password di accesso. Valore predefinito: autenticazione di Windows.|  
|**\/conn:** *\<stringa di connessione\>*|Specifica la stringa di connessione al database. Non può essere usata con l'opzione **\/server**, **\/database**, **\/user** o **\/password**.<br /><br /> Non includere il nome file nella stringa di connessione. Aggiungere invece il nome file alla riga di comando come file di input. La riga seguente, ad esempio, specifica "c:\\northwnd.mdf" come file di input: **sqlmetal \/code:"c:\\northwind.cs" \/language:csharp "c:\\northwnd.mdf"**.|  
|**\/timeout:** *\<secondi\>*|Specifica il valore di timeout quando SqlMetal accede al database. Valore predefinito: 0 \(ovvero nessun limite di tempo\).|  
  
 **Opzioni di estrazione**  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/views**|Estrae viste di database.|  
|**\/functions**|Estrae funzioni di database.|  
|**\/sprocs**|Estrae stored procedure.|  
  
 **Opzioni di output**  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/dbml** *\[:file\]*|Invia l'output come file .dbml. Non può essere usata con l'opzione **\/map**.|  
|**\/code** *\[:file\]*|Invia l'output come codice sorgente. Non può essere usata con l'opzione **\/dbml**.|  
|**\/map** *\[:file\]*|Genera un file di mapping XML anziché gli attributi. Non può essere usata con l'opzione **\/dbml**.|  
  
 **Varie**  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/language:** *\<linguaggio\>*|Specifica il linguaggio del codice sorgente.<br /><br /> Valori validi per *\<linguaggio\>*: vb, csharp.<br /><br /> Valore predefinito: derivato dall'estensione nel nome file del codice.|  
|**\/namespace:** *\<nome\>*|Specifica lo spazio dei nomi del codice generato. Valore predefinito: nessuno spazio dei nomi.|  
|**\/context:** *\<tipo\>*|Specifica il nome della classe del contesto dati. Valore predefinito: derivato dal nome del database.|  
|**\/entitybase:** *\<tipo\>*|Specifica la classe base delle classi di entità nel codice generato. Valore predefinito: le entità non dispongono di classe base.|  
|**\/pluralize**|Rende automaticamente plurali o singolari i nomi delle classi e dei membri.<br /><br /> Opzione disponibile solo nella versione in lingua inglese degli Stati Uniti.|  
|**\/serialization:** *\<opzione\>*|Genera classi serializzabili.<br /><br /> Valori validi per *\<opzione\>*: None, Unidirectional. Valore predefinito: None.<br /><br /> Per altre informazioni, vedere [Serializzazione](../../../docs/framework/data/adonet/sql/linq/serialization.md).|  
  
 **File di input**  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\<file di input\>**|Specifica un file .mdf di SQL Server Express, un file .sdf di [!INCLUDE[ssEW](../../../includes/ssew-md.md)] oppure un file .dbml intermedio.|  
  
## Note  
 Il funzionamento di SqlMetal prevede di fatto due passaggi:  
  
-   Estrazione dei metadati del database in un file .dbml.  
  
-   Generazione di un file di output di codice.  
  
     Le opzioni della riga di comando, se usate correttamente, consentono di creare codice sorgente [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] o C\# oppure un file di mapping XML.  
  
 Per estrarre i metadati da un file .mdf è necessario aggiungere il nome di tale file in coda a tutte le altre opzioni specificate.  
  
 Se non è specificato alcun valore per **\/server**, si presuppone che sia **localhost\/sqlexpress**.  
  
 [!INCLUDE[sqprsqext](../../../includes/sqprsqext-md.md)] genera un'eccezione se almeno una delle condizioni seguenti è vera:  
  
-   SqlMetal tenta di estrarre una stored procedure che chiama se stessa.  
  
-   Il livello di annidamento di una stored procedure, di una funzione o di una vista è maggiore di 32.  
  
     SqlMetal rileva questa eccezione e la segnala come avviso.  
  
 Per specificare un nome file di input, aggiungere il nome nella riga di comando come file di input. Non è possibile includere il nome file nella stringa di connessione mediante l'opzione **\/conn**.  
  
## Esempi  
 Genera un file .dbml che contiene metadati SQL estratti:  
  
 **sqlmetal \/server:myserver \/database:northwind \/dbml:mymeta.dbml**  
  
 Genera un file .dbml che contiene metadati SQL estratti da un file .mdf tramite SQL Server Express:  
  
 **sqlmetal \/dbml:mymeta.dbml mydbfile.mdf**  
  
 Genera un file .dbml che contiene metadati SQL estratti da SQL Server Express:  
  
 **sqlmetal \/server:.\\sqlexpress \/dbml:mymeta.dbml \/database:northwind**  
  
 Genera codice sorgente a partire da un file di metadati .dmbl:  
  
 **sqlmetal \/namespace:nwind \/code:nwind.cs \/language:csharp mymetal.dbml**  
  
 Genera codice sorgente direttamente da metadati SQL:  
  
 **sqlmetal \/server:myserver \/database:northwind \/namespace:nwind \/code:nwind.cs \/language:csharp**  
  
> [!NOTE]
>  Quando si usa l'opzione **\/pluralize** con il database di esempio Northwind, si verifica il comportamento seguente. Quando SqlMetal crea nomi di tipo riga per le tabelle, i relativi nomi sono al singolare. Quando crea proprietà <xref:System.Data.Linq.DataContext> per le tabelle, i relativi nomi sono invece al plurale. Per coincidenza, i nomi delle tabelle contenute nel database di esempio Northwind sono già al plurale. Pertanto, l'opzione di pluralizzazione di fatto non viene usata. Di norma le tabelle di database vengono denominate al singolare, mentre le raccolte di .NET vengono denominate al plurale.  
  
## Vedere anche  
 [Procedura: generare il modello a oggetti in Visual Basic o C\#](../../../docs/framework/data/adonet/sql/linq/how-to-generate-the-object-model-in-visual-basic-or-csharp.md)   
 [Generazione di codice in LINQ to SQL](../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)   
 [Mapping esterno](../../../docs/framework/data/adonet/sql/linq/external-mapping.md)