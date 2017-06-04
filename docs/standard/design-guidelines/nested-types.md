---
title: "Tipi annidati | Microsoft Docs"
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
  - "tipi annidati"
  - "tipi public annidati"
  - "indicazioni per la progettazione di tipo, i tipi annidati"
  - "tipi annidati"
  - "tipo di membri [.NET Framework]"
  - "tipi di classe della libreria progettazione annidati le linee guida [.NET Framework]"
ms.assetid: 12feb7f0-b793-4d96-b090-42d6473bab8c
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Tipi annidati
Un tipo annidato è un tipo definito all'interno dell'ambito di un altro tipo, che viene chiamato il tipo di inclusione. Un tipo annidato può accedere a tutti i membri del tipo di inclusione. Ad esempio, ha accesso a campi privati definiti nel tipo di inclusione e proteggere i campi definiti in tutti i predecessori del tipo di inclusione.  
  
 In generale, i tipi annidati devono essere utilizzati con cautela. Le ragioni sono molteplici. Alcuni sviluppatori non sono completamente dimestichezza con il concetto. Questi sviluppatori potrebbero, ad esempio, essere problemi con la sintassi di dichiarazione di variabili di tipi annidati. Tipi annidati sono anche molto strettamente collegati con i relativi tipi di inclusione e di conseguenza non sono adatte per essere tipi generici.  
  
 I tipi annidati sono particolarmente adatti per modellare i dettagli di implementazione dei tipi che lo contiene. L'utente finale deve raramente è necessario dichiarare le variabili di un tipo annidato e quasi mai necessario creare esplicitamente istanze di tipi annidati. Ad esempio, l'enumeratore di una raccolta può essere un tipo annidato di tale raccolta. Gli enumeratori sono in genere crea un'istanza del tipo di inclusione e poiché molte lingue supportano l'istruzione foreach, enumeratore variabili raramente devono essere dichiarate dall'utente finale.  
  
 **✓ si** utilizzare tipi annidati quando la relazione tra il tipo annidato e il relativo tipo esterno è tale che\-accessibilità del membro semantica è auspicabile.  
  
 **X non** utilizzare tipi annidati pubblici come un raggruppamento logico di costruire; utilizzare gli spazi dei nomi per questo oggetto.  
  
 **X evitare** esposte pubblicamente i tipi annidati. L'unica eccezione a questa operazione se è necessario essere dichiarato solo in rari scenari, ad esempio la creazione di sottoclassi o altri scenari di personalizzazione avanzata variabili del tipo annidato.  
  
 **X non** utilizzare tipi annidati se il tipo è probabile che venga fatto riferimento all'esterno del tipo contenitore.  
  
 Ad esempio, un'enumerazione passata a un metodo definito in una classe non deve essere definita come un tipo annidato nella classe.  
  
 **X non** utilizzare tipi annidati se è necessario creare un'istanza dal codice client.  Se un tipo ha un costruttore pubblico, probabilmente non sarà nidificato.  
  
 Se è possibile creare istanze di un tipo, che sembra indicare il tipo dispone di una posizione nel framework autonomamente \(è possibile crearlo, utilizzarlo ed eliminato senza mai utilizzare il tipo esterno\) e pertanto non deve essere nidificati. Tipi interni non devono essere riutilizzati ampiamente all'esterno del tipo esterno senza alcuna relazione verso il tipo esterno.  
  
 **X non** definisce un tipo annidato come membro di interfaccia. Molti linguaggi non supportano tale costrutto.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di tipo](../../../docs/standard/design-guidelines/type.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)