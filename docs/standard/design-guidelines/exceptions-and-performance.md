---
title: "Eccezioni e prestazioni | Microsoft Docs"
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
helpviewer_keywords: 
  - "tester-doer (modello)"
  - "TryParse (modello)"
  - "eccezioni, generazione"
  - "eccezioni, delle prestazioni"
  - "generazione di eccezioni, delle prestazioni"
ms.assetid: 3ad6aad9-08e6-4232-b336-0e301f2493e6
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Eccezioni e prestazioni
Un problema comune relative alle eccezioni è che se le eccezioni vengono utilizzate per il codice che normalmente non riesce, le prestazioni dell'implementazione saranno inaccettabili. Questo è un valido motivo di preoccupazione. Quando un membro genera un'eccezione, le prestazioni possono essere notevolmente più lenti. Tuttavia, è possibile ottenere buone prestazioni rigorosamente rimanendo conforme alle linee guida di eccezione che non consentire l'utilizzo di codici di errore. Due modelli descritti in questa sezione vengono forniti suggerimenti per eseguire questa operazione.  
  
 **X non** utilizzare codici di errore a causa di problemi che le eccezioni potrebbero influire negativamente sulle prestazioni.  
  
 Per migliorare le prestazioni, è possibile utilizzare il modello Tester\-agente o il modello di analisi Try, descritti nelle due sezioni.  
  
## Tester\-Doer \(modello\)  
 Talvolta possono migliorare le prestazioni di un membro che generano eccezioni suddividendo il membro in due. Esaminiamo il <xref:System.Collections.Generic.ICollection%601.Add%2A> metodo il <xref:System.Collections.Generic.ICollection%601> interfaccia.  
  
```  
ICollection<int> numbers = ...   
numbers.Add(1);  
```  
  
 Il metodo `Add` genera un'eccezione se la raccolta è di sola lettura. Può trattarsi di un problema di prestazioni in scenari in cui la chiamata al metodo deve spesso esito negativo. Uno dei modi per attenuare il problema consiste nel testare se la raccolta è accessibile in scrittura prima di tentare di aggiungere un valore.  
  
```  
ICollection<int> numbers = ...   
...  
if(!numbers.IsReadOnly){  
    numbers.Add(1);  
}  
```  
  
 Il membro utilizzato per testare una condizione, che in questo esempio è la proprietà `IsReadOnly`, viene definito il tester. Il membro utilizzato per eseguire un'operazione potenzialmente generando un'eccezione, il `Add` metodo nel nostro esempio, è detto dell'agente.  
  
 **✓ PROVARE** modello Tester\-Agente per i membri che potrebbero generare eccezioni in comune gli scenari per evitare problemi di prestazioni relativi alle eccezioni.  
  
## Try\-analisi modello  
 Per le API estremamente sensibili alle prestazioni, utilizzare un modello ancora più rapido del modello Tester\-Agente descritto nella sezione precedente. Il modello di chiamate per modificare il nome del membro in modo che un test ben definito caso una parte della semantica di membro. Ad esempio, <xref:System.DateTime> definisce un <xref:System.DateTime.Parse%2A> metodo che genera un'eccezione se l'analisi di una stringa ha esito negativo. Definisce inoltre un corrispondente <xref:System.DateTime.TryParse%2A> metodo che tenta di analizzare, ma restituisce false se l'analisi ha esito negativo e restituisce il risultato di una corretta analisi utilizzando un `out` parametro.  
  
```  
public struct DateTime {  
    public static DateTime Parse(string dateTime){   
        ...   
    }  
    public static bool TryParse(string dateTime, out DateTime result){  
        ...  
    }  
}  
```  
  
 Quando si utilizza questo modello, è importante definire la funzionalità try in termini di tipo strict. Se il membro non riesce per un motivo diverso da try ben definito, il membro deve ancora generare un'eccezione corrispondente.  
  
 **✓ PROVARE** il modello di analisi di prova per i membri che potrebbero generare eccezioni in comune gli scenari per evitare problemi di prestazioni relativi alle eccezioni.  
  
 **✓ si** utilizzare il prefisso "Try" e un valore booleano tipo restituito per metodi di implementazione di questo modello.  
  
 **✓ si** forniscono un membro che generano eccezioni per ogni membro utilizzando il modello di analisi di riprovare.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Linee guida di progettazione per le eccezioni](../../../docs/standard/design-guidelines/exceptions.md)