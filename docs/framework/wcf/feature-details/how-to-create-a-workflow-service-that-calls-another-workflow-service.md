---
title: "Procedura: creare un servizio di flusso di lavoro che chiama un altro servizio di flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 99b3ee3e-aeb7-4e6f-8321-60fe6140eb67
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Procedura: creare un servizio di flusso di lavoro che chiama un altro servizio di flusso di lavoro
Per un servizio di flusso di lavoro è talvolta necessario ottenere informazioni da un altro servizio analogo.In questo argomento viene illustrato come eseguire chiamate tra servizi di flusso di lavoro.Verranno creati due servizi di flusso di lavoro: uno che dispone di un metodo che inverte la stringa di input e l'altro che converte la stringa di input in caratteri maiuscoli dopo aver invertito la stringa utilizzata dal primo servizio.  
  
### Per creare il servizio di flusso di lavoro che esegue l'inversione  
  
1.  Eseguire [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] come amministratore.  
  
2.  Scegliere **Nuovo progetto** dal menu **File**.Nel nodo **Flusso di lavoro** del riquadro **Modelli installati** selezionare **Applicazione di servizi flusso di lavoro WCF**.Specificare il nome `NestedServices` per la soluzione, quindi fare clic su **OK**.  
  
3.  In **Server** verificare che sia selezionata l'opzione **Usa server Web IIS locale**.Fare clic su **Crea directory virtuale**,quindi fare clic su **OK** nella finestra di dialogo che conferma la creazione corretta della directory.  
  
4.  In Esplora soluzioni rinominare Service1.xamlx in `StringReverserService.xamlx`.  
  
5.  Nella pagina **Proprietà progetto** per il nuovo progetto fare clic sulla scheda **Web**.Impostare **Azione di avvio** su **Pagina specifica**, quindi selezionare StringReverserService.xamlx come pagina di avvio.  
  
6.  Aprire StringReverserService.xamlx nella finestra di progettazione, eliminare le attività `ReceiveRequest` e `SendReply` esistenti, quindi trascinare un'attività `ReceiveAndSendReply` nell'attività Sequence esistente.  
  
    1.  Impostare **OperationName** su ReverseString.  
  
    2.  Impostare **ServiceContractName** su IReverseString.  
  
    3.  Selezionare la casella di controllo **CanCreateInstance**.  
  
7.  Selezionare l'attività **SequentialService**, quindi fare clic sulla scheda **Variabili** nella parte inferiore della finestra di progettazione.Creare due nuove variabili di tipo String denominate StringToReverse e ReversedStringToReturn.  
  
8.  Fare clic sul collegamento **Define** nell'attività **Receive**.Fare clic su **Parameters**, quindi creare un parametro denominato InputString di tipo String da assegnare a StringToReverse.  
  
9. Fare clic sul collegamento **Define** nell'attività **SendReplyToReceive**.Fare clic su **Parameters**, quindi creare un parametro denominato ReversedString di tipo String assegnato a ReversedStringToReturn.  
  
10. Per implementare la logica per il servizio, creare una nuova classe nel progetto denominata StringLibrary.Sostituire la definizione della classe con il codice seguente.  
  
    ```  
    public class StringLibrary  
        {  
            public static String ReverseString(string StringToReverse)  
            {  
                char[] charArray = StringToReverse.ToCharArray();  
                Array.Reverse(charArray);  
                return new String(charArray);  
            }  
        }  
  
    ```  
  
11. Per chiamare il metodo ReverseString sull'input, trascinare un'attività **InvokeMethod** dalla casella degli strumenti nello spazio tra le attività **Receive** e **SendReply**.Impostare le proprietà dell'attività come indicato di seguito.  
  
    1.  **MethodName**: ReverseString  
  
    2.  **Result**: ReversedStringToReturn  
  
    3.  **Parameters**: creare un nuovo parametro impostando **Direction** su In, **Type** su String e **Value** su StringToReverse.  
  
    4.  **TargetType**: NestedServices.StringLibrary  
  
12. Premere F5 per testare il servizio.Nel client di test WCF visualizzato fare doppio clic sul metodo ReverseString\(\).Nel riquadro della richiesta immettere `Sample` come valore per il parametro InputString.Fare clic su **Richiama**.Il servizio deve restituire "elpmaS".  
  
### Per creare il servizio di flusso di lavoro che esegue la conversione in caratteri maiuscoli  
  
