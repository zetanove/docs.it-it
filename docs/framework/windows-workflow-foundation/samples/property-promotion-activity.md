---
title: "Attivit&#224; di promozione propriet&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 802196b7-1159-4c05-b41b-d3bfdfcc88d9
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Attivit&#224; di promozione propriet&#224;
In questo esempio viene fornita una soluzione end\-to\-end che integra direttamente la funzionalità di promozione <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> nella creazione di flussi di lavoro.Vengono forniti inoltre una raccolta di elementi di configurazione, attività ed estensioni del flusso di lavoro che semplificano l'utilizzo della funzionalità di promozione.Nell'esempio è contenuto infine un semplice flusso di lavoro che dimostra come utilizzare la raccolta.  
  
> [!NOTE]
>  Gli esempi vengono forniti solo a scopo didattico.Non sono destinati né sono stati testati in un ambiente di produzione.Microsoft non fornisce supporto tecnico per questi esempi.  
  
## Prerequisiti  
  
-   Un database <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> inizializzato  
  
-   [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]  
  
## Progetti di esempio  
  
-   Il progetto **PropertyPromotionActivity** contiene file relativi agli elementi di configurazione specifici della promozione nonché attività ed estensioni del flusso di lavoro.  
  
-   Il progetto **CounterServiceApplication** contiene un flusso di lavoro di esempio che utilizza il progetto **SqlWorkflowInstanceStorePromotion**.  
  
-   Uno script SQL \(PropertyPromotionActivitySQLSample.sql\) che è necessario eseguire nel database <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>.  
  
-   Un file della soluzione che collega i due progetti [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] \(`PropertyPromotionActivity.sln`\)  
  
## Per impostare ed eseguire l'esempio  
  
1.  Inizializzare un database di persistenza del flusso di lavoro.  
  
    1.  Passare alla directory di esempio \(\\WF\\Basic\\Persistence\\PropertyPromotionActivity\) ed eseguire CreateInstanceStore.cmd.  
  
    2.  Se i privilegi di amministratore non sono disponibili, creare un account di accesso di SQL Server.In SQL Server Management Studio andare a **Protezione**, **Account di accesso**.Fare clic con il pulsante destro del mouse su **Account di accesso** e creare un nuovo account.Aggiungere l'utente ACL al ruolo SQL aprendo **Database**, **InstanceStore**, **Protezione**.Fare clic con il pulsante destro del mouse su **Utenti**, quindi scegliere **Nuovo utente**.Impostare **Nome account di accesso** sull'utente creato in precedenza.Aggiungere l'utente all'appartenenza ai ruoli del database System.Activities.DurableInstancing.InstanceStoreUsers \(e altri\).Notare che l'utente potrebbe essere già presente \(ad esempio, utente dbo\).  
  
2.  Aprire il file della soluzione PropertyPromotionActivity.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
3.  Se l'archivio di istanze è stato creato in un database diverso da un'installazione locale di SQL Server Express, è necessario aggiornare la stringa di connessione di database.Modificare il file App.config in **CounterServiceApplication** impostando il valore dell'attributo `connectionString` sul nodo `sqlWorkflowInstanceStorePromotion` in modo che punti al database di persistenza inizializzato nel passaggio 1.  
  
4.  Compilare ed eseguire la soluzione.Verranno avviati il servizio Counter WF e, automaticamente, un'istanza del flusso di lavoro.  
  
