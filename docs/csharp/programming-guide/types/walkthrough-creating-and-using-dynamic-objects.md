---
title: "Procedura dettagliata: creazione e utilizzo di oggetti dinamici (C# e Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "oggetti dinamici"
  - "oggetti dinamici [C#]"
  - "oggetti dinamici [Visual Basic]"
ms.assetid: 568f1645-1305-4906-8625-5d77af81e04f
caps.latest.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 22
---
# Procedura dettagliata: creazione e utilizzo di oggetti dinamici (C# e Visual Basic)
Gli oggetti dinamici espongono membri quali proprietà e metodi in fase di esecuzione anziché in fase di compilazione.  In questo modo è possibile creare oggetti che consentono di utilizzare strutture che non corrispondono a un tipo o un formato statico.  Ad esempio, è possibile utilizzare un oggetto dinamico per fare riferimento al modello a oggetti documento \(DOM, Document Object Model\) HTML, che può contenere qualsiasi combinazione di elementi e attributi di markup HTML validi.  Poiché ogni documento HTML è univoco, i membri di un determinato documento HTML vengono determinati in fase di esecuzione.  Un metodo comune per fare riferimento a un attributo di un elemento HTML è passare il nome dell'attributo al metodo `GetProperty` dell'elemento.  Per fare riferimento all'attributo `id` dell'elemento HTML `<div id="Div1">` occorre prima ottenere un riferimento all'elemento `<div>` e quindi utilizzare `divElement.GetProperty("id")`.  Se si utilizza un oggetto dinamico, è possibile fare riferimento all'attributo `id` con `divElement.id`.  
  
 Gli oggetti dinamici forniscono inoltre un pratico accesso a linguaggi dinamici quali IronPython e IronRuby.  È possibile utilizzare un oggetto dinamico per fare riferimento a uno script dinamico interpretato in fase di esecuzione.  
  
 Per fare riferimento a un oggetto dinamico si utilizza l'associazione tardiva.  In C\# il tipo di un oggetto per cui è prevista l'associazione tardiva si specifica con `dynamic`.  In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] il tipo di un oggetto per cui è prevista l'associazione tardiva si specifica con `Object`.  Per ulteriori informazioni, vedere [dynamic](../../../csharp/language-reference/keywords/dynamic.md) e [Early and Late Binding](../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md).  
  
 È possibile creare oggetti dinamici personalizzati tramite le classi nello spazio dei nomi <xref:System.Dynamic?displayProperty=fullName>.  Ad esempio, è possibile creare un oggetto <xref:System.Dynamic.ExpandoObject> e specificarne i membri in fase di esecuzione.  È inoltre possibile creare un tipo personalizzato che eredita la classe <xref:System.Dynamic.DynamicObject>.  È quindi possibile eseguire l'override dei membri della classe <xref:System.Dynamic.DynamicObject> per fornire funzionalità dinamiche in fase di esecuzione.  
  
 In questa procedura dettagliata si eseguiranno le attività seguenti:  
  
-   Creazione di un oggetto personalizzato che espone dinamicamente il contenuto di un file di testo come proprietà di un oggetto.  
  
-   Creazione di un progetto che utilizza una libreria `IronPython`.  
  
