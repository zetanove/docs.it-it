---
title: "Serializzazione selettiva | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "serializzazione binaria, serializzazione selettiva"
  - "serializzazione, serializzazione selettiva"
ms.assetid: 39c56635-95d2-4afd-aff1-b022e7649bb3
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Serializzazione selettiva
Una classe spesso contiene campi che non devono essere serializzati.Ad esempio, si prenda in considerazione una classe che archivia un ID del thread in una variabile membro.Quando la classe viene deserializzata, il thread archivia l'ID nel caso in cui la classe serializzata non sia più in esecuzione; la serializzazione di questo valore non ha senso.È possibile evitare che le variabili membro vengano serializzate contrassegnandole con l'attributo [NonSerialized](frlrfSystemNonSerializedAttributeClassTopic) come riportato di seguito.  
  
```csharp  
[Serializable]  
public class MyObject   
{  
  public int n1;  
  [NonSerialized] public int n2;  
  public String str;  
}  
```  
  
 Se possibile, rendere non serializzabili gli oggetti che possono contenere dati sensibili alla sicurezza.Se l'oggetto deve essere serializzato, applicare l'attributo **NonSerialized** ai campi specifici che archiviano dati sensibili.Se non si escludono questi campi dalla serializzazione, è necessario essere consapevoli che i dati archiviati saranno esposti a qualsiasi codice che disponga delle autorizzazioni per la serializzazione.Per ulteriori informazioni sulla scrittura di codice di serializzazione protetto, vedere [Sicurezza e serializzazione](../../../docs/framework/misc/security-and-serialization.md).  
  
## Vedere anche  
 [Serializzazione binaria](../../../docs/framework/serialization/binary-serialization.md)   
 [Remote Objects](http://msdn.microsoft.com/it-it/515686e6-0a8d-42f7-8188-73abede57c58)   
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)   
 [Security and Serialization](../../../docs/framework/misc/security-and-serialization.md)