---
title: "Procedura: accedere a WSE 3.0 Service con un client WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1f9bcd9b-8f8f-47fa-8f1e-0d47236eb800
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Procedura: accedere a WSE 3.0 Service con un client WCF
I client [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] sono compatibili a livello di rete con Web Services Enhancements (WSE) 3.0 per i servizi Microsoft .NET quando i client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono configurati per utilizzare la versione dell'agosto 2004 della specifica WS-Addressing. Tuttavia, servizi WSE 3.0 non supporta il protocollo di exchange (MEX) dei metadati, pertanto quando si utilizza il [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per creare un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] classe client, le impostazioni di sicurezza non sono applicato all'oggetto generato [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] client. È quindi necessario specificare le impostazioni di sicurezza richieste dal servizio WSE 3.0 dopo la generazione del client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 È possibile applicare queste impostazioni di sicurezza utilizzando un'associazione personalizzata per prendere in considerazione i requisiti del servizio WSE 3.0 e i requisiti interoperativi tra un servizio WSE 3.0 e un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. I requisiti di interoperabilità includono l'utilizzo di agosto 2004 specifica WS-Addressing e WSE 3.0 protezione dei messaggi di <xref:System.ServiceModel.Security.MessageProtectionOrder>. La protezione dei messaggi predefinita per [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è <xref:System.ServiceModel.Security.MessageProtectionOrder>. In questo argomento viene illustrato come creare un'associazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che interopera con un servizio WSE 3.0. In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene fornito anche un esempio in cui è incorporata questa associazione. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]In questo esempio, vedere [interoperabilità con servizi Web ASMX](../../../../docs/framework/wcf/samples/interoperating-with-asmx-web-services.md).  
  
### <a name="to-access-a-wse-30-web-service-with-a-wcf-client"></a>Per accedere a un servizio Web WSE 3.0 con un client WCF  
  
1.  Eseguire il [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per creare un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] client per il servizio Web WSE 3.0.  
  
     Per un Servizio Web WSE 3.0, viene creato un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Dato che WSE 3.0 non supporta il protocollo MEX, non è possibile utilizzare lo strumento per recuperare i requisiti di sicurezza per il servizio Web. Lo sviluppatore dell'applicazione deve aggiungere le impostazioni di sicurezza per il client.  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]creazione di un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] client, vedere il [procedura: creare un Client](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md).  
  
2.  Creare una classe che rappresenta un'associazione che può comunicare con i servizi Web WSE 3.0.  
  
     La classe seguente fa parte di [interoperabilità con WSE](http://msdn.microsoft.com/it-it/f6816861-96a0-45f9-8736-8e4e82cd3a41) esempio:  
  
    1.  Creare una classe che deriva dal <xref:System.ServiceModel.Channels.Binding> (classe).  
  
         L'esempio di codice seguente crea una classe denominata `WseHttpBinding` che deriva dal <xref:System.ServiceModel.Channels.Binding> (classe).  
  
         [!code-csharp[c_WCFClientToWSEService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#1)]
         [!code-vb[c_WCFClientToWSEService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#1)]  
  
    2.  Aggiungere alla classe le proprietà che specificano l'asserzione turnkey WSE utilizzata dal servizio WSE, se sono necessarie chiavi derivate, se sono utilizzate sessioni protette, se sono necessarie conferme della firma e le impostazioni della protezione dei messaggi. In WSE 3.0, un'asserzione turnkey specifica i requisiti di sicurezza per un client o un servizio Web, in modo analogo alla modalità di autenticazione di un'associazione in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
         Nell'esempio di codice seguente vengono definite le proprietà `SecurityAssertion`, `RequireDerivedKeys`, `EstablishSecurityContext` e `MessageProtectionOrder` che specificano l'asserzione turnkey WSE, se sono necessarie chiavi derivate, se sono utilizzate sessioni protette, se sono necessarie conferme di firma e le impostazioni di protezione dei messaggi.  
  
         [!code-csharp[c_WCFClientToWSEService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#3)]
         [!code-vb[c_WCFClientToWSEService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#3)]  
  
    3.  Eseguire l'override di <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> per impostare le proprietà di associazione.  
  
         Nell'esempio di codice seguente vengono specificati il trasporto, la codifica messaggi e le impostazioni della protezione dei messaggi ottenendo i valori delle proprietà `SecurityAssertion` e `MessageProtectionOrder`.  
  
         [!code-csharp[c_WCFClientToWSEService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#2)]
         [!code-vb[c_WCFClientToWSEService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#2)]  
  
3.  Nel codice dell'applicazione client, aggiungere il codice per impostare le proprietà dell'associazione.  
  
     Nell'esempio di codice seguente viene specificato che il client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] deve utilizzare la protezione e l'autenticazione messaggi come definito dall'asserzione di sicurezza turnkey WSE 3.0 `AnonymousForCertificate`. Sono inoltre necessarie sessioni protette e chiavi derivate.  
  
     [!code-csharp[c_WCFClientToWSEService#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/client.cs#4)]
     [!code-vb[c_WCFClientToWSEService#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/client.vb#4)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente viene definita un'associazione personalizzata che espone proprietà che corrispondono alle proprietà di una asserzione di sicurezza turnkey WSE 3.0. L'associazione personalizzata, denominata `WseHttpBinding`, viene quindi utilizzata per specificare le proprietà di associazione per un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che comunica con l'esempio della Guida rapida WSSecurityAnonymous WSE 3.0.  
  
  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.Channels.Binding>   
 [Interoperabilità con WSE](http://msdn.microsoft.com/it-it/f6816861-96a0-45f9-8736-8e4e82cd3a41)