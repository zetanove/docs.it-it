---
title: Uso di oggetti che implementano IDisposable
description: Uso di oggetti che implementano IDisposable
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 08/19/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: df780a6e-734e-44b8-9747-9f7783f79e20
translationtype: Human Translation
ms.sourcegitcommit: 213ce098bcc2b5e31c55e759d895254d5ca33caa
ms.openlocfilehash: 51655742b8975c84eae3f58c4ef0f7381a0bed6b

---

# <a name="using-objects-that-implement-idisposable"></a>Uso di oggetti che implementano IDisposable

Garbage Collector di Common Language Runtime si occupa di recuperare la memoria usata da oggetti non gestiti. I tipi che usano risorse non gestite implementano invece l'interfaccia [IDisposable](xref:System.IDisposable) con la quale recuperare la memoria non gestita. Dopo avere usato un oggetto che implementa [IDisposable](xref:System.IDisposable), è consigliabile chiamare l'implementazione [IDisposable.Dispose](xref:System.IDisposable.Dispose) dell'oggetto. Questa operazione può essere eseguita in due modi:

* Con l'istruzione `using` in C# o l'istruzione `Using` in Visual Basic.

* Implementando un blocco `try/finally`. 

## <a name="the-using-statement"></a>Istruzione using

L'istruzione `using` in C# e l'istruzione `Using` in Visual Basic semplificano il codice da scrivere per creare e pulire un oggetto. L'istruzione `using` ottiene una o più risorse, esegue le istruzioni specificate ed elimina l'oggetto in modo automatico. L'istruzione `using` è comunque utile solo per gli oggetti usati nell'ambito del metodo in cui vengono costruiti. 

L'esempio seguente impiega l'istruzione `using` per creare e rilasciare un oggetto [System.IO.StreamReader](xref:System.IO.StreamReader).

```cs
using System;
using System.IO;

public class Example
{
   public static void Main()
   {
      Char[] buffer = new Char[50];
      using (StreamReader s = new StreamReader("File1.txt")) {
         int charsRead = 0;
         while (s.Peek() != -1) {
            charsRead = s.Read(buffer, 0, buffer.Length);
            //
            // Process characters read.
            //   
         }
         s.Close();    
      }

   }
}
```

```vb
Imports System.IO

Module Example
   Public Sub Main()
      Dim buffer(49) As Char
      Using s As New StreamReader("File1.txt")
         Dim charsRead As Integer
         Do While s.Peek() <> -1
            charsRead = s.Read(buffer, 0, buffer.Length)         
            ' 
            ' Process characters read.
            '
         Loop
         s.Close()
      End Using
   End Sub
End Module
```

Si noti che, anche se la classe [StreamReader](xref:System.IO.StreamReader) implementa l'interfaccia [IDisposable](xref:System.IDisposable), a indicare che usa una risorsa non gestita, nell'esempio non viene chiamato il metodo [StreamReader.Dispose](xref:System.IO.StreamReader.Dispose(System.Boolean)) in modo esplicito. Quando nel compilatore C# o Visual Basic viene rilevata l'istruzione `using`, viene generato il linguaggio intermedio (IL) equivalente al codice seguente, che contiene un blocco `try/finally` in modo esplicito. 

```cs
using System;
using System.IO;

public class Example
{
   public static void Main()
   {
      Char[] buffer = new Char[50];
      {
         StreamReader s = new StreamReader("File1.txt"); 
         try {
            int charsRead = 0;
            while (s.Peek() != -1) {
               charsRead = s.Read(buffer, 0, buffer.Length);
               //
               // Process characters read.
               //   
            }
            s.Close();
         }
         finally {
            if (s != null)
               ((IDisposable)s).Dispose();     
         }       
      }
   }
}
```

```vb
Imports System.IO

Module Example
   Public Sub Main()
      Dim buffer(49) As Char
''      Dim s As New StreamReader("File1.txt")
With s As New StreamReader("File1.txt")
      Try
         Dim charsRead As Integer
         Do While s.Peek() <> -1
            charsRead = s.Read(buffer, 0, buffer.Length)         
            ' 
            ' Process characters read.
            '
         Loop
         s.Close()
      Finally
         If s IsNot Nothing Then DirectCast(s, IDisposable).Dispose()
      End Try
End With
   End Sub
End Module
```

