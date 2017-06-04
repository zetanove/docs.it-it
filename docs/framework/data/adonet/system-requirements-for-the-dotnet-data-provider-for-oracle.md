---
title: "Requisiti di sistema per il provider di dati.NET Framework per Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 054f76b9-1737-43f0-8160-84a00a387217
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Requisiti di sistema per il provider di dati.NET Framework per Oracle
Per usare il provider di dati .NET Framework per Oracle, è necessario disporre di Microsoft Data Access Components \(MDAC\) 2.6 o versione successiva.  Si consiglia l'uso di MDAC 2.8 SP1.  
  
 È inoltre necessario installare il client Oracle 8i Release 3 \(8.1.7\) o versione successiva.  
  
 Non è possibile eseguire l'accesso ai database UTF16 mediante i software client Oracle precedenti alla versione Oracle 9i in quanto UTF16 è una nuova funzione di Oracle 9i.  Per usare questa funzione, è necessario aggiornare il software client alla versione Oracle 9i o versione successiva.  
  
## Utilizzo del provider di dati per dati Oracle e Unicode  
 Di seguito è riportato un elenco di problemi relativi a Unicode da tenere presente quando si usano il provider di dati .NET Framework per Oracle e le librerie del client Oracle.  Per altre informazioni, vedere la documentazione di Oracle.  
  
### Impostazione del valore Unicode in un attributo della stringa di connessione  
 Quando si usa Oracle, è possibile usare l'attributo della stringa di connessione  
  
```  
Unicode=True   
```  
  
 per l'inizializzazione delle librerie del client Oracle in modalità UTF\-16.  In questo modo le librerie del client Oracle accetteranno stringhe UTF\-16 \(molto simili a quelle UCS\-12\) anziché multibyte.  Ciò consente al provider di dati per Oracle di usare qualsiasi pagina di codice Oracle senza eseguire ulteriori operazioni di conversione.  Questa configurazione è utile solo se per la comunicazione con un database Oracle 9i viene usato un client Oracle 9i e un set di caratteri alternativo di AL16UTF16.  Per la comunicazione tra un client Oracle 9i e un server Oracle 9i, è necessario disporre di ulteriori risorse che consentano di convertire i valori **CommandText** Unicode nel set di caratteri multibyte appropriato usato dal server Oracle9i.  Questo può essere evitato se si è certi di disporre della configurazione corretta, aggiungendo `Unicode=True` alla stringa di connessione.  
  
### Combinazione di versioni del client e del server Oracle  
 I client Oracle 8i non possono accedere ai dati **NCHAR**, **NVARCHAR2** o **NCLOB** dei database Oracle 9i quando il set di caratteri nazionale del server specificato è AL16UTF16 \(impostazione predefinita di Oracle 9i\)  poiché il supporto del set di caratteri UTF\-16 è stato introdotto solo con Oracle 9i.  
  
### Uso di dati UTF\-8  
 Per impostare il set di caratteri alternativo, impostare la chiave del Registro di sistema HKEY\_LOCAL\_MACHINE\\SOFTWARE\\ORACLE\\HOMEID\\NLS\_LANG su UTF8.  Per altre informazioni, vedere le note di installazione di Oracle sulla piattaforma.  L'impostazione predefinita corrisponde al set di caratteri primario della lingua in cui si esegue l'installazione del software client Oracle.  Se la lingua non viene impostata in modo che corrisponda al set di caratteri della lingua nazionale del database al quale si esegue la connessione, i dati inviati e ricevuti dall'associazione delle colonne e dei parametri saranno basati sul set di caratteri del database primario anziché sul set di caratteri nazionale.  
  
### OracleLob consente di aggiornare solo caratteri completi.  
 Per motivi di usabilità, l'oggetto <xref:System.Data.OracleClient.OracleLob> eredita dalla classe Stream di .NET Framework e fornisce i metodi **ReadByte** e **WriteByte**.  Implementa, inoltre, metodi quali **CopyTo** ed **Erase**, da usare sulle sezioni degli oggetti **LOB** di Oracle.  Al contrario, il software client Oracle mette a disposizione vari API per l'uso con i tipi di dati **LOB** \(**CLOB** e **NCLOB**\).  Tuttavia, queste API funzionano solo con i caratteri completi.  A causa di questa differenza, il provider di dati per Oracle implementa il supporto di **Read** e **ReadByte** per l'uso con i dati UTF\-16 in modalità byte per byte.  Tuttavia, gli altri metodi dell'oggetto **OracleLob** consentono solo operazioni con caratteri completi.  
  
## Vedere anche  
 [Oracle e ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)