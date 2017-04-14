---
title: "Creazione di servizi interoperativi WS-I Basic Profile 1.1 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "configurazione [WCF], servizi interoperabili"
ms.assetid: 91b70a21-8f5c-4679-808c-2ed5fa6b2013
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Creazione di servizi interoperativi WS-I Basic Profile 1.1
Per configurare l'interoperabilità di un endpoint del servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] con client del servizio Web [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]:  
  
-   Utilizzare il <xref:System.ServiceModel.BasicHttpBinding?displayProperty=fullName> tipo come tipo di associazione per l'endpoint del servizio.  
  
-   Non utilizzare funzioni di callback e di contratto di sessioni né comportamenti della transazione nell'endpoint del servizio.  
  
 È possibile, se lo si desidera, attivare nell'associazione il supporto per HTTPS e l'autenticazione del client a livello di trasporto.  
  
 Le caratteristiche seguenti di <xref:System.ServiceModel.BasicHttpBinding> classe richiedono funzionalità oltre a WS-I Basic Profile 1.1:  
  
-   Codifica dei messaggi Transmission Optimization Mechanism (MTOM) messaggio applicando il <xref:System.ServiceModel.BasicHttpBinding.MessageEncoding%2A?displayProperty=fullName> proprietà. Lasciare questa proprietà sul valore predefinito, ovvero <xref:System.ServiceModel.WSMessageEncoding?displayProperty=fullName> per non utilizzare MTOM.  
  
-   Sicurezza dei messaggi controllata dal <xref:System.ServiceModel.BasicHttpBinding.Security%2A?displayProperty=fullName> valore fornisce il supporto di WS-Security conforme a WS-I Basic Security Profile 1.0. Lasciare questa proprietà sul valore predefinito, ovvero <xref:System.ServiceModel.SecurityMode?displayProperty=fullName> di non utilizzare WS-Security.  
  
 Per rendere i metadati un [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] servizio disponibile per [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)], utilizzare gli strumenti di generazione client del servizio Web: [Web Services Description Language Tool (Wsdl.exe)](http://msdn.microsoft.com/it-it/b9210348-8bc2-4367-8c91-d1a04b403e88), [strumento di individuazione Servizi Web (Disco.exe)](http://msdn.microsoft.com/it-it/acd88078-c581-42bc-94ca-6633e2851979)e `Add Web Reference` funzionalità [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]; è necessario abilitare la pubblicazione dei metadati. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Gli endpoint dei metadati di pubblicazione](../../../docs/framework/wcf/publishing-metadata-endpoints.md).  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 Nell'esempio di codice seguente viene illustrato come aggiungere un endpoint [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] compatibile con i client del servizio Web [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] nel codice e, in alternativa, nei file di configurazione.  
  
### <a name="code"></a>Codice  
 [!code-csharp[C_HowTo-WCFServiceAndASMXClient#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/cs/program.cs#0)]
 [!code-vb[C_HowTo-WCFServiceAndASMXClient#0](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/vb/program.vb#0)]  
  
 [!code[C_HowTo-WCFServiceAndASMXClient#1](../../../samples/snippets/common/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/common/app.config#1)]  
  
## <a name="see-also"></a>Vedere anche  
 [Interoperabilità con servizi Web ASP.NET](../../../docs/framework/wcf/feature-details/interop-with-aspnet-web-services.md)