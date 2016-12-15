---
title: "Propriet&#224; implementate automaticamente (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "proprietà implementate automaticamente [C#]"
  - "proprietà [C#], implementate automaticamente"
ms.assetid: aa55fa97-ccec-431f-b5e9-5ac789fd32b7
caps.latest.revision: 23
caps.handback.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Propriet&#224; implementate automaticamente (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In C\# 3.0 e versioni successive, le proprietà implementate automaticamente rendono più concisa la dichiarazione di proprietà quando nelle funzioni di accesso della proprietà non è necessaria alcuna logica aggiuntiva.  Consentono inoltre al codice client di creare oggetti.  Quando si dichiara una proprietà come mostrato nel seguente esempio, il compilatore crea un campo sottostante privato anonimo accessibile solo tramite le funzioni di accesso `get` e `set` della proprietà.  
  
## Esempio  
 L'esempio seguente mostra una classe semplice con alcune proprietà implementate automaticamente:  
  
 [!code-cs[csProgGuideLINQ#28](../../../csharp/programming-guide/arrays/codesnippet/CSharp/auto-implemented-properties_1.cs)]  
  
 In C\# 6 e versioni successive, è possibile inizializzare le proprietà implementate automaticamente in modo simile ai campi:  
  
```c#  
public string FirstName { get; set; } = "Jane";  
```  
  
 La classe mostrata nell'esempio precedente è modificabile.  Il codice client può modificare i valori negli oggetti dopo che sono stati creati.  Nelle classi complesse che contengono un comportamento significativo \(metodi\) oltre ai dati, spesso è necessario disporre di proprietà pubbliche.  Tuttavia, per le classi o le struct di piccole dimensioni che incapsulano solo un set di valori \(dati\) e hanno comportamenti minimi o nulli, è consigliabile rendere gli oggetti non modificabili dichiarando la funzione di accesso set come [privata](../../../csharp/language-reference/keywords/private.md) \(non modificabile dai consumer\) o dichiarando solo una funzione di accesso get \(non modificabile ovunque tranne che nel costruttore\).  Per altre informazioni, vedere [Procedura: implementare una classe leggera con proprietà implementate automaticamente](../../../csharp/programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties.md).  
  
 Gli attributi sono consentiti nelle proprietà implementate automaticamente, ma ovviamente non nei campi sottostanti perché non sono accessibili dal codice sorgente.  Se è necessario usare un attributo nel campo sottostante di una proprietà, è sufficiente creare una normale proprietà.  
  
## Vedere anche  
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)