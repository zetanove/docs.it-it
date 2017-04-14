---
title: "How to: Hook Up a Delegate Using Reflection | Microsoft Docs"
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
  - "events [.NET Framework], adding event handlers with reflection"
  - "reflection, adding event-handler delegates"
  - "delegates [.NET Framework], adding event handlers with reflection"
ms.assetid: 076ee62d-a964-449e-a447-c31b33518b81
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# How to: Hook Up a Delegate Using Reflection
Quando si utilizza la reflection per il caricamento e l'esecuzione di assembly, non è possibile associare gli eventi tramite funzionalità quale l'operatore `+=` di C\# o l'[istruzione AddHandler](../../../ocs/visual-basic/language-reference/statements/addhandler-statement.md) di Visual Basic.  Nelle procedure riportate di seguito viene illustrato come associare un metodo esistente a un evento recuperando tutti i tipi necessari tramite la reflection e come creare un metodo dinamico utilizzando la reflection emit e associarlo a un evento.  
  
> [!NOTE]
>  L'esempio di codice per il metodo <xref:System.Reflection.EventInfo.AddEventHandler%2A> della classe <xref:System.Reflection.EventInfo> rappresenta un altro modo di associare un delegato di gestione degli eventi.  
  
### Per associare un delegato tramite la reflection  
  
