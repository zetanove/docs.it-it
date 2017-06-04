---
title: "Procedura: aggiungere zeri iniziali a un numero | Microsoft Docs"
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
  - "formattazione [.NET Framework], numeri"
  - "numeri (formattazione) [.NET Framework]"
  - "numeri [.NET Framework], stringhe di formato"
  - "stringhe di formato numerico [.NET Framework]"
ms.assetid: 0b2c2cb5-c580-4891-8d81-cb632f5ec384
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: aggiungere zeri iniziali a un numero
È possibile aggiungere degli zeri iniziali a un intero usando la [stringa di formato numerico standard](../../../docs/standard/base-types/standard-numeric-format-strings.md) "D" con un identificatore di precisione.  È possibile aggiungere zeri iniziali sia ai numeri interi che ai numeri a virgola mobile usando una  [stringa di formato numerico personalizzata](../../../docs/standard/base-types/custom-numeric-format-strings.md).  In questo argomento viene illustrato come usare entrambi i metodi per aggiungere un numero con gli zeri iniziali.  
  
### Per aggiungere un intero con gli zeri iniziali a una lunghezza specifica  
  
1.  Determinare il numero minimo di cifre da visualizzare nel valore di tipo Integer.  Includere eventuali cifre iniziali nel numero.  
  
2.  Determinare se si vuole visualizzare il valore di tipo Integer come valore decimale o esadecimale.  
  
    -   Per visualizzare il valore di tipo Integer come valore decimale, chiamare il metodo `ToString(String)` e passare la stringa "D*n*" come valore del parametro `format`, dove *n* rappresenta la lunghezza minima della stringa.  
  
    -   Per visualizzare il valore di tipo Integer come valore esadecimale, chiamare il metodo `ToString(String)` e passare la stringa "X*n*" come valore del parametro `format`, dove *n* rappresenta la lunghezza minima della stringa.  
  
     È anche possibile usare la stringa di formato in un metodo, ad esempio <xref:System.String.Format%2A> o <xref:System.Console.WriteLine%2A>, che usa la [formattazione composta](../../../docs/standard/base-types/composite-formatting.md).  
  
 Il seguente esempio formatta diversi valori di tipo Integer con gli zeri iniziali in modo che la lunghezza totale del numero formattato sia almeno di otto caratteri.  
  
 [!code-csharp[Formatting.HowTo.PadNumber#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#1)]
 [!code-vb[Formatting.HowTo.PadNumber#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#1)]  
  
### Per aggiungere un intero con un determinato numero di zeri iniziali  
  
1.  Determinare il numero di zeri iniziali da visualizzare nel valore di tipo Integer.  
  
2.  Determinare se si vuole visualizzare il valore di tipo Integer come valore decimale o esadecimale.  Se si formatta come valore decimale, è necessario usare l'identificatore di formato standard "D", mentre come valore esadecimale è necessario usare l'identificatore di formato "X".  
  
3.  Determine la lunghezza della stringa numerica non aggiunta chiamando il metodo `ToString("D").Length` o `ToString("X").Length` del valore di tipo Integer.  
  
4.  Aggiungere il numero di zeri iniziali da includere nella stringa formattata nella lunghezza della stringa numerica non aggiunta.  In questo modo si definisce la lunghezza totale della stringa aggiunta.  
  
5.  Chiamare il metodo del `ToString(String)` del valore di tipo Integer e passare la stringa "D*n*" per le stringhe decimali e la stringa "X*n*" per quelle esadecimali, dove *n* rappresenta la lunghezza totale della stringa aggiunta.  È anche possibile usare la stringa di formato "D*n*" o "X*n*" in un metodo che supporta la formattazione composta.  
  
 Il seguente esempio aggiunge un valore di tipo Integer con cinque zeri iniziali.  
  
 [!code-csharp[Formatting.HowTo.PadNumber#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#2)]
 [!code-vb[Formatting.HowTo.PadNumber#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#2)]  
  
### Per aggiungere un valore numerico con gli zeri iniziali a una lunghezza specifica  
  
1.  Determinare il numero di cifre alla sinistra del decimale che deve avere la rappresentazione della stringa del numero.  Includere gli eventuali zeri iniziali nel numero totale di cifre.  
  
2.  Definire una stringa di formato numerico personalizzata in cui è usato un segnaposto zero \("0"\) per rappresentare il numero minimo di zeri.  
  
3.  Chiamare il metodo `ToString(String)` del numero e passarlo alla stringa di formato personalizzata.  È anche possibile usare la stringa di formato personalizzata con un metodo che supporta la formattazione composta.  
  
 Il seguente esempio formatta diversi valori numerici con gli zeri iniziali in modo che la lunghezza totale del numero formattato sia almeno di otto caratteri alla sinistra del decimale.  
  
 [!code-csharp[Formatting.HowTo.PadNumber#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#3)]
 [!code-vb[Formatting.HowTo.PadNumber#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#3)]  
  
### Per aggiungere un valore numerico con un determinato numero di zeri iniziali  
  
1.  Determinare il numero di zeri iniziali che deve avere il valore numerico.  
  
2.  Determine il numero di cifre alla sinistra del decimale nella stringa numerica non aggiunta.  Per eseguire questa operazione:  
  
    1.  Determinare se la rappresentazione della stringa di un numero include un simbolo di separatore decimale.  
  
    2.  In questo caso, determinare il numero di caratteri alla sinistra del separatore decimale.  
  
         \-oppure\-  
  
         In caso contrario, determinare la lunghezza della stringa.  
  
3.  Creare una stringa di formato personalizzata in cui è usato il segnaposto zero \("0"\) per ciascuno degli zeri iniziali da visualizzare nella stringa e il segnaposto zero o il segnaposto cifra \("\#"\) per rappresentare ciascuna cifra nella stringa predefinita.  
  
4.  Fornire la stringa di formato personalizzata come parametro nel metodo `ToString(String)` del numero o in un metodo che supporta la formattazione composta.  
  
 Il seguente esempio aggiunge due valori <xref:System.Double> con cinque zeri iniziali.  
  
 [!code-csharp[Formatting.HowTo.PadNumber#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#4)]
 [!code-vb[Formatting.HowTo.PadNumber#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#4)]  
  
## Vedere anche  
 [Stringhe di formato numerico personalizzato](../../../docs/standard/base-types/custom-numeric-format-strings.md)   
 [Stringhe di formato numerico standard](../../../docs/standard/base-types/standard-numeric-format-strings.md)   
 [Formattazione composita](../../../docs/standard/base-types/composite-formatting.md)