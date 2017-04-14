---
title: "Stringhe di connessione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 78d516bc-c99f-4865-8ff1-d856bc1a01c0
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Stringhe di connessione
Una stringa di connessione contiene informazioni di inizializzazione che vengono passate come parametro da un provider di dati a un'origine dati.  La sintassi dipende dal provider di dati e la stringa di connessione viene analizzata durante il tentativo di aprire una connessione.  Le stringhe di connessione usate da Entity Framework contengono informazioni che consentono di connettersi al provider di dati ADO.NET sottostante che supporta Entity Framework, nonché  informazioni sui file di modello e di mapping richiesti.  
  
 La stringa di connessione viene usata dal provider EntityClient quando si accede ai metadati di modello e di mapping e quando si effettua la connessione all'origine dati.  Per impostare o accedere alla stringa di connessione, usare la proprietà <xref:System.Data.EntityClient.EntityConnection.ConnectionString%2A> di <xref:System.Data.EntityClient.EntityConnection>.  La classe <xref:System.Data.EntityClient.EntityConnectionStringBuilder> può essere usata a livello di codice per costruire o accedere ai parametri nella stringa di connessione.  Per altre informazioni, vedere [Procedura: compilare una stringa di connessione EntityConnection](../../../../../docs/framework/data/adonet/ef/how-to-build-an-entityconnection-connection-string.md).  
  
 Gli [strumenti di Entity Data Model](http://msdn.microsoft.com/it-it/91076853-0881-421b-837a-f582f36be527) consentono di generare una stringa di connessione che viene archiviata nel file di configurazione dell'applicazione.  L'oggetto <xref:System.Data.Objects.ObjectContext> consente di recuperare automaticamente queste informazioni di connessione quando si creano query di oggetto.  È possibile accedere all'oggetto <xref:System.Data.EntityClient.EntityConnection> usato da un'istanza di <xref:System.Data.Objects.ObjectContext> direttamente dalla proprietà <xref:System.Data.Objects.ObjectContext.Connection%2A>.  Per altre informazioni, vedere [Managing Connections and Transactions](http://msdn.microsoft.com/it-it/b6659d2a-9a45-4e98-acaa-d7a8029e5b99).  
  
## Parametri della stringa di connessione  
 Il formato di una stringa di connessione è un elenco delimitato da punti e virgola composto da coppie di parametri chiave\/valore:  
  
 `keyword1=value; keyword2=value;`  
  
 Il segno di uguale \(\=\) connette ogni parola chiave al relativo valore.  Le parole chiave non fanno distinzione tra maiuscole e minuscole e gli spazi tra coppie chiave\/valore vengono ignorati.  È tuttavia possibile che tale distinzione sia valida per i valori, a seconda dell'origine dati.  I valori contenenti punto e virgola, virgolette singole o virgolette doppie devono essere racchiusi tra virgolette doppie.  Nella tabella seguente sono inclusi i nomi validi per i valori di parola chiave nella proprietà <xref:System.Data.EntityClient.EntityConnection.ConnectionString%2A>.  
  
|Parola chiave|Descrizione|  
|-------------------|-----------------|  
|`Provider`|Obbligatoria se la parola chiave `Name` non è specificata.  Nome del provider usato per recuperare l'oggetto <xref:System.Data.Common.DbProviderFactory> per il provider sottostante.  Questo valore è costante.<br /><br /> Quando la parola chiave `Name` non è inclusa in una stringa di connessione di entità, per la parola chiave `Provider` è necessario specificare un valore non vuoto.  Questa parola chiave e la parola chiave `Name` si escludono a vicenda.|  
|`Provider Connection String`|Parametro facoltativo.  Indica la stringa di connessione specifica del provider passata all'origine dati sottostante.  Questa stringa di connessione viene espressa usando coppie parola chiave\/valore valide per il provider di dati.  Una parola chiave `Provider Connection String` non valida produrrà un errore di runtime quando viene valutata dall'origine dati.<br /><br /> Questa parola chiave e la parola chiave `Name` si escludono a vicenda.<br /><br /> Il valore della parola chiave `Provider Connection String` deve essere racchiuso tra virgolette.  Di seguito è riportato un esempio:<br /><br /> `Provider Connection String ="Server=serverName; User ID = userID";`<br /><br /> L'esempio seguente non funzionerà:<br /><br /> `Provider Connection String =Server=serverName; User ID = userID`|  
|`Metadata`|Obbligatoria se la parola chiave `Name` non è specificata.  Elenco di percorsi di directory, file e risorse delimitato da barre verticali in cui cercare informazioni relative a metadati e mapping.  Di seguito è riportato un esempio:<br /><br /> `Metadata=`<br /><br /> `c:\model &#124; c:\model\sql\mapping.msl;`<br /><br /> Gli spazi vuoti a ogni lato del separatore vengono ignorati.<br /><br /> Questa parola chiave e la parola chiave `Name` si escludono a vicenda.|  
|`Name`|L'applicazione può eventualmente specificare il nome della connessione in un file di configurazione dell'applicazione che fornisce i valori della stringa di connessione parola chiave\/valore obbligatori.  In questo caso, non è possibile specificare tali valori direttamente nella stringa di connessione.  L'utilizzo della parola chiave `Name` non è consentito in un file di configurazione.<br /><br /> Quando la parola chiave `Name` non è inclusa nella stringa di connessione, per la parola chiave Provider è necessario specificare valori non vuoti.<br /><br /> Questa parola chiave e tutte le altre parole chiave per la stringa di connessione si escludono a vicenda.|  
  
 Quello che segue è un esempio di stringa di connessione per il [modello Sales di AdventureWorks](http://msdn.microsoft.com/it-it/f16cd988-673f-4376-b034-129ca93c7832) archiviato nel file di configurazione dell'applicazione:  
  
  
  
## Percorsi dei file di modello e di mapping  
 Il parametro `Metadata` contiene un elenco di percorsi in cui il provider `EntityClient` può eseguire una ricerca di file di modello e di mapping.  I file di modello e di mapping spesso sono distribuiti nella stessa directory del file eseguibile dell'applicazione.  Tali file possono essere distribuiti anche in un percorso specifico o inclusi come risorse incorporate nell'applicazione.  
  
 Le risorse incorporate vengono specificate nel modo seguente:  
  
```  
Metadata=res://<assemblyFullName>/<resourceName>.   
```  
  
 Per la definizione del percorso di una risorsa incorporata, sono disponibili le opzioni seguenti:  
  
|||  
|-|-|  
|Opzione|Descrizione|  
|`assemblyFullName`|Nome completo di un assembly con la risorsa incorporata.  Include il nome semplice, il nome della versione, la lingua supportata e la chiave pubblica, nel modo seguente:<br /><br /> `ResourceLib, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`<br /><br /> Le risorse possono essere incorporate in qualsiasi assembly accessibile dall'applicazione.<br /><br /> Se si specifica un carattere jolly \(\*\) per `assemblyFullName`, il runtime di Entity Framework cercherà le risorse nei percorsi seguenti, in questo ordine:<br /><br /> 1.  L'assembly chiamante.<br />2.  Gli assembly a cui si fa riferimento.<br />3.  Gli assembly nella directory bin di un'applicazione.<br /><br /> Se i file non sono in uno di questi percorsi, verrà generata un'eccezione. **Note:**  Quando si usa un carattere jolly \(\*\), la ricerca di risorse con il nome corretto deve essere eseguita in tutti gli assembly.  Per migliorare le prestazioni, specificare il nome dell'assembly anziché il carattere jolly.|  
|`resourceName`|Nome della risorsa inclusa, ad esempio AdvendtureWorksModel.csdl.  I servizi di metadati cercheranno solo i file o le risorse con estensione csdl, ssdl o msl.  Se la parola chiave `resourceName` non è specificata, verranno caricate tutte le risorse dei metadati.  Le risorse devono disporre di nomi univoci all'interno di un assembly.  Se più file con lo stesso nome sono definiti in directory diverse nell'assembly, la parola chiave `resourceName` deve includere la struttura di cartelle prima del nome della risorsa, ad esempio NomeCartella.NomeFile.csdl.<br /><br /> `resourceName` non è obbligatoria quando si specifica un carattere jolly \(\*\) per `assemblyFullName`.|  
  
> [!NOTE]
>  Per migliorare le prestazioni, incorporare le risorse nell'assembly chiamante, ad eccezione degli scenari non Web in cui non è presente alcun riferimento ai file di mapping e di metadati sottostanti nell'assembly chiamante.  
  
 Nell'esempio seguente vengono caricati tutti i file di modello e di mapping nell'assembly chiamante, gli assembly a cui si fa riferimento e gli altri assembly nella directory bin di un'applicazione.  
  
```  
Metadata=res://*/  
```  
  
 Nell'esempio seguente viene caricato il file model.csdl dell'assembly AdventureWorks e vengono caricati i file model.ssdl e model.msl dalla directory predefinita dell'applicazione in esecuzione.  
  
```  
Metadata=res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.csdl|model.ssdl|model.msl  
```  
  
 Nell'esempio seguente sono caricate le tre risorse specificate dall'assembly specifico.  
  
```  
Metadata=res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.csdl|   
res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.ssdl|   
res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.msl  
```  
  
 Nell'esempio seguente sono caricate tutte le risorse incorporate con estensioni csdl, msl e ssdl dall'assembly.  
  
```  
Metadata=res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/  
```  
  
 Nell'esempio seguente vengono caricate tutte le risorse nel percorso del file relativo oltre a "datadir\\metadata \\" dal percorso dell'assembly caricato.  
  
```  
Metadata=datadir\metadata\  
```  
  
 Nell'esempio seguente vengono caricate tutte le risorse nel percorso del file relativo provenienti dal percorso dell'assembly caricato.  
  
```  
Metadata=.\  
```  
  
## Supporto per la stringa di sostituzione &#124; DataDirectory &#124; e l'operatore radice dell'applicazione Web \(~\)  
 `DataDirectory` e l'operatore ~ vengono usati nella proprietà <xref:System.Data.EntityClient.EntityConnection.ConnectionString%2A> `` come parte delle parole chiave `Metadata` e `Provider Connection String`.  <xref:System.Data.EntityClient.EntityConnection> inoltra `DataDirectory` e l'operatore ~ rispettivamente a <xref:System.Data.Metadata.Edm.MetadataWorkspace> e al provider di archiviazione.  
  
|Termine|Descrizione|  
|-------------|-----------------|  
|`&#124;DataDirectory&#124;`|Si risolve in un percorso relativo di file di mapping e di metadati.  Si tratta del valore impostato attraverso il metodo `AppDomain.SetData("DataDirectory", objValue)`.  La stringa di sostituzione `DataDirectory` deve essere circondata dai caratteri barra verticale e non può essere rappresentata da uno spazio vuoto tra il nome e i caratteri barra verticale.  Il nome `DataDirectory` non supporta la distinzione tra maiuscole e minuscole.<br /><br /> Se una directory fisica denominata "DataDirectory" deve essere passata come membro dell'elenco di percorsi di metadati, aggiungere uno spazio vuoto su un lato o su entrambi i lati del nome, ad esempio: `Metadata="DataDirectory1 &#124; DataDirectory &#124; DataDirectory2"`.  Un'applicazione ASP.NET risolve &#124; DataDirectory &#124; nella cartella "\<application root\>\/app\_data".|  
|~|Si risolve nella radice dell'applicazione Web.  Il carattere ~ in una posizione iniziale viene sempre interpretato come l'operatore radice dell'applicazione Web \(~\), sebbene possa rappresentare una sottodirectory locale valida.  Per fare riferimento a questo tipo di sottodirectory locale, l'utente deve passare in modo esplicito `./~`.|  
  
 `DataDirectory` e l'operatore ~ devono essere specificati solo all'inizio di un percorso in quanto non vengono risolti in altre posizioni.  Entity Framework tenterà di risolvere `~/data`, ma considererà `/data/~` come un percorso fisico.  
  
 Un percorso che inizia con `DataDirectory` o con l'operatore ~ non può essere risolto in un percorso fisico al di fuori del ramo di `DataDirectory` e dell'operatore ~.  Ad esempio, i percorsi seguenti risolveranno: `~` , `~/data` , `~/bin/Model/SqlServer`.  I percorsi seguenti non riusciranno a risolvere: `~/..`, `~/../other`.  
  
 `DataDirectory` e l'operatore ~ possono essere estesi per includere sottodirectory, nel modo seguente: `|DataDirectory|\Model`, `~/bin/Model`  
  
 La risoluzione della stringa di sostituzione `DataDirectory` e l'operatore ~ è non ricorsiva.  Ad esempio, quando `DataDirectory` include il carattere `~`, si verificherà un'eccezione.  In questo modo viene impedita una ricorsione infinita.  
  
## Vedere anche  
 [Utilizzo di provider di dati](../../../../../docs/framework/data/adonet/ef/working-with-data-providers.md)   
 [Considerazioni sulla distribuzione](../../../../../docs/framework/data/adonet/ef/deployment-considerations.md)   
 [Managing Connections and Transactions](http://msdn.microsoft.com/it-it/b6659d2a-9a45-4e98-acaa-d7a8029e5b99)   
 [Stringhe di connessione](../../../../../docs/framework/data/adonet/connection-strings.md)