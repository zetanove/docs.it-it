---
title: "Modifica della combinazione di maiuscole e minuscole in .NET Framework | Microsoft Docs"
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
  - "distinzione tra maiuscole e minuscole"
  - "minuscole"
  - "stringhe [.NET Framework], maiuscole e minuscole"
  - "ToLower (metodo)"
  - "ToUpper (metodo)"
  - "maiuscole"
ms.assetid: 6805f81b-e9ad-4387-9f4c-b9bdb21b87c0
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Modifica della combinazione di maiuscole e minuscole in .NET Framework
Quando si scrive un'applicazione che accetta input dall'utente non si può conoscere la combinazione di maiuscole e minuscole che verrà usata durante l'immissione dei dati.  Spesso è desiderabile che le la combinazione di maiuscole e minuscole nelle stringhe sia coerente, in particolare se le stringhe vengono visualizzate nell'interfaccia utente.  La tabella seguente descrive tre metodi per la modifica della combinazione di maiuscole e minuscole.  I primi due metodi forniscono un overload che accetta determinate impostazioni cultura.  
  
|Nome metodo|Utilizzo|  
|-----------------|--------------|  
|<xref:System.String.ToUpper%2A?displayProperty=fullName>|Converte tutti i caratteri di una stringa in lettere maiuscole.|  
|<xref:System.String.ToLower%2A?displayProperty=fullName>|Converte tutti i caratteri di una stringa in lettere minuscole.|  
|<xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=fullName>|Converte una stringa nella combinazione con tutte le iniziali maiuscole.|  
  
> [!WARNING]
>  Si noti che i metodi <xref:System.String.ToUpper%2A?displayProperty=fullName> e <xref:System.String.ToLower%2A?displayProperty=fullName> non vanno usati per convertire le stringhe a scopo di confronto o verifica dell'uguaglianza.  Per altre informazioni, vedere la sezione [Confronto di stringhe in caratteri maiuscoli e minuscoli](#Comparing).  
  
