---
title: "Nomi delle classi, struct e interfacce | Microsoft Docs"
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
  - "nomi dei tipi, le linee guida"
  - "classi [.NET Framework], nomi"
  - "enumerazioni [.NET Framework], nomi"
  - "nomi di interfacce [.NET Framework]"
  - "nomi di tipi comuni"
  - "nomi [.NET Framework], nomi dei tipi"
  - "nomi di classi [.NET Framework]"
  - "interfacce [.NET Framework], nomi"
  - "parametri di tipo generico"
ms.assetid: 87a4b0da-ed64-43b1-ac43-968576c444ce
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# Nomi delle classi, struct e interfacce
Convenzioni di denominazione che seguono si applicano per la denominazione di tipo generale.  
  
 **✓ si** nome classi e struct con sostantivi o frasi, utilizzando il sistema Pascal.  
  
 Consente di distinguere i nomi dei tipi di metodi, denominati con frasi di verbo.  
  
 **✓ si** nome interfacce frasi aggettivali o occasionalmente con sostantivi o frasi.  
  
 Sostantivi e sintagmi devono essere utilizzate raramente e potrebbero indicare che il tipo deve essere una classe astratta e non un'interfaccia.  
  
 **X non** ai nomi delle classi di un prefisso \(ad esempio, "C"\).  
  
 **✓ PROVARE** il nome della classe derivata con il nome della classe di base.  
  
 Questo è molto leggibile e illustra chiaramente la relazione. Sono riportati alcuni esempi di questo codice: `ArgumentOutOfRangeException`, ovvero un tipo di `Exception`, e `SerializableAttribute`, che è un tipo di `Attribute`. Tuttavia, è importante utilizzare valutando questa linea guida; ad esempio, la `Button` classe è un tipo di `Control` evento, sebbene `Control` non viene visualizzata nel relativo nome.  
  
 **✓ si** prefisso nei nomi di interfaccia con la lettera I, per indicare che il tipo è un'interfaccia.  
  
 Ad esempio, `IComponent` \(sostantivo descrittivo\), `ICustomAttributeProvider` \(locuzione\), e `IPersistable` \(aggettivo\) sono nomi di interfaccia appropriata. Come con altri nomi di tipi, evitare di abbreviazioni.  
  
 **✓ si** assicurarsi che i nomi differiscono solo per "I" prefisso nel nome dell'interfaccia quando si definisce una coppia: interfaccia della classe in cui la classe è un'implementazione standard dell'interfaccia.  
  
## Nomi dei parametri di tipo generico  
 I generics sono state aggiunte a .NET Framework 2.0. La funzionalità introdotto un nuovo tipo di identificatore denominato *parametro di tipo*.  
  
 **✓ si** denominare i parametri di tipo generico con nomi descrittivi, a meno che non è chiara completamente un nome lettera singola e un nome descrittivo non aggiungerebbero alcun valore.  
  
 **✓ PROVARE** utilizzando `T` come nome del parametro di tipo per i tipi con un parametro di tipo lettera singola.  
  
```  
public int IComparer<T> { ... }  
public delegate bool Predicate<T>(T item);  
public struct Nullable<T> where T:struct { ... }  
```  
  
 **✓ si** i nomi dei parametri di tipo descrittivi con prefisso `T`.  
  
```  
public interface ISessionChannel<TSession> where TSession : ISession{  
    TSession Session { get; }  
}  
```  
  
 **✓ PROVARE** che indica i vincoli posizionati su un parametro di tipo del nome del parametro.  
  
 Ad esempio, un parametro vincolato a `ISession` potrebbe essere denominata `TSession`.  
  
## Nomi di tipi comuni  
 **✓ si** seguire le istruzioni riportate nella tabella seguente per la denominazione di tipi derivati da o implementare determinati tipi di .NET Framework.  
  
|Tipo di base|Linee guida di tipo derivato implementa|  
|------------------|---------------------------------------------|  
|`System.Attribute`|**✓ si** aggiungere il suffisso "Attributo" ai nomi delle classi di attributi personalizzati. aggiungere il suffisso "Attributo" ai nomi delle classi di attributi personalizzati.|  
|`System.Delegate`|**✓ si** aggiungere il suffisso "EventHandler" ai nomi dei delegati utilizzati negli eventi.<br /><br /> **✓ si** aggiungere il suffisso "Callback" ai nomi dei delegati diversi da quelli usati come gestori eventi.<br /><br /> **X non** aggiungere il suffisso "Delegate" a un delegato.|  
|`System.EventArgs`|**✓ si** aggiungere il suffisso "EventArgs".|  
|`System.Enum`|**X non** derivano da questa classe, utilizzare la parola chiave supportata dal linguaggio di, ad esempio in c\#, utilizzare la parola chiave enum.<br /><br /> **X non** aggiungere il suffisso "Enum" o "Flag".|  
|`System.Exception`|**✓ si** aggiungere il suffisso "Exception".|  
|`IDictionary` <br /> `IDictionary<TKey,TValue>`|**✓ si** aggiungere il suffisso "Dizionario". Si noti che `IDictionary` è un tipo specifico della raccolta, ma questa linea guida ha la precedenza sul più generale raccolte che segue.|  
|`IEnumerable` <br /> `ICollection` <br /> `IList` <br /> `IEnumerable<T>` <br /> `ICollection<T>` <br /> `IList<T>`|**✓ si** aggiungere il suffisso "Raccolta".|  
|`System.IO.Stream`|**✓ si** aggiungere il suffisso "Stream".|  
|`CodeAccessPermission IPermission`|**✓ si** aggiungere il suffisso "Autorizzazione".|  
  
## Denominazione delle enumerazioni  
 I nomi di tipi di enumerazione \(detti anche enumerazioni\) in genere devono seguire le regole tipo di denominazione standard \(il sistema Pascal, ecc.\). Tuttavia, esistono ulteriori linee guida specifiche per le enumerazioni.  
  
 **✓ si** utilizzare un nome di tipo singolare per un'enumerazione, a meno che i valori sono i campi di bit.  
  
 **✓ si** utilizzare un nome plurale tipo per un'enumerazione con i campi di bit come valori, l'acronimo di enumerazione di flag.  
  
 **X non** utilizzare un suffisso "Enum" nei nomi di tipo enum.  
  
 **X non** utilizzare "Flag" o nomi dei tipi di suffissi "Flag" nell'enumerazione.  
  
 **X non** utilizzare un prefisso ai nomi di valore di enumerazione \(ad esempio, "ad" per le enumerazioni ADO.\), "rtf" per le enumerazioni RTF e così via.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Convenzioni di denominazione](../../../docs/standard/design-guidelines/naming-guidelines.md)