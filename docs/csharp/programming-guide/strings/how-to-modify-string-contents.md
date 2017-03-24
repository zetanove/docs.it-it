---
title: "Procedura: modificare il contenuto delle stringhe (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "stringhe [C#], modifica"
ms.assetid: b6c20bba-ce22-43d7-ad1b-5ce65f714055
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# Procedura: modificare il contenuto delle stringhe (Guida per programmatori C#)
Poiché le stringhe sono *non modificabili*, non è possibile modificare il valore di un oggetto stringa dopo che è stato creato senza utilizzare codice unsafe.  Ci sono tuttavia molti modi per modificare il valore di una stringa e archiviare il risultato in un nuovo oggetto stringa.  La classe <xref:System.String?displayProperty=fullName> fornisce metodi che operano su una stringa di input e restituiscono un nuovo oggetto stringa.  In molti casi, è possibile assegnare il nuovo oggetto alla variabile che conteneva la stringa originale.  La classe <xref:System.Text.RegularExpressions.Regex?displayProperty=fullName> fornisce metodi aggiuntivi che funzionano in modo simile.  La classe <xref:System.Text.StringBuilder?displayProperty=fullName> fornisce un buffer di caratteri che è possibile modificare "sul posto". Il metodo <xref:System.Text.StringBuilder.ToString%2A?displayProperty=fullName> viene chiamato per creare un nuovo oggetto stringa che contiene il contenuto corrente del buffer.  
  
## Esempio  
 Nell'esempio seguente vengono mostrati vari modi per sostituire o rimuovere sottostringhe in una stringa specifica.  
  
 [!code-cs[csProgGuideStrings#28](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-modify-string-contents_1.cs)]  
  
## Esempio  
 Per accedere ai singoli caratteri in una stringa tramite una notazione di matrice, è possibile utilizzare l'oggetto <xref:System.Text.StringBuilder> che esegue l'overload dell'operatore `[]` per fornire accesso al buffer di caratteri interno.  È anche possibile convertire la stringa in una matrice di caratteri tramite il metodo <xref:System.String.ToCharArray%2A>.  Nell'esempio seguente viene utilizzato `ToCharArray` per creare la matrice.  Alcuni elementi di questa matrice vengono quindi modificati.  Un costruttore di stringhe che accetta una matrice di caratteri come parametro di input viene quindi chiamato per creare una nuova stringa.  
  
 [!code-cs[csProgGuideStrings#24](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-modify-string-contents_2.cs)]  
  
## Esempio  
 L'esempio seguente viene fornito per quelle situazioni molto rare nelle quali si potrebbe volere modificare una stringa sul posto tramite codice unsafe, in un modo simile alle matrici di caratteri di tipo C.  Nell'esempio viene mostrato come accedere ai singoli caratteri "sul posto" tramite la parola chiave fixed.  Viene inoltre mostrato un possibile effetto collaterale di operazioni non sicure sulle stringhe che risulta dalla modalità in cui il compilatore C\# archivia \(inserisce\) stringhe all'interno.  In generale, non è consigliabile utilizzare questa tecnica a meno che sia assolutamente necessario.  
  
 [!code-cs[csProgGuideStrings#29](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-modify-string-contents_3.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)