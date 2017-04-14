---
title: "Implementazione della logica di business (LINQ to SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c4577590-7b12-42e1-84a6-95aa2562727e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Implementazione della logica di business (LINQ to SQL)
Il termine "regola business" in questo argomento si riferisce a qualsiasi regola personalizzata o test di convalida applicato ai dati prima che vengano inseriti, aggiornati o eliminati dal database.  La regola business viene talvolta definita anche "regola dominio". Nelle applicazioni a più livelli viene in genere progettata come livello logico in modo da essere modificata indipendentemente dal livello di presentazione o dal livello di accesso ai dati.  La logica di business può essere richiamata dal livello di accesso ai dati prima o dopo l'aggiornamento, l'inserimento o l'eliminazione dei dati dal database.  
  
 La regola business è semplice quanto la convalida di uno schema per assicurarsi che il tipo del campo sia compatibile con il tipo della colonna di tabella.  Oppure può essere costituita da un set di oggetti che interagiscono in modalità arbitrariamente complesse.  Le regole possono essere implementate come stored procedure nel database o come oggetti in memoria.  Indipendentemente dal modo in cui la regola business viene implementata, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] consente l'uso delle classi e dei metodi parziali per separare la regola business dal codice di accesso ai dati.  
  
## Richiamo della regola business da LINQ to SQL  
 Quando in fase di progettazione si genera una classe di entità manualmente oppure usando la [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] o SQLMetal, tale processo viene definito classe parziale.  Ciò significa che, in un file di codice separato, è possibile definire un'altra parte della classe di entità contenente la regola business personalizzata.  In fase di compilazione le due parti vengono unite in un'unica classe. È tuttavia possibile rigenerare le classi di entità utilizzando la [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] o SQLMetal, senza modificare la parte personalizzata della classe.  
  
 Le classi parziali che definiscono le entità e <xref:System.Data.Linq.DataContext> contengono metodi parziali.  Si tratta di punti di estensibilità che è possibile usare per applicare la regola business prima e dopo un aggiornamento, inserimento o eliminazione di un'entità o di una proprietà dell'entità.  È possibile considerare i metodi parziali come eventi in fase di compilazione.  Il generatore di codice definisce una firma del metodo e chiama i metodi nelle funzioni di accesso alle proprietà get e set nonché il costruttore `DataContext`, e in alcuni casi automaticamente quando viene chiamato <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.  Tuttavia, se non si implementa un particolare metodo parziale, tutti i riferimenti relativi e la definizione verranno rimossi in fase di compilazione.  
  
 Nella definizione di implementazione scritta nel file di codice separato, è possibile eseguire la regola personalizzata necessaria.  È possibile usare la classe parziale personalizzata come livello del dominio oppure è possibile chiamare dalla definizione di implementazione del metodo parziale in uno o più oggetti separati.  In entrambi i casi, la regola business viene nettamente separata dal codice di accesso ai dati e dal codice del livello di presentazione.  
  
## Informazioni dettagliate sui punti di estensibilità  
 Nell'esempio seguente viene illustrata parte del codice generato dalla [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] per la classe `DataContext` contenente due tabelle: `Customers` e `Orders`.  Tenere presente che i metodi di inserimento, aggiornamento ed eliminazione vengono definiti per ogni tabella della classe.  
  
```vb  
Partial Public Class Northwnd  
    Inherits System.Data.Linq.DataContext  
  
    Private Shared mappingSource As _  
        System.Data.Linq.Mapping.MappingSource = New _  
        AttributeMappingSource  
  
    #Region "Extensibility Method Definitions"  
    Partial Private Sub OnCreated()  
    End Sub  
    Partial Private Sub InsertCustomer(instance As Customer)  
    End Sub  
    Partial Private Sub UpdateCustomer(instance As Customer)  
    End Sub  
    Partial Private Sub DeleteCustomer(instance As Customer)  
    End Sub  
    Partial Private Sub InsertOrder(instance As [Order])  
    End Sub  
    Partial Private Sub UpdateOrder(instance As [Order])  
    End Sub  
    Partial Private Sub DeleteOrder(instance As [Order])  
    End Sub  
    #End Region  
```  
  
```csharp  
public partial class MyNorthWindDataContext : System.Data.Linq.DataContext  
    {  
        private static System.Data.Linq.Mapping.MappingSource mappingSource = new AttributeMappingSource();  
  
        #region Extensibility Method Definitions  
        partial void OnCreated();  
        partial void InsertCustomer(Customer instance);  
        partial void UpdateCustomer(Customer instance);  
        partial void DeleteCustomer(Customer instance);  
        partial void InsertOrder(Order instance);  
        partial void UpdateOrder(Order instance);  
        partial void DeleteOrder(Order instance);  
        #endregion  
```  
  
 Se si implementano i metodi di inserimento, aggiornamento ed eliminazione nella classe parziale, il runtime [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] chiamerà tali metodi anziché i metodi predefiniti personalizzati quando viene chiamato <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.  In questo modo è possibile eseguire l'override del comportamento predefinito per le operazioni di creazione, lettura, aggiornamento ed eliminazione.  Per altre informazioni, vedere [Procedura dettagliata: personalizzazione del comportamento di Insert, Update e Delete delle classi di entità](../Topic/Walkthrough:%20Customizing%20the%20insert,%20update,%20and%20delete%20behavior%20of%20entity%20classes.md).  
  
 Il metodo `OnCreated` viene chiamato nel costruttore della classe.  
  
