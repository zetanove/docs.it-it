---
title: "Procedura: creare un servizio che richiede sessioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8a7613ef-0df9-47c3-b8dc-47f42cb1fd8b
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Procedura: creare un servizio che richiede sessioni
Le sessioni creano un stato condiviso tra due o più endpoint che abilita funzionalità utili quali i callback, la sicurezza multihop e le associazioni tra istanze di client e servizi. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]le sessioni in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] applicazioni, vedere [utilizzando le sessioni](../../../../docs/framework/wcf/using-sessions.md).  
  
### <a name="to-specify-that-a-contract-require-its-binding-to-support-sessions"></a>Per specificare che un contratto richiede l'associazione per supportare sessioni  
  
1.  Creare un contratto di servizio con almeno un'operazione. Per un esempio di come creare un contratto di servizio, vedere [procedura: definire un contratto di servizio](../../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md).  
  
2.  Modificare il <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=fullName> che dichiara il contratto impostando il <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=fullName> a una delle due proprietà:  
  
    -   <xref:System.ServiceModel.SessionMode?displayProperty=fullName> se questo contratto deve essere eseguito all'interno di una sessione.  
  
    -   <xref:System.ServiceModel.SessionMode?displayProperty=fullName> se questo contratto può essere eseguito all'interno di una sessione.  
  
    -   <xref:System.ServiceModel.SessionMode?displayProperty=fullName> se questo contratto non deve essere eseguito all'interno di una sessione.  
  
3.  Configurare l'endpoint del servizio per l'utilizzo di un'associazione che supporti sessioni. Esempio di configurazione seguente viene illustrato come utilizzare il <xref:System.ServiceModel.WSDualHttpBinding?displayProperty=fullName>, che supporta un WS`-`ReliableMessaging sessione.  
  
     <!-- TODO: review snippet reference [!code[SCA.Session#2](../../../../samples/snippets/common/VS_Snippets_CFX/sca.session/common/hostapplication.exe.config#2)]  -->
     <!-- TODO: review snippet reference [!code-csharp[SCA.Session#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/sca.session/cs/hostapplication.exe.config#2)]  -->
     <!-- TODO: review snippet reference [!code-vb[SCA.Session#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.session/vb/hostapplication.exe.config#2)]  -->  
  
## <a name="example"></a>Esempio  
 Esempio di codice seguente viene illustrato come specificare un requisito di sessione a livello di contratto e utilizzare un file di configurazione per supportare tale requisito con la <xref:System.ServiceModel.WSDualHttpBinding?displayProperty=fullName> associazione.  
  
 [!code-csharp[SCA.Session#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/sca.session/cs/services.cs#1)]
 [!code-vb[SCA.Session#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.session/vb/services.vb#1)]  
  
 <!-- TODO: review snippet reference [!code[SCA.Session#2](../../../../samples/snippets/common/VS_Snippets_CFX/sca.session/common/hostapplication.exe.config#2)]  -->
 <!-- TODO: review snippet reference [!code-csharp[SCA.Session#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/sca.session/cs/hostapplication.exe.config#2)]  -->
 <!-- TODO: review snippet reference [!code-vb[SCA.Session#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.session/vb/hostapplication.exe.config#2)]  -->  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=fullName>   
 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=fullName>   
 <xref:System.ServiceModel.SessionMode?displayProperty=fullName>