---
title: "Procedura: sottoscrivere e annullare la sottoscrizione di eventi (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "Editor di codice, gestori eventi"
  - "gestori eventi [C#], creazione"
  - "eventi [C#], creazione mediante l'IDE"
ms.assetid: 6319f39f-282c-4173-8a62-6c4657cf51cd
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Procedura: sottoscrivere e annullare la sottoscrizione di eventi (Guida per programmatori C#)
Si sottoscrive un evento pubblicato da un'altra classe quando si desidera scrivere codice personalizzato che viene chiamato quando viene generato tale evento.  È ad esempio possibile sottoscrivere l'evento `click` di un pulsante affinché venga eseguita un'operazione utile nell'applicazione quando l'utente fa clic sul pulsante.  
  
### Per sottoscrivere gli eventi utilizzando l'IDE di Visual Studio  
  
1.  Se la finestra **Proprietà** non viene visualizzata, nella visualizzazione **Struttura**, fare clic con il pulsante destro del mouse sul modulo o sul controllo per cui si desidera creare un gestore dell'evento e selezionare **Proprietà**.  
  
2.  Nella parte superiore della finestra **Proprietà** fare clic sull'icona **Eventi**.  
  
3.  Fare doppio clic sull'evento che si desidera creare, ad esempio sull'evento `Load`.  
  
     In [!INCLUDE[csprcs](../../../csharp/includes/csprcs-md.md)] verrà creato un metodo di gestore eventi vuoto che verrà aggiunto al codice.  In alternativa è possibile aggiungere manualmente il codice nella visualizzazione **Codice**.  Ad esempio, le righe di codice seguenti dichiarano un metodo di gestore eventi che verrà chiamato quando la classe `Form` genera l'evento `Load`.  
  
     [!code-cs[csProgGuideEvents#11](../../../csharp/programming-guide/events/codesnippet/csharp/how-to-subscribe-to-and-_1.cs)]  
  
     La riga di codice necessaria per sottoscrivere l'evento viene generata automaticamente nel metodo `InitializeComponent` nel file Form1.Designer.cs del progetto.  Ha un aspetto simile a quanto riportato di seguito:  
  
    ```  
    this.Load += new System.EventHandler(this.Form1_Load);  
    ```  
  
### Per sottoscrivere gli eventi a livello di codice  
  
1.  Definire un metodo di gestore eventi la cui firma corrisponda alla firma del delegato per l'evento.  Ad esempio, se l'evento è basato sul tipo delegato <xref:System.EventHandler>, il codice riportato di seguito rappresenta lo stub del metodo:  
  
    ```  
    void HandleCustomEvent(object sender, CustomEventArgs a)  
    {  
       // Do something useful here.  
    }  
    ```  
  
2.  Utilizzare l'operatore di assegnazione di addizione \(`+=`\) per associare il gestore dell'evento all'evento.  Nell'esempio seguente si supponga che a un oggetto denominato `publisher` sia associato un evento denominato `RaiseCustomEvent`.  Si noti che per la classe sottoscrittore è necessario un riferimento alla classe autore per sottoscrivere gli eventi corrispondenti.  
  
    ```  
    publisher.RaiseCustomEvent += HandleCustomEvent;  
    ```  
  
     Si noti che la sintassi precedente è nuova in C\# 2.0.  È esattamente equivalente alla sintassi di C\# 1.0, in cui è necessario creare in modo esplicito il delegato incapsulante utilizzando la parola chiave `new`:  
  
    ```  
    publisher.RaiseCustomEvent += new CustomEventHandler(HandleCustomEvent);  
    ```  
  
     È possibile aggiungere inoltre un gestore eventi utilizzando un'espressione lambda:  
  
    ```  
    public Form1()  
    {  
        InitializeComponent();  
        // Use a lambda expression to define an event handler.  
        this.Click += (s,e) => { MessageBox.Show(  
           ((MouseEventArgs)e).Location.ToString());};  
    }  
    ```  
  
     Per ulteriori informazioni, vedere la classe [Procedura: utilizzare espressioni lambda al di fuori di LINQ](../../../csharp/programming-guide/statements-expressions-operators/how-to-use-lambda-expressions-outside-linq.md).  
  
### Per sottoscrivere gli eventi utilizzando un metodo anonimo  
  
-   Se non è necessario annullare la sottoscrizione di un evento in un secondo momento, è possibile utilizzare l'operatore di assegnazione di addizione \(`+=`\) per associare un metodo anonimo all'evento.  Nell'esempio seguente, si supponga che a un oggetto denominato `publisher` sia associato un evento denominato `RaiseCustomEvent`  e che sia stata definita una classe `CustomEventArgs` con informazioni specializzate sull'evento.  Si noti che per la classe sottoscrittore è necessario un riferimento alla classe `publisher` per sottoscrivere gli eventi corrispondenti.  
  
    ```  
    publisher.RaiseCustomEvent += delegate(object o, CustomEventArgs e)  
    {  
      string s = o.ToString() + " " + e.ToString();  
      Console.WriteLine(s);  
    };  
    ```  
  
     È importante notare che non si può annullare facilmente la sottoscrizione di un evento se per la sottoscrizione è stata utilizzata una funzione anonima.  Per annullare la sottoscrizione in questo scenario, è necessario tornare al codice in cui è stato sottoscritto l'evento, archiviare il metodo anonimo in una variabile del delegato, quindi aggiungere il delegato all'evento.  In generale, si consiglia di non utilizzare funzioni anonime per sottoscrivere eventi se si prevede di dover annullare la sottoscrizione all'evento in un punto successivo nel codice.  Per ulteriori informazioni sulle funzioni anonime, vedere [Funzioni anonime](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md).  
  
## Annullamento della sottoscrizione  
 Per impedire che il gestore dell'evento venga richiamato al momento della generazione dell'evento, annullare la sottoscrizione all'evento.  Per impedire perdite di risorse, è necessario annullare la sottoscrizione agli eventi prima di eliminare un oggetto sottoscrittore.  Finché non si annulla la sottoscrizione di un evento, il delegato multicast sottostante l'evento nell'oggetto di pubblicazione contiene un riferimento al delegato che incapsula il gestore eventi del sottoscrittore.  Finché l'oggetto di pubblicazione include tale riferimento, l'oggetto sottoscrittore non verrà eliminato dal processo di Garbage Collection.  
  
#### Per annullare la sottoscrizione di un evento  
  
-   Utilizzare l'operatore di assegnazione di sottrazione \(`-=`\) per annullare la sottoscrizione a un evento:  
  
    ```  
    publisher.RaiseCustomEvent -= HandleCustomEvent;  
    ```  
  
     Quando tutti i sottoscrittori hanno annullato la sottoscrizione a un evento, l'istanza dell'evento nella classe publisher viene impostata su `null`.  
  
## Vedere anche  
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [event](../../../csharp/language-reference/keywords/event.md)   
 [Procedura: pubblicare eventi conformi alle linee guida di .NET Framework](../../../csharp/programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md)   
 [Operatore \-\=](../../../csharp/language-reference/operators/subtraction-assignment-operator-1.md)   
 [Operatore \+\=](../../../csharp/language-reference/operators/addition-assignment-operator.md)