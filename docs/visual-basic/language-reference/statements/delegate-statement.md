---
title: "Delegate Statement | Microsoft Docs"
ms.custom: ""
ms.date: "12/08/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Delegate"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "delegate keyword"
  - "Delegate statement"
ms.assetid: f799c518-0817-40cc-ad0b-4da846fdba57
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Delegate Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Viene utilizzata per dichiarare un delegato.  Per delegato si intende un tipo di riferimento associato a un metodo `Shared` di un tipo o a un metodo di istanza di un oggetto.  Per creare un'istanza della classe delegata, è possibile utilizzare qualsiasi routine con tipi di parametri e tipi restituiti corrispondenti.  La routine può in seguito essere richiamata attraverso l'istanza di delegato.  
  
## Sintassi  
  
```  
[ <attrlist> ] [ accessmodifier ] _  
[ Shadows ] Delegate [ Sub | Function ] name [( Of typeparamlist )] [([ parameterlist ])] [ As type ]  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`attrlist`|Parametro facoltativo.  Elenco di attributi applicabili al delegato.  Gli attributi sono separati da una virgola.  È necessario racchiudere l'[Attribute List](../../../visual-basic/language-reference/statements/attribute-list.md) tra parentesi angolari \("`<`" e "`>`"\).|  
|`accessmodifier`|Parametro facoltativo.  Consente di specificare il tipo di codice che può accedere al delegato,  ad esempio uno dei seguenti:<br /><br /> -   [Public](../../../visual-basic/language-reference/modifiers/public.md).  Può accedere al delegato qualsiasi codice che sia in grado di accedere all'elemento che lo dichiara.<br />-   [Protected](../../../visual-basic/language-reference/modifiers/protected.md).  Può accedere al delegato solo il codice incluso nella relativa classe o in una classe derivata.<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md).  Può accedere al delegato solo il codice incluso nello stesso assembly.<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md).  Può accedere al delegato solo il codice incluso nell'elemento che lo dichiara.<br /><br /> È possibile specificare `Protected Friend` per consentire l'accesso dal codice incluso nella classe del delegato, in una classe derivata o nello stesso assembly.|  
|`Shadows`|Parametro facoltativo.  Indica che il delegato ridichiara e nasconde un elemento di programmazione omonimo, o un insieme di elementi di overload, di una classe base.  È possibile nascondere qualsiasi tipo di elemento dichiarato con qualsiasi altro tipo.<br /><br /> Un elemento nascosto non è disponibile all'interno della classe derivata che lo nasconde, a meno che l'elemento di shadowing sia inaccessibile.  Se, ad esempio, un elemento `Private` nasconde un elemento della classe base, il codice che non dispone dell'autorizzazione per accedere all'elemento `Private` accede invece all'elemento della classe base.|  
|`Sub`|Facoltativa. È necessario che sia specificato `Sub` o `Function`.  Consente di dichiarare la routine come delegata di tipo `Sub` senza la restituzione di un valore.|  
|`Function`|Facoltativa. È necessario che sia specificato `Sub` o `Function`.  Consente di dichiarare la routine come delegata di tipo `Function` con la restituzione di un valore.|  
|`name`|Obbligatorio.  Nome del tipo delegato. È necessario che sia conforme alle convenzioni di denominazione standard delle variabili.|  
|`typeparamlist`|Parametro facoltativo.  Elenco di parametri di tipo per il delegato.  I parametri sono separati da una virgola.  Se lo si desidera, è possibile dichiarare ogni parametro di tipo come variant utilizzando i modificatori generici `In` e `Out`.  L'[Type List](../../../visual-basic/language-reference/statements/type-list.md) deve essere racchiuso tra parentesi e introdotto dalla parola chiave `Of`.|  
|`parameterlist`|Parametro facoltativo.  Elenco dei parametri passati alla routine al momento della relativa chiamata.  L'[Parameter List](../../../visual-basic/language-reference/statements/parameter-list.md) deve essere racchiuso tra parentesi.|  
|`type`|Obbligatoria se viene specificata una routine `Function`.  Tipo di dati del valore restituito.|  
  
## Note  
 L'istruzione `Delegate` consente di definire i tipi di parametri e i tipi restituiti di una classe delegata.  Per creare un'istanza della classe delegata, è possibile utilizzare qualsiasi routine con tipi di parametri e tipi restituiti corrispondenti.  La routine può essere utilizzata in seguito attraverso l'istanza del delegato chiamando il metodo `Invoke` del delegato.  
  
 I delegati possono essere dichiarati a livello di spazio dei nomi, modulo, classe o struttura, ma non all'interno di routine.  
  
 Ogni classe delegata definisce un costruttore al quale viene passata la specifica di un metodo di oggetto.  Un argomento di un costruttore di delegato deve essere un riferimento a un metodo o a un'espressione lambda.  
  
 Per specificare un riferimento a un metodo, utilizzare la seguente sintassi:  
  
 `AddressOf` \[`expression`.\]`methodname`  
  
 In fase di compilazione per il tipo di `expression` è necessario specificare il nome di una classe o di un'interfaccia contenente un metodo con il nome specificato e con firma corrispondente a quella della classe delegata.  `methodname` può essere un metodo condiviso o di istanza  ma `methodname`non è facoltativo, anche se si crea un delegato per il metodo predefinito della classe.  
  
 Per specificare un'espressione lambda, utilizzare la seguente sintassi:  
  
 `Function` \(\[`parm` As `type`, `parm2` As `type2`, ...\]\) `expression`  
  
 La firma della funzione deve corrispondere a quella del tipo delegato.  Per ulteriori informazioni sulle espressioni lambda, vedere [Lambda Expressions](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
 Per ulteriori informazioni sui delegati, vedere [Delegates](../../../visual-basic/programming-guide/language-features/delegates/delegates.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'istruzione `Delegate` viene utilizzata per dichiarare un delegato che consenta di eseguire operazioni su due numeri e restituire un numero.  Il metodo `DelegateTest` accetta un'istanza di tale tipo di delegato e la utilizza per eseguire operazioni su una coppia di numeri.  
  
 [!code-vb[VbVbalrDelegates#14](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegate-statement_1.vb)]  
  
## Vedere anche  
 [AddressOf Operator](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Of](../../../visual-basic/language-reference/statements/of-clause.md)   
 [Delegates](../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [Procedura: utilizzare una classe generica](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Covarianza e controvarianza](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md)   
 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)   
 [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)