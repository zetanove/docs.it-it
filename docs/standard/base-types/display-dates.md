---
title: 'Procedura: Visualizzare le date in calendari non gregoriani'
description: Come visualizzare le date in calendari non gregoriani
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 93f06e1d-544b-4ccc-a0b2-95cd674852cb
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 85c9d450be48c553ea3a1f1a0f16c298941fa325

---

# <a name="how-to-display-dates-in-nongregorian-calendars"></a>Procedura: Visualizzare le date in calendari non gregoriani

I tipi [DateTime](xref:System.DateTime) e [DateTimeOffset](xref:System.DateTimeOffset) usano il calendario gregoriano come calendario predefinito. Ciò significa che la chiamata al metodo `ToString` di un valore di data e ora visualizza la rappresentazione di stringa di tale data e ora nel calendario gregoriano, anche se la data e l'ora sono state create usando un altro calendario. Questo processo è illustrato nell'esempio seguente in cui vengono usati due metodi diversi per creare un valore di data e ora con il calendario persiano ma i valori vengono visualizzati nel calendario gregoriano quando viene chiamato il metodo [ToString](xref:System.DateTime.ToString). L'esempio riflette due tecniche comuni ma non corrette per la visualizzazione della data in un determinato calendario.

```csharp
PersianCalendar persianCal = new PersianCalendar();

DateTime persianDate = persianCal.ToDateTime(1387, 3, 18, 12, 0, 0, 0);
Console.WriteLine(persianDate.ToString());

persianDate = new DateTime(1387, 3, 18, persianCal);
Console.WriteLine(persianDate.ToString());
// The example displays the following output to the console:
//       6/7/2008 12:00:00 PM
//       6/7/2008 12:00:00 AM
```

```vb
Dim persianCal As New PersianCalendar()

Dim persianDate As Date = persianCal.ToDateTime(1387, 3, 18, _
                                                12, 0, 0, 0)
Console.WriteLine(persianDate.ToString())

persianDate = New DateTime(1387, 3, 18, persianCal)
Console.WriteLine(persianDate.ToString())
' The example displays the following output to the console:
'       6/7/2008 12:00:00 PM
'       6/7/2008 12:00:00 AM
```

Per visualizzare la data in un determinato calendario è possibile usare due tecniche differenti. La prima richiede che il calendario sia il calendario predefinito per determinate impostazioni cultura. La seconda può essere usata con qualsiasi calendario.

## <a name="to-display-the-date-for-a-cultures-default-calendar"></a>Per visualizzare la data per il calendario predefinito di determinate impostazione cultura

1. Creare un'istanza di un oggetto calendario derivato dalla classe [Calendar](xref:System.Globalization.Calendar) che rappresenta il calendario da usare.

2. Creare un'istanza di un oggetto [CultureInfo](xref:System.Globalization.CultureInfo) che rappresenta le impostazioni cultura la cui formattazione verrà usata per la visualizzazione della data.

3. Chiamare il metodo [Array.Exists&lt;T&gt;](xref:System.Array.Exists``1(``0[],System.Predicate{``0})) per determinare se l'oggetto calendario è un membro della matrice restituita dalla proprietà [CultureInfo.OptionalCalendars](xref:System.Globalization.CultureInfo.OptionalCalendars). Ciò indica che il calendario può svolgere la funzione di calendario predefinito per l'oggetto [CultureInfo](xref:System.Globalization.CultureInfo). Se non è un membro della matrice, seguire le istruzioni riportate nella sezione "Per visualizzare la data in qualsiasi calendario".

