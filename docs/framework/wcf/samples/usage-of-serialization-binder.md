---
title: "Utilizzo del gestore di associazione della serializzazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ab46c087-200c-45bf-9c95-5a6cda6e8b98
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Utilizzo del gestore di associazione della serializzazione
In questo esempio viene illustrato come utilizzare <xref:System.Runtime.Serialization.SerializationBinder> per modificare la versione di un tipo generico quando è serializzato.  
  
## Dimostrazione  
 <xref:System.Runtime.Serialization.SerializationBinder>, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>  
  
## Discussione  
 In questo esempio viene illustrato come due entità destinate a versioni diverse di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] possono comunicare utilizzando il formattatore binario e il gestore di associazione della serializzazione.  
  
 Lo sviluppo di questo esempio è stato realizzato tramite .NET Remoting.L'esempio è costituito da un server destinato a [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] che implementa un contratto con tipi generici e due client diversi, uno destinato a [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)] e un altro destinato a [!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)].  
  
 Il server allega un oggetto <xref:System.Runtime.Serialization.SerializationBinder> al formattatore binario per essere in grado di modificare di conseguenza la versione dei tipi durante la serializzazione, consentendo a entrambi i client di deserializzare correttamente tali tipi.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Per eseguire il client, fare clic con il pulsante destro del mouse sulla soluzione SBGenericsVTS \(6 progetti\), quindi scegliere **Proprietà**.  
  
2.  In **Proprietà comuni** selezionare **Progetto di avvio**, quindi **Progetti di avvio multipli**.  
  
3.  Selezionare innanzitutto **Server**, quindi **Client20** e infine **Client40**.Selezionare l'azione **Avvia** per questi tre progetti e lasciare gli altri impostati su **Nessuno**.  
  
4.  Fare clic su **OK**, quindi premere F5 per eseguire l'esempio.