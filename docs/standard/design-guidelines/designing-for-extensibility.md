---
title: "Progettazione finalizzata all&#39;estensibilit&#224; | Microsoft Docs"
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
  - "estensione di librerie di classi"
  - "estensibilità con librerie di classi in .NET Framework"
  - "classe libreria linee guida di progettazione [.NET Framework], estendibilità"
  - "estensibilità della libreria di classi [.NET Framework]"
ms.assetid: 1cdb8740-871a-456c-9bd9-db96ca8d79b3
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Progettazione finalizzata all&#39;estensibilit&#224;
Un aspetto importante della progettazione di un framework è importante assicurarsi che di estendibilità del framework è stato considerato con attenzione. Questo è necessario comprendere i costi e vantaggi associati vari meccanismi di estensibilità. In questo capitolo consente di stabilire quale dei meccanismi di estensibilità, ovvero una sottoclasse, eventi, i membri virtuali, i callback e così via, possono meglio soddisfano i requisiti del framework di.  
  
 Esistono diversi modi per consentire di estensibilità nel Framework. Sono compresi tra meno potenti, ma meno costosa e molto potenti ma dispendioso. Per qualsiasi requisito di estendibilità specifico, è necessario scegliere il meccanismo di estendibilità meno costoso che soddisfi i requisiti. Tenere presente che è in genere, è possibile aggiungere ulteriori extensibility in un secondo momento, ma è mai possibile trasferirli immediatamente senza introdurre modifiche sostanziali.  
  
## In questa sezione  
 [Classi non sealed](../../../docs/standard/design-guidelines/unsealed-classes.md)  
 [Membri protetti](../../../docs/standard/design-guidelines/protected-members.md)  
 [Eventi e callback](../../../docs/standard/design-guidelines/events-and-callbacks.md)  
 [Membri virtuali](../../../docs/standard/design-guidelines/virtual-members.md)  
 [Astrazioni \(interfacce e tipi astratti\)](../../../docs/standard/design-guidelines/abstractions-abstract-types-and-interfaces.md)  
 [Classi di base per l'implementazione di astrazioni](../../../docs/standard/design-guidelines/base-classes-for-implementing-abstractions.md)  
 [Come rendere sealed](../../../docs/standard/design-guidelines/sealing.md)  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)