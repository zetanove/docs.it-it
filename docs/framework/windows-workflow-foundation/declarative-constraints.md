---
title: "Vincoli dichiarativi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 67001ed1-7f4d-4ada-ae57-a31176901a53
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Vincoli dichiarativi
I vincoli dichiarativi offrono un metodo potente di convalida per un'attività e le relative relazioni con altre attività.I vincoli vengono configurati per un'attività durante il processo di creazione, ma vincoli aggiuntivi possono essere specificati anche dall'host del flusso di lavoro.In questo argomento viene fornita una panoramica sull'utilizzo di vincoli dichiarativi per la convalida delle attività.  
  
## Utilizzo di vincoli dichiarativi  
 Un vincolo è un'attività che contiene la logica di convalida.Questa attività del vincolo può essere creata nel codice o in XAML.Una volta creata un'attività del vincolo, gli autori di attività aggiungono questo vincolo alla proprietà <xref:System.Activities.Activity.Constraints%2A> dell'attività da convalidare o utilizzano il vincolo per fornire un'ulteriore convalida tramite la proprietà <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> di un'istanza di <xref:System.Activities.Validation.ValidationSettings>.La logica di convalida può essere costituita da convalide semplici, ad esempio quella dei metadati di un'attività. Tuttavia una convalida può essere eseguita anche considerando la relazione dell'attività corrente con le relative attività padre, figlio e di pari livello.I vincoli vengono creati utilizzando l'attività <xref:System.Activities.Validation.Constraint%601> e molte attività di convalida aggiuntive sono fornite per consentire la creazione di errori e di avvisi di convalida nonché per fornire informazioni sulle attività correlate nel flusso di lavoro.  
  
### Oggetti AssertValidation e AddValidationError  
 L'attività <xref:System.Activities.Validation.AssertValidation> valuta l'espressione a cui fa riferimento la relativa proprietà <xref:System.Activities.Validation.AssertValidation.Assertion%2A> e se l'espressione restituisce `false`, un errore o avviso di convalida viene aggiunto all'oggetto <xref:System.Activities.Validation.ValidationResults>.La proprietà <xref:System.Activities.Validation.AssertValidation.Message%2A> descrive l'errore di convalida mentre la proprietà <xref:System.Activities.Validation.AssertValidation.IsWarning%2A> indica se l'errore di convalida è un errore effettivo o un avviso.Il valore predefinito per la proprietà <xref:System.Activities.Validation.AssertValidation.IsWarning%2A> è `false`.  
  
 Nell'esempio seguente viene dichiarato un vincolo che restituisce un avviso di convalida se la proprietà <xref:System.Activities.Activity.DisplayName%2A> dell'attività convalidata ha una lunghezza che non supera i due caratteri.Il parametro di tipo generico utilizzato per <xref:System.Activities.Validation.Constraint%601> specifica il tipo di attività convalidata dal vincolo.Questo vincolo utilizza l'oggetto <xref:System.Activities.Activity> come tipo generico e può essere utilizzato per la convalida di tutti i tipi di attività.  
  
```csharp  
public static Constraint ActivityDisplayNameIsNotSetWarning()  
{  
    DelegateInArgument<Activity> element = new DelegateInArgument<Activity>();  
  
    return new Constraint<Activity>  
    {  
        Body = new ActivityAction<Activity, ValidationContext>  
        {  
            Argument1 = element,  
            Handler = new AssertValidation  
            {  
                IsWarning = true,  
                Assertion = new InArgument<bool>(env => (element.Get(env).DisplayName.Length > 2)),  
                Message = new InArgument<string>("It is a best practice to have a DisplayName of more than 2 characters."),  
            }  
        }  
    };  
}  
```  
  
 Per specificare questo vincolo per un'attività, viene aggiunto alla proprietà <xref:System.Activities.Activity.Constraints%2A> dell'attività, come mostrato nel codice di esempio seguente.  
  
```csharp  
public sealed class SampleActivity : CodeActivity  
{  
    public SampleActivity()  
    {  
        base.Constraints.Add(ActivityDisplayNameIsNotSetWarning());  
    }  
  
    // Activity implementation omitted.  
}  
```  
  
 Questo vincolo potrebbe essere specificato anche per le attività in un flusso di lavoro dall'host utilizzando la proprietà <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A>, illustrata nella sezione successiva.  
  
 L'attività <xref:System.Activities.Validation.AddValidationError> viene utilizzata per generare un errore o avviso di convalida senza richiedere la valutazione di un'espressione.Le relative proprietà sono simili all'oggetto <xref:System.Activities.Validation.AssertValidation> che può essere utilizzato insieme alle attività di controllo del flusso di un vincolo quale l'attività <xref:System.Activities.Statements.If>.  
  
