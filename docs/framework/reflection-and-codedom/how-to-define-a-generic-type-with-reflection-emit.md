---
title: "How to: Define a Generic Type with Reflection Emit | Microsoft Docs"
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
  - "generics [.NET Framework], reflection emit"
  - "generics [.NET Framework], dynamic types"
  - "reflection emit, generic types"
ms.assetid: 07d5f01a-7b5b-40ea-9b15-f21561098fe4
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# How to: Define a Generic Type with Reflection Emit
In questo argomento viene illustrato come creare un tipo generico semplice con due parametri di tipo, nonché come applicare vincoli speciali, di classe e di interfaccia ai parametri di tipo e creare membri che utilizzano i parametri di tipo della classe come tipi di parametro o tipi restituiti.  
  
> [!IMPORTANT]
>  Un metodo non può essere considerato generico solo perché appartiene a un tipo generico e ne utilizza i parametri di tipo.  Per essere generico, un metodo deve disporre di uno specifico elenco di parametri di tipo.  La maggior parte dei metodi appartenenti a tipi generici non sono generici, come nell'esempio che segue.  Per un esempio di creazione di un metodo generico, vedere [How to: Define a Generic Method with Reflection Emit](../../../docs/framework/reflection-and-codedom/how-to-define-a-generic-method-with-reflection-emit.md).  
  
### Per definire un tipo generico  
  
