---
title: "Attivit&#224; di raccolta in WF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2680c3e2-9902-4968-b98d-cab776103dbe
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Attivit&#224; di raccolta in WF
Le attività di raccolta vengono usate per operare con gli oggetti Collection in un flusso di lavoro.  [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] dispone di attività fornite dal sistema per l'aggiunta e la rimozione di elementi da una raccolta, la verifica dell'esistenza di un elemento in una raccolta e la cancellazione di una raccolta.  `ExistsInCollection` e `RemoveFromCollectio`n hanno <xref:System.Activities.OutArgument%601> di tipo <xref:System.Boolean>, che indica il risultato.  
  
> [!IMPORTANT]
>  Se un'attività di raccolta viene eseguita prima di impostare l'oggetto Collection sottostante, viene generata un'eccezione <xref:System.InvalidOperationException> e l'attività non riesce.  
  
## Attività di raccolta  
  
|||  
|-|-|  
|<xref:System.Activities.Statements.AddToCollection%601>|Aggiunge un elemento in una raccolta specificata.|  
|<xref:System.Activities.Statements.ClearCollection%601>|Cancella tutti gli elementi da una raccolta specificata.|  
|<xref:System.Activities.Statements.ExistsInCollection%601>|Restituisce `true` se un elemento esiste in una raccolta.|  
|<xref:System.Activities.Statements.RemoveFromCollection%601>|Rimuove un elemento da una raccolta specificata e restituisce `true` se l'elemento è stato rimosso correttamente.|  
  
## Utilizzo delle attività di raccolta  
 Nell'esempio di codice seguente viene illustrato come interagire con una raccolta dichiarata come variabile del flusso di lavoro.  La raccolta usata è un oggetto <xref:System.Collections.Generic.List%E2%80%991> di oggetti <xref:System.String> denominati `fruitList`.  
  
