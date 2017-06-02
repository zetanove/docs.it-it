---
title: "Override dell&#39;identit&#224; di un servizio per l&#39;autenticazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d613a22b-07d7-41a4-bada-1adc653b9b5d
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Override dell&#39;identit&#224; di un servizio per l&#39;autenticazione
In genere non è necessario impostare l'identità in un servizio, perché la selezione del tipo di credenziale di un client impone il tipo di identità esposto nei metadati del servizio. Ad esempio, il codice di configurazione seguente usa il [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) e imposta il `clientCredentialType` attributo su Windows.  
  
  
  
 Nel frammento WSDL (Web Services Description Language) viene mostrata l'identità dell'endpoint precedentemente definito. In questo esempio, il servizio è in esecuzione come servizio indipendente in un particolare account utente (username@contoso.com) e pertanto l'identità user principal name (UPN) contiene il nome dell'account. L'UPN è anche noto anche come nome di accesso dell'utente in un dominio Windows.  
  
  
  
 Per un'applicazione di esempio che illustra l'impostazione dell'identità, vedere [esempio identità del servizio](../../../../docs/framework/wcf/samples/service-identity-sample.md). [!INCLUDE[crabout](../../../../includes/crabout-md.md)]identità del servizio, vedere [autenticazione e identità del servizio](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md).  
  
## <a name="kerberos-authentication-and-identity"></a>Autenticazione Kerberos e identità  
 Per impostazione predefinita, quando un servizio è configurato per usare una credenziale di Windows, un [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/identity.md) elemento che contiene un [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/userprincipalname.md) o [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/serviceprincipalname.md) elemento viene generato in WSDL. Se è in esecuzione il servizio di `LocalSystem`, `LocalService`, o `NetworkService` account, il nome dell'entità (SPN) viene generato per impostazione predefinita sotto forma di un servizio `host/` \< *hostname*> poiché questi account hanno accesso ai dati SPN del computer. Se il servizio è in esecuzione con un account diverso, [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] genera un UPN sotto forma di *nome utente*>@<*domainName*`>`. Questo si verifica perché l'autenticazione Kerberos richiede che venga fornito un UPN o un SPN al client per l'autenticazione del servizio.  
  
 È inoltre possibile usare lo strumento Setspn.exe per registrare un SPN aggiuntivo con l'account di un servizio in un dominio. È quindi possibile usare il nome SPN come identità del servizio. Per scaricare lo strumento, vedere [Windows 2000 Resource Kit Tool: Setspn.exe](http://go.microsoft.com/fwlink/?LinkId=91752). [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lo strumento, vedere [Panoramica su Setspn](http://go.microsoft.com/fwlink/?LinkId=61374).  
  
> [!NOTE]
>  Per usare il tipo di credenziale di Windows senza negoziazione, l'account utente del servizio deve avere accesso al nome SPN registrato con il dominio Active Directory. È possibile eseguire questa operazione nei modi seguenti:  
  
-   Usare l'account NetworkService o LocalSystem per eseguire il servizio. Poiché questi account hanno accesso al nome SPN del computer stabilito quando il computer viene associato al dominio Active Directory, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera automaticamente l'elemento SPN corretto nell'endpoint del servizio nei metadati (WSDL) del servizio.  
  
-   Usare un account di dominio Active Directory arbitrario per eseguire il servizio. In questo caso, stabilire un SPN per l'account di dominio, eventualmente usando l'utilità Setspn.exe. Dopo aver creato il nome SPN per l'account del servizio, configurare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per la pubblicazione del nome SPN in questione nei client del servizio tramite i relativi metadati (WSDL). Questa operazione viene eseguita impostando l'identità dell'endpoint esposto tramite un file di configurazione dell'applicazione o tramite codice.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]I nomi SPN, il protocollo Kerberos e Active Directory, vedere [supplemento tecnico Kerberos per Windows](http://go.microsoft.com/fwlink/?LinkId=88330).  
  
### <a name="when-spn-or-upn-equals-the-empty-string"></a>SPN o UPN corrispondente a una stringa vuota  
 Se si imposta il nome SPN o UPN come stringa vuota si verificano diverse cose, a seconda del livello di sicurezza e della modalità di autenticazione usati:  
  
-   Se si sta usando la protezione del trasporto, viene scelta l'autenticazione NT LanMan (NTLM).  
  
-   Se si sta usando la protezione dei messaggi, l'autenticazione potrebbe non riuscire, a seconda della modalità scelta:  
  
-   Se si sta usando la modalità `spnego` e l'attributo `AllowNtlm` è impostato su `false`, l'autenticazione avrà esito negativo.  
  
-   Se si sta usando la modalità `spnego` e l'attributo `AllowNtlm` è impostato su `true`, l'autenticazione avrà esito negativo se l'UPN è vuoto, ma avrà esito positivo se l'SPN è vuoto.  
  
-   Se si sta usando la modalità Kerberos diretta, nota anche come "monofase", l'autenticazione avrà esito negativo.  
  
### <a name="using-the-identity-element-in-configuration"></a>Utilizzo di <> \> elemento di configurazione  
 Se si imposta su Certificate il tipo di credenziale client nell'associazione descritta in precedenza`,` il codice WSDL generato conterrà un certificato X.509 con serializzazione Base64 per il valore dell'identità, come illustrato nel codice seguente. Si tratta dell'impostazione predefinita per tutti i tipi di credenziale client diversi da Windows.  
  
  
  
 È possibile modificare il valore dell'identità del servizio predefinita o il tipo dell'identità usando l'elemento <`identity`> nella configurazione o impostando l'identità nel codice. Nel codice di configurazione seguente viene impostata un'identità DNS (Domain Name System) con il valore `contoso.com`.  
  
  
  
### <a name="setting-identity-programmatically"></a>Impostazione dell'identità a livello di programmazione  
 Il servizio non deve necessariamente specificare in modo esplicito un'identità, poiché [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] la determina automaticamente. Tuttavia, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente di specificare un'identità su un endpoint, se necessario. Nel codice seguente viene aggiunto un nuovo endpoint di servizio con un'identità DNS specifica.  
  
 [!code-csharp[C_Identity#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_identity/cs/source.cs#5)]
 [!code-vb[C_Identity#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_identity/vb/source.vb#5)]  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: creare un verificatore di identità Client personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-custom-client-identity-verifier.md)   
 [L'autenticazione e identità del servizio](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)