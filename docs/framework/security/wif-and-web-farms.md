---
title: "WIF e Web farm | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fc3cd7fa-2b45-4614-a44f-8fa9b9d15284
caps.latest.revision: 9
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 9
---
# WIF e Web farm
Quando si utilizza Windows identità Foundation \(WIF\) per proteggere le risorse di un'applicazione di terze parti \(RP\) componente che viene distribuito in una web farm, è necessario effettuare operazioni specifiche per garantire che WIF è in grado di elaborare i token dalle istanze dell'applicazione RP in esecuzione su diversi computer della farm.  Questa elaborazione include la convalida delle firme token di sessione, la crittografia e decrittografia di token di sessione, la memorizzazione nella cache i token di sessione e l'identificazione riprodotti i token di protezione.  
  
 In genere, quando WIF viene utilizzato per proteggere le risorse di un'applicazione RP – se la RP è in esecuzione su un singolo computer o in una web farm \- viene stabilita una sessione con il client in base al token di protezione è stato ottenuto dal servizio token di protezione \(STS\).  Questo è evitare di forzare il client che esegua l'autenticazione per il servizio STS per tutte le risorse dell'applicazione protetta tramite WIF.  Per ulteriori informazioni su come WIF gestisce le sessioni, vedere [Gestione delle sessioni WIF](../../../docs/framework/security/wif-session-management.md).  
  
 Quando vengono utilizzate le impostazioni predefinite, WIF effettua le seguenti operazioni:  
  
-   Viene utilizzata un'istanza del <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> classe per leggere e scrivere un token di sessione \(un'istanza del <xref:System.IdentityModel.Tokens.SessionSecurityToken> classe\) che trasporta le attestazioni e altre informazioni per il token di protezione è stato utilizzato per l'autenticazione, nonché informazioni sulla sessione di se stesso.  Il token di sessione è fornito e memorizzato in un cookie di sessione.  Per impostazione predefinita, <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> utilizza il <xref:System.IdentityModel.ProtectedDataCookieTransform> classe che utilizza la Data Protection API \(DPAPI\), per proteggere il token di sessione.  DPAPI offre protezione utilizzando le credenziali dell'utente o del computer e memorizza i dati della chiave nel profilo utente.  
  
-   Viene utilizzato un predefinito e l'implementazione in memoria dei <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> classe per memorizzare ed elaborare il token di sessione.  
  
 Queste impostazioni predefinite funzionano in scenari in cui l'applicazione di RP è distribuita su un singolo computer; Tuttavia, quando vengono distribuiti in una web farm, ciascuna richiesta HTTP può essere inviato ed elaborato da un'altra istanza dell'applicazione RP in esecuzione su un computer diverso.  In questo scenario, le impostazioni di default WIF descritte in precedenza non funzioneranno perché il token protezione e token per la memorizzazione nella cache dipendono da un computer specifico.  
  
 Per distribuire un'applicazione RP in una web farm, è necessario assicurarsi che l'elaborazione dei token di sessione \(nonché di token riprodotti\) non dipenda l'applicazione in esecuzione su un computer specifico.  Un modo per eseguire questa operazione consiste nell'implementare l'applicazione RP in modo che utilizzi la funzionalità fornita da ASP.NET `<machineKey>` elemento di configurazione e consente la memorizzazione nella cache distribuita per l'elaborazione del token di sessione e riprodotti i token.  Il `<machineKey>` elemento consente di specificare le chiavi necessarie per convalidare, crittografare e decrittografare i token in un file di configurazione che consente di specificare le stesse chiavi in computer diversi in web farm.  WIF fornisce un gestore di token di sessione specializzati, i <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler>, che consente di proteggere i token utilizzando le chiavi specificate nel `<machineKey>` elemento.  Per implementare questa strategia, è possibile attenersi alle seguenti indicazioni:  
  