```csharp  
Variable<ICollection<string>> fruitList = new Variable<ICollection<string>>  
{  
    Default = new VisualBasicValue<ICollection<string>>("New List(Of String) From {\"Apple\", \"Orange\"}"),  
    Name = "FruitList"  
};  
  
Variable<bool> result = new Variable<bool>  
{  
    Name = "Result"  
};  
  
Activity wf = new Sequence  
{  
    Variables = { fruitList, result },  
  
    Activities =   
    {  
        new If  
        {  
            Condition = new ExistsInCollection<string>  
            {  
                Collection = fruitList,  
                Item = "Pear"  
            },  
            Then = new AddToCollection<string>  
            {  
                Collection = fruitList,  
                Item = "Pear"  
            },  
            Else = new RemoveFromCollection<string>  
            {  
                Collection = fruitList,  
                Item = "Apple"  
            }  
        },  
  
        new RemoveFromCollection<string>  
        {  
            Collection = fruitList,  
            Item = "Apple",  
            Result = result  
        },  
        new If  
        {  
            Condition = result,  
            Then = new ClearCollection<string>  
            {  
                Collection = fruitList,  
            }  
        }  
    }  
};  
  
```  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:scg="clr-namespace:System.Collections.Generic;assembly=mscorlib"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <Sequence.Variables>  
    <x:Reference>__ReferenceID0</x:Reference>  
    <x:Reference>__ReferenceID1</x:Reference>  
  </Sequence.Variables>  
  <If>  
    <If.Condition>  
      <InArgument  
         x:TypeArguments="x:Boolean">  
        <ExistsInCollection  
           x:TypeArguments="x:String"  
           Item="Pear">  
          <ExistsInCollection.Result>  
            <OutArgument  
               x:TypeArguments="x:Boolean" />  
          </ExistsInCollection.Result>  
          <InArgument  
             x:TypeArguments="scg:ICollection(x:String)">  
            <VariableValue  
               x:TypeArguments="scg:ICollection(x:String)">  
              <VariableValue.Result>  
                <OutArgument  
                   x:TypeArguments="scg:ICollection(x:String)" />  
              </VariableValue.Result>  
              <VariableValue.Variable>  
                <Variable  
                   x:TypeArguments="scg:ICollection(x:String)"  
                   x:Name="__ReferenceID0"  
                   Default="[New List(Of String) From {"Apple", "Orange"}]"  
                   Name="FruitList" />  
              </VariableValue.Variable>  
            </VariableValue>  
          </InArgument>  
        </ExistsInCollection>  
      </InArgument>  
    </If.Condition>  
    <If.Then>  
      <AddToCollection  
         x:TypeArguments="x:String"  
         Item="Pear">  
        <InArgument  
           x:TypeArguments="scg:ICollection(x:String)">  
          <VariableValue  
             x:TypeArguments="scg:ICollection(x:String)"  
             Variable="{x:Reference __ReferenceID0}">  
            <VariableValue.Result>  
              <OutArgument  
                 x:TypeArguments="scg:ICollection(x:String)" />  
            </VariableValue.Result>  
          </VariableValue>  
        </InArgument>  
      </AddToCollection>  
    </If.Then>  
    <If.Else>  
      <RemoveFromCollection  
         x:TypeArguments="x:String"  
         Item="Apple"  
         Result="{x:Null}">  
        <InArgument  
           x:TypeArguments="scg:ICollection(x:String)">  
          <VariableValue  
             x:TypeArguments="scg:ICollection(x:String)"  
             Variable="{x:Reference __ReferenceID0}">  
            <VariableValue.Result>  
              <OutArgument  
                 x:TypeArguments="scg:ICollection(x:String)" />  
            </VariableValue.Result>  
          </VariableValue>  
        </InArgument>  
      </RemoveFromCollection>  
    </If.Else>  
  </If>  
  <RemoveFromCollection  
     x:TypeArguments="x:String"  
     Item="Apple">  
    <RemoveFromCollection.Result>  
      <OutArgument  
         x:TypeArguments="x:Boolean">  
        <VariableReference  
           x:TypeArguments="x:Boolean">  
          <VariableReference.Result>  
            <OutArgument  
               x:TypeArguments="Location(x:Boolean)" />  
          </VariableReference.Result>  
          <VariableReference.Variable>  
            <Variable  
               x:TypeArguments="x:Boolean"  
               x:Name="__ReferenceID1"  
               Name="Result" />  
          </VariableReference.Variable>  
        </VariableReference>  
      </OutArgument>  
    </RemoveFromCollection.Result>  
    <InArgument  
       x:TypeArguments="scg:ICollection(x:String)">  
      <VariableValue  
         x:TypeArguments="scg:ICollection(x:String)"  
         Variable="{x:Reference __ReferenceID0}">  
        <VariableValue.Result>  
          <OutArgument  
             x:TypeArguments="scg:ICollection(x:String)" />  
        </VariableValue.Result>  
      </VariableValue>  
    </InArgument>  
  </RemoveFromCollection>  
  <If>  
    <If.Condition>  
      <InArgument  
         x:TypeArguments="x:Boolean">  
        <VariableValue  
           x:TypeArguments="x:Boolean"  
           Variable="{x:Reference __ReferenceID1}">  
          <VariableValue.Result>  
            <OutArgument  
               x:TypeArguments="x:Boolean" />  
          </VariableValue.Result>  
        </VariableValue>  
      </InArgument>  
    </If.Condition>  
    <If.Then>  
      <ClearCollection  
         x:TypeArguments="x:String">  
        <InArgument  
           x:TypeArguments="scg:ICollection(x:String)">  
          <VariableValue  
             x:TypeArguments="scg:ICollection(x:String)"  
             Variable="{x:Reference __ReferenceID0}">  
            <VariableValue.Result>  
              <OutArgument  
                 x:TypeArguments="scg:ICollection(x:String)" />  
            </VariableValue.Result>  
          </VariableValue>  
        </InArgument>  
      </ClearCollection>  
    </If.Then>  
  </If>  
</Sequence>  
  
```  
  
 Gli esempi di codice precedenti possono essere creati anche usando <xref:Microsoft.CSharp.Activities.CSharpValue%601> anziché <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>  
  
```  
Variable<ICollection<string>> fruitList = new Variable<ICollection<string>>  
{  
    Default = new CSharpValue<ICollection<string>>("new List<String> From {\"Apple\", \"Orange\"};"),  
    Name = "FruitList"  
};  
  
Variable<bool> result = new Variable<bool>  
{  
    Name = "Result"  
};  
  
Activity wf = new Sequence  
{  
    Variables = { fruitList, result },  
  
    Activities =   
    {  
        new If  
        {  
            Condition = new ExistsInCollection<string>  
            {  
                Collection = fruitList,  
                Item = "Pear"  
            },  
            Then = new AddToCollection<string>  
            {  
                Collection = fruitList,  
                Item = "Pear"  
            },  
            Else = new RemoveFromCollection<string>  
            {  
                Collection = fruitList,  
                Item = "Apple"  
            }  
        },  
  
        new RemoveFromCollection<string>  
        {  
            Collection = fruitList,  
            Item = "Apple",  
            Result = result  
        },  
        new If  
        {  
            Condition = result,  
            Then = new ClearCollection<string>  
            {  
                Collection = fruitList,  
            }  
        }  
    }  
};  
  