## Prerequisiti  
 Per completare questa procedura dettagliata, è necessario disporre di IronPython 2.6.1 per .NET 4.0.  È possibile scaricare IronPython 2.6.1 per .NET 4.0 da [CodePlex](http://go.microsoft.com/fwlink/?LinkId=187223) \(la pagina potrebbe essere in inglese\).  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
## Creazione di un oggetto dinamico personalizzato  
 Il primo progetto che si crea in questa procedura dettagliata definisce un oggetto dinamico personalizzato che esegue ricerche nel contenuto di un file di testo.  Il testo da cercare viene specificato tramite il nome di una proprietà dinamica.  Se ad esempio nel codice chiamante si specifica `dynamicFile.Sample`, la classe dinamica restituisce un elenco generico di stringhe contenente tutte le righe del file che iniziano con "Sample".  La ricerca non prevede la distinzione tra maiuscole e minuscole.  La classe dinamica supporta altri due argomenti facoltativi.  Il primo argomento è un valore di enumerazione di opzione di ricerca che specifica che la classe dinamica deve cercare corrispondenze all'inizio, alla fine o in qualsiasi punto della riga.  Il secondo argomento specifica che la classe dinamica, prima di eseguire la ricerca, deve tagliare gli spazi iniziali e finali di ogni riga.  Ad esempio, se nel codice chiamante si specifica `dynamicFile.Sample(StringSearchOption.Contains)`, la classe dinamica cerca "Sample" nell'intera riga.  Se nel codice chiamante si specifica `dynamicFile.Sample(StringSearchOption.StartsWith, false)`, la classe dinamica cerca "Sample" all'inizio di ogni riga e non rimuove gli spazi iniziali e finali.  Il comportamento predefinito della classe dinamica è cercare una corrispondenza all'inizio di ogni riga e rimuovere gli spazi iniziali e finali.  
  
#### Per creare una classe dinamica personalizzata  
  
1.  Avviare [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)].  
  
2.  Scegliere **Nuovo** dal menu **File**, quindi scegliere **Progetto**.  
  
3.  Nel riquadro **Tipi progetto** della finestra di dialogo **Nuovo progetto** verificare che sia selezionata la voce **Finestre**.  Selezionare **Applicazione console** nel riquadro **Modelli**.  Digitare `DynamicSample` nella casella **Nome**, quindi scegliere **OK**.  Verrà creato il nuovo progetto.  
  
4.  Fare clic con il pulsante destro del mouse sul progetto DynamicSample e selezionare **Aggiungi**, quindi scegliere **Classe**.  Digitare `ReadOnlyFile` nella casella **Nome**, quindi scegliere **OK**.  Verrà aggiunto un nuovo file contenente la classe ReadOnlyFile.  
  
