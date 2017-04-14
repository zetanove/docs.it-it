---
title: "Flussi di lavoro del diagramma di flusso | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b0a3475c-d22f-49eb-8912-973c960aebf5
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# Flussi di lavoro del diagramma di flusso
Un diagramma di flusso è un paradigma noto per la progettazione di programmi.L'attività Flowchart viene generalmente utilizzata per implementare i flussi di lavoro non sequenziali, tuttavia può essere sfruttata anche per i flussi di lavoro sequenziali se non viene utilizzato alcun nodo `FlowDecision`.  
  
## Struttura del flusso di lavoro del diagramma di flusso  
 Un'attività Flowchart è un'attività che contiene una raccolta di attività da eseguire.I diagrammi di flusso contengono gli elementi di controllo del flusso, come <xref:System.Activities.Statements.FlowDecision> e <xref:System.Activities.Statements.FlowSwitch>, che dirigono l'esecuzione tra le attività contenute in base ai valori delle variabili.  
  
## Tipi di nodi del flusso  
 Vengono utilizzati tipi diversi di elementi a seconda del tipo di controllo del flusso richiesto quando l'elemento viene eseguito.I tipi di elementi del diagramma di flusso includono:  
  
-   `FlowStep`: modella un passaggio di esecuzione nel diagramma di flusso.  
  
-   `FlowDecision`: esegue il branching dell'esecuzione in base a una condizione Boolean, simile a <xref:System.Activities.Statements.If>.  
  
-   `FlowSwitch`: esegue il branching dell'esecuzione in base a un'opzione esclusiva, simile all'oggetto <xref:System.Activities.Statements.Switch%601>.  
  
 Ogni collegamento dispone di una proprietà `Action` che definisce un oggetto <xref:System.Activities.ActivityAction> che può essere utilizzato per eseguire le attività figlio e una o più proprietà `Next` che definiscono quali elementi eseguire al termine dell'esecuzione dell'elemento corrente.  
  
### Creazione di una sequenza di attività di base con un nodo FlowStep  
 Per modellare una sequenza di base in cui vengono eseguite a loro volta due attività, viene utilizzato l'elemento `FlowStep`.Nell'esempio seguente vengono utilizzati due elementi `FlowStep` per eseguire due attività in sequenza.  
  
```  
<Flowchart>  
  <FlowStep>      
  <Assign DisplayName="Get Name">  
    <Assign.To>  
      <OutArgument x:TypeArguments="x:String">[result]</OutArgument>  
    </Assign.To>  
    <Assign.Value>  
      <InArgument x:TypeArguments="x:String">["User"]</InArgument>  
    </Assign.Value>  
  </Assign>  
    <FlowStep.Next>  
      <FlowStep>  
        <WriteLine Text="["Hello, " & result]"/>  
</FlowStep>  
    </FlowStep.Next>  
  </FlowStep>  
</Flowchart>  
  
```  
  
### Creazione di un diagramma di flusso condizionale con un nodo FlowDecision  
 Per modellare un nodo del flusso condizionale in un flusso di lavoro del diagramma di flusso \(ovvero per creare un collegamento che funziona come simbolo di decisione di un diagramma di flusso tradizionale\), viene utilizzato un nodo <xref:System.Activities.Statements.FlowDecision>.La proprietà <xref:System.Activities.Statements.FlowDecision.Condition%2A> del nodo è impostata su un'espressione che definisce la condizione, le proprietà <xref:System.Activities.Statements.FlowDecision.True%2A> e <xref:System.Activities.Statements.FlowDecision.False%2A> sono impostate su istanze di <xref:System.Activities.Statements.FlowNode> da eseguire se l'espressione restituisce `true` o `false`.Nell'esempio seguente viene illustrato come definire un flusso di lavoro che utilizza un nodo <xref:System.Activities.Statements.FlowDecision>.  
  
```  
<Flowchart>  
  <FlowStep>  
    <Read Result="[s]"/>  
    <FlowStep.Next>  
      <FlowDecision>  
        <IsEmpty Input="[s]" />  
        <FlowDecision.True>  
    <FlowStep>  
            <Write Text="Empty"/>  
    </FlowStep>  
        </FlowDecision.True>  
        <FlowDecision.False>  
    <FlowStep>  
            <Write Text="Non-Empty"/>  
          </FlowStep>  
        </FlowDecision.False>  
      </FlowDecision>  
    </FlowStep.Next>  
  </FlowStep>  
</Flowchart>  
  
```  
  
### Creazione di un'opzione esclusiva con un nodo FlowSwitch  
 Per modellare un diagramma di flusso in cui un percorso esclusivo viene selezionato in base a un valore corrispondente viene utilizzato il nodo <xref:System.Activities.Statements.FlowSwitch%601>.La proprietà <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> è impostata su <xref:System.Activities.Activity%601> con un parametro di tipo di <xref:System.Object> che definisce il valore con cui confrontare le scelte.La proprietà <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> definisce un dizionario di chiavi e oggetti <xref:System.Activities.Statements.FlowNode> da confrontare con l'espressione condizionale e un set di oggetti <xref:System.Activities.Statements.FlowNode> che definiscono come l'esecuzione deve proseguire se il dato caso corrisponde all'espressione condizionale.L'oggetto <xref:System.Activities.Statements.FlowSwitch%601> definisce anche una proprietà <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> che definisce il flusso dell'esecuzione se nessun caso corrisponde all'espressione della condizione.Nell'esempio seguente viene illustrato come definire un flusso di lavoro che utilizza un elemento <xref:System.Activities.Statements.FlowSwitch%601>.  
  
```  
<Flowchart>  
    <FlowSwitch>  
      <FlowStep x:Key="Red">  
        <WriteRed/>  
      </FlowStep>  
      <FlowStep x:Key="Blue">  
        <WriteBlue/>  
      </FlowStep>  
      <FlowStep x:Key="Green">  
        <WriteGreen/>  
      </FlowStep>  
    </FlowSwitch>  
</Flowchart>  
  
```