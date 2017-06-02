---
title: "Dynamically Loading and Using Types | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "late binding, about late binding"
  - "early binding"
  - "dynamically loading and using types"
  - "implicit late binding"
  - "reflection, dynamically using types"
ms.assetid: db985bec-5942-40ec-b13a-771ae98623dc
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Dynamically Loading and Using Types
La reflection fornisce un'infrastruttura utilizzata da compilatori di linguaggio quali [!INCLUDE[vbprvbext](../../../includes/vbprvbext-md.md)] e JScript per implementare l'associazione tardiva implicita.  L'associazione è il processo di individuazione della dichiarazione \(ovvero l'implementazione\), che corrisponde a un tipo specificato in modo univoco.  Quando questo processo si verifica in fase di esecuzione anziché in fase di compilazione, viene denominato associazione tardiva.  [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)] consente di utilizzare l'associazione tardiva implicita nel codice. Il compilatore di Visual Basic chiama un metodo di supporto che utilizza la reflection per ottenere il tipo di oggetto.  Gli argomenti passati al metodo di supporto determinano la chiamata, in fase di esecuzione, del metodo appropriato.  Tali argomenti sono l'istanza \(un oggetto\) su cui richiamare il metodo, il nome del metodo chiamato \(una stringa\) e gli argomenti passati al metodo chiamato \(una matrice di oggetti\).  
  
 Nell'esempio che segue dal compilatore di Visual Basic viene utilizzata la reflection in modo implicito per chiamare un metodo su un oggetto il cui tipo non è noto in fase di compilazione.  Una classe **HelloWorld** dispone di un metodo **PrintHello** che accetta una stringa e stampa il testo "Hello World" seguito dalla stringa passata al metodo **PrintHello**.  Il metodo **PrintHello** chiamato in questo esempio è in realtà un <xref:System.Type.InvokeMember%2A?displayProperty=fullName>. Il codice di Visual Basic consente di richiamare il metodo **PrintHello** come se il tipo dell'oggetto \(helloObj\) fosse noto in fase di compilazione \(associazione anticipata\) anziché in fase di esecuzione \(associazione tardiva\).  
  
```  
Imports System  
Module Hello  
    Sub Main()  
        ' Sets up the variable.  
        Dim helloObj As Object  
        ' Creates the object.  
        helloObj = new HelloWorld()  
        ' Invokes the print method as if it was early bound  
        ' even though it is really late bound.  
        helloObj.PrintHello("Visual Basic Late Bound")  
    End Sub  
End Module  
```  
  
