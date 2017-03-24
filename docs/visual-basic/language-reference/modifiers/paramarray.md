---
title: "ParamArray (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ParamArray"
  - "ParamArray"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "ParamArray keyword"
  - "ParamArray keyword, syntax"
ms.assetid: a5f18789-92bd-488f-9c7e-cf3719963635
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# ParamArray (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica l'utilizzo di una matrice facoltativa di elementi del tipo specificato da parte di un parametro di routine.  `ParamArray` può essere utilizzato solo nell'ultimo parametro di un elenco di parametri.  
  
## Note  
 `ParamArray` consente di passare alla routine un numero arbitrario di argomenti.  Un parametro `ParamArray` viene sempre passato utilizzando [ByVal](../../../visual-basic/language-reference/modifiers/byval.md).  
  
 È possibile specificare uno o più argomenti per un parametro `ParamArray` passando una matrice del tipo di dati appropriato, un elenco di valori separati da virgole oppure nessun elemento.  Per ulteriori informazioni, vedere la sezione relativa alla chiamata di ParamArray in [Parameter Arrays](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md).  
  
> [!IMPORTANT]
>  Ogni volta che viene utilizzata una matrice che può essere di dimensioni indefinite, esiste il rischio di sovraccarico della capacità interna dell'applicazione.  Se si accetta una matrice di parametri dal codice chiamante, è necessario verificarne la lunghezza ed effettuare le operazioni appropriate nel caso in cui le dimensioni siano eccessive per l'applicazione.  
  
 Il modificatore `ParamArray` può essere utilizzato nei seguenti contesti:  
  
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)   
 [Parameter Arrays](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)