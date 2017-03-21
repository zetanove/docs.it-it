---
title: Abilitazione di un&quot;origine dati per LINQ Querying2 | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: c412f0cf-ff0e-4993-ab3d-1b49e23f00f8
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 34bdc4e056d982799eac35eb2398dd3f23f6f351
ms.lasthandoff: 03/13/2017

---
# <a name="enabling-a-data-source-for-linq-querying"></a>Abilitazione di un'origine dati per l'esecuzione di query LINQ
Esistono vari modi per estendere [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] per consentire a qualsiasi origine dati deve essere sottoposto a query nel [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] modello. L'origine dati potrebbe, ad esempio, essere una struttura ad albero dei dati, un servizio Web, un file system o un database. Il modello [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] consente ai client di eseguire una query su un'origine dati per la quale è attivata l'esecuzione di query[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], poiché la sintassi e il modello della query non vengono modificati. I modi in cui [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] può essere estesa a tali dati origini includono quanto segue:  
  
-   Implementazione di <xref:System.Collections.Generic.IEnumerable%601>interfaccia in un tipo per abilitare [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] per l'esecuzione di query su oggetti di quel tipo.</xref:System.Collections.Generic.IEnumerable%601>  
  
-   Creazione, ad esempio metodi degli operatori di query standard <xref:System.Linq.Enumerable.Where%2A>e <xref:System.Linq.Enumerable.Select%2A>che estendono un tipo, per abilitare personalizzato [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] l'esecuzione di query di quel tipo.</xref:System.Linq.Enumerable.Select%2A> </xref:System.Linq.Enumerable.Where%2A>  
  
-   Creazione di un provider dell'origine dati che implementa il <xref:System.Linq.IQueryable%601>interfaccia.</xref:System.Linq.IQueryable%601> Un provider che implementa questa interfaccia riceve le query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] sotto forma di strutture ad albero dell'espressione, che possono essere eseguite in modo personalizzato, ad esempio in modalità remota.  
  
-   Creazione di un provider per l'origine dati che si avvale di un oggetto esistente [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] tecnologia. Tale provider consentirebbe non solo l'esecuzione di query, ma anche le operazioni di inserimento, aggiornamento ed eliminazione e il mapping per i tipi definiti dall'utente.  
  
 In questo argomento vengono descritte queste opzioni.  
  
## <a name="how-to-enable-linq-querying-of-your-data-source"></a>Come attivare l'esecuzione di query LINQ sull'origine dati  
  
### <a name="in-memory-data"></a>Dati in memoria  
 Esistono due modi, è possibile abilitare [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] l'esecuzione di query di dati in memoria. Se i dati di un tipo che implementa <xref:System.Collections.Generic.IEnumerable%601>, è possibile eseguire query sui dati utilizzando [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] agli oggetti.</xref:System.Collections.Generic.IEnumerable%601> Se non ha senso attivare l'enumerazione del tipo implementando il <xref:System.Collections.Generic.IEnumerable%601>interfaccia, è possibile definire [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] standard metodi degli operatori di quel tipo di query o creare [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] metodi degli operatori di query standard che estendono il tipo.</xref:System.Collections.Generic.IEnumerable%601> Le implementazioni personalizzate degli operatori di query standard devono utilizzare l'esecuzione posticipata per restituire i risultati.  
  
### <a name="remote-data"></a>Dati remoti  
 L'opzione migliore per l'abilitazione di [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] l'esecuzione di query di un'origine dati remota è implementare il <xref:System.Linq.IQueryable%601>interfaccia.</xref:System.Linq.IQueryable%601> È tuttavia diverso dall'estendere un provider come [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)] per un'origine dati. Nessun modello di provider per l'estensione esistente [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] tecnologie, ad esempio [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)]in altri tipi di origine dati sono disponibili in [!INCLUDE[vs_orcas_long](../../../../csharp/misc/includes/vs_orcas_long_md.md)].  
  
## <a name="iqueryable-linq-providers"></a>Provider LINQ IQueryable  
 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]i provider che implementano <xref:System.Linq.IQueryable%601>può variare notevolmente a seconda della complessità.</xref:System.Linq.IQueryable%601> In questa sezione vengono illustrati i diversi livelli di complessità.  
  
 Un provider `IQueryable` meno complesso potrebbe interfacciarsi con un singolo metodo di un servizio Web. Questo tipo di provider è molto specifico poiché prevede informazioni specifiche nelle query che gestisce. Ha un sistema del tipo chiuso, forse esponendo un solo tipo di risultato. La maggior parte dell'esecuzione della query avviene localmente, ad esempio utilizzando il <xref:System.Linq.Enumerable>implementazioni degli operatori di query standard.</xref:System.Linq.Enumerable> Un provider meno complesso potrebbe esaminare solo un'espressione della chiamata al metodo nella struttura ad albero dell'espressione che rappresenta la query facendo sì che la logica rimanente della query venga gestita altrove.  
  
 Un provider `IQueryable` mediamente complesso potrebbe essere destinato a un'origine dati che ha un linguaggio di query parzialmente espressivo. Se è destinato a un servizio Web, potrebbe interagire con più metodi del servizio Web e selezionare il metodo da chiamare in base alla domanda posta dalla query. Un provider mediamente complesso può avere un sistema di tipi più dettagliato rispetto a un provider semplice, ma rimane sempre un sistema di tipi fisso. Ad esempio, il provider può esporre tipi che hanno relazioni uno-a-molti che possono essere attraversate, ma non fornisce la tecnologia di mapping per i tipi definiti dall'utente.  
  
 Un provider `IQueryable` complesso, ad esempio il provider [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)], può convertire le query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] complete in un linguaggio di query espressivo, ad esempio SQL. Un provider complesso è più generale di un provider meno complesso, poiché può gestire un'ampia gamma di domande nella query. Ha anche un sistema di tipi aperto e pertanto deve contenere un'infrastruttura completa per eseguire il mapping dei tipi definiti dall'utente. Lo sviluppo di un provider complesso è molto impegnativo.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.IQueryable%601></xref:System.Linq.IQueryable%601>   
 <xref:System.Collections.Generic.IEnumerable%601></xref:System.Collections.Generic.IEnumerable%601>   
 <xref:System.Linq.Enumerable></xref:System.Linq.Enumerable>   
 [Cenni preliminari sugli operatori di Query standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)
