---
title: "Dichiarazione di variabili in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "variabili [Visual Basic], dichiarazione"
  - "variabili membro, dichiarazioni"
  - "Dim (istruzione), dichiarazione di variabile"
  - "dichiarazione di variabili"
  - "variabili [Visual Basic], ambito"
  - "variabili [Visual Basic], tipi di dati"
  - "tipi di dati [Visual Basic], dichiarazioni di variabili"
  - "durata, variabili"
  - "variabili [Visual Basic], durata"
  - "livelli di accesso, variabili"
  - "ambito, istruzioni di dichiarazione"
  - "variabili [Visual Basic], livello di accesso"
  - "variabili locali, dichiarazioni"
  - "ambito, variabili"
ms.assetid: d8f10226-92b1-480f-9f53-df377b2d7e15
caps.latest.revision: 31
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 31
---
# Dichiarazione di variabili in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Si dichiara una variabile per specificarne il nome e le caratteristiche.  L'istruzione di dichiarazione delle variabili è l'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md).  La posizione e il contenuto di tale istruzione consentono di determinare le caratteristiche di una variabile.  
  
 Per considerazioni e regole relative alla denominazione delle variabili, vedere [Declared Element Names](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
## Livelli di dichiarazione  
  
### Variabili locali e membro  
 Una *variabile locale* è una variabile dichiarata all'interno di una routine.  Una *variabile membro* è membro di un tipo di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] e viene dichiarata a livello di modulo, all'interno di una classe, una struttura o un modulo, ma non di una routine interna alla classe, alla struttura o al modulo in questione.  
  
### Variabili condivise e di istanza  
 In una classe o struttura, la categoria di una variabile membro dipende dal fatto che sia o meno condivisa.  Se viene dichiarata con la parola chiave [Shared](../../../../visual-basic/language-reference/modifiers/shared.md), si tratta di una *variabile condivisa*, di cui esiste una copia unica condivisa tra tutte le istanze della classe o struttura.  
  
 In caso contrario, si tratta di una *variabile di istanza*, della quale viene creata una copia distinta per ogni istanza della classe o struttura.  Una copia specifica di una variabile di istanza è disponibile solo all'istanza di classe o struttura in cui è stata creata.  È indipendente da una copia della variabile di istanza in un'altra istanza della classe o struttura.  
  
## Dichiarazione del tipo di dati  
 La clausola [As](../../../../visual-basic/language-reference/statements/as-clause.md) nell'istruzione di dichiarazione consente di definire il tipo di dati o di oggetti della variabile dichiarata.  È possibile specificare ciascuno dei tipi che seguono per una variabile:  
  
-   Un tipo di dati di base, come `Boolean`, `Long`o `Decimal`  
  
-   Un tipo di dati composito, come una matrice o struttura  
  
-   Un tipo di oggetto o classe definito nella propria o in un'altra applicazione  
  
-   Una classe [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)], ad esempio <xref:System.Windows.Forms.Label> o <xref:System.Windows.Forms.TextBox>  
  
-   Un tipo di interfaccia, come <xref:System.IComparable> o <xref:System.IDisposable>  
  
 È possibile dichiarare diverse variabili in un'istruzione senza necessità di ripetere il tipo di dati.  Nelle istruzioni che seguono le variabili `i`, `j` e `k` vengono dichiarate come tipo `Integer`, `l` e `m` come `Long`, `x` e `y` come `Single`:  
  
```  
Dim i, j, k As Integer  
' All three variables in the preceding statement are declared as Integer.  
Dim l, m As Long, x, y As Single  
' In the preceding statement, l and m are Long, x and y are Single.  
```  
  
 Per ulteriori informazioni sui tipi di dati, vedere [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md).  Per ulteriori informazioni sugli oggetti, vedere [Objects and Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md) e [Programming with Components](../Topic/Programming%20with%20Components.md).  
  
## Inferenza del tipo di variabile locale  
 L'*inferenza del tipo* consente di determinare i tipi di dati delle variabili locali dichiarate senza una clausola `As`.  Tramite l'inferenza, il compilatore deduce il tipo della variabile dal tipo dell'espressione di inizializzazione  consentendo di dichiarare le variabili senza dichiarare in modo esplicito un tipo.  Nell'esempio seguente `num1` e `num2` sono fortemente tipizzati come integer.  
  
 [!code-vb[VbVbalrTypeInference#1](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/variable-declaration_1.vb)]  
  
 Se si desidera utilizza l'inferenza del tipo di variabile locale, è necessario che `Option Infer` sia impostato su `On`.  Per ulteriori informazioni, vedere [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md) e [Option Infer Statement](../../../../visual-basic/language-reference/statements/option-infer-statement.md).  
  
## Caratteristiche delle variabili dichiarate  
 La *durata* di una variabile è il periodo di tempo durante il quale essa è disponibile per l'utilizzo.  In genere, la durata di una variabile corrisponde a quella dell'elemento che la dichiara, ad esempio una routine o una classe.  Se non è necessario che la variabile abbia oltre la durata dell'elemento contenitore, non è necessario eseguire alcuna operazione speciale nella dichiarazione.  In caso contrario, è possibile includere la parola chiave `Static` o `Shared` nella relativa istruzione `Dim`.  Per ulteriori informazioni, vedere [Lifetime in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md).  
  
 L'*ambito* di una variabile è l'insieme dei frammenti di codice che possono farvi riferimento senza la qualifica del nome.  L'ambito di una variabile dipende dalla posizione in cui viene dichiarata.  Il codice di una determinata area può utilizzare le variabili definite in quell'area, senza che sia necessario qualificarne i nomi.  Per ulteriori informazioni, vedere [Scope in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md).  
  
 Il *livello di accesso* di una variabile corrisponde all'estensione del codice che dispone dell'autorizzazione ad accedervi.  Tale livello è determinato dal modificatore di accesso, quale [Public](../../../../visual-basic/language-reference/modifiers/public.md) o [Private](../../../../visual-basic/language-reference/modifiers/private.md), utilizzato nell'istruzione `Dim`.  Per ulteriori informazioni, vedere [Access Levels in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
## Vedere anche  
 [How to: Create a New Variable](../../../../visual-basic/programming-guide/language-features/variables/how-to-create-a-new-variable.md)   
 [How to: Move Data Into and Out of a Variable](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md)   
 [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Protected](../../../../visual-basic/language-reference/modifiers/protected.md)   
 [Friend](../../../../visual-basic/language-reference/modifiers/friend.md)   
 [Static](../../../../visual-basic/language-reference/modifiers/static.md)   
 [Declared Element Characteristics](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Infer Statement](../../../../visual-basic/language-reference/statements/option-infer-statement.md)