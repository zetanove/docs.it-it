---
title: "Estensibilit&#224; dell&#39;archivio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7c3f4a46-4bac-4138-ae6a-a7c7ee0d28f5
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Estensibilit&#224; dell&#39;archivio
<xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> consente agli utenti di promuovere proprietà personalizzate specifiche dell'applicazione che possono essere utilizzate per eseguire query per istanze nel database di persistenza.L'atto di promuovere una proprietà fa in modo che il valore sia disponibile all'interno di una visualizzazione speciale nel database.Queste proprietà promosse, ovvero proprietà che possono essere utilizzate nelle query utente, possono essere di tipi semplici, ad esempio Int64, Guid, String e DateTime o di un tipo binario serializzato \(byte\[\]\).  
  
 La classe <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> dispone del metodo <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.Promote%2A> che può essere utilizzato per promuovere una proprietà come proprietà utilizzabile nelle query.Il seguente è un esempio end\-to\-end di estensibilità dell'archivio.  
  
1.  In questo scenario di esempio un'applicazione di elaborazione dei documenti \(DP, Document Processing\) dispone di flussi di lavoro in ognuno dei quali vengono utilizzate attività personalizzate per l'elaborazione dei documenti.Questi flussi di lavoro dispongono di un set di variabili di stato che devono essere rese visibili all'utente finale.A tale scopo, l'applicazione DP fornisce un'estensione dell'istanza di tipo <xref:System.Activities.Persistence.PersistenceParticipant>, utilizzata da attività per fornire le variabili di stato.  
  
    ```  
  
    class DocumentStatusExtension : PersistenceParticipant  
    {  
        public string DocumentId;  
        public string ApprovalStatus;  
        public string UserName;  
        public DateTime LastUpdateTime;  
    }  
  
    ```  
  
2.  La nuova estensione viene quindi aggiunta all'host.  
  
    ```  
    static Activity workflow = CreateWorkflow();  
    WorkflowApplication application = new WorkflowApplication(workflow);  
    DocumentStatusExtension documentStatusExtension = new DocumentStatusExtension ();  
    application.Extensions.Add(documentStatusExtension);  
  
    ```  
  
     Per informazioni più dettagliate sull'aggiunta di un partecipante di persistenza personalizzato, vedere l'esempio [Partecipanti di persistenza](../../../docs/framework/windows-workflow-foundation//persistence-participants.md).  
  
3.  Le attività personalizzate nell'applicazione DP popolano i vari campi di stato nel metodo **Execute**.  
  
    ```  
  
    public override void Execute(CodeActivityContext context)  
    {  
        // ...  
        context.GetExtension<DocumentStatusExtension>().DocumentId = Guid.NewGuid();  
        context.GetExtension<DocumentStatusExtension>().UserName = "John Smith";  
        context.GetExtension<DocumentStatusExtension>().ApprovalStatus = “Approved”;  
        context.GetExtension<DocumentStatusExtension>().LastUpdateTime = DateTime.Now();  
        // ...  
    }  
  
    ```  
  
4.  Quando un'istanza del flusso di lavoro raggiunge un punto di persistenza, il metodo **CollectValues** del partecipante di persistenza **DocumentStatusExtension** salva queste proprietà nella raccolta dati di persistenza.  
  
    ```  
  
    class DocumentStatusExtension : PersistenceParticipant  
    {  
        const XNamespace xNS = XNamespace.Get("http://contoso.com/DocumentStatus");  
  
        protected override void CollectValues(out IDictionary<XName, object> readWriteValues, out IDictionary<XName, object> writeOnlyValues)  
        {  
            readWriteValues = new Dictionary<XName, object>();  
            readWriteValues.Add(xNS.GetName("UserName"), this.UserName);  
            readWriteValues.Add(xNS.GetName("ApprovalStatus"), this.ApprovalStatus);  
            readWriteValues.Add(xNS.GetName("DocumentId"), this.DocumentId);  
            readWriteValues.Add(xNS.GetName("LastModifiedTime"), this.LastUpdateTime);  
  
            writeOnlyValues = null;  
        }  
        // ...  
    }  
  
    ```  
  
    > [!NOTE]
    >  Tutte queste proprietà vengono passate a **SqlWorkflowInstanceStore** dal framework di persistenza tramite la raccolta **SaveWorkflowCommand.InstanceData**.  
  
5.  L'applicazione DP inizializza l'archivio di istanze del flusso di lavoro SQL e richiama il metodo **Promote** per promuovere questi dati.  
  
    ```  
    SqlWorkflowInstanceStore store = new SqlWorkflowInstanceStore(connectionString);  
  
    List<XName> variantProperties = new List<XName>()   
    {   
        xNS.GetName("UserName"),   
        xNS.GetName("ApprovalStatus"),   
        xNS.GetName("DocumentId"),   
        xNS.GetName("LastModifiedTime")   
    };  
  
    store.Promote("DocumentStatus", variantProperties, null);  
    ```  
  
     In base a queste informazioni sulla promozione, **SqlWorkflowInstanceStore** inserisce le proprietà dei dati nelle colonne dell'oggetto [Vista [System.Activities.DurableInstancing.InstancePromotedProperties]](../../../docs/framework/windows-workflow-foundation//store-extensibility.md#InstancePromotedProperties).  
  
6.  Per eseguire una query su un subset dei dati dalla tabella di promozione, viene aggiunta una vista personalizzata nella parte superiore di tale vista da parte dell'applicazione DP.  
  
    ```  
  
    create view [dbo].[DocumentStatus] with schemabinding  
    as  
        select  P.[InstanceId] as [InstanceId],  
            P.Value1 as [UserName],  
            P.Value2 as [ApprovalStatus],  
            P.Value3 as [DocumentId],  
            P.Value4 as [LastUpdatedTime]  
    from [System.Activities.DurableInstancing].[InstancePromotedProperties] as P  
    where P.PromotionName = N'DocumentStatus'  
    go  
  
    ```  
  
##  <a name="InstancePromotedProperties"></a> Vista \[System.Activities.DurableInstancing.InstancePromotedProperties\]  
  
|Nome colonna|Tipo di colonna|Descrizione|  
|------------------|---------------------|-----------------|  
|InstanceId|GUID|Istanza del flusso di lavoro a cui appartiene questa promozione.|  
|PromotionName|nvarchar\(400\)|Nome della promozione stessa.|  
|Value1, Value2, Value3,..,Value32|sql\_variant|Valore della proprietà promossa stessa.In sql\_variant possono rientrare la maggior parte dei tipi di dati primitivi SQL, eccetto stringhe e blob binari la cui lunghezza supera gli 8000 byte.|  
|Value33, Value34, Value35, …, Value64|varbinary\(max\)|Valore di proprietà promosse dichiarate in modo esplicito come varbinary \(valore massimo\).|