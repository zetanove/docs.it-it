---
title: "&lt;client&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.ServiceModel/client"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#client"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: bf0f7031-76c8-4e7e-a6c6-9ad9119134be
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# &lt;client&gt;
L'elemento `client` definisce un elenco di endpoint ai quali può connettersi un client.  
  
## Sintassi  
  
```  
  
<system.serviceModel>  
    <client>  
        <endpoint>  
        </endpoint>  
                <metadata>  
        </metadata>  
    </client>  
</system.serviceModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 None  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<endpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-of-client.md)|Contiene una raccolta di elementi dell'endpoint che specifica a quali endpoint può connettersi questo client.|  
|[\<metadati\>](../../../../../docs/framework/configure-apps/file-schema/wcf/metadata.md)|Contiene impostazioni per l'elaborazione di metadati.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<system.serviceModel\>](../../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)|L'elemento radice di tutti gli elementi di configurazione di Windows Communication Foundation \(WCF\).|  
  
## Note  
 La sezione `client` definisce un elenco di endpoint ai quali può connettersi un client.  Ogni endpoint elencato nella sezione client definisce la propria associazione, comportamento e contratto.  È identificato in modo univoco dalla combinazione degli attributi `name` e `contract`.  Il codice client specifica il `name` al quale connettere un endpoint per il servizio implementato dal client.  Se l'attributo `name` è omesso, l'endpoint si comporta come endpoint predefinito per il contratto che implementa.  
  
 In aggiunta, questa sezione specifica anche impostazioni per l'elaborazione di metadati.  
  
## Esempio  
  
```  
<client>  
    <endpoint address="/HelloWorld/"  
              bindingConfiguration="usingDefaults"  
              name="MyBinding"  
              binding="customBinding"  
              contract="HelloWorld">  
    <addressProperties actingAs="http://www.microsoft.com/TestActor"  
             identityData="BasicReadWrite" identityType="Spn" isAddressPrivate="false">  
    </endpoint>  
</client>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ClientSection>   
 <xref:System.ServiceModel.Configuration.MetadataElement>   
 [Configurazione del client WCF](../../../../../docs/framework/wcf/feature-details/client-configuration.md)   
 [Client](../../../../../docs/framework/wcf/feature-details/clients.md)