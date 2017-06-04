---
title: "Ordine dei membri dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contratti dati [WCF], ordinamento membri"
ms.assetid: 0658a47d-b6e5-4ae0-ba72-ababc3c6ff33
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Ordine dei membri dati
In alcune applicazioni, è utile conoscere l'ordine in cui i dati dei vari membri dati vengono inviati o si prevede che siano ricevuti \(ad esempio l'ordine in cui i dati vengono visualizzati nell'XML serializzato\).Talvolta può essere necessario modificare tale ordine.In questo argomento vengono illustrate le regole di ordinamento.  
  
## Regole di base  
 Le regole di base per l'ordinamento dei dati sono le seguenti:  
  
-   Se un tipo di contratto dei dati fa parte di una gerarchia di ereditarietà, i membri dati dei relativi tipi di base sono sempre i primi dell'ordine.  
  
-   Seguono in ordine alfabetico i membri dati del tipo corrente per i quali non è impostata la proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> dell'attributo <xref:System.Runtime.Serialization.DataMemberAttribute>.  
  
-   Ci sono poi i membri dati per i quali è impostata la proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> dell'attributo <xref:System.Runtime.Serialization.DataMemberAttribute>.Questi vengono ordinati prima in base al valore della proprietà `Order` e quindi alfabeticamente in caso di presenza di più membri di un determinato valore `Order`.I valori di ordinamento possono essere ignorati.  
  
 L'ordine alfabetico viene stabilito chiamando il metodo <xref:System.String.CompareOrdinal%2A>.  
  
## Esempi  
 Si consideri il codice seguente.  
  
 [!code-csharp[C_DataContractNames#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#4)]
 [!code-vb[C_DataContractNames#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#4)]  
  
 L'XML prodotto è simile al codice seguente.  
  
```  
<DerivedType>  
    <!-- Zebra is a base data member, and appears first. -->  
    <zebra/>   
  
    <!-- Cat has no Order, appears alphabetically first. -->  
    <cat/>  
  
   <!-- Dog has no Order, appears alphabetically last. -->  
    <dog/>   
  
    <!-- Bird is the member with the smallest Order value -->  
    <bird/>  
  
    <!-- Albatross has the next Order value, alphabetically first. -->  
    <albatross/>  
  
    <!-- Parrot, with the next Order value, alphabetically last. -->  
     <parrot/>  
  
    <!-- Antelope is the member with the highest Order value. Note that   
    Order=2 is skipped -->  
     <antelope/>   
</DerivedType>  
```  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 [Equivalenza dei contratti dati](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)   
 [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)