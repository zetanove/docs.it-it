---
title: "Procedura: definire propriet&#224; astratte (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "proprietà astratte [C#]"
  - "proprietà [C#], abstract"
ms.assetid: 672a90eb-47b9-4ae0-9914-af53852fddcb
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# Procedura: definire propriet&#224; astratte (Guida per programmatori C#)
Nell'esempio seguente viene illustrato come definire proprietà [astratte](../../../csharp/language-reference/keywords/abstract.md).  La dichiarazione di una proprietà astratta non fornisce un'implementazione delle funzioni di accesso della proprietà. Viene dichiarato che la classe supporta le proprietà, ma l'implementazione delle funzioni di accesso viene demandata alle classi derivate.  Nell'esempio riportato di seguito viene illustrato come implementare le proprietà astratte ereditate da una classe base.  
  
 L'esempio include tre file, ciascuno dei quali viene compilato singolarmente e il cui assembly risultante viene utilizzato come riferimento nella compilazione successiva:  
  
-   abstractshape.cs: la classe `Shape` che contiene una proprietà `Area` astratta.  
  
-   shapes.cs: le sottoclassi della classe `Shape`.  
  
-   shapetest.cs: un programma di test per la visualizzazione delle aree di alcuni oggetti derivati da `Shape`.  
  
 Per compilare l'esempio, utilizzare il seguente comando:  
  
 `csc abstractshape.cs shapes.cs shapetest.cs`  
  
 Verrà creato il file eseguibile shapetest.exe.  
  
## Esempio  
 Questo file dichiara la classe `Shape` che contiene la proprietà `Area` del tipo `double`.  
  
 [!code-cs[csProgGuideInheritance#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-define-abstract-properties_1.cs)]  
  
-   I modificatori della proprietà sono inseriti nella dichiarazione della proprietà stessa.  Di seguito è riportato un esempio:  
  
    ```  
    public abstract double Area  
    ```  
  
-   Quando si dichiara una proprietà astratta \(quale `Area`, in questo esempio\), è sufficiente indicare le funzioni di accesso disponibili per la proprietà, senza implementarle.  In questo esempio è disponibile solo una funzione di accesso [get](../../../csharp/language-reference/keywords/get.md), pertanto la proprietà è in sola lettura.  
  
## Esempio  
 Nel codice riportato di seguito sono presenti tre sottoclassi di `Shape` di cui viene illustrato l'override della proprietà `Area` per fornire la propria implementazione.  
  
 [!code-cs[csProgGuideInheritance#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-define-abstract-properties_2.cs)]  
  
## Esempio  
 Nel codice riportato di seguito viene illustrato un programma di test che crea una serie di oggetti derivati da `Shape` e ne stampa le aree.  
  
 [!code-cs[csProgGuideInheritance#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-define-abstract-properties_3.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [Procedura: Creare e usare assembly dalla riga di comando](../Topic/How%20to:%20Create%20and%20Use%20Assemblies%20Using%20the%20Command%20Line%20\(C%23%20and%20Visual%20Basic\).md)