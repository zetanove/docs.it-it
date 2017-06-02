---
title: "Progettazione di campi | Microsoft Docs"
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
  - "campi, linee guida di progettazione"
  - "campi di sola lettura"
  - "indicazioni per la progettazione di membri, i campi"
ms.assetid: 7cb4b0f3-7a10-4c93-b84d-733f7134fcf8
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Progettazione di campi
Il principio di incapsulamento è uno dei concetti più importanti nella progettazione orientata agli oggetti. Questo principio indica che i dati archiviati all'interno di un oggetto devono essere accessibili solo a tale oggetto.  
  
 Un modo utile per interpretare il principio è significa che un tipo deve essere progettato in modo che le modifiche apportate ai campi di tale tipo \(nome o il tipo di modifica\) possono essere eseguite senza interrompere il codice diverso per i membri del tipo. Questa interpretazione immediatamente significa che tutti i campi devono essere privati.  
  
 Microsoft esclude costanti e statici campi di sola lettura da questa limitazione rigida, poiché tali campi, quasi per definizione, non dovranno modificare.  
  
 **X non** forniscono i campi di istanza pubblici sono protetti.  
  
 È necessario fornire le proprietà per l'accesso ai campi anziché renderli pubblici o protetti.  
  
 **✓ si** utilizzare i campi costanti per le costanti che non verranno mai modificato.  
  
 Il compilatore esegue il burn\-i valori dei campi const direttamente nella chiamata di codice. Pertanto, valori const non possono essere modificati senza il rischio di compromettere la compatibilità.  
  
 **✓ si** utilizzare statici pubblici `readonly` campi per le istanze di oggetto predefinito.  
  
 Se sono presenti istanze predefinite del tipo, dichiararli come public campi statici di sola lettura del tipo.  
  
 **X non** assegnare istanze di tipi modificabili per `readonly` campi.  
  
 Un tipo modificabile è un tipo con istanze che possono essere modificate dopo la creazione di istanze. Ad esempio, matrici, la maggior parte delle raccolte e i flussi sono tipi modificabili, ma <xref:System.Int32?displayProperty=fullName>, <xref:System.Uri?displayProperty=fullName>, e <xref:System.String?displayProperty=fullName> sono tutti non modificabile. Il modificatore di sola lettura su un campo di tipo riferimento impedisce l'istanza archiviato nel campo venga sostituito, ma non impedisce che i dati di campo istanza vengano modificati chiamando i membri modifica dell'istanza.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di membri](../../../docs/standard/design-guidelines/member.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)