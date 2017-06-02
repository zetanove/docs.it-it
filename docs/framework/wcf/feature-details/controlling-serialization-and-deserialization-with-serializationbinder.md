---
title: "Controllo di serializzazione e deserializzazione con SerializationBinder | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba8dcecf-acc7-467c-939d-021bbac797d4
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Controllo di serializzazione e deserializzazione con SerializationBinder
Durante la serializzazione un formattatore trasmette le informazioni necessarie per la creazione di un'istanza di un oggetto di tipo e versione corretti.  Tali informazioni comprendono in genere il nome completo del tipo e il nome dell'assembly dell'oggetto.  Per impostazione predefinita, la deserializzazione usa queste informazioni per creare un'istanza di un oggetto identico.  Per alcuni utenti potrebbe essere necessario controllare la classe da serializzare e deserializzare, in quanto la classe originale potrebbe non esistere sul computer che esegue la deserializzazione o si è spostata tra gli assembly oppure su server e client sono necessarie versioni diverse della classe.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Utilizzo del gestore di associazione della serializzazione](../../../../docs/framework/wcf/samples/usage-of-serialization-binder.md).  
  
> [!WARNING]
>  Questa funzionalità è disponibile solo se si usa <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> o <xref:System.Runtime.Serialization.NetDataContractSerializer>.  
  
## Uso di SerializationBinder  
 <xref:System.Runtime.Serialization.SerializationBinder> è una classe astratta usata per controllare i tipi effettivi usati durante la serializzazione e la deserializzazione.  Per controllare i tipi usati durante la serializzazione e la deserializzazione, derivare una classe da <xref:System.Runtime.Serialization.SerializationBinder> ed eseguire l'override dei metodi <xref:System.Runtime.Serialization.SerializationBinder.BindToName%2A> System.String, System.String)?qualifyHint=False&autoUpgrade=True e <xref:System.Runtime.Serialization.SerializationBinder.BindToType%2A> System.String)?qualifyHint=False&autoUpgrade=True.  Il metodo <xref:System.Runtime.Serialization.SerializationBinder.BindToName%2A> System.String, System.String)?qualifyHint=False&autoUpgrade=True usa un elemento <xref:System.Type> e restituisce un nome tipo e assembly.  Il metodo <xref:System.Runtime.Serialization.SerializationBinder.BindToType%2A> System.String)?qualifyHint=False&autoUpgrade=True usa un nome tipo e assembly e restituisce un elemento <xref:System.Type>.  
  
## Vedere anche  
 [Serializzazione e deserializzazione](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md)   
 [Utilizzo del gestore di associazione della serializzazione](../../../../docs/framework/wcf/samples/usage-of-serialization-binder.md)