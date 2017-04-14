---
title: "@ServiceHost | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 96ba6967-00f2-422f-9aa7-15de4d33ebf3
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# @ServiceHost
Associa la factory usata per creare l'host del servizio al servizio da ospitare e agli altri aspetti di programmazione necessari per accedere al codice host fornito nel file .svc o per compilarlo.  
  
## Sintassi  
  
```  
  
<% @ServiceHost   
Service = "Service, ServiceNamespace"   
Factory = "Factory, FactoryNamespace"  
Debug = "Debug"  
Language = "Language"   
CodeBehind = "CodeBehind"%>  
```  
  
## Attributi  
  
#### Servizio  
 Nome del tipo CLR del servizio ospitato.  Deve essere un nome completo di un tipo che implementa uno o più dei contatti del servizio.  
  
#### Factory  
 Nome del tipo CLR della factory dell'host del servizio usato per creare un'istanza dell'host del servizio.  L'attributo è facoltativo.  Se non viene specificato, viene usata la factory <xref:System.ServiceModel.Activation.ServiceHostFactory> predefinita, che restituisce un'istanza dell'host <xref:System.ServiceModel.ServiceHost>.  
  
#### Debug  
 Indica se il servizio [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] deve essere compilato con simboli di debug.  `true` se il servizio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] deve essere compilato con simboli di debug; in caso contrario, `false`.  
  
#### Linguaggio  
 Specifica il linguaggio usato per la compilazione di tutto il codice inline contenuto nel file con estensione svc.  I valori possono rappresentare qualsiasi linguaggio supportato da .NET, inclusi C\#, VB e JS, che fanno riferimento, rispettivamente, a C\#, Visual Basic .NET e JScript .NET.  L'attributo è facoltativo.  
  
#### CodeBehind  
 Specifica il file di origine per l'implementazione del servizio Web XML, quando la classe di implementazione non si trova nello stesso file e non è stata compilata in un assembly e inserita nella directory \\Bin.  
  
## Note  
 L'host <xref:System.ServiceModel.ServiceHost> usato per ospitare il servizio è un punto di estensibilità all'interno del modello di programmazione di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  Poiché un modello di factory può essere un tipo polimorfico di cui l'ambiente host non deve creare un'istanza direttamente, tale modello viene usato per creare un'istanza dell'host <xref:System.ServiceModel.ServiceHost>.  
  
 L'implementazione predefinita usa la factory <xref:System.ServiceModel.Activation.ServiceHostFactory> per creare un'istanza dell'host <xref:System.ServiceModel.ServiceHost>.  È tuttavia possibile fornire una factory personalizzata \(ovvero una factory che restituisce l'host derivato personalizzato\) specificando il nome del tipo CLR dell'implementazione di tale factory nella direttiva [@ServiceHost](../../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md).  
  
 Per usare la factory dell'host di servizio personalizzata anziché la factory predefinita è sufficiente fornire il nome del tipo nella direttiva [@ServiceHost](../../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md), come illustrato di seguito:  
  
```  
<% @ServiceHost Factory=”DerivedFactory” Service=”MyService” %>  
```  
  
 È consigliabile garantire che le implementazioni presentino la massima semplicità possibile.  Se si usa un'elevata quantità di logica personalizzata, quest'ultima è più riutilizzabile se inserita nell'host anziché nella factory.  
  
 Ad esempio, per attivare un endpoint AJAX per il servizio `MyService`, specificare la factory <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> come valore dell'attributo `Factory` anziché la factory predefinita <xref:System.ServiceModel.Activation.ServiceHostFactory> nella direttiva [@ServiceHost](../../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md), come illustrato nell'esempio seguente.  
  
## Esempio  
  
```  
<% @ServiceHost   
Service="MyService"  
Language="C#"  
Debug="true"  
Factory="WebScriptServiceHostFactory"  
%>  
```  
  
## Vedere anche  
 [Host di servizi personalizzati](../../../../../docs/framework/wcf/samples/custom-service-host.md)