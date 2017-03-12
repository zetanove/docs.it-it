---
title: "Utilizzo degli operatori di conversione (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "operatori di conversione [C#]"
  - "conversioni [C#], operatori"
  - "operatori di conversione esplicita [C#]"
  - "operatori di conversione implicita [C#]"
  - "operatori [C#], conversione"
  - "conversioni definite dall'utente [C#]"
ms.assetid: caf36e89-c6c0-4b87-9f9e-85780a45c9a4
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# Utilizzo degli operatori di conversione (Guida per programmatori C#)
È possibile utilizzare gli operatori di conversione `implicit`, che sono più facili da utilizzare, o gli operatori di conversione `explicit`, per indicare chiaramente a chiunque legga il codice che si sta convertendo un tipo.  In questo argomento vengono illustrati entrambi i tipi di operatore di conversione.  
  
> [!NOTE]
>  Per ulteriori informazioni sui convertitori di tipi, vedere [Procedura: convertire una stringa in un numero](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md), [Procedura: convertire una matrice di byte in un Integer](../../../csharp/programming-guide/types/how-to-convert-a-byte-array-to-an-int.md), [Procedura: eseguire la conversione tra stringhe esadecimali e tipi numerici](../../../csharp/programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md), oppure <xref:System.Convert>.  
  
## Esempio  
 In questo caso si parla di operatore di conversione esplicito.  Questo operatore esegue la conversione dal tipo <xref:System.Byte> a un tipo di valore denominato `Digit`.  Poiché non è possibile convertire in cifre tutti i byte, la conversione è di tipo esplicito ed è pertanto necessario utilizzare un cast, come illustrato nel metodo `Main`.  
  
 [!code-cs[csProgGuideStatements#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-conversion-operators_1.cs)]  
  
## Esempio  
 In questo esempio viene illustrato un operatore di conversione implicito definendo un operatore di conversione che annulla l'operazione eseguita nell'esempio 1: converte una classe di valori denominata `Digit` in un tipo <xref:System.Byte> integrale.  Poiché è possibile convertire ogni cifra in <xref:System.Byte>, non è necessario forzare gli utenti ad eseguire una conversione esplicita.  
  
 [!code-cs[csProgGuideStatements#12](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/using-conversion-operators_2.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori di conversione](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md)   
 [is](../../../csharp/language-reference/keywords/is.md)