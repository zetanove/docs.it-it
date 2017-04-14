---
title: "Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura nelle matrici | Microsoft Docs"
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
  - "matrici [.NET Framework], operazioni su stringhe senza distinzione di impostazioni cultura"
  - "parametro di confronto"
  - "operazioni su stringhe senza distinzione di impostazioni cultura, in matrici"
ms.assetid: f12922e1-6234-4165-8896-63f0653ab478
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura nelle matrici
Per impostazione predefinita, gli overload dei metodi <xref:System.Array.Sort%2A?displayProperty=fullName> e <xref:System.Array.BinarySearch%2A?displayProperty=fullName> consentono di eseguire ordinamenti dipendenti dalle impostazioni cultura utilizzando la proprietà <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=fullName>.  I risultati dipendenti dalle impostazioni cultura restituiti da questi metodi possono variare in base alle impostazioni cultura, a causa delle differenze nei criteri di ordinamento.  Per eliminare il comportamento dipendente dalle impostazioni cultura, utilizzare uno degli overload del metodo che accettano un parametro `comparer`.  Il parametro `comparer` specifica l'implementazione di <xref:System.Collections.IComparer> da utilizzare per il confronto degli elementi all'interno della matrice.  Per il parametro, specificare una classe di operatori di confronto invariante personalizzata che utilizzi <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.  Per un esempio di classe di questo tipo, vedere la sezione "Utilizzo della classe SortedList" dell'argomento [Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura nelle raccolte](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-collections.md).  
  
 **Nota** Se si passa **CultureInfo.InvariantCulture** a un metodo di confronto, viene eseguito un confronto indipendente dalla lingua.  Non viene tuttavia eseguito un confronto non linguistico, ad esempio per percorsi di file, chiavi del Registro di sistema e variabili di ambiente  e non sono supportate le decisioni relative alla sicurezza basate sul risultato del confronto.  Per un confronto non linguistico o per il supporto delle decisioni relative alla sicurezza basate sul risultato, l'applicazione deve utilizzare un metodo di confronto che accetti un valore <xref:System.StringComparison>.  L'applicazione deve quindi passare <xref:System.StringComparison>.  
  
## Vedere anche  
 <xref:System.Array.Sort%2A?displayProperty=fullName>   
 <xref:System.Array.BinarySearch%2A?displayProperty=fullName>   
 <xref:System.Collections.IComparer>   
 [Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)