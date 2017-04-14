---
title: "Nomi dei membri dei tipi | Microsoft Docs"
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
  - "eventi [.NET Framework], nomi"
  - "metodi [.NET Framework], nomi"
  - "membri di tipi"
  - "proprietà di nomi [.NET Framework]"
  - "i nomi di campi"
  - "nomi dei campi"
  - "nomi di membri dei tipi [.NET Framework]"
  - "tipo di membri [.NET Framework]"
ms.assetid: af5a0903-36af-4c2a-b848-cf959affeaa5
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Nomi dei membri dei tipi
I tipi sono costituiti da membri: metodi, proprietà, eventi, costruttori e campi. Le sezioni seguenti descrivono le linee guida per la denominazione dei membri dei tipi.  
  
## Nomi dei metodi  
 Poiché i metodi sono i mezzi per eseguire azioni, linee guida di progettazione richiedono che i nomi di metodo verbi o frasi di verbo. Seguendo questa linea Guida anche viene usato per distinguere i nomi dei metodi da nomi di proprietà e il tipo, ovvero frasi o aggettivali.  
  
 **✓ si** assegnare nomi di metodi che sono verbi o frasi di verbo.  
  
```  
public class String {  
    public int CompareTo(...);  
    public string[] Split(...);  
    public string Trim();  
}  
  
```  
  
## Nomi delle proprietà  
 A differenza di altri membri, proprietà devono avere nomi aggettivali o sintagma nominale. Infatti, una proprietà fa riferimento a dati e il nome della proprietà riflette che. Il sistema Pascal viene sempre utilizzato per i nomi delle proprietà.  
  
 **✓ si** nome proprietà usando un sostantivo, locuzione o aggettivo.  
  
 **X non** dispongono di proprietà che corrispondono al nome dei metodi "Get" come nell'esempio seguente:  
  
 `public string TextWriter { get {...} set {...} }`   
 `public string GetTextWriter(int value) { ... }`  
  
 Questo modello è in genere indica che la proprietà deve essere effettivamente un metodo.  
  
 **✓ si** nome proprietà della raccolta con una frase plurale che descrive gli elementi della raccolta anziché una frase singolare seguita da "List" o "Raccolta".  
  
 **✓ si** proprietà booleane con una frase affermativa \(`CanSeek` anziché `CantSeek`\). Facoltativamente, è possibile anteporre anche le proprietà booleane con "Is", "può" o "Ha" ma solo se aggiunge valore.  
  
 **✓ PROVARE** assegnare lo stesso nome di tipo a una proprietà.  
  
 Ad esempio, la proprietà seguente correttamente viene impostato un valore enum denominato `Color`, pertanto la proprietà è denominata `Color`:  
  
```  
public enum Color {...}  
public class Control {  
    public Color Color { get {...} set {...} }  
}  
```  
  
## Nomi degli eventi  
 Gli eventi fanno sempre riferiscono a un'azione, un problema o quello che si è verificato. Come con i metodi, eventi vengono denominati con i verbi e tempi verbali di verbi viene utilizzato per indicare l'ora quando viene generato l'evento.  
  
 **✓ si** gli eventi con un verbo o una frase verbo.  
  
 Gli esempi includono `Clicked`, `Painting`, `DroppedDown`, e così via.  
  
 **✓ si** assegnare nomi di eventi con un concetto di prima e dopo, utilizzando il presente e negli ultimi tempi.  
  
 Ad esempio, potrebbe essere chiamato un evento di chiusura che viene generato prima della chiusura di una finestra `Closing`, e uno che viene generato dopo la chiusura della finestra `Closed`.  
  
 **X non** utilizzare "Before" o "After" prefissi o suffissi per indicare pre\- e post\-eventi. Utilizzare presente e negli ultimi tempi come descritto in precedenza.  
  
 **✓ si** denominare i gestori di eventi \(delegati utilizzati come tipi di eventi\) con il suffisso "EventHandler", come illustrato nell'esempio seguente:  
  
 `public delegate void ClickedEventHandler(object sender, ClickedEventArgs e);`  
  
 **✓ si** utilizzare due parametri denominati `sender` e `e` nei gestori eventi.  
  
 Il parametro mittente rappresenta l'oggetto che ha generato l'evento. Il parametro mittente è in genere di tipo `object`, anche se è possibile utilizzare un tipo più specifico.  
  
 **✓ si** nome evento classi dell'argomento con il suffisso "EventArgs".  
  
## Nomi dei campi  
 Le convenzioni di denominazione per campo si applicano ai campi statici pubblici e protetti. Campi interni e privati non sono coperti da linee guida e i campi di istanza pubblici o protetti non sono consentiti per il [indicazioni per la progettazione di membri](../../../docs/standard/design-guidelines/member.md).  
  
 **✓ si** utilizzare il sistema Pascal nei nomi di campo.  
  
 **✓ si** nome campi utilizzando un sostantivo, locuzione o aggettivo.  
  
 **X non** utilizzare un prefisso per i nomi dei campi.  
  
 Ad esempio, non utilizzare "g \_" o "s \_" per indicare i campi statici.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Convenzioni di denominazione](../../../docs/standard/design-guidelines/naming-guidelines.md)