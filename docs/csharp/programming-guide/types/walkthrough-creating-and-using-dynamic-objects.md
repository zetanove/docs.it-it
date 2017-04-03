---
title: 'Procedura dettagliata: Creazione e uso di oggetti dinamici (C# e Visual Basic) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- dynamic objects [Visual Basic]
- dynamic objects
- dynamic objects [C#]
ms.assetid: 568f1645-1305-4906-8625-5d77af81e04f
caps.latest.revision: 22
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 64f6354a6a5f2fdd078e7ae9a1bfafc65d53373d
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-creating-and-using-dynamic-objects-c-and-visual-basic"></a>Procedura dettagliata: creazione e utilizzo di oggetti dinamici (C# e Visual Basic)
Gli oggetti dinamici espongono i membri, ad esempio proprietà e metodi, in fase di esecuzione anziché in fase di compilazione. In questo modo è possibile creare oggetti da usare con le strutture che non corrispondono a un tipo o formato statico. Ad esempio, è possibile usare un oggetto dinamico per fare riferimento al modello a oggetti documenti (DOM, Document Object Model) HTML, che può contenere qualsiasi combinazione di attributi ed elementi di markup HTML validi. Poiché ogni documento HTML è univoco, i membri per un particolare documento HTML vengono determinati in fase di esecuzione. Un metodo comune per fare riferimento a un attributo di un elemento HTML consiste nel passare il nome dell'attributo al metodo `GetProperty` dell'elemento. Per fare riferimento all'attributo `id` dell'elemento HTML `<div id="Div1">`, per prima cosa è necessario ottenere un riferimento all'elemento `<div>` e quindi usare `divElement.GetProperty("id")`. Se si usa un oggetto dinamico, è possibile fare riferimento all'attributo `id` come `divElement.id`.  
  
 Gli oggetti dinamici offrono anche un comodo accesso a linguaggi dinamici come IronPython e IronRuby. È possibile usare un oggetto dinamico per fare riferimento a uno script dinamico che viene interpretato in fase di esecuzione.  
  
 Si fa riferimento a un oggetto dinamico usando l'associazione tardiva. In C# specificare il tipo di un oggetto ad associazione tardiva come `dynamic`. In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] specificare il tipo di un oggetto ad associazione tardiva come `Object`. Per altre informazioni, vedere [dynamic](../../../csharp/language-reference/keywords/dynamic.md) e [Associazione anticipata e tardiva](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md).  
  
 È possibile creare oggetti dinamici personalizzati usando le classi dello spazio dei nomi <xref:System.Dynamic?displayProperty=fullName>. Ad esempio, è possibile creare un oggetto <xref:System.Dynamic.ExpandoObject> e specificare i membri di tale oggetto in fase di esecuzione. È anche possibile creare un proprio tipo che eredita la classe <xref:System.Dynamic.DynamicObject>. È quindi possibile sostituire i membri della classe <xref:System.Dynamic.DynamicObject> per rendere disponibili funzionalità dinamiche in fase di esecuzione.  
  
 In questa procedura verranno illustrate le attività seguenti:  
  
-   Creare un oggetto personalizzato che espone dinamicamente il contenuto di un file di testo come proprietà di un oggetto.  
  
-   Creare un progetto che usa una libreria `IronPython`.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per completare questa procedura, è necessario avere IronPython 2.6.1 per .NET 4.0. È possibile scaricare IronPython 2.6.1 per .NET 4.0 da [CodePlex](http://go.microsoft.com/fwlink/?LinkId=187223).  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## <a name="creating-a-custom-dynamic-object"></a>Creare un oggetto dinamico personalizzato  
 Il primo progetto creato in questa procedura dettagliata definisce un oggetto dinamico personalizzato che esegue la ricerca del contenuto di un file di testo. Il testo da cercare viene specificato dal nome di una proprietà dinamica. Ad esempio, se il codice chiamante specifica `dynamicFile.Sample`, la classe dinamica restituisce un elenco generico di stringhe che contiene tutte le righe del file che iniziano con "Sample". La ricerca non fa distinzione tra maiuscole e minuscole. La classe dinamica supporta inoltre due argomenti facoltativi. Il primo argomento è un valore di enumerazione dell'opzione di ricerca che indica che la classe dinamica deve cercare le corrispondenze all'inizio della riga, alla fine della riga o in un punto qualsiasi nella riga. Il secondo argomento specifica che la classe dinamica deve eliminare gli spazi iniziali e finali da ogni riga prima di eseguire la ricerca. Ad esempio, se il codice chiamante specifica `dynamicFile.Sample(StringSearchOption.Contains)`, la classe dinamica cerca "Sample" in qualsiasi punto di una riga. Se il codice chiamante specifica `dynamicFile.Sample(StringSearchOption.StartsWith, false)`, la classe dinamica cerca "Sample" all'inizio di ogni riga e non rimuove gli spazi iniziali e finali. Il comportamento predefinito della classe dinamica è cercare una corrispondenza all'inizio di ogni riga e rimuovere gli spazi iniziali e finali.  
  
#### <a name="to-create-a-custom-dynamic-class"></a>Per creare una classe dinamica personalizzata  
  
1.  Avviare [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)].  
  
2.  Scegliere **Nuovo** dal menu **File** , quindi scegliere **Progetto**.  
  
3.  Nel riquadro **Tipi di progetto** della finestra di dialogo **Nuovo progetto** verificare che sia selezionata l'opzione **Windows**. Selezionare **Applicazione console** nel riquadro **Modelli**. Nella casella **Nome** digitare `DynamicSample` e quindi fare clic su **OK**. Il nuovo progetto viene creato.  
  
4.  Fare clic con il pulsante destro del mouse sul progetto DynamicSample e scegliere **Aggiungi**, quindi fare clic su **Classe**. Nella casella **Nome** digitare `ReadOnlyFile`, quindi fare clic su **OK**. Viene aggiunto un nuovo file che contiene la classe ReadOnlyFile.  
  
5.  Nella parte superiore del file ReadOnlyFile.cs o ReadOnlyFile.vb aggiungere il codice seguente per importare gli spazi dei nomi <xref:System.IO?displayProperty=fullName> e <xref:System.Dynamic?displayProperty=fullName>.  
  
     [!code-cs[VbDynamicWalkthrough#1](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_1.cs)]
     [!code-vb[VbDynamicWalkthrough#1](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_1.vb)]  
  
6.  L'oggetto dinamico personalizzato usa un'enumerazione per determinare i criteri di ricerca. Prima dell'istruzione di classe, aggiungere la seguente definizione di enumerazione.  
  
     [!code-cs[VbDynamicWalkthrough#2](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_2.cs)]
     [!code-vb[VbDynamicWalkthrough#2](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_2.vb)]  
  
7.  Aggiornare la dichiarazione di classe per ereditare la classe `DynamicObject`, come illustrato nell'esempio di codice seguente.  
  
     [!code-cs[VbDynamicWalkthrough#3](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_3.cs)]
     [!code-vb[VbDynamicWalkthrough#3](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_3.vb)]  
  
8.  Aggiungere il codice seguente alla classe `ReadOnlyFile` per definire un campo privato per il percorso del file e un costruttore per la classe `ReadOnlyFile`.  
  
     [!code-cs[VbDynamicWalkthrough#4](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_4.cs)]
     [!code-vb[VbDynamicWalkthrough#4](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_4.vb)]  
  
9. Aggiungere il metodo `GetPropertyValue` seguente alla classe `ReadOnlyFile`. Il metodo `GetPropertyValue` accetta come input i criteri di ricerca e restituisce le righe di un file di testo che soddisfano tali criteri di ricerca. I metodi dinamici specificati dalla classe `ReadOnlyFile` chiamano il metodo `GetPropertyValue` per recuperare i rispettivi risultati.  
  
     [!code-cs[VbDynamicWalkthrough#5](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_5.cs)]
     [!code-vb[VbDynamicWalkthrough#5](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_5.vb)]  
  
10. Dopo il metodo `GetPropertyValue` aggiungere il codice seguente per eseguire l'override del metodo <xref:System.Dynamic.DynamicObject.TryGetMember%2A> della classe <xref:System.Dynamic.DynamicObject>. Il metodo <xref:System.Dynamic.DynamicObject.TryGetMember%2A> viene chiamato quando viene richiesto un membro di una classe dinamica e non vengono specificati argomenti. L'argomento `binder` contiene informazioni relative al membro a cui viene fatto riferimento e l'argomento `result` fa riferimento al risultato restituito per il membro specificato. Il metodo <xref:System.Dynamic.DynamicObject.TryGetMember%2A> restituisce un valore booleano che restituisce `true` se il membro richiesto esiste, altrimenti restituisce `false`.  
  
     [!code-cs[VbDynamicWalkthrough#6](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_6.cs)]
     [!code-vb[VbDynamicWalkthrough#6](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_6.vb)]  
  
11. Dopo il metodo `TryGetMember` aggiungere il codice seguente per eseguire l'override del metodo <xref:System.Dynamic.DynamicObject.TryInvokeMember%2A> della classe <xref:System.Dynamic.DynamicObject>. Il metodo <xref:System.Dynamic.DynamicObject.TryInvokeMember%2A> viene chiamato quando viene richiesto un membro di una classe dinamica con argomenti. L'argomento `binder` contiene informazioni relative al membro a cui viene fatto riferimento e l'argomento `result` fa riferimento al risultato restituito per il membro specificato. L'argomento `args` contiene una matrice degli argomenti passati al membro. Il metodo <xref:System.Dynamic.DynamicObject.TryInvokeMember%2A> restituisce un valore booleano che restituisce `true` se il membro richiesto esiste, altrimenti restituisce `false`.  
  
     La versione personalizzata del metodo `TryInvokeMember` prevede che il primo argomento sia un valore dell'enumerazione `StringSearchOption` definita in un passaggio precedente. Il metodo `TryInvokeMember` prevede che il secondo argomento sia un valore booleano. Se uno o entrambi gli argomenti sono valori validi, vengono passati al metodo `GetPropertyValue` per recuperare i risultati.  
  
     [!code-cs[VbDynamicWalkthrough#7](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_7.cs)]
     [!code-vb[VbDynamicWalkthrough#7](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_7.vb)]  
  
12. Salvare e chiudere il file.  
  
#### <a name="to-create-a-sample-text-file"></a>Per creare un file di testo di esempio  
  
1.  Fare clic con il pulsante destro del mouse sul progetto DynamicSample e scegliere **Aggiungi**, quindi fare clic su **Nuovo elemento**. Nel riquadro **Modelli installati** selezionare **Generale**, quindi il modello **File di testo**. Lasciare il nome predefinito TextFile1.txt nella casella **Nome** e quindi fare clic su **Aggiungi**. Un nuovo file di testo viene aggiunto al progetto.  
  
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
  
#### <a name="to-create-a-sample-application-that-uses-the-custom-dynamic-object"></a>Per creare un'applicazione di esempio che usa l'oggetto dinamico personalizzato  
  
1.  In **Esplora Soluzioni** fare doppio clic sul file Module1.vb se si usa [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] o sul file Program.cs se si usa Visual C#.  
  
2.  Aggiungere il seguente codice alla routine Main per creare un'istanza della classe `ReadOnlyFile` per il file TextFile1.txt. Il codice usa l'associazione tardiva per chiamare i membri dinamici e recuperare le righe di testo che contengono la stringa "Customer".  
  
     [!code-cs[VbDynamicWalkthrough#8](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_8.cs)]
     [!code-vb[VbDynamicWalkthrough#8](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_8.vb)]  
  
3.  Salvare il file e premere CTRL+F5 per compilare ed eseguire l'applicazione.  
  
## <a name="calling-a-dynamic-language-library"></a>Chiamare una libreria di linguaggio dinamico  
 Il progetto successivo di questa procedura dettagliata accede a una libreria scritta nel linguaggio dinamico IronPython. Prima di creare il progetto, è necessario installare IronPython 2.6.1 per .NET 4.0. È possibile scaricare IronPython 2.6.1 per .NET 4.0 da [CodePlex](http://go.microsoft.com/fwlink/?LinkId=187223).  
  
#### <a name="to-create-a-custom-dynamic-class"></a>Per creare una classe dinamica personalizzata  
  
1.  In [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] scegliere **Nuovo** dal menu **File** e quindi fare clic su **Progetto**.  
  
2.  Nel riquadro **Tipi di progetto** della finestra di dialogo **Nuovo progetto** verificare che sia selezionata l'opzione **Windows**. Selezionare **Applicazione console** nel riquadro **Modelli**. Nella casella **Nome** digitare `DynamicIronPythonSample` e quindi fare clic su **OK**. Il nuovo progetto viene creato.  
  
3.  Se si usa [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], fare clic con il pulsante destro del mouse sul progetto DynamicIronPythonSample e quindi fare clic su **Proprietà**. Fare clic sulla scheda **Riferimenti**. Fare clic sul pulsante **Aggiungi**. Se si usa Visual C#, in **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella **Riferimenti** e quindi fare clic su **Aggiungi riferimento**.  
  
4.  Nella scheda **Sfoglia** passare alla cartella in cui sono installate le librerie di IronPython. Ad esempio, C:\Programmi\IronPython 2.6 for .NET 4.0. Selezionare le librerie **IronPython.dll**, **IronPython.Modules.dll**, **Microsoft.Scripting.dll** e **Microsoft.Dynamic.dll**. Fare clic su **OK**.  
  
5.  Se si usa [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], modificare il file Module1.vb. Se si usa Visual C#, modificare il file Program.cs.  
  
6.  Nella parte superiore del file aggiungere il codice seguente per importare gli spazi dei nomi `Microsoft.Scripting.Hosting` e `IronPython.Hosting` dalle librerie di IronPython.  
  
     [!code-cs[VbDynamicWalkthroughIronPython#1](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_9.cs)]
     [!code-vb[VbDynamicWalkthroughIronPython#1](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_9.vb)]  
  
7.  Nel metodo Main aggiungere il codice seguente per creare un nuovo oggetto `Microsoft.Scripting.Hosting.ScriptRuntime` per ospitare le librerie di IronPython. L'oggetto `ScriptRuntime` carica il modulo di libreria random.py di IronPython.  
  
     [!code-cs[VbDynamicWalkthroughIronPython#2](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_10.cs)]
     [!code-vb[VbDynamicWalkthroughIronPython#2](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_10.vb)]  
  
8.  Dopo il codice che carica il modulo random.py, aggiungere il codice seguente per creare una matrice di numeri interi. La matrice viene passata al metodo `shuffle` del modulo random.py, che ordina i valori nella matrice in modo casuale.  
  
     [!code-cs[VbDynamicWalkthroughIronPython#3](../../../csharp/programming-guide/types/codesnippet/CSharp/walkthrough-creating-and-using-dynamic-objects_11.cs)]
     [!code-vb[VbDynamicWalkthroughIronPython#3](../../../csharp/programming-guide/types/codesnippet/VisualBasic/walkthrough-creating-and-using-dynamic-objects_11.vb)]  
  
9. Salvare il file e premere CTRL+F5 per compilare ed eseguire l'applicazione.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Dynamic?displayProperty=fullName>   
 <xref:System.Dynamic.DynamicObject?displayProperty=fullName>   
 [Uso del tipo dinamico](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [Associazione anticipata e tardiva](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)   
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)   
 [Implementazione delle interfacce dinamiche (blog esterno)](http://go.microsoft.com/fwlink/?LinkId=230895)
