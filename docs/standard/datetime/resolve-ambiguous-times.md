---
title: 'Procedura: Risolvere orari ambigui'
description: Come risolvere gli orari ambigui
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 08/16/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: e86050c6-d16d-405e-8bba-7205945c9a81
translationtype: Human Translation
ms.sourcegitcommit: c40c28da09e8a122b542463c197196c82c81dd19
ms.openlocfilehash: b31ea18cd7a7e32863f384cb279dc715fd62b3df

---

# <a name="how-to-resolve-ambiguous-times"></a>Procedura: Risolvere orari ambigui

Un'ora ambigua è un'ora associata a più ore UTC (Coordinated Universal Time). Si verifica quando l'orologio viene riportato indietro, ad esempio durante la transizione dall'ora legale all'ora solare di un determinato fuso orario. Quando si gestisce un'ora ambigua è possibile eseguire una delle operazioni seguenti:

* Fare una supposizione sulla modalità di associazione dell'ora all'ora UTC. Si può, ad esempio, presupporre che un'ora ambigua sia sempre espressa nell'ora solare del fuso orario.

* Se l'ora ambigua è un elemento di dati immesso dall'utente, sarà l'utente a risolvere l'ambiguità.

In questo articolo viene illustrato come risolvere un'ora ambigua presupponendo che rappresenti l'ora solare del fuso orario.

## <a name="to-map-an-ambiguous-time-to-a-time-zones-standard-time"></a>Per eseguire il mapping di un'ora ambigua all'ora solare del fuso orario

1. Chiamare il metodo[System.TimeZoneInfo.IsAmbiguousTime(DateTime)](xref:System.TimeZoneInfo.IsAmbiguousTime(System.DateTime)) o [System.TimeZoneInfo.IsAmbiguousTime(DateTimeOffset)](xref:System.TimeZoneInfo.IsAmbiguousTime(System.DateTimeOffset)) per determinare se l'ora è ambigua.

2. Se l'ora è ambigua, sottrarre l'ora dall'oggetto [TimeSpan](xref:System.TimeSpan) restituito dalla proprietà [BaseUtcOffset](xref:System.TimeZoneInfo.BaseUtcOffset) del fuso orario.

3. Chiamare il metodo `static` (`Shared` in Visual Basic) [SpecifyKind](xref:System.DateTime.SpecifyKind(System.DateTime,System.DateTimeKind)) per impostare la proprietà [Kind](xref:System.DateTime.Kind) del valore di data e ora UTC su [DateTimeKind.Utc](xref:System.DateTimeKind.Utc).

## <a name="example"></a>Esempio

Nell'esempio seguente viene illustrato come convertire un valore [DateTime](xref:System.DateTime) ambiguo in ora UTC, presupponendo che rappresenti l'ora solare del fuso orario locale. 

```csharp
private DateTime ResolveAmbiguousTime(DateTime ambiguousTime)
{
   // Time is not ambiguous
   if (! TimeZoneInfo.Local.IsAmbiguousTime(ambiguousTime))
   { 
      return ambiguousTime; 
   }
   // Time is ambiguous
   else
   {
      DateTime utcTime = DateTime.SpecifyKind(ambiguousTime - TimeZoneInfo.Local.BaseUtcOffset, 
                                              DateTimeKind.Utc);      
      Console.WriteLine("{0} local time corresponds to {1} {2}.", 
                        ambiguousTime, utcTime, utcTime.Kind.ToString());
      return utcTime;            
   }   
}
```

```vb
Private Function ResolveAmbiguousTime(ambiguousTime As Date) As Date
   ' Time is not ambiguous
   If Not TimeZoneInfo.Local.IsAmbiguousTime(ambiguousTime) Then 
      Return TimeZoneInfo.ConvertTimeToUtc(ambiguousTime) 
   ' Time is ambiguous
   Else
      Dim utcTime As Date = DateTime.SpecifyKind(ambiguousTime - TimeZoneInfo.Local.BaseUtcOffset, DateTimeKind.Utc)      
      Console.WriteLine("{0} local time corresponds to {1} {2}.", ambiguousTime, utcTime, utcTime.Kind.ToString())
      Return utcTime            
   End If   
End Function
```

L'esempio è costituito da un metodo denominato `ResolveAmbiguousTime` che determina se il valore [DateTime](xref:System.DateTime) passato è ambiguo. Se il valore è ambiguo, il metodo restituisce un valore [DateTime](xref:System.DateTime) che rappresenta l'ora UTC corrispondente. Il metodo gestisce questa conversione sottraendo il valore della proprietà [BaseUtcOffset](xref:System.TimeZoneInfo.BaseUtcOffset) del fuso orario locale dall'ora locale. 

In genere, un'ora ambigua viene gestita chiamando il metodo [GetAmbiguousTimeOffsets](xref:System.TimeZoneInfo.GetAmbiguousTimeOffsets(System.DateTime)) per recuperare una matrice di oggetti [TimeSpan](xref:System.TimeSpan) contenenti i possibili offset dall'ora UTC dell'ora ambigua. Tuttavia, in questo esempio si presuppone che un'ora ambigua deve sempre essere mappata all'ora solare del fuso orario. La proprietà [BaseUtcOffset](xref:System.TimeZoneInfo.BaseUtcOffset) restituisce l'offset tra l'ora UTC e l'ora solare di un fuso orario.

## <a name="see-also"></a>Vedere anche

[Date, ore e fusi orari](index.md)

[Procedura: Consentire agli utenti di risolvere orari ambigui](let-users-resolve-ambiguous-times.md)




<!--HONumber=Nov16_HO3-->


