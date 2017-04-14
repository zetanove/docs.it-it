---
title: "Overload degli operatori | Microsoft Docs"
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
  - "operatori di overload [.NET Framework]"
  - "operatori di overload nomi [.NET Framework]"
  - "indicazioni per la progettazione di membri, operatori"
  - "overload di operatori"
ms.assetid: 37585bf2-4c27-4dee-849a-af70e3338cc1
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Overload degli operatori
Overload degli operatori consente tipi framework vengono visualizzati come se fossero primitive del linguaggio predefiniti.  
  
 Sebbene consentiti e utile in alcune situazioni, overload dell'operatore devono essere utilizzati con cautela. Esistono molte situazioni in cui operatore overload ha protezione, ad esempio avvio progettisti del framework come utilizzare gli operatori per le operazioni che devono essere metodi semplici. Le seguenti linee guida dovrebbero consentire di decidere quando e come utilizzare l'overload degli operatori.  
  
 **X evitare** la definizione di overload degli operatori, tranne nei tipi che dovrebbero risultare come tipi primitivi \(predefiniti\).  
  
 **✓ PROVARE** definire overload dell'operatore in un tipo che deve essere un tipo primitivo.  
  
 Ad esempio, <xref:System.String?displayProperty=fullName> è `operator==` e `operator!=` definito.  
  
 **✓ si** definire overload dell'operatore in strutture che rappresentano numeri \(ad esempio <xref:System.Decimal?displayProperty=fullName>\).  
  
 **X non** essere simpatica overload dell'operatore.  
  
 Overload dell'operatore è utile nei casi in cui è immediatamente ovvio il risultato dell'operazione sarà. Ad esempio, è opportuno essere in grado di sottrarre uno <xref:System.DateTime> da un altro `DateTime` e ottenere un <xref:System.TimeSpan>. Tuttavia, non è appropriata per utilizzare l'operatore di unione logica per le query di unione due database o per utilizzare l'operatore di spostamento per scrivere un flusso.  
  
 **X non** forniscono gli overload di operatori, a meno che almeno uno degli operandi è di tipo che definisce l'overload.  
  
 **✓ si** overload degli operatori in modo simmetrico.  
  
 Ad esempio, se si esegue l'overload di `operator==`, inoltre, è necessario eseguire l'overload di `operator!=`. Analogamente, se esegue l'overload di `operator<`, è inoltre necessario eseguire l'overload di `operator>`, e così via.  
  
 **✓ PROVARE** fornendo i metodi con nomi descrittivi che corrispondono a ogni operatore di overload.  
  
 Molti linguaggi non supportano l'overload degli operatori. Per questo motivo, è consigliabile che i tipi che l'overload degli operatori includono un metodo secondario con un nome specifico di dominio appropriato che fornisce una funzionalità equivalente.  
  
 Nella tabella seguente contiene un elenco di operatori e i nomi di metodo descrittivo corrispondente.  
  
|Simbolo dell'operatore c\#|Nome dei metadati|Nome descrittivo|  
|--------------------------------|-----------------------|----------------------|  
|`N/A`|`op_Implicit`|`To<TypeName>/From<TypeName>`|  
|`N/A`|`op_Explicit`|`To<TypeName>/From<TypeName>`|  
|`+ (binary)`|`op_Addition`|`Add`|  
|`- (binary)`|`op_Subtraction`|`Subtract`|  
|`* (binary)`|`op_Multiply`|`Multiply`|  
|`/`|`op_Division`|`Divide`|  
|`%`|`op_Modulus`|`Mod or Remainder`|  
|`^`|`op_ExclusiveOr`|`Xor`|  
|`& (binary)`|`op_BitwiseAnd`|`BitwiseAnd`|  
|`&#124;`|`op_BitwiseOr`|`BitwiseOr`|  
|`&&`|`op_LogicalAnd`|`And`|  
|`&#124;&#124;`|`op_LogicalOr`|`Or`|  
|`=`|`op_Assign`|`Assign`|  
|`<<`|`op_LeftShift`|`LeftShift`|  
|`>>`|`op_RightShift`|`RightShift`|  
|`N/A`|`op_SignedRightShift`|`SignedRightShift`|  
|`N/A`|`op_UnsignedRightShift`|`UnsignedRightShift`|  
|`==`|`op_Equality`|`Equals`|  
|`!=`|`op_Inequality`|`Equals`|  
|`>`|`op_GreaterThan`|`CompareTo`|  
|`<`|`op_LessThan`|`CompareTo`|  
|`>=`|`op_GreaterThanOrEqual`|`CompareTo`|  
|`<=`|`op_LessThanOrEqual`|`CompareTo`|  
|`*=`|`op_MultiplicationAssignment`|`Multiply`|  
|`-=`|`op_SubtractionAssignment`|`Subtract`|  
|`^=`|`op_ExclusiveOrAssignment`|`Xor`|  
|`<<=`|`op_LeftShiftAssignment`|`LeftShift`|  
|`%=`|`op_ModulusAssignment`|`Mod`|  
|`+=`|`op_AdditionAssignment`|`Add`|  
|`&=`|`op_BitwiseAndAssignment`|`BitwiseAnd`|  
|`&#124;=`|`op_BitwiseOrAssignment`|`BitwiseOr`|  
|`,`|`op_Comma`|`Comma`|  
|`/=`|`op_DivisionAssignment`|`Divide`|  
|`--`|`op_Decrement`|`Decrement`|  
|`++`|`op_Increment`|`Increment`|  
|`- (unary)`|`op_UnaryNegation`|`Negate`|  
|`+ (unary)`|`op_UnaryPlus`|`Plus`|  
|`~`|`op_OnesComplement`|`OnesComplement`|  
  
### Overload dell'operatore \= \=  
 L'overload `operator ==` è piuttosto complicato. La semantica dell'operatore desidera essere compatibili con molti altri membri, ad esempio <xref:System.Object.Equals%2A?displayProperty=fullName>.  
  
### Operatori di conversione  
 Operatori di conversione sono gli operatori unari che consentono la conversione da un tipo a altro. Gli operatori devono essere definiti come membri statici in operando o il tipo restituito. Esistono due tipi di operatori di conversione: implicite ed esplicite.  
  
 **X non** forniscono un operatore di conversione se la conversione non è chiaramente prevista dagli utenti finali.  
  
 **X non** definire operatori di conversione di fuori di dominio del tipo.  
  
 Ad esempio, <xref:System.Int32>, <xref:System.Double>, e <xref:System.Decimal> sono tutti i tipi numerici, mentre <xref:System.DateTime> non. Pertanto, non deve essere presente nessun operatore di conversione per convertire un `Double(long)` a un `DateTime`. In questo caso è preferibile utilizzare un costruttore.  
  
 **X non** forniscono un operatore di conversione implicita, se la conversione è potenzialmente perdita di dati.  
  
 Ad esempio, non sarà più presente una conversione implicita da `Double` a `Int32` poiché `Double` ha una gamma più ampia rispetto a `Int32`. Anche se la conversione è potenzialmente perdita di dati, è possibile specificare un operatore di conversione esplicita.  
  
 **X non** generare eccezioni da cast impliciti.  
  
 È molto difficile per gli utenti finali a comprendere cosa accade, poiché potrebbe non essere consapevoli che una conversione ha luogo.  
  
 **✓ si** generare <xref:System.InvalidCastException?displayProperty=fullName> Se una chiamata a un operatore cast comporta una perdita di dati conversione e il contratto dell'operatore non consente le conversioni di perdita di dati.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di membri](../../../docs/standard/design-guidelines/member.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)