4. Assegnare l'oggetto calendario alla proprietà [Calendar](xref:System.Globalization.DateTimeFormatInfo.Calendar) dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) restituito dalla proprietà [CultureInfo.DateTimeFormat](xref:System.Globalization.CultureInfo.DateTimeFormat).

  > [!NOTE]
  > La classe [CultureInfo](xref:System.Globalization.CultureInfo) ha anche una proprietà [Calendar](xref:System.Globalization.CultureInfo.Calendar). È tuttavia costante e di sola lettura e non viene modificata per riflettere il nuovo calendario predefinito assegnato alla proprietà [DateTimeFormatInfo.Calendar](xref:System.Globalization.DateTimeFormatInfo.Calendar).
  
5. Chiamare il metodo [DateTime.ToString(IFormatProvider)](xref:System.DateTime.ToString(System.IFormatProvider)) o [DateTime.ToString(String,IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) e passare l'oggetto [CultureInfo](xref:System.Globalization.CultureInfo) il cui calendario predefinito è stato modificato nel passaggio precedente.

## <a name="to-display-the-date-in-any-calendar"></a>Per visualizzare la data in qualsiasi calendario

1. Creare un'istanza di un oggetto calendario derivato dalla classe [Calendar](xref:System.Globalization.Calendar) che rappresenta il calendario da usare.

2. Determinare gli elementi di data e ora da visualizzare nella rappresentazione di stringa del valore di data e ora.

3. Per ogni elemento di data e ora da visualizzare, chiamare il metodo `Get…` dell'oggetto calendario. Sono disponibili i metodi seguenti:

    * [GetYear](xref:System.Globalization.Calendar.GetYear(System.DateTime)), per visualizzate l'anno nel calendario appropriato.
    
    * [GetMonth](xref:System.Globalization.Calendar.GetMonth(System.DateTime)), per visualizzate il mese nel calendario appropriato. 
    
    * [GetDayOfMonth](xref:System.Globalization.Calendar.GetDayOfMonth(System.DateTime)), per visualizzate il numero del giorno del mese nel calendario appropriato.
    
    * [GetHour](xref:System.Globalization.Calendar.GetHour(System.DateTime)), per visualizzate l'ora del giorno nel calendario appropriato.
    
    * [GetMinute](xref:System.Globalization.Calendar.GetMinute(System.DateTime)), per visualizzate i minuti dell'ora nel calendario appropriato.
    
    * [GetSecond](xref:System.Globalization.Calendar.GetSecond(System.DateTime)), per visualizzate i secondi del minuto nel calendario appropriato. 
    
    * [GetMilliseconds](xref:System.Globalization.Calendar.GetMilliseconds(System.DateTime)), per visualizzate i millisecondi del secondo nel calendario appropriato.
    
## <a name="example"></a>Esempio
    
L'esempio visualizza una data usando due calendari diversi. La data viene visualizzata dopo aver definito il calendario Hijri come calendario predefinito per le impostazioni cultura ar-JO e usando il calendario persiano che non è supportato come calendario facoltativo nelle impostazioni cultura fa-IR.

```csharp
using System;
using System.Globalization;

public class CalendarDates
{
   public static void Main()
   {
      HijriCalendar hijriCal = new HijriCalendar();
      CalendarUtility hijriUtil = new CalendarUtility(hijriCal);
      DateTime dateValue1 = new DateTime(1429, 6, 29, hijriCal);
      DateTimeOffset dateValue2 = new DateTimeOffset(dateValue1, 
                                  TimeZoneInfo.Local.GetUtcOffset(dateValue1));
      CultureInfo jc = CultureInfo.CreateSpecificCulture("ar-JO");

      // Display the date using the Gregorian calendar.
      Console.WriteLine("Using the system default culture: {0}", 
                        dateValue1.ToString("d"));
      // Display the date using the ar-JO culture's original default calendar.
      Console.WriteLine("Using the ar-JO culture's original default calendar: {0}", 
                        dateValue1.ToString("d", jc));
      // Display the date using the Hijri calendar.
      Console.WriteLine("Using the ar-JO culture with Hijri as the default calendar:");
      // Display a Date value.
      Console.WriteLine(hijriUtil.DisplayDate(dateValue1, jc));
      // Display a DateTimeOffset value.
      Console.WriteLine(hijriUtil.DisplayDate(dateValue2, jc));

      Console.WriteLine();

      PersianCalendar persianCal = new PersianCalendar();
      CalendarUtility persianUtil = new CalendarUtility(persianCal);
      CultureInfo ic = CultureInfo.CreateSpecificCulture("fa-IR");

      // Display the date using the ir-FA culture's default calendar.
      Console.WriteLine("Using the ir-FA culture's default calendar: {0}",       
                        dateValue1.ToString("d", ic));
      // Display a Date value.
      Console.WriteLine(persianUtil.DisplayDate(dateValue1, ic));
      // Display a DateTimeOffset value.
      Console.WriteLine(persianUtil.DisplayDate(dateValue2, ic));
   }
}

public class CalendarUtility
{
   private Calendar thisCalendar;
   private CultureInfo targetCulture;

   public CalendarUtility(Calendar cal)
   {
      this.thisCalendar = cal;
   }

   private bool CalendarExists(CultureInfo culture)
   {
      this.targetCulture = culture;
      return Array.Exists(this.targetCulture.OptionalCalendars, 
                          this.HasSameName);
   }

   private bool HasSameName(Calendar cal)
   {
      if (cal.ToString() == thisCalendar.ToString())
         return true;
      else
         return false;
   }

   public string DisplayDate(DateTime dateToDisplay, CultureInfo culture)
   {
      DateTimeOffset displayOffsetDate = dateToDisplay;
      return DisplayDate(displayOffsetDate, culture);
   }

   public string DisplayDate(DateTimeOffset dateToDisplay, 
                             CultureInfo culture)
   {
      string specifier = "yyyy/MM/dd";

      if (this.CalendarExists(culture))
      {
         Console.WriteLine("Displaying date in supported {0} calendar...", 
                           this.thisCalendar.GetType().Name);
         culture.DateTimeFormat.Calendar = this.thisCalendar;
         return dateToDisplay.ToString(specifier, culture);
      }
      else
      {
         Console.WriteLine("Displaying date in unsupported {0} calendar...", 
                           thisCalendar.GetType().Name);

         string separator = targetCulture.DateTimeFormat.DateSeparator;

         return thisCalendar.GetYear(dateToDisplay.DateTime).ToString("0000") +
                separator +
                thisCalendar.GetMonth(dateToDisplay.DateTime).ToString("00") + 
                separator +
                thisCalendar.GetDayOfMonth(dateToDisplay.DateTime).ToString("00"); 
      }
   } 
}
// The example displays the following output to the console:
//       Using the system default culture: 7/3/2008
//       Using the ar-JO culture's original default calendar: 03/07/2008
//       Using the ar-JO culture with Hijri as the default calendar:
//       Displaying date in supported HijriCalendar calendar...
//       1429/06/29
//       Displaying date in supported HijriCalendar calendar...
//       1429/06/29
//       
//       Using the ir-FA culture's default calendar: 7/3/2008
//       Displaying date in unsupported PersianCalendar calendar...
//       1387/04/13
//       Displaying date in unsupported PersianCalendar calendar...
//       1387/04/13
```

```vb
Imports System.Globalization

Public Class CalendarDates
   Public Shared Sub Main()
      Dim hijriCal As New HijriCalendar()
      Dim hijriUtil As New CalendarUtility(hijriCal)
      Dim dateValue1 As Date = New Date(1429, 6, 29, hijriCal)
      Dim dateValue2 As DateTimeOffset = New DateTimeOffset(dateValue1, _
                                         TimeZoneInfo.Local.GetUtcOffset(dateValue1))
      Dim jc As CultureInfo = CultureInfo.CreateSpecificCulture("ar-JO")

      ' Display the date using the Gregorian calendar.
      Console.WriteLine("Using the system default culture: {0}", _
                        dateValue1.ToString("d"))
      ' Display the date using the ar-JO culture's original default calendar.
      Console.WriteLine("Using the ar-JO culture's original default calendar: {0}", _
                        dateValue1.ToString("d", jc))
      ' Display the date using the Hijri calendar.
      Console.WriteLine("Using the ar-JO culture with Hijri as the default calendar:")
      ' Display a Date value.
      Console.WriteLine(hijriUtil.DisplayDate(dateValue1, jc))
      ' Display a DateTimeOffset value.
      Console.WriteLine(hijriUtil.DisplayDate(dateValue2, jc))

      Console.WriteLine()

      Dim persianCal As New PersianCalendar()
      Dim persianUtil As New CalendarUtility(persianCal)
      Dim ic As CultureInfo = CultureInfo.CreateSpecificCulture("fa-IR")

      ' Display the date using the ir-FA culture's default calendar.
      Console.WriteLine("Using the ir-FA culture's default calendar: {0}", _      
                        dateValue1.ToString("d", ic))
      ' Display a Date value.
      Console.WriteLine(persianUtil.DisplayDate(dateValue1, ic))
      ' Display a DateTimeOffset value.
      Console.WriteLine(persianUtil.DisplayDate(dateValue2, ic))
   End Sub
End Class

Public Class CalendarUtility
   Private thisCalendar As Calendar
   Private targetCulture As CultureInfo

   Public Sub New(cal As Calendar)
      Me.thisCalendar = cal
   End Sub

   Private Function CalendarExists(culture As CultureInfo) As Boolean
      Me.targetCulture = culture
      Return Array.Exists(Me.targetCulture.OptionalCalendars, _
                          AddressOf Me.HasSameName)
   End Function 

   Private Function HasSameName(cal As Calendar) As Boolean
      If cal.ToString() = thisCalendar.ToString() Then
         Return True
      Else
         Return False
      End If
   End Function

   Public Function DisplayDate(dateToDisplay As Date, _
                               culture As CultureInfo) As String
      Dim displayOffsetDate As DateTimeOffset = dateToDisplay
      Return DisplayDate(displayOffsetDate, culture)
   End Function

   Public Function DisplayDate(dateToDisplay As DateTimeOffset, _
                               culture As CultureInfo) As String
      Dim specifier As String = "yyyy/MM/dd"

      If Me.CalendarExists(culture) Then
         Console.WriteLine("Displaying date in supported {0} calendar...", _
                           thisCalendar.GetType().Name)
         culture.DateTimeFormat.Calendar = Me.thisCalendar
         Return dateToDisplay.ToString(specifier, culture)
      Else
         Console.WriteLine("Displaying date in unsupported {0} calendar...", _
                           thisCalendar.GetType().Name)

         Dim separator As String = targetCulture.DateTimeFormat.DateSeparator

         Return thisCalendar.GetYear(dateToDisplay.DateTime).ToString("0000") & separator & _
                thisCalendar.GetMonth(dateToDisplay.DateTime).ToString("00") & separator & _
                thisCalendar.GetDayOfMonth(dateToDisplay.DateTime).ToString("00") 
      End If             
   End Function
End Class
' The example displays the following output to the console:
'       Using the system default culture: 7/3/2008
'       Using the ar-JO culture's original default calendar: 03/07/2008
'       Using the ar-JO culture with Hijri as the default calendar:
'       Displaying date in supported HijriCalendar calendar...
'       1429/06/29
'       Displaying date in supported HijriCalendar calendar...
'       1429/06/29
'       
'       Using the ir-FA culture's default calendar: 7/3/2008
'       Displaying date in unsupported PersianCalendar calendar...
'       1387/04/13
'       Displaying date in unsupported PersianCalendar calendar...
'       1387/04/13
```

Ogni oggetto [CultureInfo](xref:System.Globalization.CultureInfo) può supportare uno o più calendari, indicati dalla proprietà [OptionalCalendars](xref:System.Globalization.CultureInfo.OptionalCalendars). Uno di questi è designato come calendario predefinito delle impostazioni cultura e viene restituito dalla proprietà di sola lettura [CultureInfo.Calendar](xref:System.Globalization.CultureInfo.Calendar). È possibile designare come impostazione predefinita un altro calendario facoltativo assegnando un oggetto [Calendar](xref:System.Globalization.Calendar) che rappresenta il calendario alla proprietà [DateTimeFormatInfo.Calendar](xref:System.Globalization.DateTimeFormatInfo.Calendar) restituita dalla proprietà [CultureInfo.DateTimeFormat](xref:System.Globalization.CultureInfo.DateTimeFormat). Alcuni calendari, tuttavia, ad esempio quello persiano rappresentato dalla classe [PersianCalendar](xref:System.Globalization.PersianCalendar), non svolgono la funzione di calendari facoltativi per tutte le impostazioni cultura.   

Nell'esempio viene definita la classe dell'utilità di calendario riutilizzabile `CalendarUtility` per gestire molti dei dettagli relativi alla generazione della rappresentazione di stringa di una data mediante un determinato calendario. La classe `CalendarUtility` ha i seguenti membri: 

* Un costruttore con parametri il cui solo parametro è un oggetto [Calendar](xref:System.Globalization.Calendar) nel quale deve essere rappresentata una data. Viene assegnato a un campo privato della classe.

* ,`CalendarExists` un metodo privato che restituisce un valore booleano che indica se il calendario rappresentato dall'oggetto `CalendarUtility` è supportato dall'oggetto [CultureInfo](xref:System.Globalization.CultureInfo) passato al metodo come parametro. Il metodo esegue il wrapping di una chiamata al metodo [Array.Exists&lt;T&gt;](xref:System.Array.Exists``1(``0[],System.Predicate{``0})) al quale passa la matrice [CultureInfo.OptionalCalendars](xref:System.Globalization.CultureInfo.OptionalCalendars).

* `HasSameName`, un metodo privato assegnato al delegato [Predicate&lt;T&gt;](xref:System.Predicate%601) che viene passato come parametro al metodo [Array.Exists&lt;T&gt;](xref:System.Array.Exists``1(``0[],System.Predicate{``0})). Ogni membro della matrice viene passato al metodo finché quest'ultimo non restituisce `true`. Il metodo determina se il nome di un calendario facoltativo è identico a quello del calendario rappresentato dall'oggetto `CalendarUtility`.

* `DisplayDate`, un metodo pubblico di overload al quale vengono passati due parametri, ovvero un valore [DateTime](xref:System.DateTime) o [DateTimeOffset](xref:System.DateTimeOffset) da esprimere nel calendario rappresentato dall'oggetto `CalendarUtility` e le impostazioni cultura di cui usare le regole di formattazione. Il comportamento nella restituzione della rappresentazione di stringa di una data varia a seconda che il calendario di destinazione sia supportato dalle impostazioni cultura le cui regole di formattazione devono essere usate.

Indipendentemente dal calendario usato per creare un valore [DateTime](xref:System.DateTime) o [DateTimeOffset](xref:System.DateTimeOffset) in questo esempio, il valore viene in genere espresso in formato gregoriano. in quanto i tipi [DateTime](xref:System.DateTime) e [DateTimeOffset](xref:System.DateTimeOffset) non mantengono le informazioni del calendario. Internamente vengono rappresentati come numero di cicli trascorsi dopo la mezzanotte del 1 gennaio 0001. L'interpretazione del numero dipende dal calendario. Per la maggior parte delle impostazioni cultura, il calendario predefinito è il calendario gregoriano. 

## <a name="see-also"></a>Vedere anche

[Esecuzione di operazioni di formattazione](performing-formatting-operations.md)



<!--HONumber=Nov16_HO3-->