5.  Selezionare rapidamente tutte le righe nella vista \[dbo\].\[CounterService\] del database di persistenza \(aggiunta tramite l'esecuzione di CreateInstanceStore.cmd nel passaggio 1\).Il set di risultati sarà analogo al seguente:  
  
    |InstanceId|CounterValue|CounterValueLastUpdated|  
    |----------------|------------------|-----------------------------|  
    |2FA2C302\-929E\-4C0D\-8C25\-768A3DA20CE5|12|2010\-02\-18 22:48:01.740|  
  
     Man mano che si procede con l'aggiornamento della vista, si noterà che gli elementi CounterValue e CounterValueLastUpdated vengono modificati ogni due secondi,che rappresentano l'intervallo di aggiornamento del contatore.CounterValue e CounterValueLastUpdated rappresentano proprietà promosse per questo flusso di lavoro.  
  
## Per rimuovere l'esempio  
  
-   Eseguire RemoveInstanceStore.cmd nella directory di esempio \(\\WF\\Basic\\Persistence\\PropertyPromotionActivity\).  
  
## Informazioni sull'esempio  
 Nell'esempio sono contenuti due progetti e un file SQL:  
  
-   **CounterServiceApplication** è un'applicazione console che ospita un servizio Counter WF semplice.Alla ricezione di un messaggio unidirezionale tramite l'endpoint `Start`, il flusso di lavoro conta da 0 a 29, incrementando una variabile del contatore ogni due secondi.Dopo ogni incremento del contatore, il flusso di lavoro è persistente e le proprietà promosse vengono aggiornate nella vista \[dbo\].\[CounterService\].Quando viene eseguita, l'applicazione console ospita il servizio WF e invia un messaggio all'endpoint `Start`, creando un'istanza di Counter WF.  
  
-   **PropertyPromotionActivity** è una libreria di classi che contiene gli elementi di configurazione e le attività e le estensioni del flusso di lavoro utilizzate da **CounterServiceApplication**.  
  
-   **PropertyPromotionActivitySQLSample.sql** crea e aggiunge la vista \[dbo\].\[CounterService\] al database.  
  
### CounterServiceApplication  
  
#### Utilizzo dell'elemento di configurazione SqlWorkflowInstanceStorePromotion  
 L'elemento di configurazione `SqlWorkflowInstanceStorePromotion` eredita dall'elemento di configurazione `SqlWorkflowInstanceStore`, ma aggiunge un ulteriore elemento denominato `promotionSets`.L'elemento `promotionSets` consente all'utente di specificare proprietà promosse tramite la configurazione.Il file di configurazione utilizzato nell'esempio è il seguente:  
  
```xml  
<sqlWorkflowInstanceStorePromotion connectionString ="Data Source=.;Initial Catalog=SqlWorkflowInstanceStoreTest;Integrated Security=True;">  
  <promotionSets>  
    <promotionSet name="CounterService">  
      <promotedValue propertyName="Count"/>  
      <promotedValue propertyName="LastIncrementedAt"/>  
    </promotionSet>  
  </promotionSets>  
</sqlWorkflowInstanceStorePromotion>  
```  
  
 Esaminare la definizione per la vista \[dbo\].\[CounterService\].  
  
```sql  
create view [dbo].[CounterService] as  
      select [InstanceId],  
 [Value1] as [CounterValue],  
 [Value2] as [CounterValueLastUpdated]  
      from [System.Activities.DurableInstancing].[InstancePromotedProperties]  
      where [PromotionName] = 'CounterService'  
go  
  
```  
  
 Quando un'istanza del flusso di lavoro è persistente, una riga viene inserita nella vista `InstancePromotedProperties` per ogni `PromotionSet` definito nella configurazione.Questa riga contiene tutte le proprietà promosse di `PromotionSet` \(una proprietà promossa per colonna\).Questo elemento `PromotionSet` è collegato con chiave dalla tupla `InstanceId, PromotionName`.In questo esempio è presente un elemento `PromotionSet` definito in una configurazione il cui attributo name è `CounterService`.Si noti che il valore della colonna `PromotionSet` è uguale all'attributo name `PromotionName`.  
  
 L'ordine degli elementi di `promotedValue` è correlato alla posizione delle proprietà promosse nella visualizzazione `InstancePromotedProperties`.`Count` è il primo elemento di `promotedValue`.Di conseguenza, tale elemento viene mappato alla colonna `Value1` nella vista `InstancePromotedProperties`.`LastIncrementedAt` è il secondo elemento di `promotedValue`.Di conseguenza, tale elemento viene mappato alla colonna `Value2` nella vista `InstancePromotedProperties`.  
  
#### Utilizzo dell'attività PromoteValue  
 Esaminare il file CounterService.xamlx nella finestra di progettazione di [!INCLUDE[wf2](../../../../includes/wf2-md.md)].Si noti che sono presenti due attività speciali nella definizione WF, ovvero `PromoteValue<DateTime>` e `PromoteValue<Int32>`.  
  
 All'attività `PromoteValue<Int32>` è associato il membro `Name` definito come `Count`che corrisponde al primo elemento `promotedValue` nella configurazione e per cui il relativo elemento `Value` è definito come variabile del flusso di lavoro `Counter`.Quando il flusso di lavoro è persistente, la variabile del flusso di lavoro `Counter` viene resa persistente come proprietà promossa nella colonna `Value1` della vista `InstancePromotedProperties`.  
  
 All'attività `PromoteValue<DateTime>` è associato il membro `Name` definito come `LastIncrementedAt`che corrisponde al secondo elemento `promotedValue` nella configurazione e per cui il relativo elemento `Value` è definito come variabile del flusso di lavoro `TimeLastIncremented`.Questo significa che quando il flusso di lavoro è persistente, la variabile del flusso di lavoro `TimeLastIncremented` verrà resa persistente come proprietà promossa nella colonna `Value2` della vista `InstancePromotedProperties`.  
  
 Si noti che all'attività `PromotedValue` è inoltre associato un membro di tipo Boolean denominato `ClearExistingPromotedData`.Quando questo membro è impostato su `true`, vengono cancellate tutti i valori della proprietà promossa fino al punto specifico nel flusso di lavoro.Se ad esempio un'attività Sequence è definita come segue:  
  
1.  PromoteValue { Name \= “Count”, Value \= 3}  
  
2.  PromoteValue {Name \= “LastIncrementedAt”, Value \= 1\-1\-2000 }  
  
3.  Persist  
  
4.  PromoteValue {Name \= “Count”, Value \= 4, ClearExistingPromotedData \= true}  
  
5.  Persist  
  
 Al secondo Persist, il valore promosso per `Count` sarà 4e il valore promosso per `LastIncrementedAt` sarà `NULL`.Se `ClearExistingPromotedData` non fosse stato impostato su `true` nel passaggio 4, dopo il secondo Persist il valore promosso per Count sarebbe 4.Di conseguenza, il valore promosso per `LastIncrementedAt` sarebbe ancora 1\-1\-2000.  
  
### PropertyPromotionActivity  
 Questa libreria di classi contiene le seguenti classi pubbliche che consentono di semplificare l'utilizzo della funzionalità di promozione <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>.  
  
#### Classe PromoteValue  
 Questa classe promuove una proprietà.Il nome della proprietà promossa deve corrispondere a un attributo name dell'elemento `promotedValue` nella configurazione.Questa attività può essere utilizzata in Progettazione flussi di lavoro.Per un esempio di utilizzo, vedere CounterServiceApplication.  
  
```csharp  
public class PromoteValue<T> : CodeActivity  
{  
    public PromoteValue()  
    {  
    }  
  
    public bool ClearExistingPromotedData { get; set; }  
    public string Name { get; set; }  
    public InArgument<T> Value { get; set; }  
}  
  
```  
  
 ClearExistingPromotedData \(Bool\)  
 Cancella tutti i valori promossi prima di questa attività.  
  
 Name \(stringa\)  
 Nome che rappresenta la proprietà.Tale nome deve corrispondere all'attributo name di un elemento \<promotedValue\> nella configurazione.  
  
 Value \(InArgument\<T\>\)  
 La variabile o il valore da desidera archiviare nella colonna.  
  
#### Classe PromoteValues  
 Questa classe promuove più proprietà.I nomi delle proprietà promosse devono corrispondere a tutti gli attributi name degli elementi `promotedValue` nella configurazione.L'utilizzo è analogo a quello dell'attività `PromoteValue`, ad eccezione del fatto che è possibile promuovere più proprietà contemporaneamente.Questa attività non può essere utilizzata in Progettazione flussi di lavoro.  
  
```  
public class PromoteValues : CodeActivity  
{  
    public PromoteValues()  
    {  
        this.ValuesToPromote = new Dictionary<string, InArgument>();  
    }  
  
    public bool ClearExistingPromotedData { get; set; }  
    public IDictionary<string, InArgument> ValuesToPromote { get; set; }  
}  
```  
  
#### SqlWorkflowInstanceStorePromotionBehavior  
 Classe derivata da `SqlWorkflowInstanceStoreBehavior`che aggiunge un partecipante di persistenza personalizzato \(appartenente anche a questa libreria\) come estensione del flusso di lavoro.L'implementazione delle due attività del flusso di lavoro precedenti si basa su questo partecipante di persistenza personalizzato.  
  
```  
public class SqlWorkflowInstanceStorePromotionBehavior :  
             SqlWorkflowInstanceStoreBehavior, IServiceBehavior  
{  
        public void Promote(string name, IEnumerable<string> promoteAsSqlVariant,  
                            IEnumerable<string> promoteAsBinary)  
  
}  
  
```  
  
 Questa libreria di classi contiene inoltre l'implementazione di `ConfigurationElement` per `SqlWorkflowInstanceStorePromotionElement` e un partecipante di persistenza personalizzato utilizzati dalle attività di promozione precedenti.  
  
### PropertyPromotionActivitySQLSample  
 Questo file SQL crea una vista `[dbo].[CounterService]`, oltre alla vista `[InstancePromotedProperties]`, per l'esecuzione di query su tutte le istanze a cui è associato una promozione CounterService impostata.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Persistence\PropertyPromotionActivity`  
  
## Vedere anche  
 [Hosting e salvataggio permanente](http://go.microsoft.com/fwlink/?LinkId=193961)