### Attività di relazioni di flussi di lavoro  
 Sono disponibili numerose attività di convalida che forniscono informazioni sulle altre attività del flusso di lavoro in relazione all'attività da convalidare.<xref:System.Activities.Validation.GetParentChain> restituisce una raccolta di attività contenente tutte le attività tra l'attività in corso e l'attività radice.<xref:System.Activities.Validation.GetChildSubtree> fornisce una raccolta di attività contenente le attività figlio nel modello ricorsivo e <xref:System.Activities.Validation.GetWorkflowTree> ottiene tutte le attività nel flusso di lavoro.  
  
 Nell'esempio seguente dell'esempio [Convalida di relazioni tra attività](../../../docs/framework/windows-workflow-foundation/samples/activity-relationships-validation.md) viene definita un'attività `CreateState`.L'attività `CreateState` deve essere contenuta all'interno di un'attività `CreateCountry` e il metodo `GetParent` restituisce un vincolo che applica questo requisito.`GetParent` utilizza l'attività <xref:System.Activities.Validation.GetParentChain> insieme a un'attività <xref:System.Activities.Statements.ForEach%601> per controllare le attività padre dell'attività `CreateState` per determinare se il requisito è stato rispettato.  
  
```csharp  
public sealed class CreateState : CodeActivity  
{  
    public CreateState()  
    {  
        base.Constraints.Add(CheckParent());  
        this.Cities = new List<Activity>();              
    }  
  
    public List<Activity> Cities { get; set; }  
  
    public string Name { get; set; }    
  
    static Constraint CheckParent()  
    {  
        DelegateInArgument<CreateState> element = new DelegateInArgument<CreateState>();  
        DelegateInArgument<ValidationContext> context = new DelegateInArgument<ValidationContext>();                          
        Variable<bool> result = new Variable<bool>();  
        DelegateInArgument<Activity> parent = new DelegateInArgument<Activity>();  
  
        return new Constraint<CreateState>  
        {                                     
            Body = new ActivityAction<CreateState,ValidationContext>  
            {                      
                Argument1 = element,  
                Argument2 = context,  
                Handler = new Sequence  
                {  
                    Variables =  
                    {  
                        result   
                    },  
                    Activities =  
                    {  
                        new ForEach<Activity>  
                        {                                  
                            Values = new GetParentChain  
                            {  
                                ValidationContext = context                                      
                            },  
                            Body = new ActivityAction<Activity>  
                            {     
                                Argument = parent,   
                                Handler = new If()  
                                {                                            
                                    Condition = new InArgument<bool>((env) => object.Equals(parent.Get(env).GetType(),typeof(CreateCountry))),                                          
                                    Then = new Assign<bool>  
                                    {  
                                        Value = true,  
                                        To = result  
                                    }  
                                }  
                            }                                  
                        },  
                        new AssertValidation  
                        {  
                            Assertion = new InArgument<bool>(result),  
                            Message = new InArgument<string> ("CreateState has to be inside a CreateCountry activity"),                                                                  
                        }  
                    }  
                }  
            }  
        };  
    }  
  
    protected override void Execute(CodeActivityContext context)  
    {  
        // not needed for the sample  
    }  
}  
```  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] gli esempi di [Convalida](../../../docs/framework/windows-workflow-foundation/samples/validation.md) di Windows Workflow Foundation.  
  
## Vincoli aggiuntivi  
 Gli autori di host del flusso di lavoro possono specificare vincoli di convalida aggiuntivi per le attività in un flusso di lavoro creando vincoli e aggiungendoli al dizionario <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> di un'istanza di <xref:System.Activities.Validation.ValidationSettings>.Ogni elemento nella proprietà <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> contiene il tipo di attività per il quale vengono applicati i vincoli e un elenco dei vincoli aggiuntivi per quel tipo di attività.Quando la convalida viene richiamata per il flusso di lavoro, ogni attività del tipo specificato, incluse le classi derivate, valuta i vincoli.In questo esempio il vincolo `ActivityDisplayNameIsNotSetWarning` della sezione precedente viene applicato a tutte le attività in un flusso di lavoro.  
  
```csharp  
Activity wf = new Sequence  
{  
    // Workflow Details Omitted.  
};  
  
ValidationSettings settings = new ValidationSettings()  
{  
  
    AdditionalConstraints =  
    {  
        {typeof(Activity), new List<Constraint> {ActivityDisplayNameIsNotSetWarning()}},       
    }  
};  
  
// Validate the workflow.  
ValidationResults results = ActivityValidationServices.Validate(wf, settings);  
  
// Evaluate the results.  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error in " + error.Source.DisplayName + ": " + error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning in " + warning.Source.DisplayName + ": " + warning.Message);  
    }  
}  
```  
  
 Se la proprietà <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> dell'oggetto <xref:System.Activities.Validation.ValidationSettings> è `true`, solo i vincoli aggiuntivi specificati vengono valutati quando la convalida viene richiamata mediante la chiamata al metodo <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>.Ciò può essere utile per esaminare i flussi di lavoro per configurazioni di convalida specifiche.Si noti tuttavia che quando viene richiamato il flusso di lavoro, la logica di convalida configurata nel flusso di lavoro viene valutata e deve passare per il flusso di lavoro per iniziare correttamente.[!INCLUDE[crabout](../../../includes/crabout-md.md)]l richiamo di convalida, vedere [Richiamo della convalida di attività](../../../docs/framework/windows-workflow-foundation//invoking-activity-validation.md).