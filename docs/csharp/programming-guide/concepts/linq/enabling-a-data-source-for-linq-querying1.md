---
title: Abilitazione di un&quot;origine dati per l&quot;esecuzione di query LINQ | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: d2ef04a5-31a6-45cb-af9a-a5ce7732662c
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a5eaa6472c5fd7942f345dc5b4401b85c33504c9
ms.lasthandoff: 03/13/2017

---
# <a name="enabling-a-data-source-for-linq-querying"></a>Abilitazione di un'origine dati per l'esecuzione di query LINQ
Esistono diversi modi per estendere [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] in modo da consentire l'esecuzione di una query su un'origine dati nel modello [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]. L'origine dati potrebbe, ad esempio, essere una struttura ad albero dei dati, un servizio Web, un file system o un database. Il modello [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] consente ai client di eseguire una query su un'origine dati per la quale è attivata l'esecuzione di query[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], poiché la sintassi e il modello della query non vengono modificati. Di seguito vengono riportati i modi in cui è possibile estendere [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] a queste origini dati:  
  
-   Implementazione dell'interfaccia <xref:System.Collections.Generic.IEnumerable%601> in un tipo per abilitare l'esecuzione di query di quel tipo tramite [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] to Objects.  
  
-   Creazione di metodi di operatore query standard, ad esempio <xref:System.Linq.Enumerable.Where%2A> e <xref:System.Linq.Enumerable.Select%2A>, in grado di estendere un tipo, per consentire l'esecuzione di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] di quel tipo.  
  
-   Creazione di un provider per l'origine dati in grado di implementare l'interfaccia <xref:System.Linq.IQueryable%601>. Un provider che implementa questa interfaccia riceve le query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] sotto forma di strutture ad albero dell'espressione, che possono essere eseguite in modo personalizzato, ad esempio in modalità remota.  
  
-   Creazione di un provider per l'origine dati in grado di sfruttare una tecnologia [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] esistente. Tale provider consentirebbe non solo l'esecuzione di query, ma anche le operazioni di inserimento, aggiornamento ed eliminazione e il mapping per i tipi definiti dall'utente.  
  
 In questo argomento vengono descritte queste opzioni.  
  
## <a name="how-to-enable-linq-querying-of-your-data-source"></a>Come attivare l'esecuzione di query LINQ sull'origine dati  
  
### <a name="in-memory-data"></a>Dati in memoria  
 Per consentire l'esecuzione di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] sui dati in memoria sono disponibili due modi. Se il tipo di dati implementa <xref:System.Collections.Generic.IEnumerable%601>, è possibile eseguire una query sui dati tramite [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] to Objects. Se non ha senso abilitare l'enumerazione del tipo voluto implementando l'interfaccia <xref:System.Collections.Generic.IEnumerable%601>, è possibile definire metodi operatore query standard [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] all'interno del tipo stesso oppure creare metodi operatore query standard [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] che estendono il tipo. Le implementazioni personalizzate degli operatori di query standard devono utilizzare l'esecuzione posticipata per restituire i risultati.  
  
### <a name="remote-data"></a>Dati remoti  
 L'opzione più efficiente per abilitare l'esecuzione di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] su un'origine dati remota è l'implementazione dell'interfaccia <xref:System.Linq.IQueryable%601>. È tuttavia diverso dall'estendere un provider come [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)] per un'origine dati. In [!INCLUDE[vs_orcas_long](../../../../csharp/misc/includes/vs_orcas_long_md.md)] non sono disponibili modelli di provider per l'estensione di tecnologie [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] esistenti, quale [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)], ad altri tipi di origine dati.  
  
## <a name="iqueryable-linq-providers"></a>Provider LINQ IQueryable  
 I provider [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] che implementano <xref:System.Linq.IQueryable%601> possono variare notevolmente per quanto riguarda la complessità. In questa sezione vengono illustrati i diversi livelli di complessità.  
  
 Un provider `IQueryable` meno complesso potrebbe interfacciarsi con un singolo metodo di un servizio Web. Questo tipo di provider è molto specifico poiché prevede informazioni specifiche nelle query che gestisce. Ha un sistema del tipo chiuso, forse esponendo un solo tipo di risultato. La maggior parte dell'esecuzione della query avviene localmente, tramite ad esempio le implementazioni di <xref:System.Linq.Enumerable> degli operatori query standard. Un provider meno complesso potrebbe esaminare solo un'espressione della chiamata al metodo nella struttura ad albero dell'espressione che rappresenta la query facendo sì che la logica rimanente della query venga gestita altrove.  
  
 Un provider `IQueryable` mediamente complesso potrebbe essere destinato a un'origine dati che ha un linguaggio di query parzialmente espressivo. Se è destinato a un servizio Web, potrebbe interagire con più metodi del servizio Web e selezionare il metodo da chiamare in base alla domanda posta dalla query. Un provider mediamente complesso può avere un sistema di tipi più dettagliato rispetto a un provider semplice, ma rimane sempre un sistema di tipi fisso. Ad esempio, il provider può esporre tipi che hanno relazioni uno-a-molti che possono essere attraversate, ma non fornisce la tecnologia di mapping per i tipi definiti dall'utente.  
  
 Un provider `IQueryable` complesso, ad esempio il provider [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)], può convertire le query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] complete in un linguaggio di query espressivo, ad esempio SQL. Un provider complesso è più generale di un provider meno complesso, poiché può gestire un'ampia gamma di domande nella query. Ha anche un sistema di tipi aperto e pertanto deve contenere un'infrastruttura completa per eseguire il mapping dei tipi definiti dall'utente. Lo sviluppo di un provider complesso è molto impegnativo.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.IQueryable%601>   
 <xref:System.Collections.Generic.IEnumerable%601>   
 <xref:System.Linq.Enumerable>   
 [Panoramica degli operatori query standard (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [LINQ to Objects (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-objects.md)