5.  All'inizio del file ReadOnlyFile.cs o ReadOnlyFile.vb, aggiungere il codice seguente per importare gli spazi dei nomi <xref:System.IO?displayProperty=fullName> e <xref:System.Dynamic?displayProperty=fullName>.  
  
     [!code-cs[VbDynamicWalkthrough#1](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_1.cs)]
     [!code-vb[VbDynamicWalkthrough#1](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_1.vb)]  
  
6.  L'oggetto dinamico personalizzato utilizza un'enumerazione per determinare i criteri di ricerca.  Prima dell'istruzione class, aggiungere la definizione di enumerazione seguente.  
  
     [!code-cs[VbDynamicWalkthrough#2](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_2.cs)]
     [!code-vb[VbDynamicWalkthrough#2](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_2.vb)]  
  
7.  Aggiornare l'istruzione class in modo che erediti la classe `DynamicObject`, come illustrato nell'esempio di codice seguente.  
  
     [!code-cs[VbDynamicWalkthrough#3](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_3.cs)]
     [!code-vb[VbDynamicWalkthrough#3](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_3.vb)]  
  
8.  Aggiungere il codice seguente alla classe `ReadOnlyFile` per definire un campo privato per il percorso del file e un costruttore per la classe `ReadOnlyFile`.  
  
     [!code-cs[VbDynamicWalkthrough#4](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_4.cs)]
     [!code-vb[VbDynamicWalkthrough#4](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_4.vb)]  
  
9. Aggiungere il seguente metodo `GetPropertyValue` alla classe `ReadOnlyFile`.  Il metodo `GetPropertyValue` accetta come input i criteri di ricerca e restituisce le righe contenute in un file di testo che soddisfano tali criteri.  I metodi dinamici forniti dalla classe `ReadOnlyFile` chiamano il metodo `GetPropertyValue` per recuperare i rispettivi risultati.  
  
     [!code-cs[VbDynamicWalkthrough#5](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_5.cs)]
     [!code-vb[VbDynamicWalkthrough#5](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_5.vb)]  
  
10. Dopo il metodo `GetPropertyValue`, aggiungere il codice seguente per eseguire l'override del metodo <xref:System.Dynamic.DynamicObject.TryGetMember%2A> della classe <xref:System.Dynamic.DynamicObject>.  Il metodo <xref:System.Dynamic.DynamicObject.TryGetMember%2A> viene chiamato quando viene richiesto un membro di una classe dinamica e non è specificato alcun argomento.  L'argomento `binder` contiene informazioni sul membro a cui si fa riferimento e l'argomento `result` fa riferimento al risultato restituito per il membro specificato.  Il metodo <xref:System.Dynamic.DynamicObject.TryGetMember%2A> restituisce un valore booleano che restituisce `true` se il membro richiesto esiste. In caso contrario, restituisce `false`.  
  
     [!code-cs[VbDynamicWalkthrough#6](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_6.cs)]
     [!code-vb[VbDynamicWalkthrough#6](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_6.vb)]  
  
11. Dopo il metodo `TryGetMember`, aggiungere il codice seguente per eseguire l'override del metodo <xref:System.Dynamic.DynamicObject.TryInvokeMember%2A> della classe <xref:System.Dynamic.DynamicObject>.  Il metodo <xref:System.Dynamic.DynamicObject.TryInvokeMember%2A> viene chiamato quando viene richiesto un membro di una classe dinamica e si specificano argomenti.  L'argomento `binder` contiene informazioni sul membro a cui si fa riferimento e l'argomento `result` fa riferimento al risultato restituito per il membro specificato.  L'argomento `args` contiene una matrice degli argomenti passati al membro.  Il metodo <xref:System.Dynamic.DynamicObject.TryInvokeMember%2A> restituisce un valore booleano che restituisce `true` se il membro richiesto esiste. In caso contrario, restituisce `false`.  
  
     La versione personalizzata del metodo `TryInvokeMember` prevede che il primo argomento sia un valore ottenuto dall'enumerazione `StringSearchOption` definita in un passaggio precedente.  Il metodo `TryInvokeMember` prevede che il secondo argomento sia un valore booleano.  Se uno o entrambi gli argomenti sono valori validi, vengono passati al metodo `GetPropertyValue` per recuperare i risultati.  
  
     [!code-cs[VbDynamicWalkthrough#7](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_7.cs)]
     [!code-vb[VbDynamicWalkthrough#7](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_7.vb)]  
  
12. Salvare e chiudere il file.  
  
#### Per creare un file di testo di esempio  
  
1.  Fare clic con il pulsante destro del mouse sul progetto DynamicSample e selezionare **Aggiungi**, quindi scegliere **Nuovo elemento**.  Nel riquadro **Modelli installati**, selezionare **Generale**, quindi selezionare il modello **File di testo**.  Non modificare il nome predefinito TextFile1.txt nella casella **Nome**, quindi fare clic su **Aggiungi**.  Un nuovo file di testo verrà aggiunto al progetto.  
  
2.  Copiare il testo seguente nel file TextFile1.txt.  
  
    ```  
    List of customers and suppliers  
  
    Supplier: Lucerne Publishing (http://www.lucernepublishing.com/)  
    Customer: Preston, Chris  
    Customer: Hines, Patrick  
    Customer: Cameron, Maria  
    Supplier: Graphic Design Institute (http://www.graphicdesigninstitute.com/)   
    Supplier: Fabrikam, Inc. (http://www.fabrikam.com/)   
    Customer: Seubert, Roxanne  
    Supplier: Proseware, Inc. (http://www.proseware.com/)   
    Customer: Adolphi, Stephan  
    Customer: Koch, Paul  
    ```  
  
3.  Salvare e chiudere il file.  
  
#### Per creare un'applicazione di esempio che utilizza l'oggetto dinamico personalizzato  
  
1.  In **Esplora soluzioni**, fare doppio clic sul file Module1.vb se si utilizza [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] oppure sul file Program.cs se si utilizza Visual C\#.  
  
2.  Aggiungere il codice seguente alla routine Main per creare un'istanza della classe `ReadOnlyFile` per il file TextFile1.txt.  Il codice utilizza l'associazione tardiva per chiamare i membri dinamici e recuperare le righe di testo che contengono la stringa "Customer".  
  
     [!code-cs[VbDynamicWalkthrough#8](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_8.cs)]
     [!code-vb[VbDynamicWalkthrough#8](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_8.vb)]  
  
3.  Salvare il file e premere CTRL\+F5 per compilare ed eseguire l'applicazione.  
  
## Chiamata di una DLL  
 Il progetto successivo che si creerà in questa procedura dettagliata consentirà di accedere a una libreria scritta nel linguaggio dinamico IronPython.  Prima di creare il progetto, è necessario disporre di IronPython 2.6.1 per .NET 4,0 installato.  È possibile scaricare IronPython 2.6.1 per .NET 4.0 da [CodePlex](http://go.microsoft.com/fwlink/?LinkId=187223) \(la pagina potrebbe essere in inglese\).  
  
#### Per creare una classe dinamica personalizzata  
  
1.  Scegliere **Nuovo** dal menu **File** di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)], quindi fare clic su **Progetto**.  
  
2.  Nel riquadro **Tipi progetto** della finestra di dialogo **Nuovo progetto** verificare che sia selezionata la voce **Finestre**.  Selezionare **Applicazione console** nel riquadro **Modelli**.  Nella casella **Nome** digitare `DynamicIronPythonSample`, quindi fare clic su **OK**.  Verrà creato il nuovo progetto.  
  
3.  Se si utilizza [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], fare clic con il pulsante destro del mouse sul progetto DynamicIronPythonSample e scegliere **Proprietà**.  Fare clic sulla scheda **Riferimenti**.  Fare clic sul pulsante **Aggiungi**.  Se si utilizza Visual C\#, fare clic con il pulsante destro del mouse sulla cartella **Riferimenti** in **Esplora soluzioni**, quindi scegliere **Aggiungi riferimento**.  
  
4.  Nella scheda **Sfoglia** passare alla cartella in cui sono installate le librerie di IronPython.  Ad esempio, C:\\Programmi\\IronPython 2.6 per .NET 4.0.  Selezionare le librerie **IronPython.dll**, **IronPython.Modules.dll**, **Microsoft.Scripting.dll** e **Microsoft.Dynamic.dll**.  Fare clic su **OK**.  
  
5.  Se si utilizza [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], modificare il file Module1.vb.  Se si utilizza Visual C\#, modificare il file Program.cs.  
  
6.  All'inizio del file, aggiungere il codice seguente per importare gli spazi dei nomi `Microsoft.Scripting.Hosting` e `IronPython.Hosting` dalle librerie di IronPython.  
  
     [!code-cs[VbDynamicWalkthroughIronPython#1](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_9.cs)]
     [!code-vb[VbDynamicWalkthroughIronPython#1](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_9.vb)]  
  
7.  Nel metodo principale, aggiungere il seguente codice per creare un nuovo oggetto `Microsoft.Scripting.Hosting.ScriptRuntime` per contenere le librerie di IronPython.  L'oggetto `ScriptRuntime` carica il modulo di libreria random.py di IronPython.  
  
     [!code-cs[VbDynamicWalkthroughIronPython#2](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_10.cs)]
     [!code-vb[VbDynamicWalkthroughIronPython#2](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_10.vb)]  
  
8.  Dopo il codice per aggiungere il modulo random.py, aggiungere il seguente codice per creare una matrice di integer.  La matrice viene passata al metodo `shuffle` del modulo random.py, che ordina casualmente i valori nella matrice.  
  
     [!code-cs[VbDynamicWalkthroughIronPython#3](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_11.cs)]
     [!code-vb[VbDynamicWalkthroughIronPython#3](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_11.vb)]  
  
9. Salvare il file e premere CTRL\+F5 per compilare ed eseguire l'applicazione.  
  
## Vedere anche  
 <xref:System.Dynamic?displayProperty=fullName>   
 <xref:System.Dynamic.DynamicObject?displayProperty=fullName>   
 [Utilizzo del tipo dinamico](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [Early and Late Binding](../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md)   
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)   
 [Implementazione delle interfacce dinamiche \(blog esterno\)](http://go.microsoft.com/fwlink/?LinkId=230895)