---
title: "Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura | Microsoft Docs"
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
  - "mapping di maiuscole e minuscole"
  - "maiuscole e minuscole (mapping personalizzati)"
  - "impostazioni cultura, regole di ordinamento personalizzate"
  - "regole di ordinamento personalizzate"
  - "operazioni sulle stringhe indipendenti dalle impostazioni cultura, opzioni per l'esecuzione"
  - "impostazioni cultura, maiuscole e minuscole (mapping personalizzati)"
  - "operazioni sulle stringhe indipendenti dalle impostazioni cultura, overload di metodi"
ms.assetid: 579ef891-1f83-4c63-9ebd-2f40406b5b91
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura
Per la maggior parte, i metodi di .NET Framework che eseguono operazioni sulle stringhe dipendenti dalle impostazioni cultura forniscono, per impostazione predefinita, overload dei metodi che consentono di specificare in modo esplicito le impostazioni cultura da utilizzare mediante il passaggio di un parametro <xref:System.Globalization.CultureInfo>.  Questi overload consentono di eliminare le variazioni legate alle impostazioni cultura in mapping tra maiuscole e minuscole e regole di ordinamento e garantiscono risultati indipendenti dalle impostazioni cultura.  
  
 In questa sezione vengono forniti gli argomenti elencati di seguito, in cui viene illustrato come eseguire operazioni sulle stringhe indipendenti dalle impostazioni cultura utilizzando metodi .NET Framework che per impostazione predefinita sono dipendenti dalle impostazioni cultura.  
  
## In questa sezione  
 [Esecuzione di confronti di stringhe indipendenti dalle impostazioni cultura](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-comparisons.md)  
 Viene illustrato come utilizzare i metodi <xref:System.String.Compare%2A?displayProperty=fullName> e <xref:System.String.CompareTo%2A?displayProperty=fullName> per eseguire confronti di stringhe indipendenti dalle impostazioni cultura.  
  
 [Esecuzione di modifiche di maiuscole e minuscole indipendenti dalle impostazioni cultura](../../../docs/standard/globalization-localization/performing-culture-insensitive-case-changes.md)  
 Viene illustrato come utilizzare i metodi <xref:System.String.ToUpper%2A?displayProperty=fullName>, <xref:System.String.ToLower%2A?displayProperty=fullName>, <xref:System.Char.ToUpper%2A?displayProperty=fullName> e <xref:System.Char.ToLower%2A?displayProperty=fullName> per eseguire modifiche delle lettere maiuscole e minuscole indipendenti dalle impostazioni cultura.  
  
 [Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura nelle raccolte](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-collections.md)  
 Viene descritto come utilizzare le classi [CaseInsensitiveComparer](frlrfSystemCollectionsCaseInsensitiveComparerClassTopic), <xref:System.Collections.CaseInsensitiveHashCodeProvider> e [SortedList](frlrfSystemCollectionsSortedListClassTopic) e i metodi [ArrayList.Sort](https://msdn.microsoft.com/en-us/library/system.collections.arraylist.sort.aspx) e [CollectionsUtil.CreateCaseInsensitiveHashtable](frlrfSystemCollectionsSpecializedCollectionsUtilClassCreateCaseInsensitiveHashtableTopic) per eseguire operazioni indipendenti dalle impostazioni cultura nelle raccolte.  
  
 [Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura nelle matrici](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-arrays.md)  
 Viene illustrato come utilizzare i metodi <xref:System.Array.Sort%2A?displayProperty=fullName> e <xref:System.Array.BinarySearch%2A?displayProperty=fullName> per eseguire operazioni nelle matrici indipendenti dalle impostazioni cultura.  
  
## Sezioni correlate  
 [Operazioni sulle stringhe indipendenti dalle impostazioni cultura](../../../docs/standard/globalization-localization/culture-insensitive-string-operations.md)  
 Vengono descritti i motivi per cui è opportuno tenere in considerazione le impostazioni cultura in occasione dell'esecuzione di operazioni sulle stringhe e vengono fornite indicazioni sui casi in cui devono essere eseguite operazioni dipendenti dalle impostazioni cultura o operazioni indipendenti dalle impostazioni cultura.