---
title: "Procedura: configurare un servizio WCF che interagisca con client di servizi Web ASP.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 48e1cd90-de80-4d6c-846e-631878955762
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Procedura: configurare un servizio WCF che interagisca con client di servizi Web ASP.NET
Per configurare un [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] endpoint del servizio per l'interoperabilità con [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] client del servizio Web, utilizzare il <xref:System.ServiceModel.BasicHttpBinding?displayProperty=fullName> tipo come tipo di associazione per l'endpoint del servizio.  
  
 È possibile, se lo si desidera, attivare nell'associazione il supporto per HTTPS e l'autenticazione del client a livello di trasporto. [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]Client del servizio Web non supportano codifica MTOM, pertanto la <xref:System.ServiceModel.BasicHttpBinding.MessageEncoding%2A?displayProperty=fullName> proprietà deve essere lasciata come valore predefinito, ovvero <xref:System.ServiceModel.WSMessageEncoding?displayProperty=fullName>. Client del servizio Web ASP.Net non supportano WS-Security, in modo che il <xref:System.ServiceModel.BasicHttpBinding.Security%2A?displayProperty=fullName> deve essere impostato su <xref:System.ServiceModel.BasicHttpSecurityMode>.  
  
 Per rendere i metadati un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] servizio disponibile per [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] strumenti di generazione proxy del servizio Web (vale a dire [Web Services Description Language Tool (Wsdl.exe)](http://go.microsoft.com/fwlink/?LinkId=73833), [strumento di individuazione Servizi Web (Disco.exe)](http://go.microsoft.com/fwlink/?LinkId=73834)e la funzionalità Aggiungi riferimento Web in Visual Studio), è necessario esporre un endpoint di metadati HTTP/GET.  
  
### <a name="to-add-a-wcf-endpoint-that-is-compatible-with-aspnet-web-service-clients-in-code"></a>Per aggiungere un endpoint WCF compatibile con client di servizi Web ASP.NET nel codice  
  
1.  Creare un nuovo <xref:System.ServiceModel.BasicHttpBinding> istanza  
  
2.  Attivare facoltativamente la protezione di trasporto per questa associazione dell'endpoint del servizio impostando la modalità di sicurezza per l'associazione su <xref:System.ServiceModel.BasicHttpSecurityMode>. Per informazioni dettagliate, vedere [la sicurezza del trasporto](../../../../docs/framework/wcf/feature-details/transport-security.md).  
  
3.  Aggiungere un nuovo endpoint applicazione all'host del servizio utilizzando l'istanza di associazione appena creata. Per informazioni dettagliate su come aggiungere un endpoint del servizio nel codice, vedere il [procedura: creare un Endpoint del servizio nel codice](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-code.md).  
  
4.  Attivare un endpoint dei metadati HTTP/GET per il servizio. Per ulteriori informazioni vedere [procedura: pubblicare metadati per un servizio utilizzando codice](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md).  
  
### <a name="to-add-a-wcf-endpoint-that-is-compatible-with-aspnet-web-service-clients-in-a-configuration-file"></a>Per aggiungere un endpoint WCF compatibile con client di servizi Web ASP.NET in un file di configurazione  
  
1.  Creare un nuovo <xref:System.ServiceModel.BasicHttpBinding> configurazione dell'associazione. Per informazioni dettagliate, vedere il [procedura: specificare un'associazione al servizio nella configurazione](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md).  
  
2.  Attivare facoltativamente la protezione di trasporto per questa configurazione dell'associazione dell'endpoint del servizio impostando la modalità di sicurezza per l'associazione su <xref:System.ServiceModel.BasicHttpSecurityMode>. Per informazioni dettagliate, vedere [la sicurezza del trasporto](../../../../docs/framework/wcf/feature-details/transport-security.md).  
  
3.  Configurare un nuovo endpoint applicazione per il servizio utilizzando la configurazione dell'associazione appena creata. Per informazioni dettagliate su come aggiungere un endpoint del servizio in un file di configurazione, vedere il [procedura: creare un Endpoint del servizio nella configurazione](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md).  
  
4.  Attivare un endpoint dei metadati HTTP/GET per il servizio. Per informazioni dettagliate, vedere il [procedura: pubblicare metadati per un servizio utilizzando un File di configurazione](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente viene illustrato come aggiungere un endpoint [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] compatibile con i client di servizi Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] nel codice e, in alternativa, nei file di configurazione.  
  
 [!code-csharp[C_HowTo-WCFServiceAndASMXClient#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/cs/program.cs#0)]
 [!code-vb[C_HowTo-WCFServiceAndASMXClient#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/vb/program.vb#0)]  
  
 <!-- TODO: review snippet reference [!code[C_HowTo-WCFServiceAndASMXClient#1](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/common/app.config#1)]  -->  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: creare un Endpoint del servizio nel codice](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-code.md)   
 [Procedura: pubblicare metadati per un servizio tramite codice](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)   
 [Procedura: specificare un'associazione al servizio nella configurazione](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)   
 [Procedura: creare un Endpoint del servizio nella configurazione](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)   
 [Procedura: pubblicare metadati per un servizio utilizzando un File di configurazione](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)   
 [Sicurezza del trasporto](../../../../docs/framework/wcf/feature-details/transport-security.md)   
 [Utilizzo dei metadati](../../../../docs/framework/wcf/feature-details/using-metadata.md)