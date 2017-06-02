---
title: "Servizio casella degli strumenti | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 742212d0-445e-41ed-9739-9ee848ce7f1b
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Servizio casella degli strumenti
In questo esempio viene illustrato come aggiornare le attività della casella degli strumenti di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] in base al contesto del flusso di lavoro.L'esempio contiene un flusso di lavoro che modifica il contenuto della casella degli strumenti in base alla selezione o meno di un'attività personalizzata.  
  
## Discussione  
 Durante la creazione di flussi di lavoro, i clienti generalmente desiderano che Casella degli strumenti sia sensibile al contesto.Ad esempio, l'utente può volersi assicurare che nella Casella degli strumenti siano visualizzate alcune attività aggiuntive quando un'attività specifica viene aggiunta al flusso di lavoro.Se le attività vengono rimosse dal flusso di lavoro, la casella degli strumenti deve riflettere in modo appropriato i requisiti del dominio.  
  
 In una finestra di progettazione del flusso di lavoro riallocata è possibile verificare il controllo Casella degli strumenti e assicurarsi che in base alle modifiche del Modello nel flusso di lavoro, l'host attivi modifiche appropriate nel controllo Casella degli strumenti.Tuttavia, in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)], la casella degli strumenti non viene controllata dall'utente e quindi per modificarne il contenuto è necessaria un'interfaccia.`IActivityToolboxService` è l'interfaccia necessaria.  
  
 L'API fornisce i quattro metodi seguenti.  
  
```  
public interface IActivityToolboxService   
{   
        void AddCategory(string categoryName);   
        void RemoveCategory(string categoryName);   
        void AddItem(string qualifiedTypeName, string categoryName);   
        void RemoveItem(string qualifiedTypeName, string categoryName);   
        IList<string> EnumCategories();   
        IList<string> EnumItems(string categoryName);   
}  
```  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione WorkflowSimulator.sln.  
  
2.  Premere CTRL\+MAIUSC\+B per compilare la soluzione,  
  
3.  Aprire il file Workflow.xaml.  
  
4.  Aggiungere un oggetto **CustomActivity** trascinandolo dalla casella degli strumenti.Notare la presenza di una categoria Casella degli strumenti aggiuntiva denominata **Nuova categoria WF** con un'attività aggiuntiva **Assegna**.  
  
5.  Deselezionare **CustomActivity** trascinandovi sopra un'altra attività.  
  
6.  L'elemento **Assegna** nella categoria **Nuova categoria WF** nella Casella degli strumenti viene rimosso.Inoltre, poiché non sono rimasti elementi nella categoria, questa viene anch'essa rimossa.  
  
7.  Selezionare di nuovo **CustomActivity**. La categoria e l'attività **Assegna** vengono nuovamente aggiunte.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Designer\IActivityToolboxService`