```  
  
```  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:scg="clr-namespace:System.Collections.Generic;assembly=mscorlib"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <Sequence.Variables>  
    <x:Reference>__ReferenceID0</x:Reference>  
    <x:Reference>__ReferenceID1</x:Reference>  
  </Sequence.Variables>  
  <If>  
    <If.Condition>  
      <InArgument  
         x:TypeArguments="x:Boolean">  
        <ExistsInCollection  
           x:TypeArguments="x:String"  
           Item="Pear">  
          <ExistsInCollection.Result>  
            <OutArgument  
               x:TypeArguments="x:Boolean" />  
          </ExistsInCollection.Result>  
          <InArgument  
             x:TypeArguments="scg:ICollection(x:String)">  
            <VariableValue  
               x:TypeArguments="scg:ICollection(x:String)">  
              <VariableValue.Result>  
                <OutArgument  
                   x:TypeArguments="scg:ICollection(x:String)" />  
              </VariableValue.Result>  
              <VariableValue.Variable>  
                <Variable  
                   x:TypeArguments="scg:ICollection(x:String)"  
                   x:Name="__ReferenceID0"  
                   Default="[new List<String> From {"Apple", "Orange"};]"  
                   Name="FruitList" />  
              </VariableValue.Variable>  
            </VariableValue>  
          </InArgument>  
        </ExistsInCollection>  
      </InArgument>  
    </If.Condition>  
    <If.Then>  
      <AddToCollection  
         x:TypeArguments="x:String"  
         Item="Pear">  
        <InArgument  
           x:TypeArguments="scg:ICollection(x:String)">  
          <VariableValue  
             x:TypeArguments="scg:ICollection(x:String)"  
             Variable="{x:Reference __ReferenceID0}">  
            <VariableValue.Result>  
              <OutArgument  
                 x:TypeArguments="scg:ICollection(x:String)" />  
            </VariableValue.Result>  
          </VariableValue>  
        </InArgument>  
      </AddToCollection>  
    </If.Then>  
    <If.Else>  
      <RemoveFromCollection  
         x:TypeArguments="x:String"  
         Item="Apple"  
         Result="{x:Null}">  
        <InArgument  
           x:TypeArguments="scg:ICollection(x:String)">  
          <VariableValue  
             x:TypeArguments="scg:ICollection(x:String)"  
             Variable="{x:Reference __ReferenceID0}">  
            <VariableValue.Result>  
              <OutArgument  
                 x:TypeArguments="scg:ICollection(x:String)" />  
            </VariableValue.Result>  
          </VariableValue>  
        </InArgument>  
      </RemoveFromCollection>  
    </If.Else>  
  </If>  
  <RemoveFromCollection  
     x:TypeArguments="x:String"  
     Item="Apple">  
    <RemoveFromCollection.Result>  
      <OutArgument  
         x:TypeArguments="x:Boolean">  
        <VariableReference  
           x:TypeArguments="x:Boolean">  
          <VariableReference.Result>  
            <OutArgument  
               x:TypeArguments="Location(x:Boolean)" />  
          </VariableReference.Result>  
          <VariableReference.Variable>  
            <Variable  
               x:TypeArguments="x:Boolean"  
               x:Name="__ReferenceID1"  
               Name="Result" />  
          </VariableReference.Variable>  
        </VariableReference>  
      </OutArgument>  
    </RemoveFromCollection.Result>  
    <InArgument  
       x:TypeArguments="scg:ICollection(x:String)">  
      <VariableValue  
         x:TypeArguments="scg:ICollection(x:String)"  
         Variable="{x:Reference __ReferenceID0}">  
        <VariableValue.Result>  
          <OutArgument  
             x:TypeArguments="scg:ICollection(x:String)" />  
        </VariableValue.Result>  
      </VariableValue>  
    </InArgument>  
  </RemoveFromCollection>  
  <If>  
    <If.Condition>  
      <InArgument  
         x:TypeArguments="x:Boolean">  
        <VariableValue  
           x:TypeArguments="x:Boolean"  
           Variable="{x:Reference __ReferenceID1}">  
          <VariableValue.Result>  
            <OutArgument  
               x:TypeArguments="x:Boolean" />  
          </VariableValue.Result>  
        </VariableValue>  
      </InArgument>  
    </If.Condition>  
    <If.Then>  
      <ClearCollection  
         x:TypeArguments="x:String">  
        <InArgument  
           x:TypeArguments="scg:ICollection(x:String)">  
          <VariableValue  
             x:TypeArguments="scg:ICollection(x:String)"  
             Variable="{x:Reference __ReferenceID0}">  
            <VariableValue.Result>  
              <OutArgument  
                 x:TypeArguments="scg:ICollection(x:String)" />  
            </VariableValue.Result>  
          </VariableValue>  
        </InArgument>  
      </ClearCollection>  
    </If.Then>  
  </If>  
</Sequence>  
  
```  
  
## Vedere anche  
 [Creazione di flussi di lavoro, attività ed espressioni tramite codice imperativo](../../../docs/framework/windows-workflow-foundation//authoring-workflows-activities-and-expressions-using-imperative-code.md)