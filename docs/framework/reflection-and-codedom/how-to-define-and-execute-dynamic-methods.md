---
title: "How to: Define and Execute Dynamic Methods | Microsoft Docs"
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
  - "reflection emit, dynamic methods"
  - "dynamic methods"
ms.assetid: 07d08a99-62c5-4254-bce2-2a75e55a18ab
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# How to: Define and Execute Dynamic Methods
Nelle procedure riportate di seguito viene illustrato come definire ed eseguire un metodo dinamico semplice e un metodo dinamico associato a un'istanza di una classe.  Per ulteriori informazioni sui metodi dinamici, vedere la classe <xref:System.Reflection.Emit.DynamicMethod> e [Reflection Emit Dynamic Method Scenarios](http://msdn.microsoft.com/it-it/7c27ea3d-0f24-4bf3-8ceb-f49d33faca5e).  
  
### Per definire ed eseguire un metodo dinamico  
  
1.  Dichiarare un tipo delegato per l'esecuzione del metodo.  È opportuno utilizzare un delegato generico per ridurre al minimo il numero di tipi delegati da dichiarare.  Nel codice riportato di seguito vengono dichiarati due tipi delegati, uno dei quali generico, che possono essere utilizzati per il metodo `SquareIt`.  
  
     [!code-cpp[DynamicMethodHowTo#2](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#2)]
     [!code-csharp[DynamicMethodHowTo#2](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#2)]
     [!code-vb[DynamicMethodHowTo#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#2)]  
  
2.  Creare una matrice che specifica i tipi di parametro relativi al metodo dinamico.  In questo esempio l'unico parametro disponibile è un `int` \(`Integer` in Visual Basic\). Di conseguenza, la matrice contiene un solo elemento.  
  
     [!code-cpp[DynamicMethodHowTo#3](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#3)]
     [!code-csharp[DynamicMethodHowTo#3](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#3)]
     [!code-vb[DynamicMethodHowTo#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#3)]  
  
3.  Creare un oggetto <xref:System.Reflection.Emit.DynamicMethod>.  In questo esempio il metodo è denominato `SquareIt`.  
  
    > [!NOTE]
    >  Non è necessario assegnare un nome ai metodi dinamici, che non possono essere richiamati per nome.  È possibile che più metodi dinamici abbiano lo stesso nome.  Il nome viene comunque visualizzato negli stack delle chiamate e può risultare utile per operazioni di debug.  
  
     Il tipo del valore restituito è specificato come `long`.  Il metodo viene associato al modulo contenente la classe `Example`, in cui è incluso il codice di esempio.  Può essere specificato qualsiasi modulo caricato.  Il metodo dinamico funge da metodo `static` \(`Shared` in Visual Basic\) a livello di modulo  
  
     [!code-cpp[DynamicMethodHowTo#4](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#4)]
     [!code-csharp[DynamicMethodHowTo#4](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#4)]
     [!code-vb[DynamicMethodHowTo#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#4)]  
  
4.  Creare il corpo del metodo.  In questo esempio viene utilizzato un oggetto <xref:System.Reflection.Emit.ILGenerator> per creare il codice MSIL.  In alternativa, è possibile utilizzare un oggetto <xref:System.Reflection.Emit.DynamicILInfo> insieme a generatori di codice non gestito per creare il corpo del metodo relativo a un <xref:System.Reflection.Emit.DynamicMethod>.  
  
     In questo esempio il codice MSIL carica l'argomento \(`int`\) nello stack, lo converte in un `long`, duplica il `long` ed esegue la moltiplicazione tra i due numeri.  Il prodotto elevato al quadrato rimane nello stack e il metodo termina.  
  
     [!code-cpp[DynamicMethodHowTo#5](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#5)]
     [!code-csharp[DynamicMethodHowTo#5](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#5)]
     [!code-vb[DynamicMethodHowTo#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#5)]  
  
5.  Creare un'istanza del delegato dichiarato nel primo passaggio che rappresenta il metodo dinamico chiamando il metodo <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A>.  La creazione del delegato rende il metodo completo e qualsiasi successivo tentativo di modifica, ad esempio l'aggiunta di ulteriore codice MSIL, verrà ignorato.  Nel codice riportato di seguito il delegato viene creato, quindi richiamato tramite un delegato generico.  
  
     [!code-cpp[DynamicMethodHowTo#6](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#6)]
     [!code-csharp[DynamicMethodHowTo#6](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#6)]
     [!code-vb[DynamicMethodHowTo#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#6)]  
  
### Per definire ed eseguire un metodo dinamico associato a un oggetto  
  
1.  Dichiarare un tipo delegato per l'esecuzione del metodo.  È opportuno utilizzare un delegato generico per ridurre al minimo il numero di tipi delegati da dichiarare.  Nel codice seguente viene dichiarato un delegato generico che può essere utilizzato per eseguire qualsiasi metodo con un parametro e un valore restituito o, se il delegato è associato a un oggetto, un metodo con due parametri e un valore restituito.  
  
     [!code-cpp[DynamicMethodHowTo#12](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#12)]
     [!code-csharp[DynamicMethodHowTo#12](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#12)]
     [!code-vb[DynamicMethodHowTo#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#12)]  
  
2.  Creare una matrice che specifica i tipi di parametro relativi al metodo dinamico.  Se il delegato che rappresenta il metodo è associato a un oggetto, il primo parametro deve corrispondere al tipo a cui è associato il delegato.  In questo esempio sono disponibili due parametri, uno di tipo `Example` e uno di tipo `int` \(`Integer` in Visual Basic\).  
  
     [!code-cpp[DynamicMethodHowTo#13](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#13)]
     [!code-csharp[DynamicMethodHowTo#13](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#13)]
     [!code-vb[DynamicMethodHowTo#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#13)]  
  
3.  Creare un oggetto <xref:System.Reflection.Emit.DynamicMethod>.  In questo esempio il metodo è senza nome.  Il tipo del valore restituito è specificato come `int` \(`Integer` in Visual Basic\).  Il metodo dispone dell'accesso ai membri privati e protetti della classe `Example`.  
  
     [!code-cpp[DynamicMethodHowTo#14](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#14)]
     [!code-csharp[DynamicMethodHowTo#14](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#14)]
     [!code-vb[DynamicMethodHowTo#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#14)]  
  
4.  Creare il corpo del metodo.  In questo esempio viene utilizzato un oggetto <xref:System.Reflection.Emit.ILGenerator> per creare il codice MSIL.  In alternativa, è possibile utilizzare un oggetto <xref:System.Reflection.Emit.DynamicILInfo> insieme a generatori di codice non gestito per creare il corpo del metodo relativo a un <xref:System.Reflection.Emit.DynamicMethod>.  
  
     In questo esempio il codice MSIL carica il primo argomento, un'istanza della classe `Example`, e lo utilizza per caricare il valore di un campo di istanza privato di tipo `int`.  Viene caricato il secondo argomento e viene eseguita la moltiplicazione tra i due numeri.  Se il prodotto è maggiore di `int`, il valore viene troncato e i bit più significativi vengono ignorati.  Il metodo termina lasciando il valore restituito nello stack.  
  
     [!code-cpp[DynamicMethodHowTo#15](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#15)]
     [!code-csharp[DynamicMethodHowTo#15](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#15)]
     [!code-vb[DynamicMethodHowTo#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#15)]  
  
5.  Creare un'istanza del delegato dichiarato nel primo passaggio che rappresenta il metodo dinamico chiamando l'overload del metodo <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%28System.Type%2CSystem.Object%29>.  La creazione del delegato rende il metodo completo e qualsiasi successivo tentativo di modifica, ad esempio l'aggiunta di ulteriore codice MSIL, verrà ignorato.  
  
    > [!NOTE]
    >  È possibile chiamare il metodo <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A> più volte per creare delegati associati ad altre istanze del tipo di destinazione.  
  
     Nel codice riportato di seguito il metodo viene associato a una nuova istanza della classe `Example`, il cui campo di test privato è impostato su 42.  In altri termini, ogni volta che viene richiamato il delegato, l'istanza di `Example` viene passata al primo parametro del metodo.  
  
     Viene utilizzato il delegato `OneParameter` perché il primo parametro del metodo riceve sempre l'istanza di `Example`.  Quando il delegato viene richiamato, sarà necessario solo il secondo parametro.  
  
     [!code-cpp[DynamicMethodHowTo#16](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#16)]
     [!code-csharp[DynamicMethodHowTo#16](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#16)]
     [!code-vb[DynamicMethodHowTo#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#16)]  
  
## Esempio  
 Nell'esempio di codice riportato di seguito vengono illustrati un metodo dinamico semplice e un metodo dinamico associato a un'istanza di una classe.  
  
 Il metodo dinamico semplice accetta un unico argomento, un intero a 32 bit, e ne restituisce il quadrato a 64 bit.  Per richiamare il metodo, viene utilizzato un delegato generico.  
  
 Il secondo metodo dinamico dispone di due parametri, uno di tipo `Example` e uno di tipo `int` \(`Integer` in Visual Basic\).  Non appena viene creato, il metodo dinamico viene associato a un'istanza di `Example` tramite un delegato generico che dispone di un unico argomento di tipo `int`.  Il delegato non dispone di un argomento di tipo `Example` perché il primo parametro del metodo riceve sempre l'istanza associata di `Example`.  Quando il delegato viene richiamato, verrà fornito solo l'argomento `int`.  Questo metodo dinamico accede a un campo privato della classe `Example` e restituisce il prodotto tra il campo privato e l'argomento `int`.  
  
 Nell'esempio di codice vengono definiti i delegati che possono essere utilizzati per l'esecuzione dei metodi.  
  
 [!code-cpp[DynamicMethodHowTo#1](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#1)]
 [!code-csharp[DynamicMethodHowTo#1](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#1)]
 [!code-vb[DynamicMethodHowTo#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#1)]  
  
## Compilazione del codice  
  
-   Nel codice sono incluse le istruzioni `using` di C\# \(`Imports` in Visual Basic\) necessarie per la compilazione.  
  
-   Non sono necessari altri riferimenti ad assembly.  
  
-   Compilare il codice alla riga di comando utilizzando csc.exe, vbc.exe o cl.exe.  Per compilare il codice in Visual Studio, inserirlo in un modello di progetto di applicazione console.  
  
## Vedere anche  
 <xref:System.Reflection.Emit.DynamicMethod>   
 [Using Reflection Emit](http://msdn.microsoft.com/it-it/ccc6540d-0e2c-4d89-b456-eb7353f9e9ac)   
 [Reflection Emit Dynamic Method Scenarios](http://msdn.microsoft.com/it-it/7c27ea3d-0f24-4bf3-8ceb-f49d33faca5e)