---
title: "Procedura: eseguire una query che restituisce tipi complessi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "ESQL"
  - "jsharp"
ms.assetid: c2209fdb-70ef-4dea-8bb8-097fe96f5563
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: eseguire una query che restituisce tipi complessi
In questo argomento viene illustrato come eseguire una query [!INCLUDE[esql](../../../../../includes/esql-md.md)] che restituisce oggetti del tipo di entità contenenti una proprietà di un tipo complesso.  
  
### Per eseguire il codice in questo esempio  
  
1.  Aggiungere [AdventureWorks Sales Model](http://msdn.microsoft.com/it-it/f16cd988-673f-4376-b034-129ca93c7832) al progetto e configurare il progetto per l'uso di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Per altre informazioni, vedere [How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/it-it/dadb058a-c5d9-4c5c-8b01-28044112231d).  
  
2.  Nella tabella codici per l'applicazione aggiungere le istruzioni `using` seguenti \(`Imports` in Visual Basic\):  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
3.  Fare doppio clic sul file edmx per visualizzare il modello nella [finestra Browser modello](http://msdn.microsoft.com/it-it/94e836e8-a5ea-47ff-aa3e-599d8a02ebfd) di Entity Designer.  Nell'area di Entity Designer selezionare le proprietà `Email` e `Phone` del tipo di entità `Contact`, quindi fare clic con il pulsante destro del mouse e scegliere **Effettua refactoring nel nuovo tipo complesso**.  
  
4.  Un nuovo tipo complesso con le proprietà selezionate `Email` e `Phone` verrà aggiunto a **Browser modello**.  Al tipo complesso viene assegnato un nome predefinito: rinominare il tipo in `EmailPhone` nella finestra **Proprietà**.  Viene inoltre aggiunta, una nuova proprietà `ComplexProperty` al tipo di entità `Contact`.  Rinominare la proprietà in `EmailPhoneComplexType.`  
  
     Per informazioni sulla creazione e la modifica di tipi complessi tramite la procedura guidata Entity Data Model, vedere [How to: Refactor Existing Properties into a Complex Type Property](http://msdn.microsoft.com/it-it/5b2eb3b3-693d-42cb-b43a-405812d677eb) e[How to: Create and Modify Complex Types](http://msdn.microsoft.com/it-it/afb8e206-0ffe-4597-b6d4-6ab566897e1d).  
  
## Esempio  
 Nell'esempio riportato di seguito viene eseguita una query che restituisce una raccolta di oggetti `Contact` e visualizza due proprietà degli oggetti `Contact` : `ContactID` e i valori del tipo complesso `EmailPhoneComplexType`.  
  
 [!code-csharp[DP EntityServices Concepts#ComplexTypeWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#complextypewithentitycommand)]
 [!code-vb[DP EntityServices Concepts#ComplexTypeWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#complextypewithentitycommand)]