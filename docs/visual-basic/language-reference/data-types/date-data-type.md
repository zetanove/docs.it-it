---
title: "Date Data Type (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Date"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Date data type"
  - "dates, Visual Basic data types"
  - "times, Date data type"
  - "Date literals"
  - "data values"
  - "times, Visual Basic data types"
  - "dates, Date data type"
  - "data types [Visual Basic], assigning"
  - "literals, Date"
  - "# specifier for Date literals"
ms.assetid: d9edf5b0-e85e-438b-a1cf-1f321e7c831b
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Date Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Contiene valori a 64 bit \(8 byte\) conformi alle specifiche IEEE che rappresentano le date comprese tra l'1 gennaio dell'anno 0001 e il 31 dicembre dell'anno 9999 e le ore comprese tra le 00.00.00 \(mezzanotte\) e le 23.59.59.9999999.  Ogni incremento rappresenta 100 nanosecondi di tempo trascorso dall'inizio del 1° gennaio dell'anno 1 del calendario gregoriano.  Il valore massimo rappresenta 100 nanosecondi prima dell'inizio del 1° gennaio dell'anno 10000.  
  
## Note  
 Usare il tipo di dati `Date` per contenere valori di data, di ora o entrambi.  
  
 Il valore predefinito di `Date` è 00.00.00 \(mezzanotte\) del 1° gennaio 0001.  
  
 È possibile ottenere la data e l'ora corrente dalla classe <xref:Microsoft.VisualBasic.DateAndTime>.  
  
## Requisiti di formato  
 È necessario racchiudere un valore letterale `Date` tra simboli di cancelletto \(`# #`\).  Il valore della data deve essere specificato nel formato M\/g\/aaaa, ad esempio `#5/31/1993#`, oppure aaaa\-MM\-gg, ad esempio `#1993-5-31#`.  Quando si specifica prima l'anno, è possibile usare le barre.  Questo requisito è indipendente dalle impostazioni locali usate e dalle impostazioni relative al formato di data e ora del computer.  
  
 Il motivo di questa limitazione è che il significato del codice non deve mai cambiare a seconda delle impostazioni locali con cui l'applicazione viene eseguita.  Si supponga di impostare come hardcoded il valore letterale `Date` `#3/4/1998#` per rappresentare la data del 4 marzo 1998.  Se nelle impostazioni locali è definito il formato mm\/gg\/aaaa, la compilazione di 3\/4\/1998 viene eseguita nel modo desiderato.  Si supponga però di distribuire l'applicazione in molti paesi.  Se nelle impostazioni locali è definito il formato gg\/mm\/aaaa, il valore letterale hardcoded verrà compilato come 3 aprile 1998.  Se invece è definito il formato aaaa\/mm\/gg, il valore letterale non sarà valido \(1998 aprile 0003\) e verrà generato un errore del compilatore.  
  
## Soluzioni  
 Per convertire un valore letterale `Date` nel formato delle impostazioni locali in uso o in un formato personalizzato, fornire il valore letterale alla funzione <xref:Microsoft.VisualBasic.Strings.Format%2A>, specificando un formato di data predefinito o definito dall'utente.  Nell'esempio che segue viene illustrato quanto descritto.  
  
```  
MsgBox("The formatted date is " & Format(#5/31/1993#, "dddd, d MMM yyyy"))  
```  
  
 In alternativa, si può usare uno dei costruttori di overload della struttura <xref:System.DateTime> per assemblare un valore di data e ora.  L'esempio seguente crea un valore per rappresentare le ore 12.14 del 31 maggio 1993.  
  
```  
Dim dateInMay As New System.DateTime(1993, 5, 31, 12, 14, 0)   
```  
  
## Formato dell'ora  
 È possibile specificare il valore dell'ora nel formato 12 o 24 ore, ad esempio `#1:15:30 PM#` o `#13:15:30#`.   Tuttavia, se non si specificano i minuti o i secondi, è necessario indicare AM o PM.  
  
## Valori predefiniti di data e ora  
 Se non si include una data in un valore letterale di data\/ora, Visual Basic imposta la parte del valore relativa alla data sul 1° gennaio 0001.  Se non si include un'ora in un valore letterale di data\/ora, Visual Basic imposta la parte del valore relativa all'ora sull'inizio della giornata, ossia mezzanotte \(00.00.00\).  
  
## Conversione di tipi  
 Se un valore `Date` viene convertito nel tipo `String`, Visual Basic esegue il rendering della data e dell'ora rispettivamente in base al formato breve e al formato 12 o 24 ore specificati nelle impostazioni locali di runtime.  
  
## Suggerimenti per la programmazione  
  
-   **Considerazioni sull'interoperabilità.** Se si prevede l'interazione con componenti non scritti per .NET Framework, ad esempio oggetti COM o di automazione, tenere presente che i tipi di data\/ora in altri ambienti non sono compatibili con il tipo `Date` di Visual Basic.  Se si passa un argomento di data\/ora a un componente di questo tipo, nel nuovo codice Visual Basic è necessario dichiararlo come `Double` anziché come `Date` e usare i metodi di conversione <xref:System.DateTime.FromOADate%2A?displayProperty=fullName> e <xref:System.DateTime.ToOADate%2A?displayProperty=fullName>.  
  
-   **Caratteri tipo.** `Date` non ha alcun carattere di tipo letterale o di tipo identificatore.  Il compilatore considera tuttavia i valori letterali racchiusi tra simboli del cancelletto \(`# #`\) come valori `Date`.  
  
-   **Tipo di framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.DateTime?displayProperty=fullName>.  
  
## Esempio  
 Una variabile o una costante del tipo di dati `Date` contiene sia la data che l'ora.  Questa condizione è illustrata nell'esempio seguente.  
  
```  
Dim someDateAndTime As Date = #8/13/2002 12:14 PM#  
```  
  
## Vedere anche  
 <xref:System.DateTime?displayProperty=fullName>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Stringhe di formato di data e ora standard](../Topic/Standard%20Date%20and%20Time%20Format%20Strings.md)   
 [Stringhe di formato di data e ora personalizzato](../Topic/Custom%20Date%20and%20Time%20Format%20Strings.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)