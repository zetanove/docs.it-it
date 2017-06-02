---
title: "LINQ e ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bf0c8f93-3ff7-49f3-8aed-f2b7ac938dec
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# LINQ e ADO.NET
Attualmente molti sviluppatori aziendali devono usare due o più linguaggi di programmazione: un linguaggio di alto livello per i livelli di presentazione e della logica di business \(ad esempio [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] o [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]\) e un linguaggio di query per interagire con il database \(ad esempio [!INCLUDE[tsql](../../../../includes/tsql-md.md)]\).  Tale necessità non solo richiede una conoscenza approfondita di diversi linguaggi da parte degli sviluppatori, ma provoca anche problemi di mancata corrispondenza tra linguaggi nell'ambiente di sviluppo.  Ad esempio, in un'applicazione che usa un'API di accesso ai dati per eseguire una query su un database la query viene specificata come valore letterale stringa racchiuso tra virgolette.  Tale stringa di query è tuttavia illeggibile per il compilatore e non è possibile eseguire su di essa un controllo per verificare la presenza di errori, ad esempio l'uso di sintassi non valida o l'effettiva esistenza delle colonne o delle righe cui fa riferimento.  Non viene eseguito il controllo dei tipi dei parametri della query, né è disponibile il supporto per `IntelliSense`.  
  
 [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] consente agli sviluppatori di formare query basate su set nel codice dell'applicazione, senza dover usare un linguaggio di query diverso.  È possibile scrivere query [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] su diverse origini dati enumerabili \(ovvero origini dati che implementano l'interfaccia <xref:System.Collections.IEnumerable>\), ad esempio strutture dei dati in memoria, documenti XML, database SQL e oggetti <xref:System.Data.DataSet>.  Sebbene queste origini dati enumerabili vengono implementate in modi diversi, espongono tutte la stessa sintassi e gli stessi costrutti di linguaggio.  Poiché è possibile formare query nel linguaggio di programmazione stesso, non è necessario usare un altro linguaggio di query incorporato sotto forma di valori letterali stringa che il compilatore non è in grado di riconoscere o verificare.  L'integrazione di query nel linguaggio di programmazione contribuisce inoltre a incrementare la produttività dei programmatori [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] fornendo il controllo dei tipi e della sintassi e il supporto per `IntelliSense` in fase di compilazione.  Queste funzionalità riducono l'esigenza di debug e correzione degli errori delle query.  
  
 Il trasferimento di dati da tabelle SQL in oggetti in memoria è un'operazione spesso laboriosa e soggetta a errori.  Il provider [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]implementato da [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] e [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] converte i dati di origine in raccolte di oggetti basate su <xref:System.Collections.IEnumerable>.  Il programmatore visualizza sempre i dati sotto forma di una raccolta <xref:System.Collections.IEnumerable>, sia quando si esegue una query che quando si effettua un aggiornamento.  Per la scrittura di query da eseguire su tali raccolte, viene fornito il supporto per `IntelliSense`.  
  
 Sono disponibili tre diverse tecnologie [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] ADO.NET: [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] e [!INCLUDE[linq_entities](../../../../includes/linq-entities-md.md)].  [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] offre un supporto più completo e ottimizzato per l'esecuzione di query su <xref:System.Data.DataSet>, [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] consente di eseguire query direttamente sugli schemi di database di [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] e [!INCLUDE[linq_entities](../../../../includes/linq-entities-md.md)] consente di eseguire query su [!INCLUDE[adonet_edm](../../../../includes/adonet-edm-md.md)].  
  
 Nel diagramma seguente viene fornita una panoramica della correlazione tra le tecnologie LINQ ADO.NET, i linguaggi di programmazione di alto livello e le origini dati con supporto LINQ.  
  
 ![Cenni preliminari su LINQ to ADO.NET](../../../../docs/framework/data/adonet/media/dpue-linqtoadonetoverview-bpuedev11.png "DPUE\_LinqToAdoNetOverview\_bpuedev11")  
  
 Per informazioni generali sulle funzionalità del linguaggio LINQ, vedere [Introduction to LINQ](../../../../ocs/visual-basic/programming-guide/language-features/linq/introduction-to-linq.md).  Per informazioni sull'utilizzo di LINQ nelle applicazioni, vedere la sezione [NOT IN BUILD: LINQ General Programming Guide](http://msdn.microsoft.com/it-it/609c7a6b-cbdd-429d-99f3-78d13d3bc049) in cui sono disponibili informazioni dettagliate sull'utilizzo delle tecnologie LINQ.  
  
 Nelle sezioni seguenti vengono fornite ulteriori informazioni su [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] e [!INCLUDE[linq_entities](../../../../includes/linq-entities-md.md)].  
  
## LINQ to DataSet  
 <xref:System.Data.DataSet> rappresenta un elemento chiave del modello di programmazione disconnesso su cui si basa [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] ed è ampiamente usato.  [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] consente agli sviluppatori di compilare funzionalità di query più complesse in <xref:System.Data.DataSet> usando lo stesso meccanismo di formulazione delle query disponibile per molte altre origini dati.  Per altre informazioni, vedere [LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset.md).  
  
## LINQ to SQL  
 [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] è uno strumento utile per gli sviluppatori che non necessitano del mapping a un modello concettuale.  Con [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] è possibile usare il modello di programmazione di [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] direttamente sullo schema del database esistente.  [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] consente agli sviluppatori di generare classi di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] che rappresentano i dati.  Anziché eseguire il mapping a un modello di dati concettuale, tali classi generate vengono mappate direttamente a tabelle di database, visualizzazioni, stored procedure e funzioni definite dall'utente.  
  
 Con [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] gli sviluppatori possono scrivere il codice direttamente nello schema di archiviazione usando lo stesso modello di programmazione [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] delle raccolte in memoria e di <xref:System.Data.DataSet>, oltre ad altre origini dati, quali XML.  Per altre informazioni, vedere [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md).  
  
## LINQ to Entities  
 La maggior parte delle applicazioni viene attualmente scritta basandosi su database relazionali.  A un certo punto è necessario che queste applicazioni interagiscano con i dati rappresentati in forma relazionale.  Gli schemi di database non costituiscono sempre la soluzione ideale per la compilazione di applicazioni e i modelli concettuali di applicazione non corrispondono ai modelli logici di database.  [!INCLUDE[adonet_edm](../../../../includes/adonet-edm-md.md)] è un modello di dati concettuale che può essere usato per modellare i dati di un dominio particolare in modo che le applicazioni possano interagire con i dati come oggetti.  Per altre informazioni, vedere [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md).  
  
 Tramite [!INCLUDE[adonet_edm](../../../../includes/adonet-edm-md.md)], i dati relazionali vengono esposti come oggetti nell'ambiente .NET.  Ciò rende il livello di oggetto una destinazione ideale per il supporto di [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)], consentendo agli sviluppatori di formulare query sul database a partire dal linguaggio usato per compilare la logica di business.  Questa funzionalità è nota come [!INCLUDE[linq_entities](../../../../includes/linq-entities-md.md)].  Per altre informazioni, vedere [LINQ to Entities](../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md).  
  
## Vedere anche  
 [LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset.md)   
 [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md)   
 [LINQ to Entities](../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)