1.  Caricare un assembly contenente un tipo che genera eventi.  Gli assembly vengono in genere caricati con il metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>.  Per evitare che l'esempio diventi troppo complesso, viene utilizzato un form derivato nell'assembly corrente, pertanto quest'ultimo viene caricato tramite il metodo <xref:System.Reflection.Assembly.GetExecutingAssembly%2A>.  
  
     [!code-cpp[HookUpDelegate#3](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#3)]
     [!code-csharp[HookUpDelegate#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#3)]
     [!code-vb[HookUpDelegate#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#3)]  
  
2.  Ottenere un oggetto <xref:System.Type> che rappresenta il tipo e creare un'istanza del tipo.  Nel codice che segue viene utilizzato il metodo <xref:System.Activator.CreateInstance%28System.Type%29> perché il form dispone di un costruttore predefinito.  Se il tipo creato è privo di un costruttore predefinito, è possibile utilizzare altri overload del metodo <xref:System.Activator.CreateInstance%2A>.  Affinché sembri che non sia disponibile alcuna informazione sull'assembly, la nuova istanza viene memorizzata come tipo <xref:System.Object>. In effetti, la reflection consente di ottenere i tipi in un assembly senza sia necessario conoscerne i nomi in anticipo.  
  
     [!code-cpp[HookUpDelegate#4](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#4)]
     [!code-csharp[HookUpDelegate#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#4)]
     [!code-vb[HookUpDelegate#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#4)]  
  
3.  Ottenere un oggetto <xref:System.Reflection.EventInfo> che rappresenta l'evento e utilizzare la proprietà <xref:System.Reflection.EventInfo.EventHandlerType%2A> per recuperare il tipo del delegato utilizzato per la gestione dell'evento.  Nel codice riportato di seguito viene recuperato un oggetto <xref:System.Reflection.EventInfo> relativo all'evento <xref:System.Windows.Forms.Control.Click>.  
  
     [!code-cpp[HookUpDelegate#5](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#5)]
     [!code-csharp[HookUpDelegate#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#5)]
     [!code-vb[HookUpDelegate#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#5)]  
  
4.  Ottenere un oggetto <xref:System.Reflection.MethodInfo> che rappresenta il metodo che gestisce l'evento.  Nel codice del programma completo, riportato nella sezione Esempio più avanti in questo argomento, è presente un metodo che corrisponde alla firma del delegato <xref:System.EventHandler> che gestisce l'evento <xref:System.Windows.Forms.Control.Click>, ma è anche possibile generare metodi dinamici in fase di esecuzione.  Per informazioni dettagliate, vedere la procedura associata per generare un gestore eventi in fase di esecuzione tramite un metodo dinamico.  
  
     [!code-cpp[HookUpDelegate#6](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#6)]
     [!code-csharp[HookUpDelegate#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#6)]
     [!code-vb[HookUpDelegate#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#6)]  
  
5.  Creare un'istanza del delegato utilizzando il metodo <xref:System.Delegate.CreateDelegate%2A>.  Poiché il metodo è statico \(`Shared` in Visual Basic\), è necessario specificare il tipo delegato.  Si consiglia di utilizzare gli overload del metodo <xref:System.Delegate.CreateDelegate%2A>, che accettano un oggetto <xref:System.Reflection.MethodInfo>.  
  
     [!code-cpp[HookUpDelegate#7](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#7)]
     [!code-csharp[HookUpDelegate#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#7)]
     [!code-vb[HookUpDelegate#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#7)]  
  
6.  Ottenere il metodo della funzione di accesso `add` e richiamarlo per associare l'evento.  Tutti gli eventi dispongono di una funzione di accesso `add` e di una funzione di accesso `remove`, nascoste dalla sintassi dei linguaggi ad alto livello.  Per associare gli eventi, ad esempio, C\# utilizza l'operatore `+=`, mentre Visual Basic utilizza l'[istruzione AddHandler](../../../ocs/visual-basic/language-reference/statements/addhandler-statement.md).  Nel codice riportato di seguito viene ottenuta la funzione di accesso `add` dell'evento <xref:System.Windows.Forms.Control.Click>, che viene quindi richiamata con associazione tardiva passando l'istanza del delegato.  Gli argomenti devono essere passati come matrice.  
  
     [!code-cpp[HookUpDelegate#8](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#8)]
     [!code-csharp[HookUpDelegate#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#8)]
     [!code-vb[HookUpDelegate#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#8)]  
  
7.  Verificare l'evento.  Nel codice seguente viene illustrato il form definito nell'esempio.  Facendo clic sul form, verrà richiamato il gestore eventi.  
  
     [!code-cpp[HookUpDelegate#12](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#12)]
     [!code-csharp[HookUpDelegate#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#12)]
     [!code-vb[HookUpDelegate#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#12)]  
  
<a name="procedureSection1"></a>   
### Per generare un gestore eventi in fase di esecuzione tramite un metodo dinamico  
  
1.  I metodi per la gestione degli eventi possono essere generati in fase di esecuzione utilizzando metodi dinamici di tipo lightweight e la reflection emit.  Per costruire un gestore eventi, è necessario disporre del tipo restituito e dei tipi di parametro del delegato,  che possono essere ottenuti esaminando il metodo `Invoke` del delegato.  Nel codice riportato di seguito vengono utilizzati i metodi `GetDelegateReturnType` e `GetDelegateParameterTypes` per il recupero di tali informazioni.  Il codice relativo a questi metodi è disponibile nella sezione Esempio più avanti in questo argomento.  
  
     Poiché non è necessario assegnare un nome a <xref:System.Reflection.Emit.DynamicMethod>, può essere utilizzata la stringa vuota.  Nel codice riportato di seguito l'ultimo argomento associa il metodo dinamico al tipo corrente, concedendo al delegato l'accesso a tutti i membri pubblici e privati della classe `Example`.  
  
     [!code-cpp[HookUpDelegate#9](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#9)]
     [!code-csharp[HookUpDelegate#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#9)]
     [!code-vb[HookUpDelegate#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#9)]  
  
2.  Generare il corpo di un metodo.  Quest'ultimo carica una stringa, chiama l'overload del metodo <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName> che accetta una stringa, estrae il valore restituito dallo stack perché il gestore non ha alcun tipo restituito e termina.  Per ulteriori informazioni sulla creazione di metodi dinamici, vedere [How to: Define and Execute Dynamic Methods](../../../docs/framework/reflection-and-codedom/how-to-define-and-execute-dynamic-methods.md).  
  
     [!code-cpp[HookUpDelegate#10](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#10)]
     [!code-csharp[HookUpDelegate#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#10)]
     [!code-vb[HookUpDelegate#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#10)]  
  
3.  Completare il metodo dinamico chiamando il relativo metodo <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A>.  Utilizzare la funzione di accesso `add` per aggiungere il delegato all'elenco di chiamate per l'evento.  
  
     [!code-cpp[HookUpDelegate#11](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#11)]
     [!code-csharp[HookUpDelegate#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#11)]
     [!code-vb[HookUpDelegate#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#11)]  
  
4.  Verificare l'evento.  Nel codice riportato di seguito viene caricato il form definito nell'esempio.  Facendo clic sul form, verranno richiamati sia il gestore eventi predefinito che il gestore eventi creato.  
  
     [!code-cpp[HookUpDelegate#12](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#12)]
     [!code-csharp[HookUpDelegate#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#12)]
     [!code-vb[HookUpDelegate#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#12)]  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come associare un metodo esistente a un evento tramite la reflection, nonché come utilizzare la classe <xref:System.Reflection.Emit.DynamicMethod> per creare un metodo in fase di esecuzione e associarlo a un evento.  
  
 [!code-cpp[HookUpDelegate#1](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#1)]
 [!code-csharp[HookUpDelegate#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#1)]
 [!code-vb[HookUpDelegate#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#1)]  
  
## Compilazione del codice  
  
-   Nel codice sono incluse le istruzioni `using` di C\# \(`Imports` in Visual Basic\) necessarie per la compilazione.  
  
-   Per la compilazione dalla riga di comando, non sono necessari altri riferimenti ad assembly.  Poiché questo esempio rappresenta un'applicazione console, in Visual Studio sarà necessario aggiungere un riferimento a System.Windows.Forms.dll.  
  
-   Compilare il codice alla riga di comando utilizzando csc.exe, vbc.exe o cl.exe.  Per compilare il codice in Visual Studio, inserirlo in un modello di progetto di applicazione console.  
  
## Vedere anche  
 <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>   
 <xref:System.Reflection.Emit.DynamicMethod>   
 <xref:System.Activator.CreateInstance%2A>   
 <xref:System.Delegate.CreateDelegate%2A>   
 [How to: Define and Execute Dynamic Methods](../../../docs/framework/reflection-and-codedom/how-to-define-and-execute-dynamic-methods.md)   
 [Reflection](../../../docs/framework/reflection-and-codedom/reflection.md)