---
title: "&lt;bindingExtensions&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8373f94d-d095-486f-8f1e-4ac2f72b58c7
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# &lt;bindingExtensions&gt;
Questa sezione consente l'uso di un'associazione definita dall'utente dal file di configurazione di un computer o di un'applicazione.  È possibile aggiungere un binding definito dall'utente a questa raccolta usando la parola chiave `add` e impostando l'attributo `type` dell'elemento su un'associazione definita dall'utente e anche l'attributo `name` sul nome dell'associazione definita dall'utente.  
  
 Le estensioni dell'associazione consentono di creare associazioni definite dall'utente da usare come parte di una configurazione di endpoint.  A livello di programmazione, un'estensione di associazione è un tipo che implementa la classe astratta <xref:System.ServiceModel.Channels.Binding>.  
  
 Nell'esempio seguente viene usato l'elemento `add` e l'attributo `name` per aggiungere un'estensione di associazione alla sezione `bindingElementExtensions` del file di configurazione.  
  
```  
<system.serviceModel>  
    <extensions>  
        <bindingExtensions>  
           <add name="MyBinding" type="Microsoft.ServiceModel.Samples.MyBinding, MyBinding,  
                Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
        </bindingExtensions>  
    </extensions>  
</system.serviceModel>  
```  
  
 Per aggiungere capacità di configurazione all'elemento, è necessario scrivere e registrare un elemento `bindingSection`.  Per altre informazioni a tal proposito, vedere la documentazione di <xref:System.Configuration>.  
  
 Dopo la definizione dell'elemento e del relativo tipo di configurazione, è possibile usare l'estensione in un endpoint come illustrato nell'esempio seguente.  
  
```  
<services>  
    <service name="MyService">  
        <endpoint address="myAddress" binding="MyBinding" />  
    </service>  
</services>  
  
```  
  
## Vedere anche  
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)