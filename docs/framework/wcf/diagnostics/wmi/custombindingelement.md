---
title: "CustomBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: df959dc5-1aef-4338-a123-6ff3e7bc37af
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# CustomBindingElement
CustomBindingElement  
  
## Sintassi  
  
```  
class CustomBindingElement : BindingElement  
{  
  string Name;  
};  
```  
  
## Metodi  
 La classe CustomBindingElement non definisce metodi.  
  
## Proprietà  
 La classe CustomBindingElement dispone della proprietà seguente:  
  
### Nome  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Stringa che contiene il nome della configurazione dell'associazione.  Questo valore è una stringa definita dall'utente che deve essere univoca in quanto funge da stringa di identificazione dell'associazione personalizzata.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.CustomBinding>