-   Utilizzare ASP.NET `<machineKey>` elemento di configurazione per specificare esplicitamente le chiavi di crittografia e la firma che possono essere utilizzate su computer della farm.  il XML riportato di seguito viene illustrata la specifica del `<machineKey>` elemento sotto il `<system.web>` elemento in un file di configurazione.  
  
    ```xml  
    <machineKey compatibilityMode="Framework45" decryptionKey="CC510D … 8925E6" validationKey="BEAC8 … 6A4B1DE" />  
    ```  
  
-   Configurare l'applicazione per utilizzare il <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler> , aggiungerlo all'insieme di gestore del token.  È innanzitutto necessario rimuovere il <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> \(o qualsiasi gestore derivato dal <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> classe\) dall'insieme di token gestore se è presente un gestore di questo tipo.  Il <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler> utilizza il <xref:System.IdentityModel.Services.MachineKeyTransform> classe, che consente di proteggere i dati del cookie di sessione utilizzando il materiale di crittografia specificato nel `<machineKey>` elemento.  Il file XML riportato di seguito viene illustrato come aggiungere il <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler> a un insieme di gestore del token.  
  
    ```xml  
    <securityTokenHandlers>  
      <remove type="System.IdentityModel.Tokens.SessionSecurityTokenHandler, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
      <add type="System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    </securityTokenHandlers>  
    ```  
  
-   Derivare da <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> e implementare distribuiti nella cache, vale a dire una cache che è accessibile da tutti i computer della farm in cui può essere eseguito il RP.  Configurare RP per utilizzare la cache distribuita specificando il [\<sessionSecurityTokenCache\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/sessionsecuritytokencache.md) elemento nel file di configurazione.  È possibile eseguire l'override di <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache.LoadCustomConfiguration%2A?displayProperty=fullName> metodo nella classe derivata per implementare gli elementi figlio del `<sessionSecurityTokenCache>` elemento se sono necessari.  
  
    ```xml  
    <caches>  
      <sessionSecurityTokenCache type="MyCacheLibrary.MySharedSessionSecurityTokenCache, MyCacheLibrary">  
        <!—optional child configuration elements, if implemented by the derived class -->  
      </sessionSecurityTokenCache>  
    </caches>  
    ```  
  
     Un modo per implementare la memorizzazione nella cache distribuita è fornire un front\-end WCF per la cache personalizzata.  Per ulteriori informazioni sull'implementazione di un servizio di caching di WCF, vedere [Il servizio di memorizzazione nella cache di WCF](#BKMK_TheWCFCachingService).  Per ulteriori informazioni sull'implementazione di un client WCF che l'applicazione RP può utilizzare per chiamare il servizio di memorizzazione nella cache, vedere [La memorizzazione nella cache Client WCF](#BKMK_TheWCFClient).  
  
-   Se l'applicazione rileva rieseguiti token è necessario seguire una simile distribuito la memorizzazione nella cache di strategia per la cache del token per la riproduzione mediante la derivazione da <xref:System.IdentityModel.Tokens.TokenReplayCache> che fa riferimento il token di servizio cache in riproduzione e la [\<tokenReplayCache\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/tokenreplaycache.md) elemento di configurazione.  
  
