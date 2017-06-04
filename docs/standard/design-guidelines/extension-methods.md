---
title: "Metodi di estensione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 5de945cb-88f4-49d7-b0e6-f098300cf357
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# Metodi di estensione
Metodi di estensione sono una funzionalità del linguaggio che consente metodi statici per essere chiamato utilizzando la sintassi di chiamata del metodo di istanza. Questi metodi devono accettare almeno un parametro, che rappresenta l'istanza che è il metodo su cui operare.  
  
 La classe che definisce tali metodi di estensione è definita come la classe "sponsor" e devono essere dichiarati come static. Per utilizzare i metodi di estensione, uno necessario importare lo spazio dei nomi che definisce la classe di sponsor.  
  
 **X evitare** frivolously definisce i metodi di estensione, soprattutto in tipi non si è proprietari.  
  
 Se si è proprietari codice sorgente di un tipo, provare a utilizzare normali metodi di istanza. Se non si è proprietari e si desidera aggiungere un metodo, prestare molta attenzione. Il libero utilizzo dei metodi di estensione è in grado di occupare le API di tipi che non sono stati progettati per questi metodi.  
  
 **✓ PROVARE** utilizzando metodi di estensione in uno dei seguenti scenari:  
  
-   Per fornire supporto funzionalità rilevanti per ogni implementazione di un'interfaccia, se ha funzionalità possono essere scritti in termini di interfaccia principale. In questo modo le implementazioni concrete in caso contrario non è possibile assegnare alle interfacce. Ad esempio, il `LINQ to Objects` gli operatori vengono implementati come metodi di estensione per tutti <xref:System.Collections.Generic.IEnumerable%601> tipi. Pertanto, qualsiasi `IEnumerable<>` implementazione è automaticamente abilitata per LINQ.  
  
-   Quando un metodo di istanza introdurrebbe una dipendenza da un tipo, ma tale dipendenza comporta l'interruzione di regole di gestione delle dipendenze. Ad esempio, una dipendenza da <xref:System.String> a <xref:System.Uri?displayProperty=fullName> probabilmente non è opportuno e pertanto `String.ToUri()` metodo di istanza restituzione `System.Uri` sarebbe la progettazione errata da una prospettiva di gestione delle dipendenze. Un metodo di estensione statici `Uri.ToUri(this string str)` restituzione `System.Uri` sarebbe migliore progettazione.  
  
 **X evitare** la definizione di metodi di estensione su <xref:System.Object?displayProperty=fullName>.  
  
 Gli utenti di Visual Basic non saranno in grado di chiamare tali metodi nei riferimenti agli oggetti utilizzando la sintassi del metodo di estensione. VB non supporta la chiamata di questi metodi perché, in Visual Basic, dichiarare un riferimento come oggetto forza tutte le chiamate di metodo su di essa per ritardo associato \(membro effettivo denominato viene determinato in fase di esecuzione\), mentre le associazioni ai metodi di estensione vengono determinate in fase di compilazione \(associazione anticipata\).  
  
 Si noti che la linea guida si applicano ad altri linguaggi, in cui è presente lo stesso comportamento di associazione, o in cui non sono supportati i metodi di estensione.  
  
 **X non** inserire i metodi di estensione nello spazio dei nomi stesso come tipo esteso a meno che non sia per l'aggiunta di metodi a interfacce o per la gestione delle dipendenze.  
  
 **X evitare** la definizione di due o più metodi di estensione con la stessa firma, anche se si trovano in diversi spazi dei nomi.  
  
 **✓ PROVARE** la definizione di metodi di estensione nello spazio dei nomi stesso come tipo esteso se il tipo è un'interfaccia e i metodi di estensione sono concepiti per essere utilizzate in molti o tutti i casi.  
  
 **X non** definire metodi di estensione che implementa una funzionalità negli spazi dei nomi in genere associati con altre funzionalità. Definire invece li nello spazio dei nomi associato alla funzione che a cui appartengono.  
  
 **X evitare** generico di denominazione degli spazi dei nomi dedicato ai metodi di estensione \(ad esempio, "estensioni"\). Utilizzare un nome descrittivo \(ad esempio, "Routing"\) invece.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di membri](../../../docs/standard/design-guidelines/member.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)