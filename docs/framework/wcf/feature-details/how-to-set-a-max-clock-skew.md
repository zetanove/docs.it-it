---
title: "Procedura: impostare lo sfasamento massimo dei segnali di clock | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Proprietà MaxClockSkew"
  - "WCF, associazioni personalizzate"
ms.assetid: 491d1705-eb29-43c2-a44c-c0cf996f74eb
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Procedura: impostare lo sfasamento massimo dei segnali di clock
È possibile un malfunzionamento delle funzioni dipendenti dall'orario quando le impostazioni dell'orologio in due computer sono differenti.  Per limitare questo problema, è possibile impostare la proprietà `MaxClockSkew` su un <xref:System.TimeSpan>.  Questa proprietà è disponibile in due classi:  
  
 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>  
  
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>  
  
> [!IMPORTANT]
>  Importante   Per una conversazione sicura, è necessario apportare modifiche alla proprietà `MaxClockSkew` quando il servizio o il client viene avviato automaticamente.  A tale scopo, è necessario impostare la proprietà sull'oggetto <xref:System.ServiceModel.Channels.SecurityBindingElement> restituito da <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters.BootstrapSecurityBindingElement%2A>.  
  
 Per modificare la proprietà in una delle associazioni fornite dal sistema, è necessario trovare l'elemento di associazione di sicurezza nella raccolta di associazioni e impostare la proprietà `MaxClockSkew` su un valore nuovo.  Le due classi derivano da <xref:System.ServiceModel.Channels.SecurityBindingElement>: <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> e <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>.  Quando si recupera l'associazione di sicurezza dalla raccolta, è necessario eseguire il cast a uno di questi tipi per impostare correttamente la proprietà `MaxClockSkew`.  Nell'esempio seguente viene utilizzato <xref:System.ServiceModel.WSHttpBinding> che utilizza <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>.  Per un elenco che specifica quale tipo di associazione di sicurezza usare in ogni associazione fornita dal sistema, vedere [Associazioni fornite dal sistema](../../../../docs/framework/wcf/system-provided-bindings.md).  
  
### Per creare un'associazione personalizzata con un nuovo valore dello sfasamento dei segnali di clock nel codice  
  
1.  > [!WARNING]
    >  Nota   Aggiungere riferimenti agli spazi dei nomi seguenti nel codice: <xref:System.ServiceModel.Channels>, <xref:System.ServiceModel.Description>, <xref:System.Security.Permissions>e <xref:System.ServiceModel.Security.Tokens>.  
  
     Creare un'istanza della classe <xref:System.ServiceModel.WSHttpBinding> e impostarne la modalità di sicurezza su <xref:System.ServiceModel.SecurityMode>.  
  
2.  Creare una nuova istanza della classe <xref:System.ServiceModel.Channels.BindingElementCollection> chiamando il metodo <xref:System.ServiceModel.WSHttpBinding.CreateBindingElements%2A>.  
  
3.  Utilizzare il metodo <xref:System.ServiceModel.Channels.BindingElementCollection.Find%2A> della classe <xref:System.ServiceModel.Channels.BindingElementCollection> per trovare l'elemento di associazione di sicurezza.  
  
4.  Quando si utilizza il metodo <xref:System.ServiceModel.Channels.BindingElementCollection.Find%2A>, eseguire il cast al tipo effettivo.  Nell'esempio seguente viene eseguito il cast al tipo <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>.  
  
5.  Impostare la proprietà <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxClockSkew%2A> sull'elemento di associazione di sicurezza.  
  
6.  Creare un <xref:System.ServiceModel.ServiceHost> con un tipo di servizio e un indirizzo di base appropriati.  
  
7.  Utilizzare il metodo <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> per aggiungere un endpoint e includere <xref:System.ServiceModel.Channels.CustomBinding>.  
  
     [!code-csharp[c_MaxClockSkew#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_maxclockskew/cs/source.cs#1)]
     [!code-vb[c_MaxClockSkew#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_maxclockskew/vb/source.vb#1)]  
  
### Per impostare MaxClockSkew nella configurazione  
  
1.  Creare un [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) nella sezione dell'elemento [\<associazioni\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md).  
  
2.  Creare un elemento [\<associazione\>](../../../../docs/framework/misc/binding.md) e impostare l'attributo `name` su un valore appropriato.  Nell'esempio seguente viene impostato su `MaxClockSkewBinding`.  
  
3.  Aggiungere un elemento di codifica.  L'esempio seguente aggiunge un [\<codificaMessaggiTesto\>](../../../../docs/framework/configure-apps/file-schema/wcf/textmessageencoding.md).  
  
4.  Aggiungere un elemento [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) e specificare un'impostazione appropriata per l'attributo `authenticationMode`.  Nell'esempio seguente l'attributo viene impostato su `Kerberos` per specificare che il servizio utilizza l'autenticazione di Windows.  
  
5.  Aggiungere un elemento [\<impostazioniServizioLocali\>](../../../../docs/framework/configure-apps/file-schema/wcf/localservicesettings-element.md) e impostare l'attributo `maxClockSkew` su un valore nel formato `"##:##:##"`.  Nell'esempio seguente viene impostato su 7 minuti.  Aggiungere facoltativamente un [\<impostazioniServizioLocali\>](../../../../docs/framework/configure-apps/file-schema/wcf/localservicesettings-element.md) e specificare un'impostazione appropriata per l'attributo `maxClockSkew`.  
  
6.  Aggiungere un elemento trasporto.  L'esempio seguente usa un [\<trasportoHttp\>](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md).  
  
7.  Per una conversazione sicura, le impostazioni di sicurezza devono essere applicate all'avvio automatico nell'elemento [\<bootstrapConversazioneProtetta\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md).  
  
    ```  
  
    <bindings>  
      <customBinding>  
        <binding name="MaxClockSkewBinding">  
            <textMessageEncoding />  
            <security authenticationMode="Kerberos">  
               <localClientSettings maxClockSkew="00:07:00" />  
               <localServiceSettings maxClockSkew="00:07:00" />  
               <secureConversationBootstrap>  
                  <localClientSettings maxClockSkew="00:30:00" />  
                  <localServiceSettings maxClockSkew="00:30:00" />  
               </secureConversationBootstrap>  
            </security>  
            <httpTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
  
    ```  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>   
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Procedura: creare un'associazione personalizzata utilizzando SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)