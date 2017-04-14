---
title: "Procedura: creare un servizio di flusso di lavoro che utilizza un contratto di servizio esistente | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 11d11b59-acc4-48bf-8e4b-e97b516aa0a9
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Procedura: creare un servizio di flusso di lavoro che utilizza un contratto di servizio esistente
[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] offre una maggiore integrazione tra i servizi Web e i flussi di lavoro sotto forma di sviluppo di flussi di lavoro con priorità al contratto.Lo strumento di sviluppo di flussi di lavoro con priorità al contratto consente di progettare il contratto innanzitutto nel codice.Lo strumento consente di generare automaticamente un modello di attività nella casella degli strumenti per le operazioni nel contratto.  
  
> [!NOTE]
>  In questo argomento vengono fornite le istruzioni dettagliate per la creazione di un servizio del flusso di lavoro con priorità al contratto \("contract\-first"\).[!INCLUDE[crabout](../../../includes/crabout-md.md)]llo sviluppo del servizio del flusso di lavoro con priorità al contratto \("contract\-first"\), vedere [Sviluppo del servizio del flusso di lavoro con priorità al contratto \("contract\-first"\)](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md).  
  
### Creazione del progetto flusso di lavoro  
  
1.  In [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] fare clic su **File**, quindi su **Nuovo progetto**.Selezionare il nodo **WCF** nel nodo **C\#** nell'albero **Modelli** e selezionare il modello **Applicazione di servizi flusso di lavoro WCF**.  
  
2.  Assegnare il nome `ContractFirst` al nuovo progetto, quindi fare clic su **OK**.  
  
### Creazione del contratto di servizio  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Aggiungi**, **Nuovo elemento…**.Selezionare il nodo **Codice** a sinistra e il modello **Classe** a destra.Assegnare il nome `IBookService` alla nuova classe e fare clic su **OK**.  
  
2.  Nella parte superiore della finestra del codice visualizzata, aggiungere un'istruzione Using a `System.Servicemodel`.  
  
    ```  
    using System.ServiceModel;  
    ```  
  
3.  Modificare la definizione della classe di esempio nella definizione di interfaccia seguente.  
  
    ```  
    [ServiceContract]  
        public interface IBookService  
        {  
            [OperationContract]  
            void Buy(string bookName);  
  
            [OperationContract(IsOneWay=true)]  
            void Checkout();  
        }  
    ```  
  
4.  Premere **CTRL\+MAIUSC\+B** per compilare il progetto.  
  
### Importazione del contratto di servizio  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e selezionare **Importa contratto del servizio**.In **\<Progetto corrente\>** aprire tutti i sottonodi e selezionare **IBookService**.Scegliere **OK**.  
  
2.  Verrà visualizzata una finestra di dialogo indicante che l'operazione è stata completata correttamente e che le attività generate verranno inserite nella casella degli strumenti dopo che il progetto sarà stato compilato.Scegliere **OK**.  
  
3.  Compilare il progetto premendo **CTRL\+MAIUSC\+B**; in questo modo le attività importate saranno visualizzate nella casella degli strumenti.  
  
4.  In **Esplora soluzioni** aprire il file Service1.xamlx.Il servizio del flusso di lavoro verrà visualizzata nella finestra di progettazione.  
  
5.  Selezionare l'attività **Sequence**.Nella finestra Proprietà fare clic sul pulsante **…** nella proprietà **ImplementedContract**.Nella finestra **Editor raccolta di tipi** che viene visualizzata fare clic sul menu a discesa **Tipo** e selezionare la voce **Cerca tipi**.Nella finestra di dialogo **Cerca e seleziona un tipo .NET**, in **\<Progetto corrente\>**, aprire tutti i sottonodi e selezionare **IBookService**.Scegliere **OK**.Nella finestra di dialogo **Editor raccolta di tipi** fare clic su **OK**.  
  
6.  Selezionare ed eliminare le attività **ReceiveRequest** e **SendResponse**.  
  
7.  Dalla casella degli strumenti, trascinare un'attività **Buy\_ReceiveAndSendReply** e un'attività **Checkout\_Receive** sull'attività **Sequential Service**.