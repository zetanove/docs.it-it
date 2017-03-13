---
title: "Procedura: confrontare stringhe (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "confronto di stringhe [C#]"
  - "stringhe [C#], confronto"
ms.assetid: e1268e28-ee98-4695-98e9-92280f1c33c0
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# Procedura: confrontare stringhe (Guida per programmatori C#)
Quando si confrontano stringhe, si produce un risultato che indica che una stringa è maggiore o minore dell'altra o che le due stringhe sono uguali.  Le regole in base alle quali viene determinato il risultato sono diverse a seconda che si esegua un *confronto ordinale* o un *confronto dipendente dalle impostazioni cultura*.  È importante utilizzare il tipo corretto di confronto per l'attività specifica.  
  
 Utilizzare confronti ordinali di base quando è necessario confrontare o ordinare i valori di due stringhe indipendentemente dalle convenzioni linguistiche.  Un confronto ordinale di base \(`System.StringComparison.Ordinal`\) distingue tra maiuscole e minuscole, cioè le due stringhe devono corrispondere esattamente carattere per carattere: "file" non equivale a "FILE" né a "File".  Una variazione utilizzata frequentemente è `System.StringComparison.OrdinalIgnoreCase`, che consente la corrispondenza di "file", "File" e "FILE".  `StringComparison.OrdinalIgnoreCase` viene spesso utilizzato per confrontare nomi di file, nomi di percorsi, percorsi di rete e qualsiasi altra stringa il cui valore non cambia in base alle impostazioni locali del computer dell'utente.  Per ulteriori informazioni, vedere <xref:System.StringComparison?displayProperty=fullName>.  
  
 I confronti dipendenti dalle impostazioni cultura sono utilizzati in genere per confrontare e ordinare stringhe che sono input di utenti finali, perché i caratteri e le convenzioni di ordinamento di queste stringhe possono variare a seconda delle impostazioni locali del computer dell'utente.  Anche stringhe che contengono caratteri identici potrebbero essere ordinate in modo diverso a seconda delle impostazioni cultura del thread corrente.  
  
> [!NOTE]
>  Quando si confrontano stringhe, è opportuno utilizzare i metodi che specificano in modo esplicito il tipo di confronto che si intende eseguire.  In questo modo il codice può essere gestito e letto con maggiore facilità.  Quando possibile, utilizzare gli overload dei metodi delle classi <xref:System.String?displayProperty=fullName> e <xref:System.Array?displayProperty=fullName> che accettano un parametro di enumerazione <xref:System.StringComparison>, in modo da poter specificare il tipo di confronto da eseguire.  È meglio evitare l'utilizzo degli operatori `==` e `!=` quando si confrontano stringhe.  Inoltre, evitare di utilizzare i metodi di istanza <xref:System.String.CompareTo%2A?displayProperty=fullName> perché nessuno degli overload accetta <xref:System.StringComparison>.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come confrontare correttamente stringhe i cui valori non cambiano in base alle impostazioni locali del computer dell'utente.  Viene inoltre illustrata la funzionalità *inserimento di stringa* di C\#.  Quando un programma dichiara due o più variabili di stringa identiche, il compilatore le archivia tutte nella stessa posizione.  Chiamando il metodo <xref:System.Object.ReferenceEquals%2A>, è possibile vedere che le due stringhe si riferiscono allo stesso oggetto in memoria.  Utilizzare il metodo <xref:System.String.Copy%2A?displayProperty=fullName> per evitare l'inserimento di stringa, come mostrato nell'esempio.  
  
 [!code-cs[csProgGuideStrings#11](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-compare-strings_1.cs)]  
  
## Esempio  
 Nell'esempio seguente viene mostrato come confrontare stringhe nel modo preferito tramite i metodi <xref:System.String?displayProperty=fullName> che accettano un'enumerazione <xref:System.StringComparison>.  Notare che i metodi di istanza <xref:System.String.CompareTo%2A?displayProperty=fullName> non vengono utilizzati qui, perché nessuno degli overload accetta <xref:System.StringComparison>.  
  
 [!code-cs[csProgGuideStrings#31](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-compare-strings_2.cs)]  
  
## Esempio  
 Nell'esempio seguente viene mostrato come ordinare e cercare stringhe in una matrice in modo dipendente dalle impostazioni cultura tramite i metodi <xref:System.Array> statici che accettano un parametro <xref:System.StringComparer?displayProperty=fullName>.  
  
 [!code-cs[csProgGuideStrings#32](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-compare-strings_3.cs)]  
  
 Le classi di raccolte quali <xref:System.Collections.Hashtable?displayProperty=fullName>, <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> e <xref:System.Collections.Generic.List%601?displayProperty=fullName> dispongono di costruttori che accettano un parametro <xref:System.StringComparer?displayProperty=fullName> quando il tipo degli elementi o delle chiavi è `string`.  In generale, è consigliabile utilizzare questi costruttori quando possibile e specificare `Ordinal` o `OrdinalIgnoreCase`.  
  
## Vedere anche  
 <xref:System.Globalization.CultureInfo?displayProperty=fullName>   
 <xref:System.StringComparer?displayProperty=fullName>   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)   
 [Confronto di stringhe](../Topic/Comparing%20Strings%20in%20the%20.NET%20Framework.md)   
 [Globalizzazione e localizzazione di applicazioni](/visual-studio/ide/globalizing-and-localizing-applications)