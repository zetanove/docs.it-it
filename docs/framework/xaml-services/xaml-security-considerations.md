---
title: "XAML Security Considerations | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "security [XAML Services], .NET XAML services"
  - "XAML security [XAML Services]"
ms.assetid: 544296d4-f38e-4498-af49-c9f4dad28964
caps.latest.revision: 7
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 7
---
# XAML Security Considerations
In questo argomento vengono illustrate le procedure consigliate per la sicurezza nelle applicazioni in caso di utilizzo di XAML e dell'API dei servizi XAML di .NET Framework.  
  
## XAML non attendibile nelle applicazioni  
 Nel senso più generale, il codice XAML non attendibile è qualsiasi origine XAML non inclusa o generata in modo specifico dall'applicazione.  
  
 Il codice XAML compilato o archiviato come risorsa di tipo `resx` all'interno di un assembly attendibile e firmato non è considerato non attendibile in modo implicito.  È possibile considerare attendibile il codice XAML allo stesso modo in cui si considera attendibile l'assembly nel suo complesso.  Nella maggior parte dei casi, l'unica preoccupazione sono gli aspetti relativi all'attendibilità del codice XAML separato, che è un'origine XAML caricata da un flusso o altro IO.  Lo XAML separato non è una componente o una funzionalità specifica di un modello dell'applicazione con un'infrastruttura di distribuzione e creazione di pacchetti.  Tuttavia, è possibile che un assembly implementi un comportamento che prevede il caricamento di XAML separato.  
  
 A livello generale, è necessario gestire il codice XAML non attendibile come se si trattasse di codice non attendibile.  Utilizzare il sandboxing o altre metafore per impedire il possibile accesso di XAML non attendibile al codice attendibile.  
  
 La natura delle funzionalità XAML concede al codice XAML il diritto di costruire oggetti e impostare le proprietà corrispondenti.  Queste funzionalità includono inoltre l'accesso a convertitori di tipi, il mapping e l'accesso ad assembly nel dominio dell'applicazione mediante estensioni di markup, blocchi `x:Code` e così via.  
  
 Oltre alle funzionalità a livello di linguaggio, XAML viene utilizzato per la definizione dell'interfaccia utente in molte tecnologie.  Il caricamento di codice XAML non attendibile può significare il caricamento di un'interfaccia utente di spoofing dannosa.  
  
## Condivisione del contesto tra reader e writer  
 L'architettura dei servizi XAML di .NET Framework per reader XAML e writer XAML richiede spesso la condivisione di un reader XAML per un writer XAML oppure un contesto dello schema XAML condiviso.  La condivisione di oggetti o contesti potrebbe essere necessaria quando si scrive la logica del ciclo del nodo XAML o si fornisce un percorso di salvataggio personalizzato.  Non è necessario condividere le istanze del reader XAML, il contesto dello schema XAML non predefinito o le impostazioni per le classi di reader\/writer XAML tra codice attendibile e non attendibile.  
  
 La maggior parte degli scenari e delle operazioni che comportano la scrittura di oggetti XAML per il supporto di tipi basati su CLR può utilizzare il contesto dello schema XAML predefinito.  Il contesto dello schema XAML predefinito non include in modo esplicito impostazioni che potrebbero compromettere l'attendibilità totale.  È pertanto possibile condividere il contesto in modo sicuro tra componenti reader\/writer XAML non attendibili.  In questo caso, è tuttavia consigliabile mantenere tali reader e writer in ambiti <xref:System.AppDomain> separati, con uno di questi destinato in modo specifico a contesti di attendibilità parziale o creato mediante sandbox.  
  
## Spazi dei nomi XAML e attendibilità degli assembly  
 La sintassi non qualificata di base e la definizione della modalità di interpretazione da parte di XAML di un mapping dello spazio dei nomi XAML personalizzato in un assembly non fanno distinzione tra un assembly attendibile e uno non attendibile caricato nel dominio dell'applicazione.  È pertanto tecnicamente possibile che un assembly non attendibile effettui lo spoofing di un mapping dello spazio dei nomi XAML di un assembly attendibile e acquisisca l'oggetto dichiarato e le informazioni sulle proprietà di un'origine XAML.  Se si dispone dei requisiti di sicurezza per evitare questa situazione, il mapping dello spazio dei nomi XAML desiderato potrà essere eseguito mediante una delle tecniche seguenti:  
  
-   Utilizzare un nome di assembly completo con nome sicuro in qualsiasi mapping dello spazio dei nomi XAML eseguito dal codice XAML dell'applicazione.  
  
-   Limitare il mapping di assembly a un set di assembly di riferimento fisso mediante la costruzione di un oggetto <xref:System.Xaml.XamlSchemaContext> specifico per reader XAML e writer di oggetti XAML.  Vedere <xref:System.Xaml.XamlSchemaContext.%23ctor%28System.Collections.Generic.IEnumerable%7BSystem.Reflection.Assembly%7D%29>.  
  
## Mapping di tipi XAML e accesso al sistemi di tipi  
 XAML supporta un sistema di tipi specifico che per molti versi è simile al modo in cui CLR implementa il sistema di tipi CLR.  Tuttavia, per determinati aspetti di compatibilità dei tipi in cui vengono prese decisioni sull'attendibilità di un tipo in base alle informazioni sui tipi corrispondenti, è necessario fare riferimento alle informazioni sui tipi disponibili nei tipi di supporto CLR.  Questo dipende dal fatto che alcune delle funzionalità di segnalazione specifiche del sistema di tipi XAML vengono lasciate aperte come metodi virtuali e non sono pertanto completamente sottoposte al controllo delle implementazioni dei servizi XAML di .NET Framework originali.  Questi punti di flessibilità esistono perché il sistema di tipi XAML è estensibile, consentendo di contrapporre l'estensibilità di XAML e delle possibili strategie di mapping dei tipi alternative corrispondenti all'implementazione supportata da CLR predefinita e al contesto dello schema XAML predefinito.  Per ulteriori informazioni, vedere le note specifiche relative alla diverse proprietà di <xref:System.Xaml.XamlType> e <xref:System.Xaml.XamlMember>.  
  
## Vedere anche  
 <xref:System.Xaml.Permissions.XamlAccessLevel>