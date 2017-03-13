---
title: "Overload Resolution (Visual Basic) | Microsoft Docs"
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
  - "Visual Basic code, procedures"
  - "overload resolution"
  - "procedures, overloading"
  - "procedures, calling"
  - "procedure overloading, overload resolution"
  - "signatures, procedure"
  - "overloads, resolution"
ms.assetid: 766115d1-4352-45fb-859f-6063e0de0ec0
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# Overload Resolution (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È necessario che il compilatore di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] decida quale overload chiamare quando rileva una chiamata a una routine definita in diverse versioni di overload.  Questa operazione viene eseguita attenendosi alla procedura che segue:  
  
1.  **Accessibilità.** Eliminazione di tutti gli overload con un livello di accesso che impedisce al codice chiamante di chiamarli.  
  
2.  **Numero di parametri.** Eliminazione di eventuali overload che definiscano un numero diverso di parametri rispetto a quello fornito nella chiamata.  
  
3.  **Tipi di dati dei parametri.** Il compilatore preferisce i metodi di istanza ai metodi di estensione.  Se viene rilevato un metodo di istanza che richiede solo conversioni verso un tipo di dati più grande per corrispondere alla chiamata di routine, tutti i metodi di estensione vengono rilasciati e il compilatore continua solo con i candidati del metodo di istanza.  Se tale metodo di istanza non viene rilevato, continua sia con i metodi di istanza che con i metodi di estensione.  
  
     In questo passaggio vengono eliminati eventuali overload per i quali i tipi di dati degli argomenti di chiamata non possano essere convertiti nei tipi di parametri definiti nell'overload.  
  
4.  **Conversioni verso tipi di dati più piccoli.** Eliminazione di eventuali overload che richiedano una conversione verso un tipo di dati più piccolo dai tipi di argomento di chiamata ai tipi di parametro definiti.  Questa operazione viene eseguita indipendentemente dal fatto che l'opzione di controllo dei tipi \([Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)\) sia `On` o `Off`.  
  
5.  **Conversione verso tipi di dati più grandi.** Il compilatore considera gli overload rimanenti a coppie.  Per ogni coppia, il compilatore confronta i tipi di dati dei parametri definiti.  Se i tipi in uno degli overload sono tutti ampliati nei tipi corrispondenti nell'altro, il compilatore elimina quest'ultimo.  In altre parole, viene mantenuto l'overload che richiede l'ampliamento minore.  
  
6.  **Candidato singolo.** Gli overload continuano ad essere considerati a coppie fino a quando non rimane solo un overload, su cui viene risolta la chiamata.  Se il compilatore non è in grado di ridurre gli overload a uno solo, viene generato un errore.  
  
 Nella seguente figura viene illustrato il processo che determina quale versione di un insieme di versioni di overload chiamare.  
  
 ![Diagramma di flusso del processo di risoluzione degli overload](../../../../visual-basic/programming-guide/language-features/procedures/media/overloadres.gif "OverloadRes")  
Risoluzione delle versioni di overload  
  
 Nell'esempio riportato di seguito viene illustrato il processo di risoluzione degli overload.  
  
 [!code-vb[VbVbcnProcedures#62](./codesnippet/VisualBasic/overload-resolution_1.vb)]  
  
 [!code-vb[VbVbcnProcedures#63](./codesnippet/VisualBasic/overload-resolution_2.vb)]  
  
 Durante la prima chiamata il compilatore elimina il primo overload poiché il tipo del primo argomento \(`Short`\) esegue la conversione verso il tipo di dati più piccolo \(`Byte`\) del parametro corrispondente.  Viene quindi eliminato il terzo overload poiché ogni tipo di argomento del secondo overload \(`Short` e `Single`\) esegue la conversione verso il tipo di dati più grande corrispondente del terzo overload \(`Integer` e `Single`\).  Il secondo overload richiede un minore ampliamento dei dati e viene quindi utilizzato dal compilatore per la chiamata.  
  
 Durante la seconda chiamata il compilatore non è in grado di eliminare alcun overload in base al meccanismo della conversione verso un tipo di dati più piccolo.  Viene eliminato il terzo overload per lo stesso motivo indicato nella prima chiamata, in quanto è possibile chiamare il secondo overload con un ampliamento minore dei tipi degli argomenti.  Tuttavia, il compilatore non è in grado di scegliere tra il primo e il secondo overload.  Ciascun overload dispone di un tipo di parametro definito che viene convertito verso il tipo più grande corrispondente nell'altro overload \(`Byte` in `Short` e `Single` in `Double`\).  Il compilatore, di conseguenza, genera un errore di risoluzione dell'overload.  
  
## Argomenti di overload Optional e ParamArray  
 Se due overload di una routine hanno firme identiche con l'unica eccezione che l'ultimo parametro è dichiarato [Optional](../../../../visual-basic/language-reference/modifiers/optional.md) in uno e [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) nell'altro, il compilatore risolve una chiamata di tale routine nel modo seguente:  
  
|||  
|-|-|  
|Se l'ultimo argomento viene fornito dalla chiamata come|Il compilatore risolve la chiamata dell'overload dichiarando l'ultimo argomento come|  
|Nessun valore \(argomento omesso\)|`Optional`|  
|Un valore|`Optional`|  
|Due o più valori in un elenco separato da virgola|`ParamArray`|  
|Una matrice di qualunque lunghezza \(inclusa una matrice vuota\)|`ParamArray`|  
  
## Vedere anche  
 [Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [Parameter Arrays](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Troubleshooting Procedures](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [How to: Define Multiple Versions of a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md)   
 [How to: Call an Overloaded Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-overloaded-procedure.md)   
 [How to: Overload a Procedure that Takes Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [How to: Overload a Procedure that Takes an Indefinite Number of Parameters](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [Considerations in Overloading Procedures](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)   
 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md)   
 [Metodi di estensione](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)