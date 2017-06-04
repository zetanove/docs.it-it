---
title: "Classe e propriet&#224; dell&#39;eccezione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Exception (classe)"
  - "eccezioni, Exception (classe)"
ms.assetid: e2e1f8c4-e7b4-467d-9a66-13c90861221d
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Classe e propriet&#224; dell&#39;eccezione
La classe <xref:System.Exception> rappresenta la classe base da cui ereditano le eccezioni.  Gli oggetti eccezione costituiscono per la maggior parte istanze di classi derivate da **Exception**, ma è possibile generare come eccezione qualsiasi oggetto derivato dalla classe <xref:System.Object>.  Si noti che non tutti i linguaggi supportano la generazione e l'intercettazione di oggetti non derivati da **Exception**.  Nella quasi totalità dei casi è consigliabile generare e intercettare solo oggetti **Exception**.  
  
 La classe **Exception** presenta varie proprietà che semplificano la comprensione delle eccezioni.  Queste proprietà includono:  
  
-   La proprietà <xref:System.Exception.StackTrace%2A>.  
  
     Contiene una traccia dello stack utilizzabile per determinare se si è verificato un errore.  La traccia dello stack include il nome del file di origine e il numero di riga del programma, se sono disponibili informazioni di debug.  
  
-   La proprietà <xref:System.Exception.InnerException%2A>.  
  
     Utilizzabile per creare e preservare una serie di eccezioni durante la gestione delle eccezioni stesse.  È possibile utilizzare questa proprietà per creare una nuova eccezione contenente eccezioni intercettate in precedenza.  L'eccezione originale può essere catturata dalla seconda eccezione della proprietà **InnerException**, consentendo al codice che gestisce la seconda eccezione di esaminare le informazioni aggiuntive.  
  
     Si supponga ad esempio di disporre di un metodo con cui viene letto un file e vengono formattati i dati.  Nel codice viene tentata la lettura del contenuto del file, ma viene generata un'eccezione FileException.  Il metodo intercetta l'eccezione FileException e genera un'eccezione BadFormatException.  In questo caso è possibile salvare FileException nella proprietà **InnerException** di BadFormatException.  
  
     Per consentire al chiamante di determinare più facilmente la ragione alla base della generazione di un'eccezione, è talvolta utile che un metodo intercetti un'eccezione generata da una routine di supporto, generando a propria volta un'eccezione più indicativa dell'errore che si è verificato.  Verrà creata un'eccezione nuova e più significativa, nella quale si imposta per l'eccezione interna un riferimento all'eccezione originale.  Tale eccezione più significativa potrà quindi essere generata per il chiamante.  Si noti che, grazie a questa funzionalità, è possibile creare una serie di eccezioni collegate che termina con la prima eccezione generata.  
  
-   La proprietà <xref:System.Exception.Message%2A>.  
  
     Fornisce informazioni dettagliate sulla causa di un'eccezione.  **Message** è la lingua specificata nella proprietà proprietà <xref:System.Threading.Thread.CurrentUICulture%2A?displayProperty=fullName> del thread che genera l'eccezione.  
  
-   La proprietà <xref:System.Exception.HelpLink%2A>.  
  
     Può contenere l'URL \(o URN\) di un file della Guida in cui sono fornite informazioni dettagliate sulla causa di un'eccezione.  
  
-   Proprietà <xref:System.Exception.Data%2A>  
  
     Si tratta di una proprietà IDictionary che conserva dati arbitrari in coppie chiave\-valore.  
  
 La maggior parte delle classi che ereditano dall'oggetto **Exception** non implementano membri aggiuntivi né forniscono funzionalità supplementari; si limitano a ereditare dall'oggetto **Exception**\\.  È pertanto possibile trovare le informazioni più importanti per un'eccezione nella gerarchia delle eccezioni, nel nome dell'eccezione e nelle informazioni contenute nell'eccezione stessa.  
  
## Vedere anche  
 [Gerarchia delle eccezioni](../../../docs/standard/exceptions/exception-hierarchy.md)   
 [Nozioni fondamentali sulla gestione delle eccezioni](../../../docs/standard/exceptions/exception-handling-fundamentals.md)   
 [Suggerimenti per le eccezioni](../../../docs/standard/exceptions/best-practices-for-exceptions.md)   
 [Eccezioni](../../../docs/standard/exceptions/index.md)