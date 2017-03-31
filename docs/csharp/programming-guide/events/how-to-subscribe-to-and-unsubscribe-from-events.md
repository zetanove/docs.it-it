---
title: 'Procedura: Sottoscrivere e annullare la sottoscrizione di eventi (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- event handlers [C#], creating
- Code Editor, event handlers
- events [C#], creating using the IDE
ms.assetid: 6319f39f-282c-4173-8a62-6c4657cf51cd
caps.latest.revision: 15
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
ms.openlocfilehash: 583168bc8cce2f4bee9a2dd35d1e59c7a0f380a6
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-subscribe-to-and-unsubscribe-from-events-c-programming-guide"></a>Procedura: sottoscrivere e annullare la sottoscrizione di eventi (Guida per programmatori C#)
Si sottoscrive un evento pubblicato da un'altra classe quando si vuole scrivere codice personalizzato che viene chiamato quando viene generato tale evento. È ad esempio possibile sottoscrivere l'evento `click` di un pulsante perché l'applicazione esegua un'operazione utile quando l'utente fa clic sul pulsante in questione.  
  
### <a name="to-subscribe-to-events-by-using-the-visual-studio-ide"></a>Per sottoscrivere gli eventi usando l'IDE di Visual Studio  
  
1.  Se la finestra **Proprietà** non viene visualizzata, nella visualizzazione **Progettazione** fare clic con il pulsante destro del mouse sul modulo o sul controllo per cui si vuole creare un gestore eventi e selezionare **Proprietà**.  
  
2.  Nella parte superiore della finestra **Proprietà** fare clic sull'icona **Eventi**.  
  
3.  Fare doppio clic sull'evento che si vuole creare, ad esempio sull'evento `Load`.  
  
     [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] crea un metodo del gestore eventi vuoto e lo aggiunge al codice. In alternativa, è possibile aggiungere manualmente il codice nella visualizzazione **Codice**. Ad esempio, le righe di codice seguenti dichiarano un metodo del gestore eventi che verrà chiamato quando la classe `Form` genera l'evento `Load`.  
  
     [!code-cs[csProgGuideEvents#11](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-subscribe-to-and-unsubscribe-from-events_1.cs)]  
  
     La riga di codice necessaria per sottoscrivere l'evento viene generata automaticamente nel metodo `InitializeComponent` nel file Form1.Designer.cs del progetto. La riga ha un aspetto simile a quanto riportato di seguito:  
  
    ```  
    this.Load += new System.EventHandler(this.Form1_Load);  
    ```  
  
### <a name="to-subscribe-to-events-programmatically"></a>Per sottoscrivere gli eventi a livello di codice  
  
1.  Definire un metodo del gestore eventi la cui firma corrisponda alla firma del delegato per l'evento. Se ad esempio l'evento è basato sul tipo di delegato <xref:System.EventHandler>, il codice riportato di seguito rappresenta lo stub del metodo:  
  
    ```  
    void HandleCustomEvent(object sender, CustomEventArgs a)  
    {  
       // Do something useful here.  
    }  
    ```  
  
2.  Usare l'operatore di assegnazione di addizione (`+=`) per associare il gestore eventi all'evento. Nell'esempio seguente si supponga che a un oggetto denominato `publisher` sia associato un evento denominato `RaiseCustomEvent`. Si noti che per la classe subscriber è necessario un riferimento alla classe publisher per sottoscrivere gli eventi corrispondenti.  
  
    ```  
    publisher.RaiseCustomEvent += HandleCustomEvent;  
    ```  
  
     Si noti che la sintassi precedente è nuova in C# 2.0. Equivale esattamente alla sintassi di C# 1.0, in cui è necessario creare in modo esplicito il delegato incapsulante tramite la parola chiave `new`:  
  
    ```  
    publisher.RaiseCustomEvent += new CustomEventHandler(HandleCustomEvent);  
    ```  
  
     È possibile aggiungere un gestore eventi anche tramite un'espressione lambda:  
  
    ```  
    public Form1()  
    {  
        InitializeComponent();  
        // Use a lambda expression to define an event handler.  
        this.Click += (s,e) => { MessageBox.Show(  
           ((MouseEventArgs)e).Location.ToString());};  
    }  
    ```  
  
     Per altre informazioni, vedere [Procedura: Usare espressioni lambda al di fuori di LINQ (Guida per programmatori C#)](../../../csharp/programming-guide/statements-expressions-operators/how-to-use-lambda-expressions-outside-linq.md).  
  
### <a name="to-subscribe-to-events-by-using-an-anonymous-method"></a>Per sottoscrivere gli eventi usando un metodo anonimo  
  
-   Se non è necessario annullare la sottoscrizione di un evento in un secondo momento, è possibile usare l'operatore di assegnazione di addizione (`+=`) per associare un metodo anonimo all'evento. Nell'esempio seguente si supponga che a un oggetto denominato `publisher` sia associato un evento denominato `RaiseCustomEvent` e che sia stata definita una classe `CustomEventArgs` con informazioni specializzate sull'evento. Si noti che per la classe subscriber è necessario un riferimento alla classe `publisher` per sottoscrivere gli eventi corrispondenti.  
  
    ```  
    publisher.RaiseCustomEvent += delegate(object o, CustomEventArgs e)  
    {  
      string s = o.ToString() + " " + e.ToString();  
      Console.WriteLine(s);  
    };  
    ```  
  
     È importante notare che non si può annullare facilmente la sottoscrizione di un evento se per la sottoscrizione è stata usata una funzione anonima. Per annullare la sottoscrizione in questo scenario, è necessario tornare al codice in cui è stato sottoscritto l'evento, archiviare il metodo anonimo in una variabile del delegato e quindi aggiungere il delegato all'evento. In generale è consigliabile non usare funzioni anonime per sottoscrivere eventi se si prevede di dover annullare la sottoscrizione all'evento in un punto successivo nel codice. Per altre informazioni sulle funzioni anonime, vedere [Funzioni anonime](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md).  
  
## <a name="unsubscribing"></a>Annullamento della sottoscrizione  
 Per evitare che il gestore eventi venga chiamato al momento della generazione dell'evento, annullare la sottoscrizione all'evento stesso. Per evitare di perdere risorse, è necessario annullare la sottoscrizione agli eventi prima di eliminare un oggetto sottoscrittore. Finché non si annulla la sottoscrizione di un evento, il delegato multicast sottostante all'evento nell'oggetto publisher contiene un riferimento al delegato che incapsula il gestore eventi del sottoscrittore. Finché l'oggetto publisher include tale riferimento, l'oggetto subscriber non verrà eliminato dal processo di Garbage Collection.  
  
#### <a name="to-unsubscribe-from-an-event"></a>Per annullare la sottoscrizione di un evento  
  
-   Usare l'operatore di assegnazione di sottrazione (`-=`):  
  
    ```  
    publisher.RaiseCustomEvent -= HandleCustomEvent;  
    ```  
  
     Quando tutti i sottoscrittori hanno annullato la sottoscrizione a un evento, l'istanza dell'evento nella classe publisher viene impostata su `null`.  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [event](../../../csharp/language-reference/keywords/event.md)   
 [Procedura: Pubblicare eventi conformi alle linee guida di .NET Framework](../../../csharp/programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md)   
 [Operatore -= (Riferimenti per C#)](../../language-reference/operators/subtraction-assignment-operator.md)   
 [Operatore +=](../../../csharp/language-reference/operators/addition-assignment-operator.md)

