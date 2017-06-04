---
title: "How to: Examine and Instantiate Generic Types with Reflection | Microsoft Docs"
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
  - "reflection, generic types"
  - "generics [.NET Framework], reflection"
ms.assetid: f93b03b0-1778-43fc-bc6d-35983d210e74
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# How to: Examine and Instantiate Generic Types with Reflection
Le informazioni sui tipi generici vengono ottenute esattamente come quelle relative ad altri tipi, ovvero esaminando un oggetto <xref:System.Type> che rappresenta il tipo generico.  La differenza principale è data dal fatto che un tipo generico dispone di un elenco di oggetti <xref:System.Type> che rappresentano i relativi parametri di tipo generico.  Nella prima procedura riportata in questa sezione vengono esaminati i tipi generici.  
  
 È possibile creare un oggetto <xref:System.Type> che rappresenta un tipo costruito associando argomenti di tipo ai parametri di tipo di una definizione di tipo generico.  Questo concetto è illustrato nella seconda procedura.  
  
### Per esaminare un tipo generico e i relativi parametri di tipo  
  
1.  Ottenere un'istanza di <xref:System.Type> che rappresenta il tipo generico.  Nel codice riportato di seguito il tipo viene ottenuto utilizzando l'operatore `typeof` di C\# \(`GetType` in Visual Basic e `typeid` in Visual C\+\+\).  Per informazioni su come ottenere un oggetto <xref:System.Type> in altri modi, vedere l'argomento relativo alla classe <xref:System.Type>.  Si noti che nella parte restante di questa procedura il tipo è contenuto in un parametro di metodo denominato `t`.  
  
     [!code-cpp[HowToGeneric#2](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#2)]
     [!code-csharp[HowToGeneric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#2)]
     [!code-vb[HowToGeneric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#2)]  
  
2.  Utilizzare la proprietà <xref:System.Type.IsGenericType%2A> per stabilire se il tipo è generico e la proprietà <xref:System.Type.IsGenericTypeDefinition%2A> per stabilire se il tipo è una definizione di tipo generico.  
  
     [!code-cpp[HowToGeneric#3](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#3)]
     [!code-csharp[HowToGeneric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#3)]
     [!code-vb[HowToGeneric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#3)]  
  
3.  Ottenere una matrice contenente gli argomenti di tipo generico utilizzando il metodo <xref:System.Type.GetGenericArguments%2A>.  
  
     [!code-cpp[HowToGeneric#4](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#4)]
     [!code-csharp[HowToGeneric#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#4)]
     [!code-vb[HowToGeneric#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#4)]  
  
4.  Per ogni argomento di tipo, stabilire se è un parametro di tipo, ad esempio in una definizione di tipo generico, oppure un tipo specificato per un parametro di tipo, ad esempio in un tipo costruito, utilizzando la proprietà <xref:System.Type.IsGenericParameter%2A>.  
  
     [!code-cpp[HowToGeneric#5](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#5)]
     [!code-csharp[HowToGeneric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#5)]
     [!code-vb[HowToGeneric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#5)]  
  
5.  Nell'ambito del sistema di tipi un parametro di tipo generico è rappresentato da un'istanza di <xref:System.Type>, esattamente come i tipi ordinari.  Nel codice riportato di seguito vengono indicati il nome e la posizione del parametro di un oggetto <xref:System.Type>, che rappresenta un parametro di tipo generico.  In questo contesto la posizione del parametro non è un'informazione rilevante, ma rappresenta un dato significativo per l'esame di un parametro di tipo utilizzato come argomento di tipo di un altro tipo generico.  
  
     [!code-cpp[HowToGeneric#6](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#6)]
     [!code-csharp[HowToGeneric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#6)]
     [!code-vb[HowToGeneric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#6)]  
  
6.  Stabilire i vincoli del tipo base e dell'interfaccia di un parametro di tipo generico utilizzando il metodo <xref:System.Type.GetGenericParameterConstraints%2A> per ottenere tutti i vincoli in una singola matrice.  I vincoli non vengono necessariamente restituiti in un ordine specifico.  
  
     [!code-cpp[HowToGeneric#7](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#7)]
     [!code-csharp[HowToGeneric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#7)]
     [!code-vb[HowToGeneric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#7)]  
  
7.  Utilizzare la proprietà <xref:System.Type.GenericParameterAttributes%2A> per individuare i vincoli speciali applicati a un parametro di tipo, ad esempio quelli necessari perché il parametro sia un tipo di riferimento.  La proprietà include anche valori che rappresentano la varianza, che è possibile nascondere nel modo indicato nel codice riportato di seguito.  
  
     [!code-cpp[HowToGeneric#8](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#8)]
     [!code-csharp[HowToGeneric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#8)]
     [!code-vb[HowToGeneric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#8)]  
  
8.  Gli attributi di vincolo speciale sono flag. Il flag \(<xref:System.Reflection.GenericParameterAttributes?displayProperty=fullName>\) non rappresenta né i vincoli speciali né covarianza e controvarianza.  Pertanto, per eseguire il test di queste condizioni, è necessario utilizzare la maschera appropriata.  Nel caso specifico, utilizzare <xref:System.Reflection.GenericParameterAttributes?displayProperty=fullName> per isolare i flag di vincolo speciale.  
  
     [!code-cpp[HowToGeneric#9](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#9)]
     [!code-csharp[HowToGeneric#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#9)]
     [!code-vb[HowToGeneric#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#9)]  
  
## Costruzione di un'istanza di un tipo generico  
 Un tipo generico è analogo a un modello.  Non è possibile crearne istanze, se non specificando i tipi reali associati ai relativi parametri di tipo generico.  Per effettuare questa operazione in fase di esecuzione utilizzando la reflection, è necessario utilizzare il metodo <xref:System.Type.MakeGenericType%2A>.  
  
#### Per costruire un'istanza di un tipo generico  
  
1.  Ottenere un oggetto <xref:System.Type> che rappresenta il tipo generico.  Nel codice riportato di seguito il tipo generico <xref:System.Collections.Generic.Dictionary%602> viene ottenuto in due modi diversi: utilizzando l'overload del metodo <xref:System.Type.GetType%28System.String%29?displayProperty=fullName> con una stringa di descrizione del tipo e chiamando il metodo <xref:System.Type.GetGenericTypeDefinition%2A> sul tipo costruito `Dictionary\<String, Example>` \(`Dictionary(Of String, Example)` in Visual Basic\).  Il metodo <xref:System.Type.MakeGenericType%2A> richiede una definizione di tipo generico.  
  
     [!code-cpp[HowToGeneric#10](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#10)]
     [!code-csharp[HowToGeneric#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#10)]
     [!code-vb[HowToGeneric#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#10)]  
  
2.  Costruire una matrice di argomenti di tipo da sostituire ai parametri di tipo.  Nella matrice deve essere incluso il numero corretto di oggetti <xref:System.Type>, nello stesso ordine in cui sono disposti nell'elenco di parametri di tipo.  In questo caso la chiave \(il primo parametro di tipo\) è di tipo <xref:System.String> e i valori nel dizionario sono istanze di una classe denominata `Example`.  
  
     [!code-cpp[HowToGeneric#11](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#11)]
     [!code-csharp[HowToGeneric#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#11)]
     [!code-vb[HowToGeneric#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#11)]  
  
3.  Chiamare il metodo <xref:System.Type.MakeGenericType%2A> per associare gli argomenti di tipo ai parametri di tipo e costruire il tipo.  
  
     [!code-cpp[HowToGeneric#12](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#12)]
     [!code-csharp[HowToGeneric#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#12)]
     [!code-vb[HowToGeneric#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#12)]  
  
4.  Utilizzare l'overload del metodo <xref:System.Activator.CreateInstance%28System.Type%29> per creare un oggetto del tipo costruito.  Nel codice riportato di seguito vengono archiviate due istanze della classe `Example` nell'oggetto `Dictionary<String, Example>` risultante.  
  
     [!code-cpp[HowToGeneric#13](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#13)]
     [!code-csharp[HowToGeneric#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#13)]
     [!code-vb[HowToGeneric#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#13)]  
  
## Esempio  
 Nel codice riportato di seguito viene definito un metodo `DisplayGenericType` che consente di esaminare le definizioni di tipo generico e i tipi costruiti utilizzati nel codice, nonché di visualizzare le relative informazioni.  Il metodo `DisplayGenericType` indica come utilizzare le proprietà <xref:System.Type.IsGenericType%2A>, <xref:System.Type.IsGenericParameter%2A> e <xref:System.Type.GenericParameterPosition%2A> e il metodo <xref:System.Type.GetGenericArguments%2A>.  
  
 Nell'esempio viene anche definito un metodo `DisplayGenericParameter` per esaminare un parametro di tipo generico e visualizzare i vincoli a esso associati.  
  
 Nell'esempio di codice viene definito un insieme di tipi di test, incluso un tipo che indica i vincoli di parametro di tipo, e viene illustrato come visualizzare informazioni su questi tipi.  
  
 Nell'esempio viene costruito un tipo della classe <xref:System.Collections.Generic.Dictionary%602> creando una matrice di argomenti di tipo e chiamando il metodo <xref:System.Type.MakeGenericType%2A>.  Nel programma viene eseguito un confronto tra l'oggetto <xref:System.Type> costruito utilizzando il metodo <xref:System.Type.MakeGenericType%2A> e un oggetto <xref:System.Type> ottenuto utilizzando `typeof` \(`GetType` in Visual Basic\) e viene dimostrato che i due oggetti sono equivalenti.  Analogamente, nel programma viene utilizzato il metodo <xref:System.Type.GetGenericTypeDefinition%2A> per ottenere la definizione di tipo generico del tipo costruito, di cui viene quindi eseguito il confronto con l'oggetto <xref:System.Type> che rappresenta la classe <xref:System.Collections.Generic.Dictionary%602>.  
  
 [!code-cpp[HowToGeneric#1](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/ur.cpp#1)]
 [!code-csharp[HowToGeneric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/ur.cs#1)]
 [!code-vb[HowToGeneric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/ur.vb#1)]  
  
## Compilazione del codice  
  
-   Nel codice sono incluse le istruzioni `using` di C\# \(`Imports` in Visual Basic\) necessarie per la compilazione.  
  
-   Non sono necessari altri riferimenti ad assembly.  
  
-   Compilare il codice alla riga di comando utilizzando csc.exe, vbc.exe o cl.exe.  Per compilare il codice in Visual Studio, inserirlo in un modello di progetto di applicazione console.  
  
## Vedere anche  
 <xref:System.Type>   
 <xref:System.Reflection.MethodInfo>   
 [Reflection and Generic Types](../../../docs/framework/reflection-and-codedom/reflection-and-generic-types.md)   
 [Viewing Type Information](../../../docs/framework/reflection-and-codedom/viewing-type-information.md)   
 [Generics](../../../docs/standard/generics/index.md)