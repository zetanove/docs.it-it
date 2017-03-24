---
title: "Parameter Arrays (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "parameter arrays, about parameter arrays"
  - "ParamArray keyword, parameter arrays"
  - "Visual Basic code, procedures"
  - "parameters, parameter arrays"
  - "arguments [Visual Basic], parameter arrays"
  - "procedures, indefinite number of argument values"
  - "arrays [Visual Basic], parameter arrays"
ms.assetid: c43edfae-9114-4096-9ebc-8c5c957a1067
caps.latest.revision: 26
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 26
---
# Parameter Arrays (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Non è solitamente possibile chiamare una routine con più argomenti di quelli specificati nella dichiarazione di routine.  Quando è necessario disporre di un numero indefinito di argomenti, è possibile dichiarare una *matrice di parametri* che consente a una routine di accettare una matrice di valori per un parametro.  Non è necessario conoscere il numero degli elementi nella matrice di parametri quando si definisce la routine.  La dimensione della matrice è determinata singolarmente da ciascuna chiamata alla routine.  
  
## Dichiarazione di una ParamArray  
 Utilizzare la parola chiave [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) per indicare una matrice di parametri nell'elenco di parametri.  È necessario attenersi alle regole che seguono:  
  
-   Una routine può definire solo una matrice di parametri e deve rappresentare l'ultimo parametro nella definizione della routine.  
  
-   È necessario che la matrice di parametri sia passata tramite valore.  È buona norma di programmazione includere la parola chiave [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) in modo esplicito nella definizione della routine.  
  
-   La matrice di parametri è automaticamente facoltativa.  Il suo valore predefinito è una matrice unidimensionale vuota del tipo di elementi della matrice di parametri.  
  
-   È necessario che tutti i parametri che precedono la matrice di parametri siano obbligatori  e che la matrice di parametri sia l'unico parametro facoltativo.  
  
## Chiamata di una ParamArray  
 Quando si chiama una routine che definisce una matrice di parametri, è possibile fornire l'argomento attraverso uno dei metodi illustrati di seguito.  
  
-   Nothing, ovvero è possibile omettere l'argomento [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md).  In questo caso, alla routine viene passata una matrice vuota.  È anche possibile passare la parola chiave [Nothing](../../../../visual-basic/language-reference/nothing.md), con lo stesso risultato.  
  
-   Un elenco di un numero arbitrario di argomenti, separati da virgole.  È necessario che il tipo di dati di ciascun argomento sia convertibile in modo implicito nel tipo di elemento `ParamArray`.  
  
-   Una matrice con lo stesso tipo di elemento del tipo di elemento della matrice di parametri.  
  
 In tutti i casi il codice all'interno della routine considera la matrice di parametri come una matrice unidimensionale in cui ogni elemento è dello stesso tipo di dati del tipo di dati `ParamArray`.  
  
> [!IMPORTANT]
>  Ogni volta che viene utilizzata una matrice che può essere di dimensioni indefinite, esiste il rischio di sovraccarico della capacità interna dell'applicazione.  Se si accetta una matrice di parametri, è necessario verificare le dimensioni della matrice passate dal codice chiamante.  Qualora tali dimensioni risultino eccessive per l'applicazione che si sta sviluppando, intraprendere le azioni appropriate.  Per ulteriori informazioni, vedere [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
## Esempio  
 In l ' esempio seguente viene definita e chiamata la funzione `calcSum`.  Il modificatore di `ParamArray` per il parametro `args` consente alla funzione di accettare un numero variabile di argomenti.  
  
 [!code-vb[VbVbalrStatements#26](../../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/parameter-arrays_1.vb)]  
  
 Nell'esempio riportato di seguito viene definita una routine con una matrice di parametri e vengono generati i valori di tutti gli elementi della matrice passati alla matrice di parametri.  
  
 [!code-vb[VbVbcnProcedures#48](./codesnippet/VisualBasic/parameter-arrays_2.vb)]  
  
 [!code-vb[VbVbcnProcedures#49](./codesnippet/VisualBasic/parameter-arrays_3.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Information.UBound%2A>   
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Passing Arguments by Value and by Reference](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Passing Arguments by Position and by Name](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md)