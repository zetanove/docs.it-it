# [Schema di configurazione di WCF](index.md)
## [<system.serviceModel>](system-servicemodel.md)
### [<comportamenti>](behaviors.md)
#### [<comportamentiEndpoint>](endpointbehaviors.md)
##### [<comportamento>](behavior-of-endpointbehaviors.md)
###### [<credenzialiClient>](clientcredentials.md)
####### [<certificatoClient>](clientcertificate-of-clientcredentials-element.md)
####### [<httpDigest>](httpdigest-element.md)
####### [<tokenEmesso>](issuedtoken.md)
######## [<issuerChannelBehaviors>](issuerchannelbehaviors-element.md)
######### [<aggiunta>](add-of-issuerchannelbehaviors.md)
######## [<emittenteLocale>](localissuer.md)
######### [<intestazioni>](headers-element.md)
####### [<peer>](peer-of-clientcredentials-element.md)
######## [<certificato>](certificate-element.md)
######## [<autenticazioneMittenteMessaggio>](messagesenderauthentication-element.md)
######## [<autenticazionePeer>](peerauthentication-element.md)
####### [<certificatoServizio>](servicecertificate-of-clientcredentials-element.md)
######## [<autenticazione>](authentication-of-servicecertificate-element.md)
######## [<certificatoPredefinito>](defaultcertificate-element.md)
######## [<certificatiConAmbito>](scopedcertificates-element.md)
######### [<aggiunta>](add-of-scopedcertificates-element.md)
####### [<finestre>](windows-of-clientcredentials-element.md)
###### [<debugCallback>](callbackdebug.md)
###### [<timeoutCallback>](callbacktimeouts.md)
###### [<clientVia>](clientvia.md)
###### [<dataContractSerializer>](datacontractserializer.md)
###### [<dispatcherSynchronization>](dispatchersynchronization.md)
###### [<enableWebScript>](enablewebscript.md)
###### [<endpointDiscovery>](endpointdiscovery.md)
####### [<scopes>](scopes.md)
######## [<aggiunta>](add-of-scopes.md)
####### [<estensioni>](extensions.md)
###### [<soapProcessing>](soapprocessing.md)
###### [<ricezioneSincrona>](synchronousreceive-element.md)
###### [<batchTransazionale>](transactedbatching.md)
###### [<webHttp>](webhttp.md)
#### [<comportamentiServizio>](servicebehaviors.md)
##### [<comportamento>](behavior-of-servicebehaviors.md)
###### [<dataContractSerializer>](datacontractserializer-element.md)
###### [<providerPersistenza>](persistenceprovider.md)
###### [<routing>](routing-of-servicebehavior.md)
###### [<serviceAuthenticationManager>](serviceauthenticationmanager.md)
###### [<autorizzazioneServizio>](serviceauthorization-element.md)
####### [<authorizationPolicies>](authorizationpolicies.md)
######## [<aggiunta>](add-of-authorizationpolicies.md)
###### [<credenzialiServizio>](servicecredentials.md)
####### [<certificatoClient>](clientcertificate-of-servicecredentials.md)
######## [<authentication>](authentication-of-clientcertificate-element.md)
######## [<certificato>](certificate-of-clientcertificate-element.md)
####### [<autenticazioneTokenEmesso>](issuedtokenauthentication-of-servicecredentials.md)
######## [<allowedAudienceUris>](allowedaudienceuris.md)
######### [<aggiunta>](add-of-allowedaudienceuris.md)
######## [<certificatiNoti>](knowncertificates.md)
######### [<aggiunta>](add-of-knowncertificates.md)
####### [<peer>](peer-of-servicecredentials.md)
######## [<certificato>](certificate-of-peer.md)
######## [<autenticazioneMittenteMessaggio>](messagesenderauthentication.md)
######## [<autenticazionePeer>](peerauthentication.md)
####### [<certificatoServizio>](servicecertificate-of-servicecredentials.md)
####### [<autenticazioneConversazioneProtetta>](secureconversationauthentication-of-servicecredential.md)
####### [<autenticazioneNomeUtente>](usernameauthentication.md)
####### [<autenticazioneWindows>](windowsauthentication-of-servicecredentials.md)
###### [<debugServizio>](servicedebug.md)
###### [<serviceDiscovery>](servicediscovery.md)
###### [<serviceMetadata>](servicemetadata.md)
###### [<controlloSicurezzaServizio>](servicesecurityaudit.md)
###### [<limitazioneServizio>](servicethrottling.md)
###### [<serviceTimeouts>](servicetimeouts.md)
###### [<runtimeFlussoDiLavoro>](workflowruntime.md)
####### [<commonParameters>](commonparameters.md)
######## [<aggiunta>](add-of-commonparameters.md)
####### [<servizi>](services-of-workflowruntime.md)
######## [<aggiunta>](add-of-services.md)
###### [<useRequestHeadersForMetadataAddress>](userequestheadersformetadataaddress.md)
####### [<defaultPorts>](defaultports.md)
######## [<add> di <defaultPorts>](add-of-defaultports.md)
### [<associazioni>](bindings.md)
#### [<basicHttpBinding>](basichttpbinding.md)
##### [<sicurezza>](security-of-basichttpbinding.md)
###### [<messaggio>](message-of-basichttpbinding.md)
###### [<transport>](transport-of-basichttpbinding.md)
#### [<basicHttpContextBinding>](basichttpcontextbinding.md)
#### [<mexHttpBinding>](mexhttpbinding.md)
#### [<mexHttpsBinding>](mexhttpsbinding.md)
#### [<mexNamedPipeBinding>](mexnamedpipebinding.md)
#### [<mexTcpBinding>](mextcpbinding.md)
#### [<msmqIntegrationBinding></msmqIntegrationBinding>](msmqintegrationbinding.md)
##### [<sicurezza>](security-of-msmqintegrationbinding.md)
###### [<transport>](transport-of-msmqintegrationbinding.md)
#### [<netMsmqBinding>](netmsmqbinding.md)
##### [<sicurezza>](security-of-netmsmqbinding.md)
###### [<messaggio>](message-of-netmsmqbinding.md)
###### [<transport>](transport-of-netmsmqbinding.md)
#### [<netNamedPipeBinding>](netnamedpipebinding.md)
##### [<sicurezza>](security-of-netnamedpipebinding.md)
###### [<transport>](transport-of-netnamedpipebinding.md)
#### [<netPeerTcpBinding>](netpeertcpbinding.md)
##### [<resolver>](resolver.md)
###### [<personalizzati>](custom.md)
##### [<sicurezza>](security-of-netpeerbinding.md)
###### [<transport>](transport-of-netpeertcpbinding.md)
#### [<netTcpBinding>](nettcpbinding.md)
##### [<sicurezza>](security-of-nettcpbinding.md)
###### [<transport>](transport-of-nettcpbinding.md)
###### [<messaggio>](message-element-of-nettcpbinding.md)
#### [<netTcpContextBinding>](nettcpcontextbinding.md)
#### [<webHttpBinding>](webhttpbinding.md)
##### [<sicurezza>](security-of-webhttpbinding.md)
###### [<transport>](transport-of-webhttpbinding.md)
#### [<wsDualHttpBinding>](wsdualhttpbinding.md)
##### [<sicurezza>](security-of-wsdualhttpbinding.md)
###### [<messaggio>](message-of-wsdualhttpbinding.md)
#### [<wsFederationHttpBinding>](wsfederationhttpbinding.md)
##### [<sicurezza>](security-of-wsfederationhttpbinding.md)
###### [<message>](message-element-of-wsfederationhttpbinding.md)
####### [<requisitiTipoAttestazione>](claimtyperequirements-for-message.md)
######## [<aggiunta>](add-of-claimtyperequirements-element.md)
######## [<remove>](remove-of-claimtyperequirements-element.md)
######## [<clear>](clear-of-claimtyperequirements-element.md)
####### [<issuer>](issuer.md)
####### [<issuerMetadata>](issuermetadata.md)
####### [<parametriRichiestaToken>](tokenrequestparameters.md)
######## [<xmlElement>](xmlelement.md)
#### [<wsHttpBinding>](wshttpbinding.md)
##### [<sicurezza>](security-of-wshttpbinding.md)
###### [<messaggio>](message-of-wshttpbinding.md)
###### [<transport>](transport-of-wshttpbinding.md)
#### [<wsHttpContextBinding>](wshttpcontextbinding.md)
#### [<ws2007FederationHttpBinding>](ws2007federationhttpbinding.md)
##### [<sicurezza>](security-element-of-ws2007federationhttpbinding.md)
###### [<messaggio>](message-element-of-ws2007federationhttpbinding.md)
#### [<ws2007HttpBinding>](ws2007httpbinding.md)
##### [<sicurezza>](security-of-ws2007httpbinding.md)
###### [<messaggio>](message-of-ws2007httpbinding.md)
###### [<transport>](transport-of-ws2007httpbinding.md)
#### [<customBinding>](custombinding.md)
##### [< compositeDuplex >](compositeduplex.md)
##### [<discoveryClient>](discoveryclient.md)
##### [Codifica dei messaggi](message-encoding.md)
###### [<codificaMessaggiBinaria>](binarymessageencoding.md)
###### [<codificaMessaggiMtom>](mtommessageencoding.md)
###### [<codificaMessaggiTesto>](textmessageencoding.md)
###### [<webMessageEncoding>](webmessageencoding.md)
###### [<byteStreamMessageEncoding>](bytestreammessageencoding.md)
##### [<oneWay>](oneway.md)
###### [<impostazioniPoolCanali>](channelpoolsettings.md)
##### [<resolverPeerPnrp>](pnrppeerresolver.md)
##### [<uriInformativaPrivacy>](privacynoticeat.md)
##### [<sessioneAttendibile>](reliablesession.md)
##### [<sicurezza>](security-of-custombinding.md)
###### [<parametriTokenEmesso>](issuedtokenparameters.md)
####### [<parametriRichiestaAggiuntivi>](additionalrequestparameters-element.md)
####### [<requisitiTipoAttestazione>](claimtyperequirements-element.md)
######## [<aggiunta>](add-of-claimtyperequirements.md)
####### [<issuer>](issuer-of-issuedtokenparameters.md)
####### [<issuerMetadata>](issuermetadata-of-issuedtokenparameters.md)
###### [<impostazioniClientLocali>](localclientsettings-element.md)
###### [<impostazioniServizioLocali>](localservicesettings-element.md)
###### [<bootstrapConversazioneProtetta>](secureconversationbootstrap.md)
##### [<sslStreamSecurity>](sslstreamsecurity.md)
##### [<transactionFlow>](transactionflow.md)
##### [Trasporti](transports.md)
###### [<trasportoHttp>](httptransport.md)
###### [<trasportoHttps>](httpstransport.md)
###### [<integrazioneMsmq>](msmqintegration.md)
####### [<sicurezzaTrasportoMsmq>](msmqtransportsecurity.md)
###### [<trasportoMsmq>](msmqtransport.md)
###### [<trasportoNamedPipe>](namedpipetransport.md)
####### [<connectionPoolSettings> di <namedPipeTransport>](connectionpoolsettings.md)
###### [<trasportoPeer>](peertransport.md)
####### [<sicurezza>](security-of-peertransport.md)
######## [<transport>](transport-of-peertransport.md)
###### [<trasportoTcp>](tcptransport.md)
####### [<impostazioniPoolConnessioni>](connectionpoolsettings-of-tcptransport.md)
##### [<unrecognizedPolicyAssertion>](unrecognizedpolicyassertion.md)
##### [<useManagedPresentation>](usemanagedpresentation.md)
##### [<sicurezzaFlussoWindows>](windowsstreamsecurity.md)
#### [<netHttpBinding>](nethttpbinding.md)
##### [<sicurezza>](security-of-nethttpbinding.md)
###### [<messaggio>](message-of-nethttpbinding.md)
###### [<transport>](transport-of-nethttpbinding.md)
##### [<webSocketSettings>](websocketsettings.md)
#### [<netHttpsBinding>](nethttpsbinding.md)
#### [<udpBinding>](udpbinding.md)
### [<client>](client.md)
#### [<endpoint>](endpoint-of-client.md)
##### [<intestazioni>](headers.md)
##### [<identità>](identity.md)
###### [<certificato>](certificate-for-identity.md)
###### [<certificateReference>](certificatereference-for-identity.md)
###### [<dns>](dns.md)
###### [<rsa>](rsa.md)
###### [<servicePrincipalName>](serviceprincipalname.md)
###### [<nomeEntitàUtente>](userprincipalname.md)
#### [<metadati>](metadata.md)
##### [<wsdlImporters>](wsdlimporters.md)
###### [<wsdlImporter>](wsdlimporter.md)
##### [<policyImporters>](policyimporters.md)
###### [<policyImporter>](policyimporter.md)
### [<comContracts>](comcontracts.md)
#### [<contrattoCom>](comcontract.md)
##### [<exposedMethods>](exposedmethods.md)
###### [<exposedMethod>](exposedmethod.md)
##### [<persistableTypes>](persistabletypes.md)
###### [<persistableType>](persistabletype.md)
##### [<userDefinedTypes>](userdefinedtypes.md)
###### [<tipoDefinitoDaUtente>](userdefinedtype.md)
### [<comportamentiComuni>](commonbehaviors.md)
### [<diagnostica>](diagnostics.md)
#### [<endToEndTracing>](endtoendtracing.md)
#### [<messageLogging></messageLogging>](messagelogging.md)
##### [<filtri>](filters.md)
###### [<aggiunta>](add-of-filters.md)
### [<estensioni>](extensions-section.md)
#### [<behaviorExtensions>](behaviorextensions.md)
#### [<bindingElementExtensions>](bindingelementextensions.md)
#### [<bindingExtensions>](bindingextensions.md)
#### [<endpointExtensions>](endpointextensions.md)
### [<protocolMapping>](protocolmapping.md)
#### [<aggiunta>](add-of-protocolmapping.md)
### [<routing>](routing.md)
#### [<backupLists>](backuplists.md)
##### [<backupList>](backuplist.md)
###### [<aggiunta>](add-of-backuplist.md)
#### [<filtri>](filters-of-routing.md)
##### [<filtro>](filter.md)
#### [<filterTables>](filtertables.md)
##### [<filterTable>](filtertable.md)
###### [<entries>](entries.md)
####### [<aggiunta>](add-of-entries.md)
#### [<namespaceTable>](namespacetable.md)
##### [<add> di <namespaceTable>](add-of-namespacetable.md)
### [<serviceHostingEnvironment>](servicehostingenvironment.md)
#### [<FiltriPrefissoIndirizzoBase>](baseaddressprefixfilters.md)
##### [<aggiunta>](add-of-baseaddressprefixfilter.md)
#### [<serviceActivations>](serviceactivations.md)
##### [<aggiunta>](add-of-serviceactivations.md)
#### [<transportConfigurationTypes>](transportconfigurationtypes.md)
##### [<aggiunta>](add-of-transportconfigurationtype.md)
### [<servizi>](services.md)
#### [<service>](service.md)
##### [<host>](host.md)
###### [<indirizziDiBase>](baseaddresses.md)
####### [<aggiunta>](add-of-baseaddresses.md)
###### [<timeOuts>](timeouts.md)
##### [<endpoint>](endpoint-element.md)
### [<standardEndpoints>](standardendpoints.md)
#### [<announcementEndpoint>](announcementendpoint.md)
#### [<discoveryEndpoint>](discoveryendpoint.md)
#### [<dynamicEndpoint>](dynamicendpoint.md)
##### [<discoveryClientSettings>](discoveryclientsettings.md)
###### [<findCriteria>](findcriteria.md)
####### [<contractTypeNames>](contracttypenames.md)
######## [<aggiunta>](add-of-contracttypenames.md)
#### [<mexEndpoint>](mexendpoint.md)
#### [<udpAnnoucementEndpoint>](udpannoucementendpoint.md)
##### [<udpTransportSettings>](udptransportsettings-of-udpannouncementendpoint.md)
#### [<udpDiscoveryEndpoint>](udpdiscoveryendpoint.md)
##### [<udpTransportSettings>](udptransportsettings.md)
#### [<webHttpEndpoint>](webhttpendpoint.md)
#### [<webScriptEndpoint>](webscriptendpoint.md)
#### [<workflowControlEndpoint>](workflowcontrolendpoint.md)
### [<gestione>](tracking-of-wcf.md)
#### [<participants>](participants-of-wcf.md)
##### [<aggiunta>](add-of-wcf.md)
#### [<trackingProfile>](trackingprofile-of-wcf.md)
##### [<flusso di lavoro>](workflow-of-wcf.md)
###### [<activityScheduledQueries>](activityscheduledqueries-of-wcf.md)
####### [<activityScheduledQuery>](activityscheduledquery-of-wcf.md)
###### [<activityStateQueries>](activitystatequeries-of-wcf.md)
####### [<activityStateQuery>](activitystatequery-of-wcf.md)
###### [<bookmarkResumptionQueries>](bookmarkresumptionqueries-of-wcf.md)
####### [<bookmarkResumptionQuery>](bookmarkresumptionquery-of-wcf.md)
###### [<cancelRequestedQueries>](cancelrequestedqueries-of-wcf.md)
####### [<cancelRequestedQuery>](cancelrequestedquery-of-wcf.md)
###### [<customTrackingQueries>](customtrackingqueries-of-wcf.md)
####### [<customTrackingQuery>](customtrackingquery-of-wcf.md)
###### [<faultPropagationQueries>](faultpropagationqueries-of-wcf.md)
####### [<faultPropagationQuery>](faultpropagationquery-of-wcf.md)
###### [<workflowInstanceQueries>](workflowinstancequeries-of-wcf.md)
####### [<workflowInstanceQuery>](workflowinstancequery-of-wcf.md)
######## [<stati>](states-of-wcf-workflowinstancequery.md)
######### [<stato>](state-of-wcf-workflowinstancequery.md)
## [<system.serviceModel.activation>](system-servicemodel-activation.md)
### [<diagnostica>](diagnostics-for-activation.md)
### [<net.pipe>](net-pipe.md)
#### [<consentiAccount>](allowaccounts.md)
##### [<aggiunta>](add-of-allowaccounts.md)
### [<net.tcp>](net-tcp.md)
## [<system.runtime.serialization>](system-runtime-serialization.md)
### [<dataContractSerializer>](datacontractserializer-of-system-runtime-serialization.md)
#### [<declaredTypes>](declaredtypes.md)
##### [<aggiunta>](add-of-declaredtypes-element.md)
###### [<knownType>](knowntype.md)
####### [<parametro>](parameter.md)