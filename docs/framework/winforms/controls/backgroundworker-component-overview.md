---
title: "Cenni preliminari sul componente BackgroundWorker | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "BackgroundWorker"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Modello asincrono"
  - "operazioni in background"
  - "attività in background"
  - "BackgroundWorker (componente)"
  - "componenti [Windows Form], asincrono"
  - "form, operazioni in background"
  - "form, multithreading"
  - "threading [Windows Form], operazioni in background"
ms.assetid: 64e9b3ab-7443-4a77-ab17-b8b8c0cb3f62
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Cenni preliminari sul componente BackgroundWorker
Molte operazioni comuni hanno tempi di esecuzione particolarmente lunghi,  ad esempio:  
  
-   Download di immagini  
  
-   Chiamate di servizi Web  
  
-   Download e caricamento di file \(anche per applicazioni peer\-to\-peer\)  
  
-   Calcoli locali complessi  
  
-   Transazioni di database  
  
-   Accesso locale ai dischi, a causa della velocità ridotta rispetto all'accesso alla memoria  
  
 Durante l'esecuzione di questo tipo di operazioni è possibile che l'interfaccia utente si blocchi.  Nel caso sia necessario eseguire operazioni di questo genere ma si vogliano evitare ritardi di risposta dell'interfaccia utente, il componente <xref:System.ComponentModel.BackgroundWorker> costituisce la soluzione ideale.  
  
 Il componente <xref:System.ComponentModel.BackgroundWorker> offre la possibilità di eseguire operazioni che richiedono molto tempo in modo asincrono \(in background\) su un thread diverso da quello usato dall'interfaccia utente principale dell'applicazione.  Per usare un componente <xref:System.ComponentModel.BackgroundWorker>, è sufficiente indicare il metodo di lavoro da eseguire in background e quindi chiamare il metodo <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A>.  Il thread chiamante continua l'esecuzione normale mentre il metodo di lavoro viene eseguito in modo asincrono.  Al completamento dell'esecuzione del metodo, il componente <xref:System.ComponentModel.BackgroundWorker> avvisa il thread chiamante attivando l'evento <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>, in cui è possibile includere i risultati dell'operazione.  
  
 Il componente <xref:System.ComponentModel.BackgroundWorker> è disponibile mediante la **Casella degli strumenti** della scheda **Componenti**.  Per aggiungere un componente <xref:System.ComponentModel.BackgroundWorker> al form, trascinarlo nel form.  Verrà visualizzato nella barra dei componenti e le relative proprietà verranno incluse nella finestra **Proprietà**.  
  
 Per avviare l'operazione asincrona, usare il metodo <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A>.  Il metodo <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> accetta un parametro `object` facoltativo, che può essere usato per passare gli argomenti al metodo di lavoro.  La classe <xref:System.ComponentModel.BackgroundWorker> espone l'evento <xref:System.ComponentModel.BackgroundWorker.DoWork> a cui viene collegato il thread di lavoro mediante un gestore eventi <xref:System.ComponentModel.BackgroundWorker.DoWork>.  
  
 Il gestore eventi <xref:System.ComponentModel.BackgroundWorker.DoWork> accetta un parametro <xref:System.ComponentModel.DoWorkEventArgs> che include una proprietà <xref:System.ComponentModel.DoWorkEventArgs.Argument%2A>.  Questa proprietà riceve il parametro da <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> e può essere passata al metodo di lavoro, che verrà chiamato nel gestore eventi <xref:System.ComponentModel.BackgroundWorker.DoWork>.  L'esempio seguente illustra come assegnare un risultato proveniente da un metodo di lavoro denominato `ComputeFibonacci`.  Questo codice fa parte di un esempio più esaustivo fornito in [Procedura: implementare un form che utilizza un'operazione in background](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md).  
  
 [!code-cpp[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#5)]
 [!code-csharp[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#5)]
 [!code-vb[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#5)]  
  
 Per altre informazioni sull'uso dei gestori eventi, vedere [Eventi](../../../../docs/standard/events/index.md).  
  
> [!CAUTION]
>  L'uso di qualsiasi tipo di multithreading determina la potenziale esposizione a bug seri e complessi.  Prima di implementare qualsiasi soluzione che preveda l'uso del multithreading, vedere [Managed Threading Best Practices](../../../../docs/standard/threading/managed-threading-best-practices.md).  
  
 Per altre informazioni sull'uso della classe <xref:System.ComponentModel.BackgroundWorker>, vedere [Procedura: eseguire un'operazione in background](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md).  
  
## Vedere anche  
 [NOT IN BUILD: Multithreading in Visual Basic](http://msdn.microsoft.com/it-it/c731a50c-09c1-4468-9646-54c86b75d269)   
 [Procedura: implementare un form che utilizza un'operazione in background](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)