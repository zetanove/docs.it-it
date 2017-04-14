---
title: "Supporto di configurazione e metadati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27c240cb-8cab-472c-87f8-c864f4978758
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Supporto di configurazione e metadati
In questo argomento viene illustrato come abilitare il supporto della configurazione e dei metadati per associazioni ed elementi di associazione.  
  
## Panoramica della configurazione e dei metadati  
 In questo argomento vengono illustrate le attività seguenti, corrispondenti agli elementi facoltativi 1, 2 e 4 nell'elenco delle attività [Sviluppo di canali](../../../../docs/framework/wcf/extending/developing-channels.md).  
  
-   Attivazione del supporto dei file di configurazione per un elemento di associazione.  
  
-   Attivazione del supporto dei file di configurazione per un'associazione.  
  
-   Esportazione di asserzioni di criteri e WSDL per un elemento di associazione.  
  
-   Identificazione di asserzioni di criteri e WSDL per inserire e configurare l'associazione o l'elemento di associazione.  
  
 Per informazioni sulla creazione di associazioni definite dall'utente e di elementi di associazione, vedere [Creazione di associazioni definite dall'utente](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md) e [Creazione di una classe BindingElement](../../../../docs/framework/wcf/extending/creating-a-bindingelement.md) rispettivamente.  
  
## Aggiunta del supporto di configurazione  
 Per abilitare il supporto del file di configurazione per un canale, è necessario implementare due sezioni di configurazione, <xref:System.ServiceModel.Configuration.BindingElementExtensionElement?displayProperty=fullName> che abilita il supporto della configurazione per gli elementi di associazione e <xref:System.ServiceModel.Configuration.StandardBindingElement?displayProperty=fullName> e <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602?displayProperty=fullName> che abilita il supporto della configurazione per le associazioni.  
  
 Un modo più semplice di attivazione consiste nell'utilizzare lo strumento di esempio [ConfigurationCodeGenerator](../../../../docs/framework/wcf/samples/configurationcodegenerator.md) per generare codice di configurazione per associazioni ed elementi di associazione.  
  
### Estensione BindingElementExtensionElement  
 Il codice di esempio seguente è stato preso dall'esempio [Trasporto UDP](../../../../docs/framework/wcf/samples/transport-udp.md).`UdpTransportElement` è un oggetto <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> che espone `UdpTransportBindingElement` al sistema di configurazione.Con alcuni override di base, nell'esempio vengono definiti il nome della sezione di configurazione, il tipo dell'elemento di associazione e come creare l'elemento di associazione.Gli utenti possono quindi registrare la sezione di estensione in un file di configurazione come segue.  
  
```  
<configuration>  
  <system.serviceModel>  
    <extensions>  
      <bindingElementExtensions>  
      <add name="udpTransport" type="Microsoft.ServiceModel.Samples.UdpTransportElement, UdpTransport />  
      </bindingElementExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 È possibile fare riferimento all'estensione da associazioni personalizzate per utilizzare UDP come trasporto.  
  
```  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <customBinding>  
       <binding configurationName="UdpCustomBinding">  
         <udpTransport/>  
       </binding>  
      </customBinding>  
    </bindings>  
  </system.serviceModel>  
</configuration>  
  
```  
  
### Aggiunta di configurazione per un'associazione.  
 La sezione `SampleProfileUdpBindingCollectionElement` è una classe <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602> che espone `SampleProfileUdpBinding` al sistema di configurazione.La maggior parte dell'implementazione viene delegata a `SampleProfileUdpBindingConfigurationElement` che deriva da <xref:System.ServiceModel.Configuration.StandardBindingElement>.`SampleProfileUdpBindingConfigurationElement` ha proprietà che corrispondono alle proprietà in `SampleProfileUdpBinding` e funzioni per eseguire il mapping dall'associazione `ConfigurationElement` .Infine, viene eseguito l'override del metodo `OnApplyConfiguration` in `SampleProfileUdpBinding`, come illustrato nell'esempio di codice seguente.  
  
```  
protected override void OnApplyConfiguration(string configurationName)  
{  
            if (binding == null)  
                throw new ArgumentNullException("binding");  
  
            if (binding.GetType() != typeof(SampleProfileUdpBinding))  
            {  
                throw new ArgumentException(string.Format(CultureInfo.CurrentCulture,  
                    "Invalid type for binding. Expected type: {0}. Type passed in: {1}.",  
                    typeof(SampleProfileUdpBinding).AssemblyQualifiedName,  
                    binding.GetType().AssemblyQualifiedName));  
            }  
            SampleProfileUdpBinding udpBinding = (SampleProfileUdpBinding)binding;  
  
            udpBinding.OrderedSession = this.OrderedSession;  
            udpBinding.ReliableSessionEnabled = this.ReliableSessionEnabled;  
            udpBinding.SessionInactivityTimeout = this.SessionInactivityTimeout;  
            if (this.ClientBaseAddress != null)  
                   udpBinding.ClientBaseAddress = ClientBaseAddress;  
}  
  
