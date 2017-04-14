---
title: "Procedura: limitare l&#39;accesso tramite la classe PrincipalPermissionAttribute | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "Classe PrincipalPermissionAttribute"
  - "WCF, autorizzazione"
  - "WCF, protezione"
ms.assetid: 5162f5c4-8781-4cc4-9425-bb7620eaeaf4
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# Procedura: limitare l&#39;accesso tramite la classe PrincipalPermissionAttribute
Il controllo dell'accesso alle risorse di un computer appartenente a un dominio Windows è un'attività di sicurezza di base.Ad esempio, solo determinati utenti devono essere in grado di visualizzare i dati riservati, ad esempio le informazioni sulle retribuzioni dei dipendenti.In questo argomento viene descritto come consentire l'accesso a un metodo specifico esclusivamente agli utenti che appartengono a un determinato gruppo.Per un esempio funzionante, vedere [Autorizzazione dell'accesso alle operazioni del servizio](../../../docs/framework/wcf/samples/authorizing-access-to-service-operations.md).  
  
 Questa attività è costituita da due procedure distinte.La prima crea il gruppo e lo popola di utenti,mentre la seconda applica la classe <xref:System.Security.Permissions.PrincipalPermissionAttribute> per definire il gruppo.  
  
### Per creare un gruppo di Windows  
  
1.  Aprire la console **Gestione computer**.  
  
2.  Nel pannello sinistro, fare clic su **Utenti e gruppi locali**.  
  
3.  Fare clic con il pulsante destro del mouse su **Gruppi** e quindi scegliere **Nuovo gruppo**.  
  
4.  Nella casella **Nome gruppo**, digitare il nome del nuovo gruppo.  
  
5.  Nella casella **Descrizione**, digitare la descrizione del nuovo gruppo.  
  
6.  Fare clic sul pulsante **Aggiungi** per aggiungere nuovi membri al gruppo.  
  
7.  Gli utenti che si aggiungono al gruppo e desiderano testare il codice seguente devono disconnettersi dal computer e quindi connettersi nuovamente per essere inclusi effettivamente nel gruppo.  
  
### Per richiedere l'appartenenza dell'utente  
  
1.  Aprire il file di codice di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] contenente il codice del contratto del servizio implementato.[!INCLUDE[crabout](../../../includes/crabout-md.md)] implementazione di un contratto, vedere [Implementazione dei contratti di servizio](../../../docs/framework/wcf/implementing-service-contracts.md).  
  
2.  Applicare l'attributo <xref:System.Security.Permissions.PrincipalPermissionAttribute> a ogni metodo per cui si desidera che l'accesso sia consentito esclusivamente a un gruppo specifico.Impostare la proprietà <xref:System.Security.Permissions.SecurityAttribute.Action%2A> su <xref:System.Security.Permissions.SecurityAction> e la proprietà <xref:System.Security.Permissions.PrincipalPermissionAttribute.Role%2A> sul nome del gruppo.Ad esempio:  
  
     [!code-csharp[c_PrincipalPermissionAttribute#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_principalpermissionattribute/cs/source.cs#1)]
     [!code-vb[c_PrincipalPermissionAttribute#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_principalpermissionattribute/vb/source.vb#1)]  
  
    > [!NOTE]
    >  Se si applica l'attributo <xref:System.Security.Permissions.PrincipalPermissionAttribute> ad un contratto, verrà generata la classe <xref:System.Security.SecurityException>.È possibile applicare l'attributo soltanto a livello di metodo.  
  
## Utilizzo di un certificato per controllare l'accesso a un metodo  
 Se il tipo di credenziale client è un certificato, l'accesso a un metodo può anche essere controllato mediante la classe `PrincipalPermissionAttribute`.A tale scopo è necessario disporre del soggetto e dell'identificazione personale del certificato.  
  
 Per istruzioni su come ricercare e analizzare le proprietà di un certificato, vedere [Procedura: visualizzare certificati con lo snap\-in MMC](../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md).Per rilevare il valore di identificazione personale, vedere [Procedura: recuperare l'identificazione personale di un certificato](../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md).  
  
#### Per controllare l'accesso tramite un certificato  
  
1.  Applicare la classe <xref:System.Security.Permissions.PrincipalPermissionAttribute> al metodo per cui si desidera limitare l'accesso.  
  
2.  Impostare l'azione dell'attributo su <xref:System.Security.Permissions.SecurityAction?displayProperty=fullName>.  
  
3.  Impostare la proprietà `Name` su una stringa costituita dal nome del soggetto e dall'identificazione personale del certificato.Separare i due valori con un punto e virgola e un spazio, come mostrato nell'esempio seguente:  
  
     [!code-csharp[c_PrincipalPermissionAttribute#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_principalpermissionattribute/cs/source.cs#2)]
     [!code-vb[c_PrincipalPermissionAttribute#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_principalpermissionattribute/vb/source.vb#2)]  
  
4.  Impostare la proprietà <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermissionMode%2A> su <xref:System.ServiceModel.Description.PrincipalPermissionMode> come illustrato nell'esempio di configurazione seguente:  
  
    ```  
    <behaviors>  
      <serviceBehaviors>  
      <behavior name="SvcBehavior1">  
      <serviceAuthorization principalPermissionMode="UseAspNetRoles" />  
      </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
     L'impostazione di questo valore su `UseAspNetRoles` indica che la proprietà `Name` dell'elemento `PrincipalPermissionAttribute` viene utilizzata per eseguire un confronto tra stringhe.Per impostazione predefinita, quando un certificato viene utilizzato come credenziale client, [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] concatena il nome comune e l'identificazione personale del certificato con un punto e virgola allo scopo di creare un valore univoco da utilizzare come identità primaria del client.Se nel servizio la modalità `PrincipalPermissionMode` è stata impostata su `UseAspNetRoles`, questo valore di identità primaria viene confrontato con il valore della proprietà `Name` per determinare i diritti di accesso dell'utente.  
  
     In alternativa, quando si crea un servizio indipendente, impostare la proprietà <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermissionMode%2A> in codice, come mostrato nel codice seguente:  
  
     [!code-csharp[c_PrincipalPermissionAttribute#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_principalpermissionattribute/cs/source.cs#3)]
     [!code-vb[c_PrincipalPermissionAttribute#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_principalpermissionattribute/vb/source.vb#3)]  
  
## Vedere anche  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute>   
 <xref:System.Security.Permissions.PrincipalPermissionAttribute>   
 <xref:System.Security.Permissions.SecurityAction>   
 <xref:System.Security.Permissions.PrincipalPermissionAttribute.Role%2A>   
 [Autorizzazione dell'accesso alle operazioni del servizio](../../../docs/framework/wcf/samples/authorizing-access-to-service-operations.md)   
 [Cenni preliminari sulla sicurezza](../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Implementazione dei contratti di servizio](../../../docs/framework/wcf/implementing-service-contracts.md)