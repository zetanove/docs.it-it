---
title: "Confronti e ordinamenti all&#39;interno delle raccolte | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "raccolte [.NET Framework], confronti"
  - "Collections (classi)"
  - "Equals (metodo)"
  - "IComparable.CompareTo (metodo)"
  - "ordinamento dei dati, raccolte"
ms.assetid: 5e4d3b45-97f0-423c-a65f-c492ed40e73b
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# Confronti e ordinamenti all&#39;interno delle raccolte
Le classi <xref:System.Collections> eseguono confronti in quasi tutti i processi di gestione delle raccolte, ricercando l'elemento da rimuovere o restituendo il valore di una coppia chiave\-valore.  
  
 Le raccolte in genere usano un operatore di uguaglianza e\/o un confronto di ordinamento. Vengono usati due costrutti per i confronti.  
  
<a name="BKMK_Checkingforequality"></a>   
## Verifica dell'uguaglianza  
 I metodi come `Contains`, <xref:System.Collections.IList.IndexOf%2A>, <xref:System.Collections.Generic.List%601.LastIndexOf%2A> e `Remove` usano un confronto di uguaglianza per gli elementi della raccolta. Se la raccolta è generica, viene verificata l'uguaglianza degli elementi secondo le istruzioni seguenti:  
  
-   Se il tipo T implementa l'interfaccia generica <xref:System.IEquatable%601>, il confronto di uguaglianza è il metodo <xref:System.IEquatable%601.Equals%2A> di tale interfaccia.  
  
-   Se il tipo T non implementa <xref:System.IEquatable%601>, viene usato <xref:System.Object.Equals%2A?displayProperty=fullName>.  
  
 Inoltre, alcuni overload del costruttore per le raccolte dizionario accettano un'implementazione di <xref:System.Collections.Generic.IEqualityComparer%601>, che viene usata per confrontare l'uguaglianza delle chiavi. Per un esempio, vedere il costruttore <xref:System.Collections.Generic.Dictionary%602.%23ctor%2A?displayProperty=fullName>.  
  
<a name="BKMK_Determiningsortorder"></a>   
## Determinare il tipo di ordinamento  
 I metodi come `BinarySearch` e `Sort` usano un confronto di ordinamento per gli elementi della raccolta. È possibile eseguire il confronto tra gli elementi della raccolta o tra un elemento e un valore specificato. Per confrontare gli oggetti, esiste il concetto di `default comparer` e `explicit comparer`.  
  
 L'operatore di confronto predefinito si basa su almeno uno degli oggetti confrontati per implementare l'interfaccia **IComparable**. Si consiglia di implementare **IComparable** in tutte le classi che vengono usate come valori in una raccolta di elenchi o come chiavi in una raccolta di dizionari. Per una raccolta generica, il confronto di uguaglianza è determinato come segue:  
  
-   Se il tipo T implementa l'interfaccia generica <xref:System.IComparable%601?displayProperty=fullName>, l'operatore di confronto predefinito è il metodo <xref:System.IComparable%601.CompareTo%28%600%29?displayProperty=fullName> di tale interfaccia  
  
-   Se il tipo T implementa l'interfaccia non generica <xref:System.IComparable?displayProperty=fullName>, l'operatore di confronto predefinito è il metodo <xref:System.IComparable.CompareTo%28System.Object%29?displayProperty=fullName> di tale interfaccia.  
  
-   Se il tipo T non implementa alcuna interfaccia, non sarà presente nessun operatore di confronto predefinito e sarà necessario fornire in modo esplicito un delegato di confronto un o operatore di confronto.  
  
 Per fornire i confronti espliciti, alcuni metodi accettano un'implementazione **IComparer** come parametro. Ad esempio, il metodo <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=fullName> accetta un'implementazione <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName>.  
  
 L'impostazione cultura corrente del sistema può influenzare i confronti e gli ordinamenti all'interno di una raccolta. Per impostazione predefinita, i confronti e gli ordinamenti nelle classi **Collections** classi sono dipendenti dalle impostazioni cultura. Per ignorare l'impostazione cultura e quindi ottenere risultati coerenti di confronto e ordinamento, usare il <xref:System.Globalization.CultureInfo.InvariantCulture%2A> con gli overload dei membri che accettano un <xref:System.Globalization.CultureInfo>. Per altre informazioni, vedere [Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura nelle raccolte](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-collections.md) e [Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura nelle matrici](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-arrays.md).  
  
<a name="BKMK_Equalityandsortexample"></a>   
## Esempio di uguaglianza e ordinamento  
 Nel codice seguente viene illustrata un'implementazione di <xref:System.IEquatable%601> e <xref:System.IComparable%601> su un semplice oggetto business. Inoltre, quando l'oggetto viene memorizzato in un elenco e ordinato, la chiamata al metodo <xref:System.Collections.Generic.List%601.Sort> risulterà nell'uso dell'operatore di confronto predefinito per il tipo `Part` e il metodo <xref:System.Collections.Generic.List%601.Sort%28System.Comparison%7B%600%7D%29> implementato usando un metodo anonimo.  
  
 [!code-csharp[System.Collections.Generic.List.Sort#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.collections.generic.list.sort/cs/program.cs#1)]
 [!code-vb[System.Collections.Generic.List.Sort#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.collections.generic.list.sort/vb/module1.vb#1)]  
  
## Vedere anche  
 <xref:System.Collections.IComparer>   
 <xref:System.IEquatable%601>   
 <xref:System.Collections.Generic.IComparer%601>   
 <xref:System.IComparable>   
 <xref:System.IComparable%601>