---
title: "Stringhe di connessione in ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 745c5f95-2f02-4674-b378-6d51a7ec2490
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Stringhe di connessione in ADO.NET
In .NET Framework 2.0 sono state introdotte nuove funzionalità per l'uso delle stringhe di connessione, tra cui l'introduzione di nuove parole chiave nelle classi di generatori di stringhe di connessione che facilitano la creazione di stringhe di connessione valide in fase di esecuzione.  
  
 Una stringa di connessione contiene informazioni di inizializzazione che vengono passate come parametro da un provider di dati a un'origine dati.  La sintassi dipende dal provider di dati e la stringa di connessione viene analizzata durante il tentativo di aprire una connessione.  Gli errori di sintassi generano un'eccezione in fase di esecuzione, ma altri errori si verificano solo dopo che l'origine dati riceve informazioni sulla connessione.  Una volta convalidata, l'origine dati applica le opzioni specificate nella stringa di connessione e apre la connessione.  
  
 Il formato di una stringa di connessione è un elenco delimitato da punti e virgola composto da coppie di parametri chiave\/valore:  
  
 `keyword1=value; keyword2=value;`  
  
 Le parole chiave non fanno distinzione tra maiuscole e minuscole e gli spazi tra coppie chiave\/valore vengono ignorati.  Tuttavia, i valori possono fare distinzione tra maiuscole e minuscole, a seconda dell'origine dati.  I valori contenenti punto e virgola, virgolette singole o virgolette doppie devono essere racchiusi tra virgolette doppie.  
  
 La sintassi di una stringa di connessione valida varia a seconda del provider e, nel corso degli anni, si è evoluta dalle API iniziali quale ODBC.  Il provider di dati .NET Framework per SQL Server \(SqlClient\)  incorpora numerosi elementi della sintassi precedente e, in genere, presenta una sintassi delle stringhe di connessione comuni più flessibile.  Esistono spesso sinonimi ugualmente validi per gli elementi della sintassi delle stringhe di connessione, ma alcuni errori di sintassi e di ortografia possono causare problemi.  Ad esempio "`Integrated Security=true`" è valido, mentre "`IntegratedSecurity=true`" genera un errore.  Inoltre, le stringhe di connessione create in fase di esecuzione da input dell'utente non convalidato possono portare ad attacchi injection alle stringhe, compromettendo la sicurezza nell'origine dati.  
  
 Per risolvere questi problemi, in ADO.NET 2.0 sono stati introdotti nuovi generatori di stringhe di connessione per ogni provider di dati .NET Framework.  Le parole chiave sono esposte come proprietà, consentendo la convalida della sintassi delle stringhe di connessione prima dell'invio all'origine dati.  
  
## In questa sezione  
 [Compilatori di stringhe di connessione](../../../../docs/framework/data/adonet/connection-string-builders.md)  
 Viene illustrato come usare le classi `ConnectionStringBuilder` per creare stringhe di connessione valide in fase di esecuzione.  
  
 [Stringhe di connessione e file di configurazione](../../../../docs/framework/data/adonet/connection-strings-and-configuration-files.md)  
 Viene illustrato come archiviare e recuperare le stringhe di connessione nei file di configurazione.  
  
 [Sintassi della stringa di connessione](../../../../docs/framework/data/adonet/connection-string-syntax.md)  
 Viene descritto come configurare stringhe di connessione specifiche del provider per `SqlClient`, `OracleClient`, `OleDb` e `Odbc`.  
  
 [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md)  
 Vengono illustrate tecniche per proteggere le informazioni usate per la connessione a un'origine dati.  
  
## Vedere anche  
 [Connessione a un'origine dati](../../../../ocs/framework/data/adonet/connecting-to-a-data-source.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)