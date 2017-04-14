---
title: "&lt;wsdlImporter&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 986b2165-8430-4dba-b1b8-00396841bb96
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# &lt;wsdlImporter&gt;
Specifica tutte le unità di importazione WSDL per l'importazione di metadati Web Services Description Language \(WSDL\) 1.1 con allegati WS\-Policy.  
  
## Sintassi  
  
```  
  
<metadata>  
      <wsdlImporters>  
      <wsdlImporter type="string" />  
   </wsdlImporters>  
</metadata>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`type`|Tipo di questo elemento.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<wsdlImporters\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsdlimporters.md)|Specifica tutte le unità di importazione WSDL per l'importazione di metadati Web Services Description Language \(WSDL\) 1.1 con allegati WS\-Policy.|  
  
## Note  
 Un'unità di importazione WSDL viene usata per importare metadati e per convertire tali informazioni in diverse classi che rappresentano informazioni di contratto e di endpoint.  Può importare selettivamente informazioni di contratto e di endpoint e proprietà che espongono qualsiasi errore di importazione e accettano informazioni sul tipo relative al processo di importazione e di conversione.  Supporta inoltre l'importazione di informazioni dell'associazione e proprietà che forniscono accesso a qualsiasi documento di criteri, documento WSDL, estensione WSDL e documento di XML Schema.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.WsdlImporterElement>   
 <xref:System.ServiceModel.Configuration.MetadataElement>   
 <xref:System.ServiceModel.Configuration.WsdlImporterElementCollection>   
 <xref:System.ServiceModel.Description.MetadataImporter>   
 <xref:System.ServiceModel.Description.WsdlImporter>   
 [Configurazione del client WCF](../../../../../docs/framework/wcf/feature-details/client-configuration.md)   
 [Client](../../../../../docs/framework/wcf/feature-details/clients.md)