---
title: "Generics (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, generics"
  - "generics [C#]"
ms.assetid: 75ea8509-a4ea-4e7a-a2b3-cf72482e9282
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# Generics (Guida per programmatori C#)
I generics sono stati aggiunti alla versione 2.0 del linguaggio C\# e del linguaggio CLR \(Common Language Runtime\).  Introducono in .NET Framework il concetto di parametri di tipo, grazie ai quali è possibile progettare classi e metodi che rinviano la specifica di uno più tipi fino a quando il codice client non dichiara o crea un'istanza per la classe o il metodo.  Utilizzando il parametro del tipo generico T è ad esempio possibile scrivere una singola classe utilizzabile in altro codice client senza incorrere nel rischio di cast o operazioni di boxing in fase di esecuzione, come illustrato di seguito:  
  
 [!code-cs[csProgGuideGenerics#1](../../../csharp/programming-guide/generics/codesnippet/csharp/index_1.cs)]  
  
## Cenni preliminari sui generics  
  
-   Utilizzare i tipi generici per massimizzare il riutilizzo del codice, l'indipendenza dai tipi e le prestazioni.  
  
-   I generics vengono generalmente utilizzati per creare classi di raccolte.  
  
-   La libreria di classi .NET Framework contiene diverse classi di raccolte generiche nello spazio dei nomi <xref:System.Collections.Generic>,  che dovrebbero essere utilizzate quando possibile al posto di classi come <xref:System.Collections.ArrayList> nello spazio dei nomi <xref:System.Collections>.  
  
-   È possibile creare interfacce, classi, metodi, eventi e delegati generici personalizzati.  
  
-   Le classi generiche possono essere vincolate in modo da consentire l'accesso ai metodi su determinati tipi di dati.  
  
-   È possibile ottenere informazioni sui tipi utilizzati in un tipo di dati generico in fase di esecuzione tramite la reflection.  
  
## Sezioni correlate  
 Per ulteriori informazioni:  
  
-   [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md)  
  
-   [Vantaggi dei generics](../../../csharp/programming-guide/generics/benefits-of-generics.md)  
  
-   [Parametri di tipo generico](../../../csharp/programming-guide/generics/generic-type-parameters.md)  
  
-   [Vincoli sui parametri di tipo](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)  
  
-   [Classi generiche](../../../csharp/programming-guide/generics/generic-classes.md)  
  
-   [Interfacce generiche](../../../csharp/programming-guide/generics/generic-interfaces.md)  
  
-   [Metodi generici](../../../csharp/programming-guide/generics/generic-methods.md)  
  
-   [Delegati generici](../../../csharp/programming-guide/generics/generic-delegates.md)  
  
-   [Parola chiave default](../../../csharp/programming-guide/generics/default-keyword-in-generic-code.md)  
  
-   [Differenze tra modelli C\+\+ e generics C\#](../../../csharp/programming-guide/generics/differences-between-cpp-templates-and-csharp-generics.md)  
  
-   [Generics e reflection](../../../csharp/programming-guide/generics/generics-and-reflection.md)  
  
-   [Generics nel runtime](../../../csharp/programming-guide/generics/generics-in-the-run-time.md)  
  
-   [Generics nella libreria di classi .NET Framework](../../../csharp/programming-guide/generics/generics-in-the-net-framework-class-library.md)  
  
## Specifiche del linguaggio C\#  
 Per ulteriori informazioni, vedere [Specifiche del linguaggio C\#](../../../csharp/language-reference/language-specification.md).  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tipi](../../../csharp/programming-guide/types/index.md)   
 [\<typeparam\>](../../../csharp/programming-guide/xmldoc/typeparam.md)   
 [\<typeparamref\>](../../../csharp/programming-guide/xmldoc/typeparamref.md)