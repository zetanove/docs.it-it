---
title: "Utilizzo di un&#39;attivit&#224; personalizzata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8f356419-681a-4175-ae93-878eee970249
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Utilizzo di un&#39;attivit&#224; personalizzata
Le attività che derivano da <xref:System.Activities.Activity> o le relative sottoclassi possono essere composte in flussi di lavoro più grandi o create direttamente nel codice.In questo argomento viene descritto come utilizzare le attività personalizzate nei flussi di lavoro creati nel codice o nella finestra di progettazione.  
  
> [!NOTE]
>  Le attività personalizzate possono essere utilizzate nel progetto in cui vengono definite, purché sia l'attività personalizzata che l'attività che la utilizza vengono compilate, ovverocaricate da un tipo di creazione di istanza generato dal processo di compilazione. Se l'attività di riferimento viene caricata in modo dinamico \(ad esempioutilizzando ActivityXAMLServices\) l'assembly a cui si fa riferimento deve essere inserito in un progetto diverso o l'XAML generato nella finestra di progettazione deve essere modificato manualmente per abilitarlo.  
  
#### Utilizzo di un'attività personalizzata per un progetto di flusso di lavoro  
  
1.  Aggiungere un riferimento dal progetto host al progetto della libreria di attività contenente l'attività personalizzata.  
  
2.  Compilare la soluzione.  
  
3.  Per utilizzare l'attività personalizzata nella finestra di progettazione, individuare l'attività personalizzata nella casella degli strumenti e trascinare l'attività nell'area di progettazione.  
  
4.  Per utilizzare l'attività personalizzata nel codice, aggiungere un'istruzione Using che fa riferimento al progetto di attività personalizzata e passare una nuova istanza dell'attività a <xref:System.Activities.WorkflowInvoker.Invoke%2A>.