```  
  
 Per registrare questo gestore nel sistema di configurazione, aggiungere la sezione seguente al file di configurazione pertinente.  
  
```  
<configuration>  
  <configSections>  
     <sectionGroup name="system.serviceModel">  
         <sectionGroup name="bindings">  
                 <section name="sampleProfileUdpBinding" type="Microsoft.ServiceModel.Samples.SampleProfileUdpBindingCollectionElement, UdpTransport />  
         </sectionGroup>  
     </sectionGroup>  
  </configSections>  
</configuration>  
```  
  
 È possibile farvi riferimento dalla sezione di configurazione [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md).  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint configurationName="calculator"  
                address="soap.udp://localhost:8001/"   
                bindingConfiguration="CalculatorServer"  
                binding="sampleProfileUdpBinding"   
                contract= "Microsoft.ServiceModel.Samples.ICalculatorContract">  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
  
```  
  
## Aggiunta del supporto dei metadati per un elemento di associazione  
 Per essere integrato in un sistema di metadati, il canale deve supportare sia l'importazione che l'esportazione di un criterio.Ciò consente a strumenti quali [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) di generare client dell'elemento di associazione.  
  
### Aggiunta di supporto WSDL  
 L'elemento di associazione del trasporto in un'associazione è responsabile dell'esportazione e importazione delle informazioni di indirizzamento nei metadati.Quando si utilizza un'associazione SOAP, l'elemento di associazione del trasporto deve esportare anche un URI di trasporto corretto nei metadati.Il codice di esempio seguente è stato preso dall'esempio [Trasporto UDP](../../../../docs/framework/wcf/samples/transport-udp.md).  
  
#### Esportazione WSDL  
 Per esportare informazioni di indirizzamento, l'elemento `UdpTransportBindingElement` implementa l'interfaccia <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=fullName>.Il metodo <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A?displayProperty=fullName>aggiunge le informazioni di indirizzamento corrette alla porta WSDL.  
  
```  
if (context.WsdlPort != null)  
{  
    AddAddressToWsdlPort(context.WsdlPort, context.Endpoint.Address, encodingBindingElement.MessageVersion.Addressing);  
}  
```  
  
 L'implementazione di `UdpTransportBindingElement` del metodo <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A> esporta anche un URI di trasporto quando l'endpoint utilizza un'associazione SOAP:  
  
```  
WsdlNS.SoapBinding soapBinding = GetSoapBinding(context, exporter);  
if (soapBinding != null)  
{  
    soapBinding.Transport = UdpPolicyStrings.UdpNamespace;  
}  
```  
  
#### Importazione WSDL  
 Per estendere il sistema di importazione WSDL in modo da gestire l'importazione degli indirizzi, aggiungere la configurazione seguente al file di configurazione per Svcutil.exe, come illustrato nel file Svcutil.exe.config:  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <metadata>  
        <wsdlImporters>  
          <extension type=" Microsoft.ServiceModel.Samples.UdpBindingElementImporter, UdpTransport" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 Quando si esegue Svcutil.exe, esistono due opzioni per ottenere che Svcutil.exe carichi le estensioni di importazione WSDL:  
  
1.  Puntare Svcutil.exe al file di configurazione utilizzando \/SvcutilConfig:\<file\>.  
  
2.  Aggiungere la sezione di configurazione a Svcutil.exe.config nella stessa directory di Svcutil.exe.  
  
 Il tipo `UdpBindingElementImporter` implementa l'interfaccia <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=fullName>.Il metodo `ImportEndpoint` importa l'indirizzo dalla porta WSDL:  
  
```  
BindingElementCollection bindingElements = context.Endpoint.Binding.CreateBindingElements();  
TransportBindingElement transportBindingElement = bindingElements.Find<TransportBindingElement>();  
if (transportBindingElement is UdpTransportBindingElement)  
{  
    ImportAddress(context);  
}  
```  
  
### Aggiunta del supporto dei criteri  
 L'elemento di associazione personalizzato è in grado di esportare asserzioni di criteri nell'associazione WSDL affinché un endpoint del servizio esprima le funzionalità di quell'elemento di associazione.Il codice di esempio seguente è stato preso dall'esempio [Trasporto UDP](../../../../docs/framework/wcf/samples/transport-udp.md).  
  
