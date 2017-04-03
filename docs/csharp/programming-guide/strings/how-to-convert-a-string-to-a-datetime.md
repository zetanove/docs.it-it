---
title: 'Procedura: Convertire una stringa in un oggetto DateTime (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- strings [C#], converting to DateTIme
ms.assetid: 88abef11-3a06-4b49-8dd2-61ed0e876fc3
caps.latest.revision: 21
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f31deeb2b29495ab48781c7e673fed37e8ad8dce
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-convert-a-string-to-a-datetime-c-programming-guide"></a>Procedura: Convertire una stringa in un oggetto DateTime (Guida per programmatori C#)
I programmi consentono generalmente agli utenti di immettere le date come valori stringa. Per convertire una data basata su stringa in un oggetto <xref:System.DateTime?displayProperty=fullName>, è possibile usare il metodo <xref:System.Convert.ToDateTime%28System.String%29?displayProperty=fullName> o il metodo statico <xref:System.DateTime.Parse%28System.String%29?displayProperty=fullName> come illustrato nell'esempio seguente.  
  
 **Impostazioni cultura**.  In base alle diverse impostazioni cultura nel mondo le stringhe data vengono scritte in modi diversi.  Negli Stati Uniti, ad esempio, 01/20/2008 è il 20 gennaio 2008.  In Francia questo genera un'eccezione InvalidFormatException. Questo perché in Francia la data viene letta come giorno/mese/anno, mentre negli Stati Uniti è mese/giorno/anno.  
  
 Di conseguenza, una stringa come 20/01/2008 viene analizzata come 20 gennaio 2008 in Francia e genera un'eccezione InvalidFormatException negli Stati Uniti.  
  
 Per determinare le impostazioni cultura correnti, è possibile usare System.Globalization.CultureInfo.CurrentCulture.  
  
 Di seguito viene riportato un esempio semplice di conversione di una stringa in dateTime.  
  
 Per altri esempi di stringhe di data, vedere <xref:System.Convert.ToDateTime%28System.String%29?displayProperty=fullName>.  
  
```csharp  
string dateTime = "01/08/2008 14:50:50.42";  
            DateTime dt = Convert.ToDateTime(dateTime);  
            Console.WriteLine("Year: {0}, Month: {1}, Day: {2}, Hour: {3}, Minute: {4}, Second: {5}, Millisecond: {6}",  
                              dt.Year, dt.Month, dt.Day, dt.Hour, dt.Minute, dt.Second, dt.Millisecond);  
            // Specify exactly how to interpret the string.  
            IFormatProvider culture = new System.Globalization.CultureInfo("fr-FR", true);  
  
            // Alternate choice: If the string has been input by an end user, you might    
            // want to format it according to the current culture:   
            // IFormatProvider culture = System.Threading.Thread.CurrentThread.CurrentCulture;  
            DateTime dt2 = DateTime.Parse(dateTime, culture, System.Globalization.DateTimeStyles.AssumeLocal);  
            Console.WriteLine("Year: {0}, Month: {1}, Day: {2}, Hour: {3}, Minute: {4}, Second: {5}, Millisecond: {6}",  
                              dt2.Year, dt2.Month, dt2.Day, dt2.Hour, dt2.Minute, dt2.Second, dt2.Millisecond  
/* Output (assuming first culture is en-US and second is fr-FR):  
    Year: 2008, Month: 1, Day: 8, Hour: 14, Minute: 50, Second: 50, Millisecond: 420  
Year: 2008, Month: 8, Day: 1, Hour: 14, Minute: 50, Second: 50, Millisecond: 420  
Press any key to continue . . .  
 */  
```  
  
## <a name="example"></a>Esempio  
 [!code-cs[csProgGuideStrings#13](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-convert-a-string-to-a-datetime_1.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 [Stringhe](../../../csharp/programming-guide/strings/index.md)
