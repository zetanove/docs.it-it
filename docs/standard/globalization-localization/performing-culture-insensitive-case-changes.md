---
title: "Esecuzione di modifiche di maiuscole e minuscole indipendenti dalle impostazioni cultura | Microsoft Docs"
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
  - "String.ToLower (metodo)"
  - "impostazioni cultura, distinzione tra maiuscole e minuscole"
  - "Char.ToLower (metodo)"
  - "maiuscole/minuscole, modifica in stringhe indipendenti dalle impostazioni cultura"
  - "Char.ToUpper (metodo)"
  - "operazioni sulle stringhe indipendenti dalle impostazioni cultura, modifica di maiuscole/minuscole"
  - "String.ToUpper (metodo)"
  - "parametro culture"
ms.assetid: 822d551c-c69a-4191-82f4-183d82c9179c
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Esecuzione di modifiche di maiuscole e minuscole indipendenti dalle impostazioni cultura
I metodi <xref:System.String.ToUpper%2A?displayProperty=fullName>, <xref:System.String.ToLower%2A?displayProperty=fullName>, <xref:System.Char.ToUpper%2A?displayProperty=fullName> e <xref:System.Char.ToLower%2A?displayProperty=fullName> forniscono overload che non accettano parametri.  Per impostazione predefinita, gli overload privi di parametri eseguono modifiche delle lettere maiuscole e minuscole in base al valore di <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>.  Si ottengono così risultati con distinzione tra maiuscole e minuscole che possono variare in base alle impostazioni cultura  Per indicare chiaramente se si desidera eseguire modifiche delle lettere maiuscole e minuscole dipendenti o indipendenti dalle impostazioni cultura, è opportuno utilizzare gli overload di questi metodi che richiedono la specifica esplicita di un parametro `culture`.  Per le modifiche di maiuscole e minuscole dipendenti dalle impostazioni cultura, specificare `CultureInfo.CurrentCulture` per il parametro `culture`.  Per le modifiche di maiuscole e minuscole non dipendenti dalle impostazioni cultura, specificare `CultureInfo.InvariantCulture` per il parametro `culture`.  
  
 Le stringhe vengono spesso convertite in una combinazione di maiuscole e minuscole standard per semplificare successivamente la ricerca.  Quando le stringhe vengono utilizzate in questo modo, è opportuno specificare `CultureInfo.InvariantCulture` per il parametro `culture`, poiché è possibile che vengano apportate modifiche al valore di <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=fullName> tra il momento in cui vengono modificate le lettere maiuscole e minuscole e il momento in cui viene eseguita la ricerca.  
  
 Se una decisione relativa alla sicurezza è basata sul risultato di una modifica di maiuscole e minuscole, è necessario che l'operazione sia indipendente dalle impostazioni cultura affinché il risultato non sia influenzato dal valore di `CultureInfo.CurrentCulture`.  Per un esempio che dimostri come le operazioni su stringhe dipendenti dalle impostazioni cultura possano produrre risultati non coerenti, vedere la sezione "Confronti di stringhe in cui vengono utilizzate le impostazioni cultura correnti" dell'articolo [Procedure consigliate per l'utilizzo di stringhe](../../../docs/standard/base-types/best-practices-strings.md).  
  
## Utilizzo dei metodi String.ToUpper e String.ToLower  
 Per una maggiore chiarezza del codice, è consigliabile utilizzare sempre overload dei metodi `String.ToUpper` e `String.ToLower`, che consentono di specificare in modo esplicito un parametro `culture`.  Nel codice riportato di seguito, ad esempio, viene eseguita una ricerca di identificatori.  Per impostazione predefinita, l'operazione `key.ToLower` è dipendente dalle impostazioni cultura, tuttavia questo comportamento non risulta in modo evidente dalla lettura del codice.  
  
### Esempio  
  
```vb  
Shared Function LookupKey(key As String) As Object  
   Return internalHashtable(key.ToLower())  
End Function  
  
```  
  
```csharp  
static object LookupKey(string key)   
{  
    return internalHashtable[key.ToLower()];  
}  
```  
  
 Se si desidera rendere l'operazione `key.ToLower` indipendente dalle impostazioni cultura, è necessario modificare l'esempio precedente come indicato di seguito, in modo da utilizzare in modo esplicito `CultureInfo.InvariantCulture` quando viene eseguita la modifica delle lettere maiuscole e minuscole.  
  
```vb  
Shared Function LookupKey(key As String) As Object  
    Return internalHashtable(key.ToLower(CultureInfo.InvariantCulture))  
End Function  
  
```  
  
```csharp  
static object LookupKey(string key)   
{  
    return internalHashtable[key.ToLower(CultureInfo.InvariantCulture)];  
}  
```  
  
## Utilizzo dei metodi Char.ToUpper e Char.ToLower  
 Sebbene i metodi `Char.ToUpper` e `Char.ToLower` abbiano le stesse caratteristiche dei metodi `String.ToUpper` e `String.ToLower`, le uniche impostazioni cultura su cui hanno effetto sono Turco \(Turchia\) e Azero \(alfabeto latino, Azerbaijan\).  poiché costituiscono le uniche due impostazioni cultura con differenze tra lettere maiuscole e minuscole relative a singoli caratteri.  Per informazioni dettagliate su questo esclusivo mapping di maiuscole e minuscole, vedere la sezione "Maiuscole e minuscole" dell'argomento relativo alla classe <xref:System.String>.  Per una maggiore chiarezza del codice e per garantire risultati coerenti, è consigliabile utilizzare sempre gli overload di questi metodi che consentono di specificare in modo esplicito un parametro `culture`.  
  
## Vedere anche  
 <xref:System.String.ToUpper%2A?displayProperty=fullName>   
 <xref:System.String.ToLower%2A?displayProperty=fullName>   
 <xref:System.Char.ToUpper%2A?displayProperty=fullName>   
 <xref:System.Char.ToLower%2A?displayProperty=fullName>   
 [Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)