<a name="Comparing"></a>   
## Confronto di stringhe con una combinazione mista di maiuscole e minuscole  
 Per confrontare stringhe composte da una combinazione mista di maiuscole e minuscole allo scopo di determinarne l'ordinamento, chiamare uno degli overload del metodo <xref:System.String.CompareTo%2A?displayProperty=fullName> con un parametro `comparisonType` e quindi fornire un valore di <xref:System.StringComparison?displayProperty=fullName>, <xref:System.StringComparison?displayProperty=fullName> o <xref:System.StringComparison?displayProperty=fullName> per l'argomento `comparisonType`.  Per eseguire un confronto usando impostazioni cultura diverse da quelle correnti, chiamare un overload del metodo <xref:System.String.CompareTo%2A?displayProperty=fullName> con un parametro `culture` e un parametro `options` e fornire un valore di <xref:System.Globalization.CompareOptions?displayProperty=fullName> come argomento `options`.  
  
 Per confrontare stringhe in caratteri maiuscoli e minuscoli allo scopo di determinarne se sono uguali, chiamare uno degli overload del metodo <xref:System.String.Equals%2A?displayProperty=fullName> con un parametro `comparisonType` e quindi fornire un valore di <xref:System.StringComparison?displayProperty=fullName>, <xref:System.StringComparison?displayProperty=fullName> o <xref:System.StringComparison?displayProperty=fullName> per l'argomento `comparisonType`.  
  
 Per altre informazioni, vedere [Procedure consigliate per l'utilizzo di stringhe](../../../docs/standard/base-types/best-practices-strings.md).  
  
## ToUpper  
 Il metodo <xref:System.String.ToUpper%2A?displayProperty=fullName> converte tutti i caratteri di una stringa in lettere maiuscole.  L'esempio seguente converte la stringa "Hello World\!" da una combinazione mista di maiuscole e minuscole in sole lettere maiuscole.  
  
 [!code-csharp[Strings.ChangingCase#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.ChangingCase/cs/Example.cs#1)]
 [!code-vb[Strings.ChangingCase#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.ChangingCase/vb/Example.vb#1)]  
  
 L'esempio precedente dipende dalle impostazioni cultura per impostazione predefinita; applica le convenzioni sulla combinazione di maiuscole e minuscole delle impostazioni cultura correnti.  Per eseguire una modifica di maiuscole e minuscole indipendente dalle impostazioni cultura o applicare le convenzioni sulla combinazione di maiuscole e minuscole di determinate impostazioni cultura, usare l'overload del metodo <xref:System.String.ToUpper%28System.Globalization.CultureInfo%29?displayProperty=fullName> e fornire il valore <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> o un oggetto <xref:System.Globalization.CultureInfo?displayProperty=fullName> che rappresenti le impostazioni cultura specificate nel parametro *culture*.  Per un esempio in cui viene illustrato l'uso del metodo <xref:System.String.ToUpper%2A> per eseguire una modifica della combinazione di maiuscole e minuscole indipendente dalle impostazioni cultura, vedere [Esecuzione di modifiche di maiuscole e minuscole indipendenti dalle impostazioni cultura](../../../ocs/standard/globalization-localization/performing-culture-insensitive-case-changes.md).  
  
## ToLower  
 Il metodo <xref:System.String.ToLower%2A?displayProperty=fullName> è simile al precedente, con la differenza che converte tutti i caratteri di una stringa in lettere minuscole.  L'esempio seguente converte la stringa "Hello World\!" in lettere minuscole.  
  
 [!code-csharp[Strings.ChangingCase#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.ChangingCase/cs/Example.cs#2)]
 [!code-vb[Strings.ChangingCase#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.ChangingCase/vb/Example.vb#2)]  
  
 L'esempio precedente dipende dalle impostazioni cultura per impostazione predefinita; applica le convenzioni sulla combinazione di maiuscole e minuscole delle impostazioni cultura correnti.  Per eseguire una modifica di maiuscole e minuscole indipendente dalle impostazioni cultura o applicare le convenzioni sulla combinazione di maiuscole e minuscole di determinate impostazioni cultura, usare l'overload del metodo <xref:System.String.ToLower%28System.Globalization.CultureInfo%29?displayProperty=fullName> e fornire il valore <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> o un oggetto <xref:System.Globalization.CultureInfo?displayProperty=fullName> che rappresenti le impostazioni cultura specificate nel parametro *culture*.  Per un esempio in cui viene illustrato l'uso del metodo <xref:System.String.ToLower%28System.Globalization.CultureInfo%29> per eseguire una modifica della combinazione di maiuscole e minuscole indipendente dalle impostazioni cultura, vedere [Esecuzione di modifiche di maiuscole e minuscole indipendenti dalle impostazioni cultura](../../../ocs/standard/globalization-localization/performing-culture-insensitive-case-changes.md).  
  
## ToTitleCase  
 Il metodo <xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=fullName> converte il primo carattere di ogni parola in maiuscolo e i caratteri rimanenti in minuscolo.  Le parole interamente in maiuscolo, tuttavia, vengono considerate acronimi e non vengono convertite.  
  
 Il metodo <xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=fullName> è basato sulle impostazioni cultura, vale a dire che usa le convenzioni sulla combinazione di maiuscole e minuscole di determinate impostazioni cultura.  Per chiamare il metodo è innanzitutto necessario recuperare l'oggetto <xref:System.Globalization.TextInfo>, che rappresenta le convenzioni sulla combinazione di maiuscole e minuscole di determinate impostazioni cultura, dalla proprietà <xref:System.Globalization.CultureInfo.TextInfo%2A?displayProperty=fullName> di specifiche impostazioni cultura.  
  
 Nell'esempio, ogni stringa di una matrice viene passata al metodo <xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=fullName>.  Nelle stringhe sono incluse le stringhe corrette dei titoli e gli acronimi.  Le stringhe vengono convertite in maiuscole usando le convenzioni delle impostazioni cultura Inglese \(Stati Uniti\).  
  
 [!code-csharp[System.Globalization.TextInfo.ToTitleCase#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.globalization.textinfo.totitlecase/cs/totitlecase2.cs#1)]
 [!code-vb[System.Globalization.TextInfo.ToTitleCase#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.globalization.textinfo.totitlecase/vb/totitlecase2.vb#1)]  
  
 Si noti che, sebbene sia dipendente dalle impostazioni cultura, il metodo <xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=fullName> non fornisce regole sull'uso di maiuscole e minuscole linguisticamente corrette.  Ad esempio, nell'esempio precedente, il metodo converte "a tale of two cities" in "A Tale Of Two Cities".  Tuttavia, la combinazione linguisticamente corretta per le impostazioni cultura Inglese \(Stati Uniti\) è "A Tale of Two Cities."  
  
## Vedere anche  
 [Operazioni di base su stringhe](../../../docs/standard/base-types/basic-string-operations.md)   
 [Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura](../../../ocs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)