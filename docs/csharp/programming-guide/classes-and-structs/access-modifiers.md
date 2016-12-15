---
title: "Modificatori di accesso (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "modificatori di accesso [C#], informazioni"
  - "Linguaggio C#, modificatori di accesso"
ms.assetid: 6e81ee82-224f-4a12-9baf-a0dca2656c5b
caps.latest.revision: 32
caps.handback.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Modificatori di accesso (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Tutti i tipi e i membri dei tipi prevedono un livello di accessibilità che controlla se possono essere utilizzati da altro codice nell'assembly o in altri assembly.  È possibile utilizzare i seguenti modificatori di accesso per specificare l'accessibilità di un tipo o di un membro durante la relativa dichiarazione:  
  
 [public](../../../csharp/language-reference/keywords/public.md)  
 Il tipo o il membro è accessibile da altro codice nello stesso assembly o in un altro assembly che vi fa riferimento.  
  
 [private](../../../csharp/language-reference/keywords/private.md)  
 Il tipo o il membro è accessibile solo dal codice nella stessa classe o struttura.  
  
 [protected](../../../csharp/language-reference/keywords/protected.md)  
 Il tipo o il membro è accessibile solo dal codice nella stessa classe o struttura o in una classe derivata dalla prima.  
  
 [internal](../../../csharp/language-reference/keywords/internal.md)  
 Il tipo o il membro è accessibile dal codice nello stesso assembly ma non da un altro assembly.  
  
 `protected internal`  
 Il tipo o il membro è accessibile dal codice nello stesso assembly in cui è dichiarato o da una classe derivata in un altro assembly.  L'accesso da un altro assembly deve avvenire all'interno di una dichiarazione di classe che deriva dalla classe in cui l'elemento interno protetto viene dichiarato e tramite un'istanza del tipo di classe derivata.  
  
 Negli esempi seguenti viene illustrato come specificare i modificatori di accesso su un tipo e su un membro:  
  
 [!code-cs[csProgGuideObjects#72](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/access-modifiers_1.cs)]  
  
 Non tutti i modificatori di accesso possono essere utilizzati da tutti i tipi o membri in tutti i contesti e in alcuni casi l'accessibilità di un membro di un tipo è vincolata da quella del tipo che lo contiene.  Nelle sezioni seguenti sono fornite ulteriori informazioni sull'accessibilità.  
  
## Accessibilità a classi e strutture  
 Classi e struct dichiarate direttamente all'interno di uno spazio dei nomi ovvero che non sono annidate all'interno di altre classi o struct,  possono essere pubbliche o interne.  Per impostazione predefinita, se non viene specificato alcun modificatore di accesso, sono interne.  
  
 I membri struct, incluse le strutture e le classi annidate, possono essere dichiarate pubbliche, interne o private.  I membri della classe, incluse le classi annidate e le strutture, possono essere public, protected internal, protected, internal o private.  Il livello di accesso per i membri della classe e i membri struct, comprese strutture e classi annidate, è privato per impostazione predefinita.  I tipi annidati privati non sono accessibili dall'esterno del tipo che li contiene.  
  
 Le classi derivate non possono avere un'accessibilità maggiore di quella dei relativi tipi di base.  In altri termini, non è possibile disporre di una classe pubblica `B` che deriva da una classe interna `A`.  Se questo scenario fosse consentito, la classe `A` diventerebbe pubblica, perché tutti i membri protetti o interni di `A` sono accessibili dalla classe derivata.  
  
 È possibile consentire ad altri assembly specifici di accedere ai tipi interni utilizzando InternalsVisibleToAttribute.  Per ulteriori informazioni, vedere [Assembly friend](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Accessibilità a membri di classi e strutture  
 I membri delle classi \(incluse classi e strutture annidate\) possono essere dichiarati con uno dei cinque tipi di accesso disponibili.  I membri delle strutture non possono essere dichiarati come protetti perché le strutture non supportano l'ereditarietà.  
  
 Normalmente, l'accessibilità di un membro non può mai essere maggiore di quella del tipo che lo contiene.  Tuttavia, un membro pubblico di una classe interna potrebbe essere accessibile all'esterno dell'assembly se il membro implementa i metodi dell'interfaccia o esegue l'override dei metodi virtuali definiti in una classe base pubblica.  
  
 Il tipo del membro rappresentato da un campo, una proprietà o un evento deve essere accessibile almeno quanto il membro stesso.  Allo stesso modo, il tipo restituito e i tipi di parametro di qualsiasi membro che sia un metodo, un indicizzatore o un delegato devono essere almeno accessibili quanto il membro stesso.  Ad esempio, non è possibile disporre di un metodo `M` pubblico che restituisce una classe `C`, a meno che non sia pubblica anche `C`.  Analogamente, non è possibile disporre di una proprietà protetta di tipo `A` se `A` è dichiarato come privato.  
  
 Gli operatori definiti dall'utente devono essere sempre dichiarati come pubblici.  Per ulteriori informazioni, vedere [operatore](../../../csharp/language-reference/keywords/operator.md).  
  
 I distruttori non possono includere modificatori di accesso.  
  
 Per impostare il livello di accesso per il membro di una classe o di una struttura, aggiungere la parola chiave appropriata alla dichiarazione del membro, come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideObjects#73](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/access-modifiers_2.cs)]  
  
> [!NOTE]
>  Il livello di accessibilità interna protetto significa protetto O interno, non protetto E interno.  In altre parole, un membro interno protetto è accessibile da qualsiasi classe all'interno dello stesso assembly, incluso le classi derivate.  Per limitare l'accesso solo alle classi derivate presenti nello stesso assembly, dichiarare la classe stessa interna e dichiarare i relativi membri come protetti.  
  
## Altri tipi  
 Le interfacce dichiarate direttamente in uno spazio dei nomi possono essere dichiarate come pubbliche o interne e, analogamente alle classi e alle struct, per impostazione predefinita prevedono l'accesso interno.  I membri delle interfacce sono sempre pubblici, perché lo scopo di un'interfaccia è di consentire ad altri tipi l'accesso a una classe o a una struttura.  Non è possibile applicare modificatori di accesso ai membri delle interfacce.  
  
 I membri delle enumerazioni sono sempre pubblici e non è possibile applicare modificatori di accesso.  
  
 I delegati si comportano come le classi e le strutture.  Per impostazione predefinita, hanno accesso interno se dichiarati direttamente all'interno di uno spazio dei nomi e accesso se annidati.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Interfacce](../../../csharp/programming-guide/interfaces/index.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [interne](../../../csharp/language-reference/keywords/internal.md)   
 [Protected](../../../csharp/language-reference/keywords/protected.md)   
 [classe](../../../csharp/language-reference/keywords/class.md)   
 [struct](../../../csharp/language-reference/keywords/struct.md)   
 [interfaccia](../../../csharp/language-reference/keywords/interface.md)