#### Esportazione di criteri  
 Il tipo `UdpTransportBindingElement` implementa ``<xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=fullName> per aggiungere supporto ai criteri di esportazione.Di conseguenza, <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=fullName> include `UdpTransportBindingElement` nella generazione del criterio per qualsiasi associazione in cui è incluso.  
  
 In <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A?displayProperty=fullName>, aggiungere un'asserzione per UDP e un'altra asserzione se il canale è in modalità multicast.Ciò è dovuto al fatto che la modalità multicast influisce sul modo in cui viene costruito lo stack di comunicazione, pertanto deve essere coordinato tra entrambi i lati.  
  
```  
ICollection<XmlElement> bindingAssertions = context.GetBindingAssertions();  
XmlDocument xmlDocument = new XmlDocument();  
bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.TransportAssertion, UdpPolicyStrings.UdpNamespace));  
if (Multicast)  
{  
    bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.MulticastAssertion,     UdpPolicyStrings.UdpNamespace));  
}  
```  
  
 Dato che gli elementi di associazione di trasporto personalizzati sono responsabili della gestione dell'indirizzamento, l'implementazione di <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=fullName> in `UdpTransportBindingElement` deve gestire anche l'esportazione delle asserzioni di criteri di WS\-Addressing appropriate per indicare la versione di WS\-Addressing utilizzata.  
  
```  
AddWSAddressingAssertion(context, encodingBindingElement.MessageVersion.Addressing);  
```  
  
#### Importazione di criteri  
 Per estendere il sistema di importazione dei criteri, aggiungere la configurazione seguente al file di configurazione per Svcutil.exe, come illustrato nel file Svcutil.exe.config:  
  
```  
<configuration>  
  <system.serviceModel>  
    <client>  
      <metadata>  
        <policyImporters>  
          <extension type=" Microsoft.ServiceModel.Samples.UdpBindingElementImporter, UdpTransport" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 Implementare quindi <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=fullName> dalla classe registrata \(`UdpBindingElementImporter`\).In <xref:System.ServiceModel.Description.IPolicyImportExtension.ImportPolicy%2A?displayProperty=fullName>, esaminare le asserzioni nello spazio dei nomi appropriato ed elaborare quelle per generare il trasporto e controllare se è multicast.Rimuovere inoltre dall'elenco delle asserzioni di associazione quelle gestite dall'importatore.Anche in questo caso, quando si esegue Svcutil.exe esistono due opzioni per l'integrazione:  
  
1.  Puntare Svcutil.exe al file di configurazione utilizzando \/SvcutilConfig:\<file\>.  
  
2.  Aggiungere la sezione di configurazione a Svcutil.exe.config nella stessa directory di Svcutil.exe.  
  
### Aggiunta di un importatore di associazione standard personalizzato  
 Per impostazione predefinita, Svcutil.exe e il tipo <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName> riconoscono e importano associazioni fornite dal sistema.In caso contrario, l'associazione viene importata come istanza <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName>.Per consentire a Svcutil.exe e a <xref:System.ServiceModel.Description.WsdlImporter> di importare `SampleProfileUdpBinding`, `UdpBindingElementImporter` funge anche da importatore di associazione standard personalizzato.  
  
 Un importatore di associazione standard personalizzato implementa il metodo `ImportEndpoint` nell'interfaccia <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=fullName> per esaminare l'istanza <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName> importata dai metadati per controllare se poteva essere generata da un'associazione standard specifica.  
  
```  
if (context.Endpoint.Binding is CustomBinding)  
{  
    Binding binding;  
    if (transportBindingElement is UdpTransportBindingElement)  
    {  
        //if TryCreate is true, the CustomBinding will be replace by a SampleProfileUdpBinding in the  
        //generated config file for better typed generation.  
        if (SampleProfileUdpBinding.TryCreate(bindingElements, out binding))  
        {  
            binding.Name = context.Endpoint.Binding.Name;  
            binding.Namespace = context.Endpoint.Binding.Namespace;  
            context.Endpoint.Binding = binding;  
        }  
    }  
}  
```  
  
 In genere, l'implementazione di un importatore dell'associazione standard personalizzato implica il controllo delle proprietà degli elementi di associazione importati per verificare che siano cambiate solo le proprietà che avrebbero potuto essere impostate dall'associazione standard e che tutte le altre siano rimaste sulle impostazioni predefinite.Una strategia di base per l'implementazione di un importatore dell'associazione standard consiste nel creare un'istanza dell'associazione standard, propagare le proprietà dagli elementi di associazione all'istanza dell'associazione standard supportata dall'associazione standard e nel confrontare gli elementi di associazione dall'associazione standard con gli elementi di associazione importati.