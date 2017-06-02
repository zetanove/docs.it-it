---
title: "Eliminare l&#39;ambito della transazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 49fb6dd4-30d4-4067-925c-c5de44c8c740
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Eliminare l&#39;ambito della transazione
In questo esempio viene illustrato come modificare un'attività `SuppressTransactionScope` personalizzata per annullare la transazione di runtime di ambiente, se presente.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\Transactions\SuppressTransactionScope`  
  
## Dettagli dell'esempio  
 L'attività personalizzata è utile per impedire che una transazione venga propagata a un altro servizio se il flusso della transazione risulta indesiderabile per un particolare scenario.Nell'esecuzione del flusso di lavoro è presente il supporto incorporato per eliminare la transazione di ambiente nella classe <xref:System.Activities.NativeActivity>, ma per utilizzare questo supporto è necessario modificare un oggetto <xref:System.Activities.NativeActivity> personalizzato come quello utilizzato in questo esempio.  
  
 Lo scenario è costituito da tre parti.Innanzitutto, un oggetto <xref:System.Activities.Statements.TransactionScope> crea una transazione di runtime che diventa di ambiente.Questa operazione viene verificata da un'attività personalizzata che stampa gli identificatori locali e distribuiti della transazione.La transazione viene quindi propagata a un servizio remoto prima di iniziare la seconda parte.Durante la seconda parte, il flusso di lavoro apre un'attività `SuppressTransactionScope` e ripete di nuovo il processo di stampa degli identificatori della transazione e di propagazione della transazione.L'attività personalizzata non trova tuttavia una transazione di ambiente e il messaggio propagato al servizio non contiene la transazione.Di conseguenza, il servizio crea una transazione e ciò significa che l'ID distribuito stampato sul client e il servizio non corrispondono.La parte finale si verifica dopo la chiusura di `SuppressTransactionScope` e la transazione di runtime diventa nuovamente di ambiente, come risulta da un altro messaggio al servizio con un identificatore distribuito che corrisponde all'identificatore del primo messaggio.  
  
 L'attività stessa deriva da <xref:System.Activities.NativeActivity> perché deve pianificare un'attività figlio e aggiungere una proprietà di esecuzione.`SuppressTransactionScope` dispone di un oggetto <xref:System.Activities.Variable> di tipo <xref:System.Activities.RuntimeTransactionHandle> che deve essere utilizzato al posto di un campo di istanza di tipo <xref:System.Activities.RuntimeTransactionHandle> perché è necessario inizializzare l'handle.`Variable<RuntimeTransactionHandle>` viene aggiunto ai metadati dell'attività come una variabile di implementazione in quanto è utilizzato solo internamente.  
  
 Durante l'esecuzione dell'attività, viene controllato innanzitutto se è stato specificato un corpo e, in tal caso, la proprietà `SuppressTransaction` viene impostata su <xref:System.Activities.RuntimeTransactionHandle>.Una volta impostata, la proprietà viene aggiunta alle proprietà di esecuzione e diventa di ambiente.Ciò significa che qualsiasi attività figlio di `SuppressTransactionScope` è in grado di visualizzare la proprietà, pertanto viene applicata l'eliminazione della transazione di runtime e viene generata un'eccezione da parte di un oggetto <xref:System.Activities.Statements.TransactionScope> annidato.Una volta aggiunto l'handle alle proprietà di esecuzione, viene pianificata l'esecuzione del corpo.  
  
#### Per utilizzare questo esempio  
  
1.  Aprire la soluzione SuppressTransactionScope.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B o scegliere **Compila soluzione** dal menu **Compila**.  
  
3.  Una volta completata la compilazione, fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Imposta progetti di avvio**.Nella finestra di dialogo selezionare **Progetti di avvio multipli** e assicurarsi che l'azione per entrambi i progetti sia **Avvia**.  
  
4.  Premere F5 o scegliere **Avvia debug** dal menu **Debug**.In alternativa, è possibile premere CTRL\+F5 o scegliere **Avvia senza eseguire debug** dal menu **Debug** per l'esecuzione senza debug.  
  
    > [!NOTE]
    >  Il server deve essere in esecuzione prima dell'avvio del client.L'output dalla finestra della console che ospita il servizio indica quando è stato avviato.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\Transactions\SuppressTransactionScope`  
  
## Vedere anche