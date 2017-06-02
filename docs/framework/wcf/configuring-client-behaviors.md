---
title: "Configurazione dei comportamenti client | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: df5b32fa-e73b-4e8e-b66f-357c748e0173
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Configurazione dei comportamenti client
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] configura i comportamenti in due modi: facendo riferimento alle configurazioni dei comportamenti definite nella sezione `<behavior>` del file di configurazione di un'applicazione client o a livello di programmazione nell'applicazione chiamante.  In questo argomento vengono illustrati entrambi gli approcci.  
  
 Quando di usa un file di configurazione, la configurazione del comportamento è una raccolta denominata di impostazioni di configurazione.  Il nome di ogni configurazione di comportamento deve essere univoco.  Questa stringa viene usata nell'attributo `behaviorConfiguration` di una configurazione endpoint per collegare l'endpoint al comportamento.  
  
## Esempio  
 Nel codice di configurazione seguente viene definito un comportamento denominato `myBehavior`.  L'endpoint client fa riferimento a questo comportamento nell'attributo `behaviorConfiguration`.  
  
```  
<configuration>  
    <system.serviceModel>  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name="myBehavior">  
                    <clientVia />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
        <bindings>  
            <basicHttpBinding>  
                <binding name="myBinding" maxReceivedMessageSize="10000" />  
            </basicHttpBinding>  
        </bindings>  
        <client>  
            <endpoint address="myAddress" binding="basicHttpBinding" bindingConfiguration="myBinding" behaviorConfiguration="myBehavior" contract="myContract" />  
        </client>  
    </system.serviceModel>  
</configuration>  
```  
  
## Uso di comportamenti a livello di programmazione  
 È inoltre possibile configurare o inserire comportamenti a livello di programmazione individuando la proprietà `Behaviors` appropriata nell'oggetto client [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] o nell'oggetto channel factory client prima dell'apertura del client.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come inserire un comportamento a livello di programmazione accedendo alla proprietà <xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A> nell'oggetto <xref:System.ServiceModel.Description.ServiceEndpoint> restituito dalla proprietà <xref:System.ServiceModel.ChannelFactory.Endpoint%2A> prima della creazione dell'oggetto channel.  
  
 [!code-csharp[ChannelFactoryBehaviors#10](../../../samples/snippets/csharp/VS_Snippets_CFX/channelfactorybehaviors/cs/client.cs#10)]
 [!code-vb[ChannelFactoryBehaviors#10](../../../samples/snippets/visualbasic/VS_Snippets_CFX/channelfactorybehaviors/vb/client.vb#10)]  
  
## Vedere anche  
 [\<comportamenti\>](../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)