---
title: "Procedura: configurare un client WCF per interagire con i servizi WSE&amp;3;.0 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3dadd7f1-d207-4ea5-a73b-3e8aa44407f8
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Procedura: configurare un client WCF per interagire con i servizi WSE&amp;3;.0
I client [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] sono compatibili a livello di transito con Web Services Enhancements 3.0 per servizi Microsoft .NET (WSE) quando i client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono configurati per utilizzare la versione dell'agosto 2004 di WS-Addressing.  
  
### <a name="to-configure-a-wcf-client-to-interoperate-with-a-wse-30-web-service"></a>Per configurare un client WCF che interagisca con il servizio Web WSE 3.0  
  
1.  Eseguire il [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per creare un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] client per il servizio Web WSE 3.0.  
  
     Per un Servizio Web WSE viene creata una classe client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
     Per informazioni dettagliate sulla creazione di un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] client, vedere il [procedura: creare un Client](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md).  
  
2.  Creare una classe che rappresenta un'associazione che può comunicare con i servizi Web WSE 3.0.  
  
     La classe seguente fa parte di [interoperabilità con WSE](http://msdn.microsoft.com/it-it/f6816861-96a0-45f9-8736-8e4e82cd3a41) esempio.  
  
    1.  Creare una classe che deriva dal <xref:System.ServiceModel.Channels.Binding> (classe).  
  
         L'esempio di codice seguente crea una classe denominata `WseHttpBinding` che deriva dal <xref:System.ServiceModel.Channels.Binding> (classe).  
  
         [!code-csharp[c_WCFClientToWSEService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#1)]
         [!code-vb[c_WCFClientToWSEService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#1)]  
  
    2.  Aggiungere alla classe le proprietà che specificano l'asserzione turnkey WSE, se sono necessarie chiavi derivate, se vengono utilizzate sessioni protette, se sono necessarie conferme di firma e le impostazioni di protezione dei messaggi.  
  
         L'esempio di codice seguente definisce `SecurityAssertion,``RequireDerivedKeys, EstablishSecurityContext, MessageProtectionOrder` le proprietà che specificano l'asserzione turnkey WSE, se sono necessarie chiavi derivate, se vengono utilizzate sessioni protette, se sono necessarie conferme di firma e le impostazioni di protezione del messaggio, rispettivamente.  
  
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
 Nell'esempio di codice seguente viene definita un'associazione personalizzata che espone proprietà che corrispondono alle proprietà di una asserzione di sicurezza turnkey WSE 3.0. L'associazione personalizzata, denominata `WseHttpBinding` viene quindi utilizzata per specificare le proprietà dell'associazione per un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
  
[!code-csharp[c_WCFClientToWSEService#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/client.cs#0)]
[!code-vb[c_WCFClientToWSEService#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/client.vb#0)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.Channels.Binding>   
 [Interoperabilità con WSE](http://msdn.microsoft.com/it-it/f6816861-96a0-45f9-8736-8e4e82cd3a41)