---
title: "Interface Statement (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Interface"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "interface statement [Visual Basic]"
  - "interfaces, interface definition"
ms.assetid: 8997af73-bda3-4f79-bd41-ca396b610260
caps.latest.revision: 26
caps.handback.revision: 26
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Interface Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Dichiara il nome di un'interfaccia e introduce le definizioni dei membri che essa comprende.  
  
## Sintassi  
  
```  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] _  
Interface name [ ( Of typelist ) ]  
    [ Inherits interfacenames ]  
    [ [ modifiers ] Property membername ]  
    [ [ modifiers ] Function membername ]  
    [ [ modifiers ] Sub membername ]  
    [ [ modifiers ] Event membername ]  
    [ [ modifiers ] Interface membername ]  
    [ [ modifiers ] Class membername ]  
    [ [ modifiers ] Structure membername ]  
End Interface  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`attributelist`|Parametro facoltativo.  Vedere [Elenco degli attributi](../../../visual-basic/language-reference/statements/attribute-list.md).|  
|`accessmodifier`|Parametro facoltativo.  ad esempio uno dei seguenti:<br /><br /> -   [Public](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md)<br />-   `Protected Friend`<br /><br /> Vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).|  
|`Shadows`|Parametro facoltativo.  Vedere [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md).|  
|`name`|Obbligatorio.  Nome dell'interfaccia.  Per informazioni, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
|`Of`|Parametro facoltativo.  Specifica che si tratta di un'interfaccia generica.|  
|`typelist`|Obbligatorio se si utilizza la parola chiave [Of](../../../visual-basic/language-reference/statements/of-clause.md).  Elenco di parametri di tipo per l'interfaccia.  Se lo si desidera, è possibile dichiarare ogni parametro di tipo come variant utilizzando i modificatori generici `In` e `Out`.  Vedere [Elenco dei tipi](../../../visual-basic/language-reference/statements/type-list.md).|  
|`Inherits`|Parametro facoltativo.  Indica che l'interfaccia eredita gli attributi e i membri di un'altra o di altre interfacce.  Vedere [Inherits Statement](../../../visual-basic/language-reference/statements/inherits-statement.md).|  
|`interfacenames`|Obbligatoria se si utilizza l'istruzione `Inherits`.  Nomi delle interfacce dalle quali deriva lì'interfaccia.|  
|`modifiers`|Parametro facoltativo.  Modificatori corretti per il membro dell'interfaccia in corso di definizione.|  
|`Property`|Parametro facoltativo.  Definisce una proprietà che è un membro dell'interfaccia.|  
|`Function`|Parametro facoltativo.  Definisce una routine `Function` che è un membro dell'interfaccia.|  
|`Sub`|Parametro facoltativo.  Definisce una routine `Sub` che è un membro dell'interfaccia.|  
|`Event`|Parametro facoltativo.  Definisce un evento che è un membro dell'interfaccia.|  
|`Interface`|Parametro facoltativo.  Definisce un'interfaccia annidata all'interno di questa interfaccia.  La definizione dell'interfaccia annidata deve terminare con un'istruzione `End Interface`.|  
|`Class`|Parametro facoltativo.  Definisce una classe che è un membro dell'interfaccia.  La definizione della classe membro deve terminare con un'istruzione `End Class`.|  
|`Structure`|Parametro facoltativo.  Definisce una struttura che è un membro dell'interfaccia.  La definizione della struttura membro deve terminare con un'istruzione `End Structure`.|  
|`membername`|Obbligatorio per ogni proprietà, routine, evento, interfaccia, classe o struttura definita come membro dell'interfaccia.  Nome del membro.|  
|`End Interface`|Termina la definizione di `Interface`.|  
  
## Note  
 Un'*interfaccia* definisce un insieme di membri, come ad esempio proprietà e routine, che classi e strutture possono implementare.  L'interfaccia definisce soltanto le firme dei membri e non il loro funzionamento interno.  
  
 Una classe o una struttura implementa l'interfaccia fornendo il codice per ogni membro definito dall'interfaccia.  Infine, quando l'applicazione creerà un'istanza da quella classe o struttura, esisterà un oggetto che verrà eseguito in memoria.  Per ulteriori informazioni, vedere [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md) e [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md).  
  
 È possibile utilizzare `Interface` solo a livello di modulo o di spazio dei nomi.  In altri termini, il *contesto della dichiarazione* per un'interfaccia deve essere costituito da un file di origine, uno spazio dei nomi, una classe, una struttura, un modulo o un'interfaccia, ma non una routine o un blocco.  Per ulteriori informazioni, vedere [Declaration Contexts and Default Access Levels](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 L'accesso predefinito per le interfacce è di tipo [Friend](../../../visual-basic/language-reference/modifiers/friend.md).  È possibile modificarne i livelli di accesso mediante gli appositi modificatori.  Per ulteriori informazioni, vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
## Regole  
  
-   **Annidamento delle interfacce.** È possibile definire un'interfaccia all'interno di un'altra.  L'interfaccia esterna viene detta *interfaccia contenitore*, mentre l'interfaccia interna viene detta *interfaccia annidata*.  
  
-   **Dichiarazione di membro.** Quando si dichiara una proprietà o una routine come membro di un'interfaccia, si definisce soltanto la *firma* di tale proprietà o routine.  Questa comprende il tipo di elemento \(proprietà o routine\), i suoi parametri e i tipi di parametri e il tipo restituito.  Per questa ragione, la definizione del membro utilizza soltanto una riga di codice e le istruzioni di chiusura come `End Function` o `End Property` in un'interfaccia non sono valide.  
  
     Al contrario, quando si definisce un'enumerazione o una struttura o una classe o un'interfaccia annidata, è necessario includerne i membri dati.  
  
-   **Modificatori di membri.** Quando si definiscono i membri dei moduli, non è possibile utilizzare modificatori di accesso, né specificare [Shared](../../../visual-basic/language-reference/modifiers/shared.md) o qualsiasi altro modificatore di routine ad eccezione di [Overloads](../../../visual-basic/language-reference/modifiers/overloads.md).  È possibile dichiarare qualsiasi membro con [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md) e utilizzare [Default](../../../visual-basic/language-reference/modifiers/default.md), [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md) o [WriteOnly](../../../visual-basic/language-reference/modifiers/writeonly.md) nella definizione di una proprietà.  
  
-   **Ereditarietà.** Se l'interfaccia utilizza l'[Inherits Statement](../../../visual-basic/language-reference/statements/inherits-statement.md), è possibile specificare una o più interfacce di base.  È possibile ereditare da due interfacce anche se ognuna di esse definisce un membro con lo stesso nome.  In questo caso il codice di implementazione deve utilizzare la qualifica per specificare quale membro sta implementando.  
  
     Un'interfaccia non può ereditare da un'altra interfaccia con un livello di accesso più restrittivo.  Un'interfaccia `Public`, ad esempio, non può ereditare da un'interfaccia con accesso `Friend`.  
  
     Un'interfaccia non può ereditare da un'interfaccia annidata all'interno di essa.  
  
-   **Implementazione.** Quando una classe utilizza l'istruzione [Implements](../../../visual-basic/language-reference/statements/implements-clause.md) per implementare questa interfaccia, deve implementare ogni membro definito all'interno dell'interfaccia.  Ogni firma del codice di implementazione, inoltre, deve corrispondere esattamente alla firma equivalente definita nell'interfaccia.  Il nome del membro nel codice di implementazione, tuttavia, non deve corrispondere al nome del membro definito nell'interfaccia.  
  
     Quando una classe implementa una routine, quest'ultima non può essere designata come `Shared`.  
  
-   **Proprietà predefinita.** Un'interfaccia può specificare al massimo una proprietà come *proprietà predefinita*, a cui si può fare riferimento senza utilizzare il nome della proprietà.  Questa proprietà viene specificata dichiarandola con il modificatore [Default](../../../visual-basic/language-reference/modifiers/default.md).  
  
     Tenere presente che questo significa che un'interfaccia può definire una proprietà predefinita soltanto se non ne eredita nessuna.  
  
## Comportamento  
  
-   **Livello di accesso.** Tutti i membri dell'interfaccia devono disporre in modo implicito di accesso di tipo [Public](../../../visual-basic/language-reference/modifiers/public.md).  Quando si definisce un membro non è consentito utilizzare alcun modificatore di accesso.  Una classe che implementa l'interfaccia può tuttavia dichiarare un livello di accesso per ciascun membro implementato.  
  
     Se si assegna un'istanza di classe a una variabile, il livello di accesso dei suoi membri può essere diverso a seconda che il tipo di dati della variabile sia l'interfaccia sottostante o la classe che la implementa.  Questa condizione è illustrata nell'esempio che segue.  
  
     [!code-vb[VbVbalrStatements#39](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/interface-statement_1.vb)]  
  
     Se si accede ai membri della classe attraverso `varAsInterface`, essi avranno tutti un accesso di tipo Public.  Se invece si accede ai membri attraverso `varAsClass`, la routine `Sub` `doSomething` è caratterizzata da un accesso di tipo Private.  
  
-   **Ambito.** L'ambito di un'interfaccia corrisponde allo spazio dei nomi, alla classe, alla struttura o al modulo propri dell'interfaccia.  
  
     L'ambito di ogni membro dell'interfaccia è l'intera interfaccia.  
  
-   **Durata.** Un'interfaccia di per sé non ha una durata, né l'hanno i suoi membri.  Quando una classe implementa un'interfaccia e viene creato un oggetto come istanza di quella classe, l'oggetto ha una durata all'interno dell'applicazione in cui è in esecuzione.  Per ulteriori informazioni, vedere "Durata" in [Class Statement](../../../visual-basic/language-reference/statements/class-statement.md).  
  
## Esempio  
 Nell'esempio seguente l'istruzione `Interface` viene utilizzata per definire un'interfaccia denominata `thisInterface` che richiede l'implementazione con un'istruzione `Property` e un'istruzione `Function`.  
  
 [!code-vb[VbVbalrStatements#40](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/interface-statement_2.vb)]  
  
 Osservare che le istruzioni `Property` e `Function` non introducono blocchi che terminano con `End Property` e `End Function` all'interno dell'interfaccia.  L'interfaccia definisce soltanto le firme dei suoi membri.  I blocchi `Property` e `Function` completi compaiono in una classe che implementa `thisInterface`.  
  
## Vedere anche  
 [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md)   
 [Class Statement](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Module Statement](../../../visual-basic/language-reference/statements/module-statement.md)   
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Varianza nelle interfacce generiche](../Topic/Variance%20in%20Generic%20Interfaces%20\(C%23%20and%20Visual%20Basic\).md)   
 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)   
 [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)