L'istruzione `using` C# è consente anche di acquisire più risorse in un'unica istruzione, che equivale internamente all'uso di più istruzioni "using" annidate. Nell'esempio seguente viene creata l'istanza di due oggetti [StreamReader](xref:System.IO.StreamReader) per leggere il contenuto di due file diversi. 

```cs
using System;
using System.IO;

public class Example
{
   public static void Main()
   {
      Char[] buffer1 = new Char[50], buffer2 = new Char[50];

      using (StreamReader version1 = new StreamReader("file1.txt"),
                          version2 = new StreamReader("file2.txt")) {
         int charsRead1, charsRead2 = 0;
         while (version1.Peek() != -1 && version2.Peek() != -1) {
            charsRead1 = version1.Read(buffer1, 0, buffer1.Length);
            charsRead2 = version2.Read(buffer2, 0, buffer2.Length);
            //
            // Process characters read.
            //
         }
         version1.Close();
         version2.Close();
      }
   }
}
```

## <a name="tryfinally-block"></a>Blocco try/finally

Anziché eseguire il wrapping di un blocco `try/finally` in un'istruzione `using`, è possibile implementare direttamente il blocco `try/finally`. La scelta può essere espressione dello stile di codifica personale oppure essere dovuta a uno dei seguenti motivi: 

* Includere un blocco `catch` per gestire eventuali eccezioni generate nel blocco `try`. In caso contrario, tutte le eccezioni generate dall'istruzione `using` non vengono gestite, analogamente alle eccezioni generate all'interno del blocco `using` se un blocco `try/catch` non è presente. 

* Creare un'istanza di un oggetto che implementa [IDisposable](xref:System.IDisposable) il cui ambito non è locale rispetto al blocco in cui viene dichiarato. 

L'esempio seguente è simile a quello precedente, con la differenza che in questo viene usato un blocco `try/catch/finally` per creare un'istanza di un oggetto [StreamReader](xref:System.IO.StreamReader), usarla ed eliminarla, e per gestire le eccezioni generate dal costruttore [StreamReader](xref:System.IO.StreamReader) e dal relativo metodo [ReadToEnd](xref:System.IO.StreamReader.ReadToEnd). Si noti che il codice nel blocco `finally` controlla che l'oggetto che implementa [IDisposable](xref:System.IDisposable) non sia `null` prima di chiamare il metodo [Dispose](xref:System.IDisposable.Dispose). Diversamente potrebbe generarsi un'eccezione [NullReferenceException](xref:System.NullReferenceException) in fase di esecuzione. 

```cs
using System;
using System.Globalization;
using System.IO;

public class Example
{
   public static void Main()
   {
      StreamReader sr = null;
      try {
         sr = new StreamReader("file1.txt");
         String contents = sr.ReadToEnd();
         sr.Close();
         Console.WriteLine("The file has {0} text elements.", 
                           new StringInfo(contents).LengthInTextElements);    
      }      
      catch (FileNotFoundException) {
         Console.WriteLine("The file cannot be found.");
      }   
      catch (IOException) {
         Console.WriteLine("An I/O error has occurred.");
      }
      catch (OutOfMemoryException) {
         Console.WriteLine("There is insufficient memory to read the file.");   
      }
      finally {
         if (sr != null) sr.Dispose();     
      }
   }
}
```

```vb
Imports System.Globalization
Imports System.IO

Module Example
   Public Sub Main()
      Dim sr As StreamReader = Nothing
      Try 
         sr = New StreamReader("file1.txt")
         Dim contents As String = sr.ReadToEnd()
         sr.Close()
         Console.WriteLine("The file has {0} text elements.", 
                           New StringInfo(contents).LengthInTextElements)    
      Catch e As FileNotFoundException
         Console.WriteLine("The file cannot be found.")
      Catch e As IOException
         Console.WriteLine("An I/O error has occurred.")
      Catch e As OutOfMemoryException
         Console.WriteLine("There is insufficient memory to read the file.")   
      Finally 
         If sr IsNot Nothing Then sr.Dispose()     
      End Try
   End Sub
End Module
```

È possibile usare questo modello di base se si decide di implementare o è necessario implementare un blocco `try/finally`, poiché il linguaggio di programmazione non supporta un'istruzione `using`, ma consente chiamate dirette al metodo [Dispose](xref:System.IDisposable.Dispose). 

## <a name="see-also"></a>Vedere anche

[Pulizia delle risorse non gestite](unmanaged.md)





<!--HONumber=Nov16_HO1-->


