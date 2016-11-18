---
title: 'Procedura: Definire e usare provider di formati numerici personalizzati'
description: Come definire e usare provider di formati numerici personalizzati
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 9b184114-6612-4c1a-a2db-2e24e65b0f77
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: bb62bdd03d4af4f764ac3bc8734c67902fffa798

---

# <a name="how-to-define-and-use-custom-numeric-format-providers"></a>Procedura: Definire e usare provider di formati numerici personalizzati

.NET Framework offre un ampio controllo sulla rappresentazione di stringa dei valori numerici e supporta le funzionalità seguenti per la personalizzazione del formato di tali valori:

* Stringhe in formato numerico standard, che forniscono un insieme predefinito di formati per la conversione dei numeri nella rispettiva rappresentazione di stringa. È possibile usarle con qualsiasi metodo di formattazione numerica, ad esempio [Decimal.ToString(String](xref:System.Decimal.ToString(System.String)), che include un parametro format. Per informazioni dettagliate, vedere [Stringhe di formato numerico standard](standard-numeric.md).

* Stringhe in formato numerico personalizzato che forniscono un insieme di simboli che possono essere combinati per definire identificatori di formato numerico personalizzato. È anche possibile usarle con qualsiasi metodo di formattazione numerica, ad esempio [Decimal.ToString(String](xref:System.Decimal.ToString(System.String)), che include un parametro format. Per informazioni dettagliate, vedere [Stringhe in formato numerico personalizzato](custom-numeric.md).

* Oggetti [CultureInfo](xref:System.Globalization.CultureInfo) o [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo), che definiscono i simboli e i modelli di formato usati per la visualizzazione delle rappresentazioni di stringa di valori numerici. È possibile usarle con qualsiasi metodo di formattazione numerica, ad esempio [ToString](xref:System.Int32.ToString(System.IFormatProvider)), che include un parametro *provider*. In genere, il parametro *provider* viene usato per specificare informazioni di formattazione specifiche delle impostazioni cultura.

In alcuni casi, ad esempio quando un'applicazione deve visualizzare un numero di account formattato, un numero di identificazione o un codice postale, queste tre tecniche non sono adatte. .NET consente anche di definire un oggetto di formattazione diverso sia da [CultureInfo](xref:System.Globalization.CultureInfo) che da [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) per determinare la modalità di formattazione di un valore numerico. In questo argomento sono contenute istruzioni dettagliate per l'implementazione di tale oggetto ed è anche riportato un esempio di formattazione di numeri di telefono.

## <a name="to-define-a-custom-format-provider"></a>Per definire un provider di formato personalizzato

1. Definire una classe che implementa le interfacce [IFormatProvider](xref:System.IFormatProvider) e [ICustomFormatter](xref:System.ICustomFormatter). 

2. Implementare il metodo [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)). [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) è un metodo di callback chiamato dal metodo di formattazione (ad esempio dal metodo [String.Format(IFormatProvider,String,Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object))) per recuperare l'oggetto responsabile della formattazione personalizzata. Un'implementazione tipica di [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) effettua le operazioni seguenti:

    a. Determina se l'oggetto [Type](xref:System.Type) passato come parametro di metodo rappresenta un'interfaccia [ICustomFormatter](xref:System.ICustomFormatter).
    
    b. Se il parametro rappresenta l'interfaccia [ICustomFormatter](xref:System.ICustomFormatter), [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) restituisce un oggetto che implementa l'interfaccia [ICustomFormatter](xref:System.ICustomFormatter) responsabile della formattazione personalizzata. In genere, l'oggetto di formattazione personalizzata restituisce se stesso. 
    
    c. Se il parametro non rappresenta l'interfaccia [ICustomFormatter](xref:System.ICustomFormatter), [GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) restituisce `null`.
    
3. Implementare il metodo [ICustomFormatter.Format](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)). Questo metodo, chiamato dal metodo [String.Format(IFormatProvider,String,Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)), è responsabile della restituzione della rappresentazione di stringa di un numero. L'implementazione del metodo in genere implica le attività seguenti:

    a. Facoltativamente, esaminare il parametro *provider* per assicurarsi che il metodo sia correttamente destinato a fornire servizi di formattazione. Per la formattazione degli oggetti che implementano entrambi i metodi [IFormatProvider](xref:System.IFormatProvider) e [ICustomFormatter](xref:System.ICustomFormatter), questa operazione richiede il test del parametro *provider* per verificarne l'uguaglianza con l'oggetto di formattazione corrente.
    
    b. Stabilire se l'oggetto di formattazione deve supportare identificatori di formato personalizzato. Ad esempio, un identificatore di formato "N" potrebbe indicare che un numero di telefono degli Stati Uniti deve essere restituito in formato NANP e un identificatore di formato "I" potrebbe indicare l'output in formato ITU-T Recommendation E.123. Se si usano identificatori di formato, il metodo deve gestire l'identificatore di formato specifico. Quest'ultimo viene passato al metodo nel parametro. Se non è disponibile alcun identificatore, il valore del parametro *format* è [String.Empty](xref:System.String#System_String_Empty).
    
    c. Recuperare il valore numerico passato al metodo come parametro *arg*. Eseguire le eventuali modifiche necessarie per convertirlo nella relativa rappresentazione di stringa.
    
    d. Restituire la rappresentazione di stringa del parametro *arg*.
    
## <a name="to-use-a-custom-numeric-formatting-object"></a>Per usare un oggetto di formattazione numerica personalizzata

1. Creare una nuova istanza della classe di formattazione personalizzata.

2. Chiamare il metodo di formattazione [String.Format(IFormatProvider,String,Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) passando l'oggetto di formattazione personalizzata, l'identificatore di formattazione (o [String.Empty](xref:System.String.Empty) se non viene usato alcun identificatore) e il valore numerico da formattare. 

## <a name="example"></a>Esempio

Nell'esempio seguente viene definito un provider di formato numerico personalizzato denominato `TelephoneFormatter` che converte un numero che rappresenta un numero telefonico degli Stati Uniti nel suo formato NANP oppure E.123. Il metodo gestisce due identificatori di formato, "N" (che restituisce il formato NANP) e "I" (che restituisce il formato E.123 internazionale).

```csharp
using System;
using System.Globalization;

public class TelephoneFormatter : IFormatProvider, ICustomFormatter
{
   public object GetFormat(Type formatType)
   {
      if (formatType == typeof(ICustomFormatter))
         return this;
      else
         return null;
   }               

   public string Format(string format, object arg, IFormatProvider formatProvider)
   {
      // Check whether this is an appropriate callback             
      if (! this.Equals(formatProvider))
         return null; 

      // Set default format specifier             
      if (string.IsNullOrEmpty(format)) 
         format = "N";

      string numericString = arg.ToString();

      if (format == "N")
      {
         if (numericString.Length <= 4)
            return numericString;
         else if (numericString.Length == 7)
            return numericString.Substring(0, 3) + "-" + numericString.Substring(3, 4); 
         else if (numericString.Length == 10)
               return "(" + numericString.Substring(0, 3) + ") " +
                      numericString.Substring(3, 3) + "-" + numericString.Substring(6);   
         else
            throw new FormatException( 
                      string.Format("'{0}' cannot be used to format {1}.", 
                                    format, arg.ToString()));
      }
      else if (format == "I")
      {
         if (numericString.Length < 10)
            throw new FormatException(string.Format("{0} does not have 10 digits.", arg.ToString()));
         else
            numericString = "+1 " + numericString.Substring(0, 3) + " " + numericString.Substring(3, 3) + " " + numericString.Substring(6);
      }
      else
      {
         throw new FormatException(string.Format("The {0} format specifier is invalid.", format));
      } 
      return numericString;  
   }
}

public class TestTelephoneFormatter
{
   public static void Main()
   {
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0}", 0));
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0}", 911));
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0}", 8490216));
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0}", 4257884748));

      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0:N}", 0));
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0:N}", 911));
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0:N}", 8490216));
      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0:N}", 4257884748));

      Console.WriteLine(String.Format(new TelephoneFormatter(), "{0:I}", 4257884748));
   }
}
```

```vb
Public Class TelephoneFormatter : Implements IFormatProvider, ICustomFormatter
   Public Function GetFormat(formatType As Type) As Object _
                   Implements IFormatProvider.GetFormat
      If formatType Is GetType(ICustomFormatter) Then
         Return Me
      Else
         Return Nothing
      End If               
   End Function               

   Public Function Format(fmt As String, arg As Object, _
                          formatProvider As IFormatProvider) As String _
                   Implements ICustomFormatter.Format
      ' Check whether this is an appropriate callback             
      If Not Me.Equals(formatProvider) Then Return Nothing 

      ' Set default format specifier             
      If String.IsNullOrEmpty(fmt) Then fmt = "N"

      Dim numericString As String = arg.ToString

      If fmt = "N" Then
         Select Case numericString.Length
            Case <= 4 
               Return numericString
            Case 7
               Return Left(numericString, 3) & "-" & Mid(numericString, 4) 
            Case 10
               Return "(" & Left(numericString, 3) & ") " & _
                      Mid(numericString, 4, 3) & "-" & Mid(numericString, 7)   
            Case Else
               Throw New FormatException( _
                         String.Format("'{0}' cannot be used to format {1}.", _
                                       fmt, arg.ToString()))
         End Select
      ElseIf fmt = "I" Then
         If numericString.Length < 10 Then
            Throw New FormatException(String.Format("{0} does not have 10 digits.", arg.ToString()))
         Else
            numericString = "+1 " & Left(numericString, 3) & " " & Mid(numericString, 4, 3) & " " & Mid(numericString, 7)
         End If      
      Else
         Throw New FormatException(String.Format("The {0} format specifier is invalid.", fmt))
      End If 
      Return numericString  
   End Function
End Class

Public Module TestTelephoneFormatter
   Public Sub Main
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0}", 0))
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0}", 911))
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0}", 8490216))
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0}", 4257884748))

      Console.WriteLine(String.Format(New TelephoneFormatter, "{0:N}", 0))
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0:N}", 911))
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0:N}", 8490216))
      Console.WriteLine(String.Format(New TelephoneFormatter, "{0:N}", 4257884748))

      Console.WriteLine(String.Format(New TelephoneFormatter, "{0:I}", 4257884748))
   End Sub
End Module
```

Il provider di formato numerico personalizzato può essere usato solo con il metodo [String.Format(IFormatProvider,String,Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)). Gli altri overload dei metodi di formattazione numerica (ad esempio `ToString`) che hanno un parametro di tipo [IFormatProvider](xref:System.IFormatProvider) passano all'implementazione [IFormatProvider.GetFormat](xref:System.IFormatProvider.GetFormat(System.Type)) un oggetto [Type](xref:System.Type) che rappresenta il tipo [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo). In cambio si aspettano che il metodo restituisca un oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo). Se ciò non avviene, il provider di formato numerico personalizzato viene ignorato e al suo posto viene usato l'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) relativo alle impostazioni cultura correnti. Nell'esempio il metodo `TelephoneFormatter.GetFormat` gestisce la possibilità che possa essere passato erroneamente a un metodo di formattazione numerica esaminando il parametro del metodo e restituendo *null* se rappresenta un tipo diverso da [ICustomFormatter](xref:System.ICustomFormatter).

Se un provider di formato numerico personalizzato supporta un set di identificatori di formato, assicurarsi di specificare un comportamento predefinito nel caso in cui non venga fornito alcun identificatore di formato nell'elemento di formato usato nella chiamata al metodo [String.Format(IFormatProvider,String,Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)). Nell'esempio "N" è l'identificatore di formato predefinito. È pertanto possibile convertire un numero in un numero di telefono formattato specificando un identificatore di formato esplicito. Nell'esempio riportato di seguito viene illustrata questa chiamata al metodo.

```csharp
Console.WriteLine(String.Format(new TelephoneFormatter(), "{0:N}", 4257884748));
```

```vb
Console.WriteLine(String.Format(New TelephoneFormatter, "{0:N}", 4257884748))
```

L'esecuzione della conversione è possibile anche in assenza di identificatori di formato. Nell'esempio riportato di seguito viene illustrata questa chiamata al metodo.

```csharp
Console.WriteLine(String.Format(new TelephoneFormatter(), "{0}", 4257884748));
```

```vb
Console.WriteLine(String.Format(New TelephoneFormatter, "{0}", 4257884748))
```

Se non è definito alcun identificatore di formato predefinito, l'implementazione del metodo [ICustomFormatter](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)) deve includere elementi di codice come quelli riportati di seguito in modo da consentire a .NET di fornire la formattazione non supportata dal proprio codice.

```csharp
if (arg is IFormattable) 
   s = ((IFormattable)arg).ToString(format, formatProvider);
else if (arg != null)    
   s = arg.ToString();
```

```vb
If TypeOf(arg) Is IFormattable Then 
   s = DirectCast(arg, IFormattable).ToString(fmt, formatProvider)
ElseIf arg IsNot Nothing Then    
   s = arg.ToString()
End If
```

In questo esempio il metodo che implementa [ICustomFormatter](xref:System.ICustomFormatter.Format(System.String,System.Object,System.IFormatProvider)) è destinato a essere usato come metodo di callback per il metodo [String.Format(IFormatProvider,String,Object[])](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)). Tale metodo esamina dunque il parametro *formatProvider* per determinare se contiene un riferimento all'oggetto `TelephoneFormatter` corrente. Il metodo può tuttavia essere chiamato anche direttamente dal codice. In questo caso è possibile usare il parametro *formatProvider *per specificare un oggetto [CultureInfo](xref:System.Globalization.CultureInfo) o [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) che fornisce informazioni di formattazione specifiche delle impostazioni cultura.

## <a name="see-also"></a>Vedere anche

[Esecuzione di operazioni di formattazione](performing-formatting-operations.md)



<!--HONumber=Nov16_HO3-->


