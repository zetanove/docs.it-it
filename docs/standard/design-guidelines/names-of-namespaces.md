---
title: "Nomi degli spazi dei nomi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "nomi di conflitti [.NET Framework]"
  - "nomi di spazi dei nomi [.NET Framework]"
  - "conflitti di nomi di tipi"
  - "i nomi di spazi dei nomi [.NET Framework]"
  - "nomi [.NET Framework], nomi dei tipi"
ms.assetid: a49058d2-0276-43a7-9502-04adddf857b2
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Nomi degli spazi dei nomi
Come con altre linee guida per la denominazione, l'obiettivo per la denominazione degli spazi dei nomi consiste nel creare chiarezza sufficiente per il programmatore che utilizza il framework di conoscere immediatamente il contenuto dello spazio dei nomi potrebbero essere. Il modello seguente specifica la regola generale per la denominazione degli spazi dei nomi:  
  
 `<Company>.(<Product>|<Technology>)[.<Feature>][.<Subnamespace>]`  
  
 Di seguito è riportati esempi:  
  
 `Fabrikam.Math`   
 `Litware.Security`  
  
 **✓ si** prefisso spazio dei nomi con un nome della società per evitare che gli spazi dei nomi di società diverse da con lo stesso nome.  
  
 **✓ si** utilizzare un nome di prodotto stabile e indipendente dalla versione al secondo livello di uno spazio dei nomi.  
  
 **X non** utilizzare gerarchie organizzative come base per i nomi nelle gerarchie dello spazio dei nomi, perché i nomi dei gruppi all'interno di organizzazioni tendono a essere di breve durata. Organizzare la gerarchia di spazi dei nomi per i gruppi di tecnologie correlate.  
  
 **✓ si** con periodi di utilizzare il sistema Pascal e i componenti dello spazio dei nomi separato \(ad esempio, `Microsoft.Office.PowerPoint`\). Se il proprio marchio si avvale di maiuscole e minuscole non convenzionale, è necessario seguire la convenzione definita dal produttore, anche se esso devia dal maiuscole e minuscole normale spazio dei nomi.  
  
 **✓ PROVARE** utilizzando nomi plurali dove appropriato.  
  
 Ad esempio, utilizzare `System.Collections` anziché `System.Collection`. Nome del marchio e gli acronimi sono tuttavia eccezioni a questa regola. Ad esempio, utilizzare `System.IO` anziché `System.IOs`.  
  
 **X non** utilizzare lo stesso nome per uno spazio dei nomi e un tipo nello spazio dei nomi.  
  
 Ad esempio, non utilizzare `Debug` come uno spazio dei nomi nome e quindi fornire anche una classe denominata `Debug` nello spazio dei nomi stesso. Alcuni compilatori richiedono tali tipi di riferimento completo.  
  
### Spazi dei nomi e i conflitti di nomi  
 **X non** introdurre nomi di tipo generico, ad esempio `Element`, `Node`, `Log`, e `Message`.  
  
 Esiste un'alta probabilità che tale operazione comporti per digitare nome in conflitto in comune gli scenari. È necessario qualificare i nomi di tipo generico \(`FormElement`, `XmlNode`, `EventLog`, `SoapMessage`\).  
  
 Sono disponibili linee guida specifiche per evitare conflitti di nomi per le diverse categorie di spazi dei nomi.  
  
-   **Spazi dei nomi del modello di applicazione**  
  
     Gli spazi dei nomi appartenenti a un modello di applicazione singolo molto spesso vengono utilizzate insieme, ma vengono non utilizzati quasi mai con spazi dei nomi di altri modelli di applicazione. Ad esempio, il <xref:System.Windows.Forms?displayProperty=fullName> dello spazio dei nomi viene raramente utilizzata in combinazione con il <xref:System.Web.UI?displayProperty=fullName> dello spazio dei nomi. Di seguito è riportato un elenco noto modello dello spazio dei nomi di gruppi di applicazioni:  
  
     `System.Windows*`   
     `System.Web.UI*`  
  
     **X non** assegnare lo stesso nome per i tipi negli spazi dei nomi all'interno di un modello di applicazione singolo.  
  
     Ad esempio, si aggiunge un tipo denominato `Page` per il <xref:System.Web.UI.Adapters?displayProperty=fullName> dello spazio dei nomi, perché il <xref:System.Web.UI?displayProperty=fullName> dello spazio dei nomi contiene già un tipo denominato `Page`.  
  
-   **Spazi dei nomi dell'infrastruttura**  
  
     Questo gruppo contiene spazi dei nomi che raramente vengono importati durante lo sviluppo di applicazioni comuni. Ad esempio, `.Design` gli spazi dei nomi vengono utilizzati principalmente durante lo sviluppo di programmazione degli strumenti. Come evitare conflitti con i tipi di questi spazi dei nomi non sono critiche.  
  
-   **Spazi dei nomi core**  
  
     Spazi dei nomi principali includono tutti `System` gli spazi dei nomi, esclusi gli spazi dei nomi dei modelli di applicazione e gli spazi dei nomi dell'infrastruttura. Spazi dei nomi principali includono, ad esempio, `System`, `System.IO`, `System.Xml`, e `System.Net`.  
  
     **X non** assegnare tipi di nomi in conflitto con qualsiasi tipo negli spazi dei nomi principali.  
  
     Ad esempio, non utilizzare mai `Stream` come nome di tipo. Genererebbe un conflitto con <xref:System.IO.Stream?displayProperty=fullName>, un tipo comunemente utilizzata.  
  
-   **Gruppi di spazio dei nomi di tecnologia**  
  
     Questa categoria include tutti gli spazi dei nomi con i primi due nodi dello spazio dei nomi stesso `(<Company>.<Technology>*`\), ad esempio `Microsoft.Build.Utilities` e `Microsoft.Build.Tasks`. È importante che i tipi appartenenti a una singola tecnologia non sono in conflitto tra loro.  
  
     **X non** assegnare nomi di tipo in conflitto con altri tipi all'interno di una singola tecnologia.  
  
     **X non** introdurre conflitti di nomi tra i tipi negli spazi dei nomi di tecnologia e uno spazio dei nomi del modello di applicazione \(a meno che la tecnologia non deve essere utilizzato con il modello di applicazione\).  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Convenzioni di denominazione](../../../docs/standard/design-guidelines/naming-guidelines.md)