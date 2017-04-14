---
title: "Utilizzo di tipi di eccezioni Standard | Microsoft Docs"
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
  - "generazione di eccezioni, i tipi standard"
  - "rilevamento di eccezioni"
  - "eccezioni, intercettazione"
  - "eccezioni, generazione"
ms.assetid: ab22ce03-78f9-4dca-8824-c7ed3bdccc27
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# Utilizzo di tipi di eccezioni Standard
Questa sezione vengono descritte le eccezioni standard fornite da Framework e i dettagli del loro utilizzo. L'elenco è in alcun modo esaustivo. Fare riferimento alla documentazione di riferimento di .NET Framework per l'utilizzo di altri tipi di eccezione Framework.  
  
## Eccezione e SystemException  
 **X non** generare <xref:System.Exception?displayProperty=fullName> o <xref:System.SystemException?displayProperty=fullName>.  
  
 **X non** catch `System.Exception` o `System.SystemException` nel codice del framework, a meno che non si desidera rigenerare.  
  
 **X evitare** intercettazione `System.Exception` o `System.SystemException`, tranne nei gestori di eccezioni di livello superiore.  
  
## ApplicationException  
 **X non** generare o derivare da <xref:System.ApplicationException>.  
  
## InvalidOperationException  
 **✓ si** generano un <xref:System.InvalidOperationException> Se l'oggetto è in uno stato appropriato.  
  
## ArgumentException, ArgumentNullException e ArgumentOutOfRangeException  
 **✓ si** generare <xref:System.ArgumentException> o uno dei relativi sottotipi se a un membro vengono passati argomenti non validi. Scegliere il tipo più derivato di eccezione, se applicabile.  
  
 **✓ si** impostare il `ParamName` proprietà quando si genera una delle sottoclassi di `ArgumentException`.  
  
 Questa proprietà rappresenta il nome del parametro che ha causato l'eccezione viene generata. Si noti che la proprietà può essere impostata utilizzando uno degli overload del costruttore.  
  
 **✓ si** utilizzare `value` per il nome del parametro del valore implicito dell'impostazione delle proprietà.  
  
## L'eccezione NullReferenceException IndexOutOfRangeException e AccessViolationException  
 **X non** consentire ad API pubblicamente richiamabili generare in modo esplicito o implicito <xref:System.NullReferenceException>, <xref:System.AccessViolationException>, o <xref:System.IndexOutOfRangeException>. Queste eccezioni sono riservate e generata dal motore di esecuzione e nella che maggior parte dei casi indica un bug.  
  
 Eseguire un controllo per evitare la generazione di queste eccezioni di argomento. Generazione di queste eccezioni esposti dettagli di implementazione del metodo che può cambiare nel tempo.  
  
## StackOverflowException  
 **X non** generare in modo esplicito <xref:System.StackOverflowException>. L'eccezione deve essere generata in modo esplicito solo da CLR.  
  
 **X non** catch `StackOverflowException`.  
  
 È praticamente impossibile scrivere il codice gestito che siano coerente in presenza di overflow dello stack arbitrario. Le parti non gestite di CLR rimangono coerenti utilizzando probe per spostare gli overflow dello stack a posizioni ben definiti invece il backup dall'overflow dello stack arbitrario.  
  
## OutOfMemoryException  
 **X non** generare in modo esplicito <xref:System.OutOfMemoryException>. Questa eccezione viene generata solo dall'infrastruttura di CLR.  
  
## ComException e SEHException ExecutionEngineException  
 **X non** generare in modo esplicito <xref:System.Runtime.InteropServices.COMException>,  <xref:System.ExecutionEngineException>, e <xref:System.Runtime.InteropServices.SEHException>. Queste eccezioni devono essere generate solo dall'infrastruttura CLR.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Linee guida di progettazione per le eccezioni](../../../docs/standard/design-guidelines/exceptions.md)