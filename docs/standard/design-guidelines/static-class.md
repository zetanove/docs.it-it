---
title: "Progettazione di classi statiche | Microsoft Docs"
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
  - "indicazioni per la progettazione di tipo, le classi statiche"
  - "classe libreria linee guida di progettazione [.NET Framework], classi"
  - "classi [.NET Framework], statiche"
  - "classi statiche [.NET Framework]"
  - "classi [.NET Framework], linee guida di progettazione"
  - "tipo di linee guida di progettazione, classi"
ms.assetid: d67c14d8-c4dd-443f-affb-4ccae677c9b6
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Progettazione di classi statiche
Una classe statica viene definita come una classe che contiene solo membri statici \(naturalmente oltre i membri di istanza ereditati da <xref:System.Object?displayProperty=fullName> e possibilmente un costruttore privato\). Alcuni linguaggi forniscono il supporto incorporato per le classi statiche. In c\# 2.0 e versioni successive, quando viene dichiarata una classe statica, è astratto sealed e non membri di istanza possono essere sottoposto a override o dichiarati.  
  
 Le classi statiche sono un compromesso tra semplicità e pura progettazione orientata agli oggetti. Comunemente utilizzati per fornire collegamenti ad altre operazioni \(ad esempio <xref:System.IO.File?displayProperty=fullName>\), titolari di metodi di estensione o la funzionalità per il quale è non autorizzato un wrapper completa orientata agli oggetti \(ad esempio <xref:System.Environment?displayProperty=fullName>\).  
  
 **✓ si** utilizzare le classi statiche con moderazione.  
  
 Classi statiche devono essere utilizzate solo come classi di supporto per framework di base, orientato a oggetti.  
  
 **X non** considerato un bucket di varie classi statiche.  
  
 **X non** dichiarare o eseguire l'override di membri di istanza in classi statiche.  
  
 **✓ si** dichiarare classi statiche come astratto sealed e aggiungere un costruttore di istanza privata se il linguaggio di programmazione non dispone di un supporto incorporato per le classi statiche.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di tipo](../../../docs/standard/design-guidelines/type.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)