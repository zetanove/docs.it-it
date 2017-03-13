---
title: "Friend (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Friend"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Friend (parola chiave)"
  - "modificatore di accesso Friend"
  - "Friend (parola chiave), sintassi"
  - "Protected Friend (combinazione di parole chiave)"
  - "Friend (parola chiave), e Protected"
ms.assetid: b664605e-1c79-4728-b996-aa59c50846bc
caps.latest.revision: 25
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 25
---
# Friend (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica che uno o più elementi di programmazione sono accessibili solo dall'assembly che ne contiene la dichiarazione.  
  
## Note  
 In molti casi è opportuno che elementi di programmazione quali classi e strutture vengano utilizzati da tutto l'assembly, non solo dal componente che li dichiara.  Tuttavia, non possono risultare utili per essere accessibile dal codice esterno all'assembly \(ad esempio, se l'applicazione è privata\).  Se si desidera limitare l'accesso a un elemento in questo modo, è possibile dichiararlo utilizzando il modificatore di `Friend`.  
  
 Il codice incluso in altre classi, strutture e moduli compilati nello stesso assembly può accedere a tutti gli elementi `Friend` dell'assembly in questione.  
  
 l'accesso di`Friend` è spesso il livello preferito per gli elementi di programmazione di un'applicazione e `Friend` è il livello di accesso predefinito di interfaccia, modulo, di una classe, o di struttura.  
  
 È possibile utilizzare `Friend` solo al modulo, di interfaccia, o a livello di spazio dei nomi.  Di conseguenza, il contesto della dichiarazione per un elemento di `Friend` deve essere un file di origine, uno spazio dei nomi, un'interfaccia, di un modulo, una classe, una struttura, non può essere una routine.  
  
 È possibile utilizzare il modificatore `Friend` insieme al modificatore [Protected](../../../visual-basic/language-reference/modifiers/protected.md) nella stessa dichiarazione.  Questa combinazione conferisce entrambe accesso di `Friend` e accesso protetto sugli elementi dichiarati, pertanto sono accessibili da qualsiasi punto nello stesso assembly, dalla propria classe e le classi derivate.  È possibile specificare `Protected Friend` solo su membri di classi.  
  
 Per un confronto di `Friend` e gli altri modificatori di accesso, vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
> [!NOTE]
>  È possibile specificare che un altro assembly è un assembly Friend, che consente di accedere a tipi e membri contrassegnati come `Friend`.  Per ulteriori informazioni, vedere [Assembly friend](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Esempio  
 Nella classe seguente viene utilizzato il modificatore `Friend` per consentire agli altri elementi di programmazione all'interno dello stesso assembly di accedere a determinati membri.  
  
 [!code-vb[VbVbalrAccessModifiers#1](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/friend_1.vb)]  
  
## Utilizzo  
 È possibile utilizzare il modificatore di `Friend` in questi contesti:  
  
 [Istruzione Class](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Istruzione Const](../../../visual-basic/language-reference/statements/const-statement.md)  
  
 [Istruzione Declare](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Istruzione Delegate](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Istruzione Dim](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Istruzione Enum](../../../visual-basic/language-reference/statements/enum-statement.md)  
  
 [Istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Istruzione Interface](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Istruzione Module](../../../visual-basic/language-reference/statements/module-statement.md)  
  
 [Istruzione Property](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Istruzione Structure](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Istruzione Sub](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 [Public](../../../visual-basic/language-reference/modifiers/public.md)   
 [Protected](../../../visual-basic/language-reference/modifiers/protected.md)   
 [Private](../../../visual-basic/language-reference/modifiers/private.md)   
 [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [Procedures](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Structures](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)