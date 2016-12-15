---
title: "Object Variable Declaration (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "early binding"
  - "declarations, class"
  - "classes [Visual Basic], declaring"
  - "binding, late and early"
  - "object variables, declaring"
  - "variables [Visual Basic], object"
  - "declaring variables, object variables"
  - "declaring classes"
  - "late binding"
ms.assetid: 2a5a41a3-1aa8-4236-b1f0-2382af7bf715
caps.latest.revision: 33
caps.handback.revision: 33
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Object Variable Declaration (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Per dichiarare una variabile oggetto è possibile utilizzare una normale istruzione di dichiarazione.  Per il tipo di dati è necessario specificare `Object` \(ovvero il [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)\) o una classe più specifica dalla quale deve essere creato l'oggetto.  
  
 La dichiarazione di una variabile come `Object` equivale alla dichiarazione della stessa come <xref:System.Object?displayProperty=fullName>.  
  
 Quando viene dichiarata con una classe oggetto specifica, una variabile può accedere a tutti i metodi e le proprietà esposti da tale classe e dalle classi da cui eredita.  Se viene dichiarata con <xref:System.Object>, la variabile potrà accedere soltanto ai membri della classe <xref:System.Object>, a meno che non si imposti `Option Strict Off` per consentire l'associazione tardiva.  
  
## Sintassi di dichiarazione  
 Per dichiarare una variabile oggetto, utilizzare la sintassi seguente:  
  
```  
Dim variablename As [New] { objectclass | Object }  
```  
  
 Nella dichiarazione è anche possibile specificare [Public](../../../../visual-basic/language-reference/modifiers/public.md), [Protected](../../../../visual-basic/language-reference/modifiers/protected.md), [Friend](../../../../visual-basic/language-reference/modifiers/friend.md), `Protected Friend`, [Private](../../../../visual-basic/language-reference/modifiers/private.md), [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) o [Static](../../../../visual-basic/language-reference/modifiers/static.md).  Le seguenti dichiarazioni di esempio sono valide:  
  
```  
Private objA As Object  
Static objB As System.Windows.Forms.Label  
Dim objC As System.OperatingSystem  
```  
  
## Associazione tardiva e associazione anticipata  
 Talvolta la classe specifica è sconosciuta fino all'esecuzione del codice.  In questo caso, è necessario dichiarare la variabile oggetto con il tipo di dati `Object`.  In questo modo viene creato un riferimento generale a un tipo qualsiasi di oggetto e la classe specifica viene assegnata in fase di esecuzione.  Questa operazione è detta *associazione tardiva*.  L'associazione tardiva richiede un tempo di esecuzione maggiore  e consente di utilizzare nel codice soltanto i metodi e le proprietà dell'ultima classe assegnata.  Se viene effettuato un tentativo di accesso ai membri di una classe diversa, è possibile che si verifichino errori di run\-time.  
  
 Quando la classe specifica è nota in fase di compilazione, è preferibile dichiarare la variabile oggetto come appartenente a tale classe.  Questa operazione viene definita *associazione anticipata*.  L'associazione anticipata consente di migliorare le prestazioni e consente l'accesso del codice a tutti i metodi e le proprietà della classe specifica.  Nelle dichiarazioni di esempio precedenti, se la variabile `objA` utilizza soltanto oggetti della classe <xref:System.Windows.Forms.Label?displayProperty=fullName>, è necessario specificare `As System.Windows.Forms.Label` nella relativa dichiarazione.  
  
### Vantaggi dell'associazione anticipata  
 La dichiarazione di una variabile oggetto come classe specifica offre diversi vantaggi:  
  
-   Controllo automatico dei tipi  
  
-   Accesso garantito a tutti i membri della classe specifica  
  
-   Supporto Microsoft IntelliSense nell'editor di codice  
  
-   Migliore leggibilità del codice  
  
-   Minore numero di errori nel codice  
  
-   Rilevazione degli errori in fase di compilazione anziché in fase di esecuzione  
  
-   Esecuzione più rapida del codice  
  
## Accesso ai membri delle variabili oggetto  
 Quando `Option Strict` è impostata su `On`, una variabile oggetto può accedere soltanto ai metodi e alle proprietà della classe con la quale è stata dichiarata.  Questa condizione è illustrata nell'esempio che segue.  
  
```  
' Option statements must precede all other source file lines.  
Option Strict On  
' Imports statement must precede all declarations in the source file.  
Imports System.Windows.Forms  
Public Sub accessMembers()  
    Dim p As Object  
    Dim q As System.Windows.Forms.Label  
    p = New System.Windows.Forms.Label  
    q = New System.Windows.Forms.Label  
    Dim j, k As Integer  
    ' The following statement generates a compiler ERROR.  
    j = p.Left  
    ' The following statement retrieves the left edge of the label in pixels.  
    k = q.Left  
End Sub  
```  
  
 In questo esempio, `p` può utilizzare soltanto i membri della classe <xref:System.Object>, che non includono la proprietà `Left`.  D'altra parte, la variabile `q` è stata dichiarata di tipo <xref:System.Windows.Forms.Label> e può quindi utilizzare tutti i metodi e le proprietà della classe <xref:System.Windows.Forms.Label> nello spazio dei nomi <xref:System.Windows.Forms>.  
  
## Flessibilità delle variabili oggetto  
 Quando si utilizzano gli oggetti in una gerarchia di ereditarietà, è possibile scegliere la classe da utilizzare per dichiarare le variabili oggetto.  Nell'effettuare la scelta, è necessario bilanciare la flessibilità dell'assegnazione all'oggetto e l'accesso ai membri di una classe.  Si consideri, ad esempio, la gerarchia di ereditarietà che rimanda alla classe <xref:System.Windows.Forms.Form?displayProperty=fullName>:  
  
 <xref:System.Object>  
  
 `` <xref:System.ComponentModel.Component>  
  
 `` <xref:System.Windows.Forms.Control>  
  
 `` <xref:System.Windows.Forms.ScrollableControl>  
  
 `` <xref:System.Windows.Forms.ContainerControl>  
  
 `` <xref:System.Windows.Forms.Form>  
  
 Si supponga che l'applicazione definisca una classe di form denominata `specialForm`, che eredita dalla classe <xref:System.Windows.Forms.Form>.  È possibile dichiarare una variabile oggetto che faccia riferimento in modo specifico a `specialForm`, come illustrato nel seguente esempio.  
  
<CodeContentPlaceHolder>3</CodeContentPlaceHolder>  
 La dichiarazione nell'esempio precedente limita la variabile `nextForm` agli oggetti della classe `specialForm`, ma rende anche tutti i metodi e le proprietà della classe `specialForm` disponibili per `nextForm` e per tutti i membri di tutte le classi dalle quali `specialForm` eredita.  
  
 È possibile rendere più generale una variabile oggetto dichiarandola di tipo <xref:System.Windows.Forms.Form>, come illustrato di seguito.  
  
<CodeContentPlaceHolder>4</CodeContentPlaceHolder>  
 La dichiarazione nell'esempio precedente consente di assegnare a `anyForm` un qualsiasi form presente nell'applicazione.  Tuttavia, sebbene possa accedere a tutti i membri della classe <xref:System.Windows.Forms.Form>, `anyForm` non può utilizzare le proprietà o i metodi aggiuntivi definiti per form specifici, ad esempio `specialForm`.  
  
 Tutti i membri di una classe base sono disponibili per le classi derivate, ma i membri aggiuntivi di una classe derivata non sono disponibili per la classe base.  
  
## Vedere anche  
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Object Variable Assignment](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [Object Variable Values](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [How to: Declare an Object Variable and Assign an Object to It in Visual Basic](../../../../visual-basic/programming-guide/language-features/variables/how-to-declare-an-object-variable-and-assign-an-object-to-it.md)   
 [How to: Access Members of an Object](../../../../visual-basic/programming-guide/language-features/variables/how-to-access-members-of-an-object.md)   
 [New Operator](../../../../visual-basic/language-reference/operators/new-operator.md)   
 [Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)