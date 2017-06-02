---
title: "LINQ to SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 73d13345-eece-471a-af40-4cc7a2f11655
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# LINQ to SQL
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] è un componente di [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] versione 3.5 che fornisce l'infrastruttura in fase di esecuzione per la gestione di dati relazionali come oggetti.  
  
> [!NOTE]
>  I dati relazionali vengono visualizzati come una raccolta di tabelle bidimensionali \(*relazioni* o *file flat*\), in cui le colonne comuni collegano tra loro le tabelle.  Per usare [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] in modo efficiente, è necessario avere familiarità con i principi di base dei database relazionali.  
  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene eseguito il mapping del modello dati di un database relazionale a un modello a oggetti espresso nel linguaggio di programmazione dello sviluppatore.  Quando viene eseguita l'applicazione, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] converte in SQL le query LINQ \(Language Integrated Query\) nel modello a oggetti e le invia al database per l'esecuzione. Quando il database restituisce i risultati, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] li converte di nuovo in oggetti che possono essere usati nel linguaggio di programmazione dello sviluppatore.  
  
 Gli sviluppatori che usano [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)], adoperano in genere anche [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] che fornisce un'interfaccia utente per l'implementazione di molte funzionalità di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
 Nella documentazione inclusa in questa versione di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] vengono descritti i blocchi di compilazione di base, il processi e le tecniche necessari per la compilazione di applicazioni [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  È possibile effettuare la ricerca di problemi specifici in MSDN Library e partecipare al [Forum su LINQ](http://go.microsoft.com/fwlink/?LinkId=76488), dove è possibile discutere in dettaglio argomenti più complessi con gli esperti.  Infine, nel white paper relativo alla [conversione da LINQ a SQL e alle query integrate con il linguaggio .NET per i dati relazionali](http://go.microsoft.com/fwlink/?LinkId=93205) sono disponibili informazioni dettagliate sulla tecnologia [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], oltre a esempi di codice [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] e C\#.  
  
## In questa sezione  
 [Introduzione](../../../../../../docs/framework/data/adonet/sql/linq/getting-started.md)  
 Viene fornita una panoramica di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] e vengono fornite informazioni su come iniziare a usare [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
 [Guida per programmatori](../../../../../../docs/framework/data/adonet/sql/linq/programming-guide.md)  
 Vengono descritte le procedure per eseguire il mapping, creare query, eseguire operazioni di aggiornamento e debug e attività simili.  
  
 [Riferimenti](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)  
 Fornisce informazioni di riferimento sui diversi aspetti di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  Tra gli argomenti vengono descritti il mapping dei tipi CLR SQL, la conversione dell'operatore di query standard e altri.  
  
 [Esempi](../../../../../../docs/framework/data/adonet/sql/linq/samples.md)  
 Vengono forniti collegamenti a esempi di codice [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] e C\#.  
  
## Sezioni correlate  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)  
 Fornisce una panoramica delle tecnologie [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)].  
  
 [LINQ](../Topic/LINQ%20in%20Visual%20Basic.md)  
 Vengono descritte le tecnologie [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] per gli utenti di [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)].  
  
 [LINQ to ADO.NET](http://msdn.microsoft.com/it-it/be3297b9-1b54-4d4c-82a8-add0d79c2006)  
 Vengono forniti collegamenti al portale [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)].  
  
 [Procedure dettagliate relative a LINQ to SQL](http://msdn.microsoft.com/it-it/308e66ac-f704-4e00-9b4e-7af0045a2374)  
 Vengono elencate le procedure dettagliate disponibili per [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
 [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)  
 Viene descritto come scaricare i database di esempio usati nella documentazione.  
  
 [Panoramica della tecnologia LinqDataSource](http://msdn.microsoft.com/it-it/104cfc3f-7385-47d3-8a51-830dfa791136)  
 Viene descritto come il controllo <xref:System.Web.UI.WebControls.LinqDataSource> consenta di esporre [!INCLUDE[vbteclinqext](../../../../../../includes/vbteclinqext-md.md)] agli sviluppatori Web tramite l'architettura di controllo origine dati di [!INCLUDE[vstecasp](../../../../../../includes/vstecasp-md.md)].