1.  Definire un assembly dinamico denominato `GenericEmitExample1`.  Nell'esempio l'assembly viene eseguito e salvato su disco, pertanto è specificato <xref:System.Reflection.Emit.AssemblyBuilderAccess?displayProperty=fullName>.  
  
     [!code-cpp[EmitGenericType#2](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#2)]
     [!code-csharp[EmitGenericType#2](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#2)]
     [!code-vb[EmitGenericType#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#2)]  
  
2.  Definire un modulo dinamico.  Un assembly è composto da moduli eseguibili.  Per un assembly a modulo singolo, il nome del modulo è lo stesso dell'assembly e il nome del file corrisponde a quello del modulo seguito da un'estensione.  
  
     [!code-cpp[EmitGenericType#3](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#3)]
     [!code-csharp[EmitGenericType#3](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#3)]
     [!code-vb[EmitGenericType#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#3)]  
  
3.  Definire una classe.  In questo esempio la classe è denominata `Sample`.  
  
     [!code-cpp[EmitGenericType#4](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#4)]
     [!code-csharp[EmitGenericType#4](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#4)]
     [!code-vb[EmitGenericType#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#4)]  
  
4.  Definire i parametri di tipo generico di `Sample` passando una matrice di stringhe contenenti i nomi dei parametri al metodo <xref:System.Reflection.Emit.TypeBuilder.DefineGenericParameters%2A?displayProperty=fullName>.  In questo modo la classe diventa un tipo generico.  Il valore restituito è una matrice di oggetti <xref:System.Reflection.Emit.GenericTypeParameterBuilder> che rappresentano i parametri di tipo, che possono essere utilizzati nel codice creato.  
  
     Nel codice riportato di seguito la classe `Sample` diventa un tipo generico con parametri di tipo `TFirst` e `TSecond`.  Per migliorare la leggibilità del codice, ogni oggetto <xref:System.Reflection.Emit.GenericTypeParameterBuilder> viene inserito in una variabile che ha lo stesso nome del parametro di tipo.  
  
     [!code-cpp[EmitGenericType#5](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#5)]
     [!code-csharp[EmitGenericType#5](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#5)]
     [!code-vb[EmitGenericType#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#5)]  
  
5.  Aggiungere vincoli speciali ai parametri di tipo.  In questo esempio il parametro di tipo `TFirst` viene vincolato a tipi con costruttori senza parametri e a tipi di riferimento.  
  
     [!code-cpp[EmitGenericType#6](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#6)]
     [!code-csharp[EmitGenericType#6](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#6)]
     [!code-vb[EmitGenericType#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#6)]  
  
6.  Facoltativamente, aggiungere vincoli di interfaccia e di classe ai parametri di tipo.  In questo esempio il parametro di tipo `TFirst` viene vincolato a tipi che derivano dalla classe base rappresentata dall'oggetto <xref:System.Type>, contenuto nella variabile `baseType`, e implementano le interfacce i cui tipi sono contenuti nelle variabili `interfaceA` e `interfaceB`.  Per la dichiarazione e l'assegnazione di queste variabili, vedere l'esempio di codice.  
  
     [!code-cpp[EmitGenericType#7](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#7)]
     [!code-csharp[EmitGenericType#7](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#7)]
     [!code-vb[EmitGenericType#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#7)]  
  
7.  Definire un campo.  In questo esempio il tipo del campo è specificato dal parametro di tipo `TFirst`.  <xref:System.Reflection.Emit.GenericTypeParameterBuilder> deriva da <xref:System.Type>, e pertanto è possibile specificare parametri di tipo generico ovunque sia consentito l'utilizzo di un tipo.  
  
     [!code-cpp[EmitGenericType#21](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#21)]
     [!code-csharp[EmitGenericType#21](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#21)]
     [!code-vb[EmitGenericType#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#21)]  
  
8.  Definire un metodo che utilizza i parametri di tipo del tipo generico.  Si noti che tali metodi non sono generici, a meno che non dispongano di specifici elenchi di parametri di tipo.  Nel codice riportato di seguito viene definito un metodo `static` \(`Shared` in Visual Basic\) che accetta una matrice di parametri `TFirst` e restituisce un tipo `List<TFirst>` \(`List(Of TFirst)` in Visual Basic\) contenente tutti gli elementi della matrice.  Per definire questo metodo, è necessario creare il tipo `List<TFirst>` chiamando il metodo <xref:System.Type.MakeGenericType%2A> sulla definizione di tipo generico `List<T>`. Quando si utilizza l'operatore `typeof` \(`GetType` in Visual Basic\), il parametro di tipo `T` viene omesso in modo da ottenere la definizione di tipo generico. Il tipo di parametro viene creato utilizzando il metodo <xref:System.Type.MakeArrayType%2A>.  
  
     [!code-cpp[EmitGenericType#22](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#22)]
     [!code-csharp[EmitGenericType#22](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#22)]
     [!code-vb[EmitGenericType#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#22)]  
  
9. Creare il corpo del metodo.  Il corpo del metodo è costituito da tre codici operativi che caricano la matrice di input nello stack, chiamano il costruttore di `List<TFirst>` che accetta `IEnumerable<TFirst>`, con cui vengono eseguite tutte le operazioni necessarie per l'inserimento degli elementi di input nell'elenco, e terminano lasciando il nuovo oggetto <xref:System.Collections.Generic.List%601> nello stack.  Nella creazione di questo codice la difficoltà principale è rappresentata dal recupero del costruttore.  
  
     Poiché il metodo <xref:System.Type.GetConstructor%2A> non è supportato da un oggetto <xref:System.Reflection.Emit.GenericTypeParameterBuilder>, non è possibile ottenere il costruttore di `List<TFirst>` in modo diretto.  È innanzitutto necessario ottenere il costruttore della definizione di tipo generico `List<T>`, quindi chiamare un metodo che lo converta nel costruttore corrispondente di `List<TFirst>`.  
  
     Il costruttore utilizzato per questo esempio di codice accetta una definizione `IEnumerable<T>`.  Si noti tuttavia che, non trattandosi della definizione di tipo generico dell'interfaccia generica <xref:System.Collections.Generic.IEnumerable%601>, è necessario sostituire il parametro di tipo `T` di `List<T>` al parametro di tipo `T` di `IEnumerable<T>`. Per evitare che la presenza di parametri di tipo denominati `T` in entrambi i tipi generi confusione,  in questo esempio di codice vengono utilizzati i nomi `TFirst` e `TSecond`. Per ottenere il tipo dell'argomento del costruttore, creare innanzitutto la definizione di tipo generico `IEnumerable<T>`, quindi chiamare il metodo <xref:System.Type.MakeGenericType%2A> con il primo parametro di tipo generico di `List<T>`.  L'elenco di argomenti del costruttore deve essere passato come matrice che, in questo caso, contiene un unico argomento.  
  
    > [!NOTE]
    >  La definizione di tipo generico è espressa come `IEnumerable<>` quando si utilizza l'operatore `typeof` in C\# o come `IEnumerable(Of )` quando si utilizza l'operatore `GetType` in Visual Basic.  
  
     A questo punto è possibile ottenere il costruttore di `List<T>` chiamando il metodo <xref:System.Type.GetConstructor%2A> sulla definizione di tipo generico.  Per convertire questo costruttore nel costruttore corrispondente di `List<TFirst>`, passare `List<TFirst>` e il costruttore da `List<T>` al metodo statico <xref:System.Reflection.Emit.TypeBuilder.GetConstructor%28System.Type%2CSystem.Reflection.ConstructorInfo%29?displayProperty=fullName>.  
  
     [!code-cpp[EmitGenericType#23](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#23)]
     [!code-csharp[EmitGenericType#23](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#23)]
     [!code-vb[EmitGenericType#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#23)]  
  
10. Creare il tipo e salvare il file.  
  
     [!code-cpp[EmitGenericType#8](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#8)]
     [!code-csharp[EmitGenericType#8](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#8)]
     [!code-vb[EmitGenericType#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#8)]  
  
11. Richiamare il metodo.  `ExampleMethod` non è generico, ma appartiene a un tipo generico. Pertanto, per ottenere un oggetto <xref:System.Reflection.MethodInfo> che possa essere richiamato, è necessario creare un tipo costruito dalla definizione di tipo di `Sample`.  Il tipo costruito utilizza la classe `Example` che, essendo un tipo di riferimento e disponendo di un costruttore senza parametri predefinito, soddisfa i vincoli previsti per `TFirst`, nonché la classe `ExampleDerived` sottostante ai vincoli definiti per `TSecond`. Il codice per `ExampleDerived` è disponibile nella sezione del codice di esempio. Questi due tipi vengono passati al metodo <xref:System.Type.MakeGenericType%2A> per la creazione del tipo costruito.  L'oggetto <xref:System.Reflection.MethodInfo> viene quindi ottenuto utilizzando il metodo <xref:System.Type.GetMethod%2A>.  
  
     [!code-cpp[EmitGenericType#9](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#9)]
     [!code-csharp[EmitGenericType#9](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#9)]
     [!code-vb[EmitGenericType#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#9)]  
  
12. Nel codice riportato di seguito viene creata una matrice di oggetti `Example`, viene inserita tale matrice in una matrice di tipo <xref:System.Object> che rappresenta gli argomenti del metodo da richiamare e vengono passati questi argomenti al metodo [Invoke\(Object, Object\<xref:System.Reflection.MethodBase.Invoke%28System.Object%2CSystem.Object%5B%5D%29>.  Il primo argomento del metodo <xref:System.Reflection.MethodBase.Invoke%2A> è un riferimento null perché il metodo è `static`.  
  
     [!code-cpp[EmitGenericType#10](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#10)]
     [!code-csharp[EmitGenericType#10](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#10)]
     [!code-vb[EmitGenericType#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#10)]  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene definita una classe denominata `Sample`, insieme a una classe base e a due interfacce.  Nel programma vengono definiti due parametri di tipo generico per la classe `Sample`, che viene così trasformata in un tipo generico.  I parametri di tipo sono gli unici elementi in grado di rendere generico un tipo.  Nel programma questa trasformazione viene indicata tramite la visualizzazione di un messaggio di testo sia prima che dopo la definizione dei parametri di tipo.  
  
 Il parametro di tipo `TSecond` viene utilizzato per illustrare i vincoli di interfaccia e di classe tramite le interfacce e la classe base, mentre il parametro di tipo `TFirst` viene utilizzato per illustrare i vincoli speciali.  
  
 Nell'esempio di codice vengono definiti un campo e un metodo utilizzando i parametri di tipo della classe relativi al tipo di campo e al tipo restituito e di parametro del metodo.  
  
 Una volta creata la classe `Sample`, viene richiamato il metodo.  
  
 Nel programma sono inclusi due metodi, uno che fornisce informazioni su un tipo generico e un altro che illustra i vincoli speciali in un parametro di tipo.  Questi metodi vengono utilizzati per visualizzare informazioni sulla classe `Sample` completata.  
  
 Nel programma il modulo completato viene salvato su disco come `GenericEmitExample1.dll`, in modo che sia possibile aprirlo con lo strumento [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) ed esaminare il codice MSIL relativo alla classe `Sample`.  
  
 [!code-cpp[EmitGenericType#1](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#1)]
 [!code-csharp[EmitGenericType#1](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#1)]
 [!code-vb[EmitGenericType#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#1)]  
  
## Compilazione del codice  
  
-   Nel codice sono incluse le istruzioni `using` di C\# \(`Imports` in Visual Basic\) necessarie per la compilazione.  
  
-   Non sono necessari altri riferimenti ad assembly.  
  
-   Compilare il codice alla riga di comando utilizzando csc.exe, vbc.exe o cl.exe.  Per compilare il codice in Visual Studio, inserirlo in un modello di progetto di applicazione console.  
  
## Vedere anche  
 <xref:System.Reflection.Emit.GenericTypeParameterBuilder>   
 [Using Reflection Emit](http://msdn.microsoft.com/it-it/ccc6540d-0e2c-4d89-b456-eb7353f9e9ac)   
 [Reflection Emit Dynamic Assembly Scenarios](http://msdn.microsoft.com/it-it/e1cc6750-e20f-473b-bb4e-f43bc66aecce)