## Associazione personalizzata  
 Ai fini dell'associazione tardiva, oltre ad essere utilizzata in modo implicito dai compilatori, la reflection può essere utilizzata in modo esplicito nel codice.  
  
 [Common Language Runtime](../../../docs/standard/clr.md) supporta più linguaggi di programmazione e le regole di associazione di questi linguaggi differiscono.  Nel caso dell'associazione anticipata, l'associazione può essere controllata completamente dai generatori di codice.  Nell'associazione tardiva mediante reflection l'associazione deve essere invece controllata dall'associazione personalizzata.  La classe <xref:System.Reflection.Binder> fornisce il controllo personalizzato sulla selezione e la chiamata dei membri.  
  
 Utilizzando l'associazione personalizzata è possibile caricare un assembly in fase di esecuzione, ottenere informazioni sui tipi in esso contenuti, specificare il tipo desiderato e richiamarne i metodi o utilizzarne i campi o le proprietà.  Questa tecnica è utile se non si conosce il tipo di un oggetto in fase di compilazione, come avviene ad esempio quando il tipo di oggetto dipende dall'input dell'utente.  
  
 Nell'esempio di codice che segue viene illustrato un semplice gestore di associazione personalizzato da cui non viene fornita la conversione dei tipi degli argomenti.  L'esempio principale è preceduto dal codice per `Simple_Type.dll`.  Assicurarsi di compilare `Simple_Type.dll` e di includere nel progetto un riferimento ad esso durante la compilazione.  
  
 [!code-cpp[Conceptual.Types.Dynamic#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.dynamic/cpp/source1.cpp#1)]
 [!code-csharp[Conceptual.Types.Dynamic#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.dynamic/cs/source1.cs#1)]
 [!code-vb[Conceptual.Types.Dynamic#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.dynamic/vb/source1.vb#1)]  
  
### InvokeMember e CreateInstance  
 Utilizzare <xref:System.Type.InvokeMember%2A?displayProperty=fullName> per richiamare un membro di un tipo.  I metodi **CreateInstance** di varie classi, quali [System.Activator](frlrfSystemActivatorClassCreateInstanceTopic) e [System.Reflection.Assembly](frlrfSystemReflectionAssemblyClassCreateInstanceTopic), sono forme speciali di **InvokeMember** che creano nuove istanze del tipo specificato.  La classe **Binder** viene utilizzata per la risoluzione dell'overload e la conversione forzata dei tipi degli argomenti di questi metodi.  
  
 Nell'esempio che segue vengono illustrate le tre combinazioni possibili di coercizione degli argomenti \(conversione di tipo\) e selezione dei membri.  Nel caso 1 non è necessaria la selezione dei membri né la conversione forzata dei tipi degli argomenti.  Nel caso 2 è necessaria solo la selezione dei membri.  Nel caso 3 è necessaria solo la conversione forzata dei tipi degli argomenti.  
  
 [!code-cpp[Conceptual.Types.Dynamic#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.dynamic/cpp/source2.cpp#2)]
 [!code-csharp[Conceptual.Types.Dynamic#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.dynamic/cs/source2.cs#2)]
 [!code-vb[Conceptual.Types.Dynamic#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.dynamic/vb/source2.vb#2)]  
  
 La risoluzione dell'overload è necessaria quando vi sono più membri con lo stesso nome.  I metodi <xref:System.Reflection.Binder.BindToMethod%2A?displayProperty=fullName> e <xref:System.Reflection.Binder.BindToField%2A?displayProperty=fullName> vengono utilizzati per risolvere l'associazione a un singolo membro.  **Binder.BindToMethod** fornisce anche la risoluzione delle proprietà mediante le funzioni **get** e **set** per l'accesso alle proprietà.  
  
 **BindToMethod** restituisce il <xref:System.Reflection.MethodBase> da richiamare o un riferimento null \(**Nothing** in Visual Basic\) se non è possibile effettuare la chiamata.  **MethodBase** restituisce valori non necessariamente compresi tra quelli contenuti nel parametro *match*, sebbene questo sia il caso più frequente.  
  
 Quando sono presenti argomenti ByRef, è possibile che debbano essere restituiti al chiamante.  Se, pertanto, **BindToMethod** ha modificato la matrice di argomenti, **Binder** consentirà al client di eseguire il mapping della matrice di argomenti riportandola alla forma originale.  A tal fine, è necessario garantire al chiamante che l'ordine degli argomenti resti inalterato.  Quando gli argomenti vengono passati in base al nome, **Binder** riordina la matrice degli argomenti, che rappresenta quanto viene visualizzato al chiamante.  Per ulteriori informazioni, vedere <xref:System.Reflection.Binder.ReorderArgumentArray%2A?displayProperty=fullName>.  
  
 L'insieme dei membri disponibili è costituito dai membri definiti nel tipo o in qualsiasi tipo base.  Se si specifica [BindingFlags.NonPublic](frlrfSystemReflectionBindingFlagsClassTopic), il set restituito comprenderà membri di qualsiasi accessibilità.  Se **BindingFlags.NonPublic** non viene specificato, il meccanismo di associazione dovrà attivare le regole di accessibilità.  Quando si specifica il flag di associazione **Public** o **NonPublic** è necessario specificare anche il flag di associazione **Instance** o **Static**. In caso contrario non verrà restituito alcun membro.  
  
 Se vi è un solo membro del nome fornito, non occorrerà alcun callback e l'associazione verrà effettuata su tale metodo.  Nel caso 1 dell'esempio di codice viene illustrato questo punto: è disponibile un solo metodo **PrintBob** e, pertanto, il callback non è necessario.  
  
 Se nell'insieme disponibile vi sono più membri, tutti i metodi vengono passati a **BindToMethod**, che seleziona il metodo appropriato e lo restituisce.  Nel caso 2 dell'esempio di codice vi sono due metodi denominati **PrintValue**.  Il metodo appropriato viene selezionato dalla chiamata di **BindToMethod**.  
  
 <xref:System.Reflection.Binder.ChangeType%2A> esegue la conversione forzata dei tipi degli argomenti, convertendo gli argomenti effettivi nel tipo degli argomenti formali del metodo selezionato.  **ChangeType** viene chiamato per ciascun argomento anche se i tipi corrispondono esattamente.  
  
 Nel caso 3 dell'esempio di codice, un argomento effettivo di tipo **String** con valore "5.5" viene passato a un metodo con un argomento formale di tipo **Double**.  Affinché la chiamata riesca, il valore di stringa "5.5" deve essere convertito in un valore double.  La conversione viene eseguita da **ChangeType**.  
  
 Tramite **ChangeType** vengono eseguite solo [conversioni forzate verso tipi più grandi](../../../docs/standard/base-types/type-conversion.md), che non comportano perdita di informazioni, come illustrato nella tabella riportata di seguito.  
  
|Tipo di origine|Tipo di destinazione|  
|---------------------|--------------------------|  
|Qualsiasi tipo|Il relativo tipo base|  
|Qualsiasi tipo|L'interfaccia implementata|  
|Char|UInt16, UInt32, Int32, UInt64, Int64, Single e Double|  
|Byte|Char, UInt16, Int16, UInt32, Int32, UInt64, Int64, Single e Double|  
|SByte|Int16, Int32, Int64, Single e Double|  
|UInt16|UInt32, Int32, UInt64, Int64, Single e Double|  
|Int16|Int32, Int64, Single e Double|  
|UInt32|UInt64, Int64, Single e Double|  
|Int32|Int64, Single e Double|  
|UInt64|Single, Double|  
|Int64|Single, Double|  
|Single|Double|  
|Tipo non di riferimento|Tipo di riferimento|  
  
 La classe <xref:System.Type> dispone di metodi **Get** che utilizzano i parametri di tipo **Binder** per risolvere i riferimenti a un particolare membro.  <xref:System.Type.GetConstructor%2A?displayProperty=fullName>, <xref:System.Type.GetMethod%2A?displayProperty=fullName> e <xref:System.Type.GetProperty%2A?displayProperty=fullName> cercano un particolare membro del tipo corrente fornendo informazioni sulla relativa firma.  <xref:System.Reflection.Binder.SelectMethod%2A?displayProperty=fullName> e <xref:System.Reflection.Binder.SelectProperty%2A?displayProperty=fullName> vengono chiamati per selezionare le informazioni sulla firma dei metodi appropriati.  
  
## Vedere anche  
 <xref:System.Type.InvokeMember%2A?displayProperty=fullName>   
 <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>   
 [Viewing Type Information](../../../docs/framework/reflection-and-codedom/viewing-type-information.md)   
 [Conversione di tipi in .NET Framework](../../../docs/standard/base-types/type-conversion.md)