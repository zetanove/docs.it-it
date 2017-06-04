---
title: "Oggetti Attributes1 | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: ".net-framework-4.6"
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
  - "attributi [.NET Framework] su"
  - "classe libreria linee guida di progettazione [.NET Framework], gli attributi"
ms.assetid: ee0038ef-b247-4747-a650-3c5c5cd58d8b
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
---
# Attributi
<xref:System.Attribute?displayProperty=fullName> una classe di base viene utilizzata per definire gli attributi personalizzati.  
  
 Gli attributi sono le annotazioni possono essere aggiunti agli elementi di programmazione, ad esempio assembly, tipi, membri e parametri. Essi vengono archiviate nei metadati dell'assembly ed è accessibile in fase di esecuzione utilizzando le API di reflection. Ad esempio, il Framework definisce il <xref:System.ObsoleteAttribute>, che può essere applicato a un tipo o membro per indicare che il tipo o membro è stato deprecato.  
  
 Gli attributi possono disporre di una o più proprietà che contengono dati aggiuntivi relativi all'attributo. Ad esempio, `ObsoleteAttribute` potrebbe contenere informazioni aggiuntive sulla versione in un tipo o un membro ha ricevuto obsoleta e la descrizione delle nuove API sostituendo l'API obsoleta.  
  
 Alcune proprietà di un attributo deve essere specificata quando è applicato l'attributo. Questi sono definiti per le proprietà necessarie o gli argomenti obbligatori, poiché vengono rappresentate come parametri del costruttore posizionali. Ad esempio, la <xref:System.Diagnostics.ConditionalAttribute.ConditionString%2A> proprietà del <xref:System.Diagnostics.ConditionalAttribute> è una proprietà obbligatoria.  
  
 Proprietà che non hanno necessariamente per essere specificato quando è applicato l'attributo sono dette proprietà facoltative \(o gli argomenti facoltativi\). Vengono rappresentati come proprietà impostabili. I compilatori forniscono una sintassi speciale per impostare queste proprietà quando viene applicato un attributo. Ad esempio, la <xref:System.AttributeUsageAttribute.Inherited%2A?displayProperty=fullName> proprietà rappresenta un argomento facoltativo.  
  
 **✓ si** denominare le classi di attributo personalizzato con il suffisso "Attributo".  
  
 **✓ si** si applicano le <xref:System.AttributeUsageAttribute> per gli attributi personalizzati.  
  
 **✓ si** forniscono le proprietà impostabili per gli argomenti facoltativi.  
  
 **✓ si** forniscono le proprietà di sola lettura per gli argomenti obbligatori.  
  
 **✓ si** forniscono i parametri del costruttore per inizializzare le proprietà corrispondenti per gli argomenti obbligatori. Ogni parametro deve avere lo stesso nome \(anche se con maiuscole\/minuscole\) come la proprietà corrispondente.  
  
 **X evitare** fornendo i parametri del costruttore per inizializzare le proprietà corrispondenti per gli argomenti facoltativi.  
  
 In altre parole, non dispongono di proprietà che può essere impostata con un costruttore e un metodo di impostazione. Questa linea guida rende molto esplicite quali sono facoltativi e che sono necessarie ed evita due modi per eseguire la stessa operazione.  
  
 **X evitare** l'overload di costruttori di attributo personalizzato.  
  
 Presenza di un solo costruttore chiaramente comunica all'utente cui gli argomenti sono obbligatori e facoltativi.  
  
 **✓ si** il sealing di classi di attributi personalizzati, se possibile. In questo modo più veloce la ricerca per l'attributo.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Linee guida di utilizzo](../../../docs/standard/design-guidelines/usage-guidelines.md)