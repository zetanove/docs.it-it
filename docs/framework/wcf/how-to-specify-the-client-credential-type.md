---
title: "Procedura: specificare il tipo di credenziali client | Microsoft Docs"
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
  - "credenziali di sicurezza, Aggiunta di messaggi SOAP"
  - "WCF, sicurezza"
ms.assetid: 10f51bee-5f92-4c1a-9126-fa5418535d8f
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Procedura: specificare il tipo di credenziali client
Dopo avere impostato una modalità di sicurezza \(trasporto o messaggio\), è possibile impostare il tipo di credenziali client.Questa proprietà specifica il tipo di credenziali che il client deve fornire al servizio per l'autenticazione.[!INCLUDE[crabout](../../../includes/crabout-md.md)] impostazione della modalità di sicurezza \(un passaggio necessario prima di impostare il tipo di credenziali client\), vedere [Procedura: impostare la modalità di sicurezza](../../../docs/framework/wcf/how-to-set-the-security-mode.md).  
  
### Per impostare il tipo di credenziali client nel codice  
  
1.  Creare un'istanza dell'associazione che verrà utilizzata dal servizio.In questo esempio viene utilizzata l'associazione <xref:System.ServiceModel.WSHttpBinding>.  
  
2.  Impostare la proprietà <xref:System.ServiceModel.WSHttpSecurity.Mode%2A> su un valore appropriato.In questo esempio viene utilizzata la modalità messaggio.  
  
3.  Impostare la proprietà <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> su un valore appropriato.In questo esempio viene impostata per utilizzare l'autenticazione di Windows \(<xref:System.ServiceModel.MessageCredentialType>\).  
  
     [!code-csharp[c_ProgrammingSecurity#14](../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#14)]
     [!code-vb[c_ProgrammingSecurity#14](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#14)]  
  
### Per impostare il tipo di credenziali client nella configurazione  
  
1.  Aggiungere un elemento [\<system.serviceModel\>](../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) al file di configurazione.  
  
2.  Come elemento figlio, aggiungere un elemento [\<associazioni\>](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md).  
  
3.  Aggiungere un'associazione appropriata.In questo esempio viene utilizzato l'elemento [\<wsHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).  
  
4.  Aggiungere un elemento [\<associazione\>](../../../docs/framework/misc/binding.md) e impostare l'attributo `name` su un valore appropriato.In questo esempio viene utilizzato il nome "SecureBinding."  
  
5.  Aggiungere un'associazione `<security>`.Impostare l'attributo `mode` su un valore appropriato.In questo esempio viene impostato su `"Message"`.  
  
6.  Aggiungere un elemento `<message>``<transport> o` , come determinato dalla modalità di sicurezza.Impostare l'attributo `clientCredentialType` su un valore appropriato.In questo esempio viene utilizzato `"Windows"`.  
  
    ```  
    <system.serviceModel>  
      <bindings>  
        <wsHttpBinding>  
          <binding name="SecureBinding">  
            <security mode="Message">  
                 <message clientCredentialType="Windows" />  
             </security>  
          </binding>  
        </wsHttpBinding>  
      </bindings>  
    </system.serviceModel>  
    ```  
  
## Vedere anche  
 [Protezione dei servizi](../../../docs/framework/wcf/securing-services.md)   
 [Procedura: impostare la modalità di sicurezza](../../../docs/framework/wcf/how-to-set-the-security-mode.md)