> [!IMPORTANT]
>  Tutto il codice in questo argomento e XML di esempio da cui proviene il [ClaimsAwareWebFarm](http://go.microsoft.com/fwlink/?LinkID=248408) \(in ingleseLinkID \= 248408\) campione.  
  
> [!IMPORTANT]
>  Gli esempi in questo argomento vengono forniti come\-è e non destinati ad essere utilizzati nel codice di produzione senza alcuna modifica.  
  
<a name="BKMK_TheWCFCachingService"></a>   
## Il servizio di memorizzazione nella cache di WCF  
 L'interfaccia seguente definisce il contratto tra il servizio di cache di WCF e il client WCF utilizzato dall'applicazione di terze parti componente per comunicare con esso.  Essenzialmente, espone i metodi del <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> classe come operazioni di servizio.  
  
```  
[ServiceContract()]  
public interface ISessionSecurityTokenCacheService  
{  
    [OperationContract]  
    void AddOrUpdate(string endpointId, string contextId, string keyGeneration, SessionSecurityToken value, DateTime expiryTime);  
  
    [OperationContract]  
    IEnumerable<SessionSecurityToken> GetAll(string endpointId, string contextId);  
  
    [OperationContract]  
    SessionSecurityToken Get(string endpointId, string contextId, string keyGeneration);  
  
    [OperationContract(Name = "RemoveAll")]  
    void RemoveAll(string endpointId, string contextId);  
  
    [OperationContract(Name = "RemoveAllByEndpointId")]  
    void RemoveAll(string endpointId);  
  
    [OperationContract]  
    void Remove(string endpointId, string contextId, string keyGeneration);  
}  
```  
  
 Il codice riportato di seguito mostra l'implementazione di WCF di memorizzazione nella cache del servizio.  In questo esempio, l'impostazione predefinita, viene utilizzata la cache dei token di sessione in memoria implementata da WIF.  In alternativa, è possibile implementare una cache resistente da un database.  `ISessionSecurityTokenCacheService`definisce l'interfaccia illustrato sopra.  In questo esempio, non tutti i metodi necessari per implementare l'interfaccia vengono visualizzati per brevità.  
  
```  
using System;  
using System.Collections.Generic;  
using System.IdentityModel.Configuration;  
using System.IdentityModel.Tokens;  
using System.ServiceModel;  
using System.Xml;  
  
namespace WcfSessionSecurityTokenCacheService  
{  
    [ServiceBehavior(InstanceContextMode = InstanceContextMode.Single)]  
    public class SessionSecurityTokenCacheService : ISessionSecurityTokenCacheService  
    {  
        SessionSecurityTokenCache internalCache;  
  
        // sets the internal cache used by the service to the default WIF in-memory cache.  
        public SessionSecurityTokenCacheService()  
        {  
            internalCache = new IdentityModelCaches().SessionSecurityTokenCache;  
        }  
  
        ...  
  
        public SessionSecurityToken Get(string endpointId, string contextId, string keyGeneration)  
        {  
            // Delegates to the default, in-memory MruSessionSecurityTokenCache used by WIF  
            SessionSecurityToken token = internalCache.Get(new SessionSecurityTokenCacheKey(endpointId, GetContextId(contextId), GetKeyGeneration(keyGeneration)));  
            return token;  
        }  
  
        ...  
  
        private static UniqueId GetContextId(string contextIdString)  
        {  
            return contextIdString == null ? null : new UniqueId(contextIdString);  
        }  
  
        private static UniqueId GetKeyGeneration(string keyGenerationString)  
        {  
            return keyGenerationString == null ? null : new UniqueId(keyGenerationString);  
        }  
    }  
}  
```  
  
<a name="BKMK_TheWCFClient"></a>   
## La memorizzazione nella cache Client WCF  
 In questa sezione viene illustrata l'implementazione di una classe che deriva da <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> e che delega le chiamate al servizio di memorizzazione nella cache.  Si configura l'applicazione RP per utilizzare questa classe mediante il [\<sessionSecurityTokenCache\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/sessionsecuritytokencache.md) elemento come nel seguente XML  
  
```  
<caches>  
  <sessionSecurityTokenCache type="CacheLibrary.SharedSessionSecurityTokenCache, CacheLibrary">  
    <!--cacheServiceAddress points to the centralized session security token cache service running in the web farm.-->  
    <cacheServiceAddress url="http://localhost:4161/SessionSecurityTokenCacheService.svc" />  
  </sessionSecurityTokenCache>  
</caches>  
```  
  
 L'override della classe la <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache.LoadCustomConfiguration%2A> metodo per ottenere l'endpoint del servizio da personalizzati `<cacheServiceAddress>` elemento figlio dell'elemento di `<sessionSecurityTokenCache>` elemento.  L'endpoint viene utilizzato per inizializzare un `ISessionSecurityTokenCacheService` canale su cui può comunicare con il servizio.  In questo esempio, non tutti i metodi necessari per implementare la <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> classe vengono visualizzati per ragioni di brevità.  
  
```  
using System;  
using System.Configuration;  
using System.IdentityModel.Configuration;  
using System.IdentityModel.Tokens;  
using System.ServiceModel;  
using System.Xml;  
  
namespace CacheLibrary  
{  
    /// <summary>  
    /// This class acts as a proxy to the WcfSessionSecurityTokenCacheService.  
    /// </summary>  
    public class SharedSessionSecurityTokenCache : SessionSecurityTokenCache, ICustomIdentityConfiguration  
    {  
        private ISessionSecurityTokenCacheService WcfSessionSecurityTokenCacheServiceClient;  
  
        internal SharedSessionSecurityTokenCache()  
        {  
        }  
  
        /// <summary>  
        /// Creates a client channel to call the service host.  
        /// </summary>  
        protected void Initialize(string cacheServiceAddress)  
        {  
            if (this.WcfSessionSecurityTokenCacheServiceClient != null)  
            {  
                return;  
            }  
  
            ChannelFactory<ISessionSecurityTokenCacheService> cf = new ChannelFactory<ISessionSecurityTokenCacheService>(  
                new WS2007HttpBinding(SecurityMode.None),  
                new EndpointAddress(cacheServiceAddress));  
            this.WcfSessionSecurityTokenCacheServiceClient = cf.CreateChannel();  
        }  
  
        #region SessionSecurityTokenCache Members  
        // Delegates the following operations to the centralized session security token cache service in the web farm.  
  
        ...  
  
        public override SessionSecurityToken Get(SessionSecurityTokenCacheKey key)  
        {  
            return this.WcfSessionSecurityTokenCacheServiceClient.Get(key.EndpointId, GetContextIdString(key), GetKeyGenerationString(key));  
        }  
  
        ...  
  
        #endregion  
  
        #region ICustomIdentityConfiguration Members  
        // Called from configuration infrastructure to load custom elements  
        public void LoadCustomConfiguration(XmlNodeList nodeList)  
        {  
            // Retrieve the endpoint address of the centralized session security token cache service running in the web farm  
            if (nodeList.Count == 0)  
            {  
                throw new ConfigurationException("No child config element found under <sessionSecurityTokenCache>.");  
            }  
  
            XmlElement cacheServiceAddressElement = nodeList.Item(0) as XmlElement;  
            if (cacheServiceAddressElement.LocalName != "cacheServiceAddress")  
            {  
                throw new ConfigurationException("First child config element under <sessionSecurityTokenCache> is expected to be <cacheServiceAddress>.");  
            }  
  
            string cacheServiceAddress = null;  
            if (cacheServiceAddressElement.Attributes["url"] != null)  
            {  
                cacheServiceAddress = cacheServiceAddressElement.Attributes["url"].Value;  
            }  
            else  
            {  
                throw new ConfigurationException("<cacheServiceAddress> is expected to contain a 'url' attribute.");  
            }  
  
            // Initialize the proxy to the WebFarmSessionSecurityTokenCacheService  
            this.Initialize(cacheServiceAddress);  
        }  
        #endregion  
  
        private static string GetKeyGenerationString(SessionSecurityTokenCacheKey key)  
        {  
            return key.KeyGeneration == null ? null : key.KeyGeneration.ToString();  
        }  
  
        private static string GetContextIdString(SessionSecurityTokenCacheKey key)  
        {  
            return GetContextIdString(key.ContextId);  
        }  
  
        private static string GetContextIdString(UniqueId contextId)  
        {  
            return contextId == null ? null : contextId.ToString();  
        }  
    }  
}  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache>   
 <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>   
 <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler>   
 [Gestione delle sessioni WIF](../../../docs/framework/security/wif-session-management.md)