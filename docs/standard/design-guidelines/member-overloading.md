---
title: "Overload dei membri | Microsoft Docs"
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
  - "argomenti predefiniti"
  - "overload di membri [.NET Framework]"
  - "linee guida di progettazione membri [.NET Framework], overload"
  - "membri in overload"
  - "firme di membri"
ms.assetid: 964ba19e-8b94-4b5b-b1e3-5a0b531a0bb1
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Overload dei membri
Overload dei membri significa creare due o più membri sullo stesso tipo che differiscono solo per il numero o tipo di parametri, ma hanno lo stesso nome. Ad esempio, di seguito, il `WriteLine` metodo viene sottoposto a overload:  
  
```  
public static class Console {  
    public void WriteLine();  
    public void WriteLine(string value);  
    public void WriteLine(bool value);  
    ...  
}  
  
```  
  
 Poiché solo i metodi, costruttori e proprietà indicizzate possono avere parametri, solo i membri possono essere sottoposti a overload.  
  
 Eseguire l'overload è una delle tecniche più importanti per migliorare l'usabilità, la produttività e la leggibilità di librerie riutilizzabili. L'overload per il numero di parametri consente di fornire versioni semplificate di costruttori e metodi. L'overload del tipo di parametro consente di utilizzare lo stesso nome di membro per eseguire operazioni identiche su un insieme selezionato di diversi tipi di membri.  
  
 **✓ si** tenta di utilizzare nomi di parametro descrittivi per indicare il valore predefinito utilizzato dagli overload più breve.  
  
 **X evitare** arbitrariamente i nomi dei parametri in overload. Se un parametro in uno degli overload rappresenta lo stesso input di un parametro in un altro overload, tali parametri devono avere lo stesso nome.  
  
 **X evitare** incoerente nell'ordine dei parametri in membri di overload. I parametri con lo stesso nome dovrebbero essere visualizzato nella stessa posizione in tutti gli overload.  
  
 **✓ si** rendere virtuale solo l'overload più lungo \(se viene richiesta un'estensibilità\). Gli overload più brevi devono semplicemente chiamare tramite un overload più lungo.  
  
 **X non** utilizzare `ref` o `out` modificatori per eseguire l'overload di membri.  
  
 Alcuni linguaggi non possono risolvere le chiamate a overload simile al seguente. Inoltre, tali overload in genere hanno una semantica completamente diversa e probabilmente non deve essere overload ma due metodi distinti invece.  
  
 **X non** dispongono di overload con parametri alla stessa posizione e tipi simili ma con una semantica diversa.  
  
 **✓ si**  consentire `null` da passare per gli argomenti facoltativi.  
  
 **✓ si** utilizzare l'overload dei membri anziché definire membri con gli argomenti predefiniti.  
  
 Gli argomenti predefiniti non sono conformi a CLS.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di membri](../../../docs/standard/design-guidelines/member.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)