1.  Fare clic con il pulsante destro del mouse sul progetto NestedServices, quindi scegliere **Aggiungi**, **Nuovo elemento**.Nel nodo **Flusso di lavoro** selezionare **Servizio flusso di lavoro WCF**, quindi specificare il nome `UpperCaserService` per il nuovo servizio.Fare clic su **Aggiungi**.Un nuovo servizio di flusso di lavoro denominato UpperCaserService.xamlx verrà aggiunto al progetto.  
  
2.  Aprire UpperCaserService.xamlx nella finestra di progettazione, eliminare le attività **ReceiveRequest** e `SendReply` esistenti, quindi trascinare un'attività `ReceiveAndSendReply` nell'attività Sequence esistente.  
  
    1.  Impostare **OperationName** su UpperCaseString.  
  
    2.  Impostare **ServiceContractName** su IUpperCaseString.  
  
    3.  Selezionare la casella di controllo **CanCreateInstance**.  
  
3.  Selezionare l'attività SequentialService, quindi fare clic sulla scheda **Variabili** nella parte inferiore della finestra di progettazione.Creare tre nuove variabili di tipo String, denominate StringToUpper, StringToReverse e StringToReturn.  
  
4.  Fare clic sul collegamento **Define** nell'attività **Receive**.Fare clic su **Parameters**, quindi creare un parametro denominato InputString di tipo String da assegnare a StringToUpper.  
  
5.  Fare clic sul collegamento **Define** nell'attività **SendReplyToReceive**.Fare clic su **Parameters**, quindi creare un parametro denominato ModifiedString di tipo String assegnato a StringToReturn.  
  
6.  Per implementare la logica per il servizio, creare un nuovo metodo nella classe StringLibrary tramite il codice seguente.  
  
    ```  
    public static String UpperCaseString(string StringToUpperCase)  
    {  
         return StringToUpperCase.ToUpper();  
  
    }  
  
    ```  
  
7.  Per chiamare il metodo UpperCaseString sull'input, trascinare un'attività **InvokeMethod** dalla casella degli strumenti nello spazio tra le attività **Receive** e **SendReply**.Impostare le proprietà dell'attività come indicato di seguito.  
  
    1.  **MethodName**: UpperCaseString  
  
    2.  **Result**: StringToReverse  
  
    3.  **Parameters**: creare un nuovo parametro impostando **Direction** su In, **Type** su String e **Value** su StringToUpper.  
  
    4.  **TargetType**: NestedServices.StringLibrary  
  
8.  A questo punto verrà chiamato il primo servizio sulla stringa modificata.Fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Aggiungi riferimento al servizio**.Aggiungere un riferimento al servizio all'indirizzo http:\/\/localhost\/NestedServices\/StringReverserService.xamlx e compilare il progetto per creare un'attività personalizzata per accedere al primo servizio Web.  
  
9. Trascinare un'istanza della nuova attività sul flusso di lavoro, tra le attività **InvokeMethod** e **SendReplyToReceive**.Assegnare la variabile StringToReverse alla proprietà InputString della nuova attività e la variabile StringToReturn alla proprietà StringToReturn.  
  
10. Aprire la pagina Proprietà per il progetto NestedServices e impostare l'opzione **Pagina specifica** nella scheda **Web** su UpperCaserService.xamlx.  
  
11. Premere F5 per testare il servizio.Nel client di test WCF visualizzato fare doppio clic sul metodo ReverseString\(\).Nel riquadro della richiesta immettere `Sample` come valore per il parametro InputString.Fare clic su **Richiama**.Il servizio deve restituire "ELPMAS".  
  
### Per creare un client che chiami i servizi  
  
1.  Aggiungere un nuovo progetto di applicazione console denominato Client alla soluzione.  
  
2.  Fare clic con il pulsante destro del mouse sul progetto Client, quindi scegliere **Aggiungi riferimento al servizio**.Nella finestra visualizzata fare clic su **Individua**.Selezionare StringReverserService.xamlx e immettere ReverseService come spazio dei nomi.Fare clic su **OK**.  
  
3.  Sostituire il metodo Main in Program.cs con il codice seguente.  
  
    ```  
    static void Main(string[] args)  
    {  
        Console.Write("Input string to process:");  
        String input = Console.ReadLine();  
        var service = new ReverseService.ReverseStringClient();  
        Console.WriteLine("Output from service: {0}", service.ReverseString(input));  
        Console.ReadKey();  
    }  
  
    ```