```vb  
Public Sub New(ByVal connection As String)  
    MyBase.New(connection, mappingSource)  
    OnCreated()  
End Sub  
```  
  
```csharp  
public MyNorthWindDataContext(string connection) :  
            base(connection, mappingSource)  
        {  
            OnCreated();  
        }  
```  
  
 Per le classi di entità sono disponibili tre metodi che vengono chiamati dal runtime [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] quando l'entità viene creata, caricata e convalidata \(quando viene chiamato `SubmitChanges`\).  Le classi di entità dispongono inoltre di due metodi parziali per ogni proprietà, uno chiamato prima dell'impostazione della proprietà e l'altro dopo.  Nell'esempio di codice seguente vengono illustrati alcuni metodi generati per la classe `Customer`:  
  
```vb  
#Region "Extensibility Method Definitions"  
    Partial Private Sub OnLoaded()  
    End Sub  
    Partial Private Sub OnValidate(action As _  
        System.Data.Linq.ChangeAction)  
    End Sub  
    Partial Private Sub OnCreated()  
    End Sub  
    Partial Private Sub OnCustomerIDChanging(value As String)  
    End Sub  
    Partial Private Sub OnCustomerIDChanged()  
    End Sub  
    Partial Private Sub OnCompanyNameChanging(value As String)  
    End Sub  
    Partial Private Sub OnCompanyNameChanged()  
    End Sub  
' ...Additional Changing/Changed methods for each property.  
```  
  
```csharp  
#region Extensibility Method Definitions  
    partial void OnLoaded();  
    partial void OnValidate();  
    partial void OnCreated();  
    partial void OnCustomerIDChanging(string value);  
    partial void OnCustomerIDChanged();  
    partial void OnCompanyNameChanging(string value);  
    partial void OnCompanyNameChanged();  
// ...additional Changing/Changed methods for each property  
```  
  
 I metodi vengono chiamati nella funzione di accesso set della proprietà come illustrato nell'esempio seguente per la proprietà `CustomerID`:  
  
```vb  
Public Property CustomerID() As String  
    Set  
        If (String.Equals(Me._CustomerID, value) = False) Then  
            Me.OnCustomerIDChanging(value)  
            Me.SendPropertyChanging()  
            Me._CustomerID = value  
            Me.SendPropertyChanged("CustomerID")  
            Me.OnCustomerIDChanged()  
        End If  
    End Set  
End Property  
```  
  
```csharp  
public string CustomerID  
{  
    set  
    {  
        if ((this._CustomerID != value))  
        {  
            this.OnCustomerIDChanging(value);  
            this.SendPropertyChanging();  
            this._CustomerID = value;  
            this.SendPropertyChanged("CustomerID");  
            this.OnCustomerIDChanged();  
        }  
     }  
}  
```  
  
 Nella parte personalizzata della classe, scrivere una definizione di implementazione del metodo.  In [!INCLUDE[vsprvs](../../../../../../includes/vsprvs-md.md)] dopo avere digitato `parziale`, verrà visualizzato IntelliSense per le definizioni del metodo nell'altra parte della classe.  
  
```vb  
Partial Public Class Customer  
    Private Sub OnCustomerIDChanging(value As String)  
        ' Perform custom validation logic here.  
    End Sub  
End Class  
```  
  
```csharp  
partial class Customer   
    {  
        partial void OnCustomerIDChanging(string value)  
        {  
            //Perform custom validation logic here.  
        }  
    }  
```  
  
 Per altre informazioni su come aggiungere la regola business all'applicazione usando i metodi parziali, vedere gli argomenti seguenti:  
  
 [Procedura: aggiungere la convalida a classi di entità](../Topic/How%20to:%20Add%20validation%20to%20entity%20classes.md)  
  
 [Procedura dettagliata: personalizzazione del comportamento di Insert, Update e Delete delle classi di entità](../Topic/Walkthrough:%20Customizing%20the%20insert,%20update,%20and%20delete%20behavior%20of%20entity%20classes.md)  
  
 [Procedura dettagliata: aggiunta della convalida a classi di entità](../Topic/Walkthrough:%20Adding%20Validation%20to%20Entity%20Classes.md)  
  
## Vedere anche  
 [Classi e metodi parziali](../Topic/Partial%20Classes%20and%20Methods%20\(C%23%20Programming%20Guide\).md)   
 [Partial Methods](../Topic/Partial%20Methods%20\(Visual%20Basic\).md)   
 [LINQ to SQL Tools in Visual Studio](../Topic/LINQ%20to%20SQL%20Tools%20in%20Visual%20Studio2.md)   
 [SqlMetal.exe \(strumento per la generazione del codice\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)