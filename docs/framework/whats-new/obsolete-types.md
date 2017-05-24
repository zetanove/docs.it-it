---
title: Tipi obsoleti in .NET Framework | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- .NET Framework 4.5, obsolete types
- types, obsolete in .NET Framework 4.5
- obsolete types [.NET Framework]
ms.assetid: e636d024-0fac-45eb-b721-25a8c0ceca8f
caps.latest.revision: 41
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 175e46e3729190423b85296d7c7c47b136339305
ms.contentlocale: it-it
ms.lasthandoff: 04/18/2017

---
# <a name="obsolete-types-in-the-net-framework"></a>Tipi obsoleti in .NET Framework
<a name="introduction"></a> Le tabelle in questo articolo elencano i tipi obsoleti in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] e [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], organizzati per assembly. Usare i seguenti collegamenti per vedere un elenco di tipi obsoleti e le alternative consigliate in ogni assembly. Poiché questi tipi sono obsoleti, lo sono anche tutti i relativi membri. Per un elenco di altri membri obsoleti nella libreria di classi .NET Framework, vedere [Membri obsoleti](../../../docs/framework/whats-new/obsolete-members.md).  
  
-   [Tipi obsoleti negli assembly di sistema](#obsolete_types_in_system_assemblies)  
  
    -   [mscorlib.dll](#mscorlib)  
  
    -   [System.Core.dll](#Core)  
  
    -   [System.Data.dll](#data)  
  
    -   [System.Data.OracleClient.dll](#oracleclient)  
  
    -   [System.Design.dll](#design)  
  
    -   [System.dll](#system)  
  
    -   [System.EnterpriseServices.dll](#enterpriseservices)  
  
    -   [System.Net.dll](#net)  
  
    -   [System.ServiceModel.dll](#servicemodel)  
  
    -   [System.Web.dll](#web)  
  
    -   [System.Web.Mobile.dll](#mobile)  
  
    -   [System.Workflow.Activities.dll](#workflow_activities)  
  
    -   [System.Workflow.ComponentModel.dll](#workflow_componentmodel)  
  
    -   [System.Workflow.Runtime.dll](#workflow_runtime)  
  
    -   [System.WorkflowServices.dll](#workflowservices)  
  
    -   [System.Xaml.dll](#xaml)  
  
    -   [System.Xml.dll](#xml)  
  
    -   [WindowsBase.dll](#WindowsBase)  
  
-   [Tipi obsoleti negli assembly Microsoft](#obsolete_types_in_microsoft_assemblies)  
  
    -   [IEHost.dll e IEExec.exe](#IEHost)  
  
    -   [Microsoft.Build.Engine.dll](#Engine)  
  
    -   [Microsoft.JScript.dll](#jscript)  
  
    -   [Microsoft.VisualBasic.Compatibility.dll](#VBCompat)  
  
    -   [Microsoft.VisualBasic.Compatibility.Data.dll](#VBCompatData)  
  
    -   [Microsoft.VisualC.dll](#visualc)  
  
<a name="obsolete_types_in_system_assemblies"></a>   
## <a name="obsolete-types-in-system-assemblies"></a>Tipi obsoleti negli assembly di sistema  
 Nelle seguenti tabelle sono elencati i tipi dichiarati obsoleti negli assembly di sistema. Questi assembly vengono usati per lo sviluppo di applicazioni generiche destinate a .NET Framework.  
  
<a name="mscorlib"></a>   
### <a name="assembly-mscorlibdll"></a>Assembly: mscorlib.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.ExecutionEngineException?displayProperty=fullName>|Questo tipo indicava in precedenza un errore di runtime irreversibile non specificato. Il runtime non genera più questa eccezione, pertanto il tipo è obsoleto.|  
|<xref:System.Collections.CaseInsensitiveHashCodeProvider?displayProperty=fullName>|Usare invece <xref:System.StringComparer?displayProperty=fullName>.|  
|<xref:System.Collections.IHashCodeProvider?displayProperty=fullName>|Usare invece <xref:System.Collections.IEqualityComparer?displayProperty=fullName>.|  
|<xref:System.Configuration.Assemblies.AssemblyHash?displayProperty=fullName>|La classe <xref:System.Configuration.Assemblies.AssemblyHash> è stata deprecata.|  
|<xref:System.Diagnostics.Contracts.Internal.ContractHelper?displayProperty=fullName>|Deprecata inizialmente in .NET Framework 4.5. Usare invece la classe <xref:System.Runtime.CompilerServices.ContractHelper?displayProperty=fullName> nello spazio dei nomi System.Runtime.CompilerServices.|  
|<xref:System.Reflection.Emit.UnmanagedMarshal?displayProperty=fullName>|È disponibile un'API alternativa: creare invece l'attributo personalizzato <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.BIND_OPTS?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.BIND_OPTS?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.BINDPTR?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.BINDPTR?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.CALLCONV?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.CALLCONV?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.CONNECTDATA?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.CONNECTDATA?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.DESCKIND?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.DESCKIND?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.DISPPARAMS?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.DISPPARAMS?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.ELEMDESC?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.ELEMDESC?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.EXCEPINFO?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.EXCEPINFO?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.FILETIME?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.FILETIME?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.FUNCDESC?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.FUNCDESC?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.FUNCFLAGS?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.FUNCFLAGS?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.FUNCKIND?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.FUNCKIND?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.IDispatchImplAttribute?displayProperty=fullName>|Questo attributo è stato deprecato e sarà rimosso nelle versioni future.|  
|<xref:System.Runtime.InteropServices.IDispatchImplType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.IDispatchImplAttribute?displayProperty=fullName> è stato deprecato.|  
|<xref:System.Runtime.InteropServices.IDLDESC?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IDLDESC?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.IDLFLAG?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IDLFLAG?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.IMPLTYPEFLAGS?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IMPLTYPEFLAGS?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.INVOKEKIND?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.INVOKEKIND?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.LIBFLAGS?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.LIBFLAGS?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.PARAMDESC?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.PARAMDESC?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.PARAMFLAG?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.PARAMFLAG?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.SetWin32ContextInIDispatchAttribute?displayProperty=fullName>|Questo attributo è stato deprecato. I domini applicazione non rispettano più i limiti del contesto di attivazione nelle chiamate a IDispatch.|  
|<xref:System.Runtime.InteropServices.STATSTG?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.STATSTG?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.SYSKIND?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.SYSKIND?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.TYPEATTR?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.TYPEATTR?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.TYPEDESC?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.TYPEDESC?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.TYPEFLAGS?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.TYPEFLAGS?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.TYPEKIND?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.TYPEKIND?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.TYPELIBATTR?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.TYPELIBATTR?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMIBindCtx?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IBindCtx?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMIConnectionPoint?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMIConnectionPointContainer?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMIEnumConnectionPoints?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IEnumConnectionPoints?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMIEnumConnections?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IEnumConnections?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMIEnumMoniker?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IEnumMoniker?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMIEnumString?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IEnumString?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMIEnumVARIANT?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMIMoniker?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IMoniker?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMIPersistFile?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IPersistFile?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMIRunningObjectTable?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IRunningObjectTable?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMIStream?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.IStream?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMITypeComp?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.ITypeComp?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMITypeInfo?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.UCOMITypeLib?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.ITypeLib?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.VARDESC?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.VARDESC?displayProperty=fullName>.|  
|<xref:System.Runtime.InteropServices.VARFLAGS?displayProperty=fullName>|Usare invece <xref:System.Runtime.InteropServices.ComTypes.VARFLAGS?displayProperty=fullName>.|  
|<xref:System.Security.SecurityCriticalScope?displayProperty=fullName>|<xref:System.Security.SecurityCriticalScope> viene usato solo per la compatibilità con la trasparenza di .NET 2.0.|  
|<xref:System.Security.SecurityTreatAsSafeAttribute?displayProperty=fullName>|<xref:System.Security.SecurityTreatAsSafeAttribute> viene usato solo per la compatibilità con la trasparenza di .NET 2.0. Usare invece <xref:System.Security.SecuritySafeCriticalAttribute?displayProperty=fullName>.|  
|<xref:System.Security.Policy.FirstMatchCodeGroup?displayProperty=fullName>|Questo tipo è obsoleto e sarà rimosso nelle versioni future di .NET Framework.|  
|<xref:System.Security.Policy.PermissionRequestEvidence?displayProperty=fullName>|La sicurezza dichiarativa a livello di assembly è obsoleta e non viene più applicata da CLR per impostazione predefinita.|  
|<xref:System.Security.Policy.UnionCodeGroup?displayProperty=fullName>|Questo tipo è obsoleto e sarà rimosso nelle versioni future di .NET Framework.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="Core"></a>   
### <a name="assembly-systemcoredll"></a>Assembly: System.Core.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.Runtime.CompilerServices.ExecutionScope?displayProperty=fullName>|L'utilizzo di questo tipo genera un errore del compilatore.<br /><br /> Non usare questo tipo.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="data"></a>   
### <a name="assembly-systemdatadll"></a>Assembly: System.Data.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.Data.DataSysDescriptionAttribute?displayProperty=fullName>|<xref:System.Data.DataSysDescriptionAttribute> è stato deprecato.|  
|<xref:System.Data.PropertyAttributes?displayProperty=fullName>|<xref:System.Data.PropertyAttributes> è stato deprecato.|  
|<xref:System.Data.TypedDataSetGenerator?displayProperty=fullName>|La classe <xref:System.Data.TypedDataSetGenerator> verrà rimossa in una delle prossime versioni. Usare <xref:System.Data.Design.TypedDataSetGenerator?displayProperty=fullName> in System.Design.dll.|  
|<xref:System.Xml.XmlDataDocument?displayProperty=fullName>|La classe <xref:System.Xml.XmlDataDocument> verrà rimossa in una delle prossime versioni.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="oracleclient"></a>   
### <a name="assembly-systemdataoracleclientdll"></a>Assembly: System.Data.OracleClient.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.Data.OracleClient.OracleClientFactory?displayProperty=fullName>|<xref:System.Data.OracleClient.OracleClientFactory> è stato deprecato.|  
|<xref:System.Data.OracleClient.OracleCommand?displayProperty=fullName>|<xref:System.Data.OracleClient.OracleCommand> è stato deprecato.|  
|<xref:System.Data.OracleClient.OracleCommandBuilder?displayProperty=fullName>|<xref:System.Data.OracleClient.OracleCommandBuilder> è stato deprecato.|  
|<xref:System.Data.OracleClient.OracleConnection?displayProperty=fullName>|<xref:System.Data.OracleClient.OracleConnection> è stato deprecato.|  
|<xref:System.Data.OracleClient.OracleConnectionStringBuilder?displayProperty=fullName>|<xref:System.Data.OracleClient.OracleConnectionStringBuilder> è stato deprecato.|  
|<xref:System.Data.OracleClient.OracleDataAdapter?displayProperty=fullName>|<xref:System.Data.OracleClient.OracleDataAdapter> è stato deprecato.|  
|<xref:System.Data.OracleClient.OraclePermission?displayProperty=fullName>|<xref:System.Data.OracleClient.OraclePermission> è stato deprecato.|  
|<xref:System.Data.OracleClient.OraclePermissionAttribute?displayProperty=fullName>|<xref:System.Data.OracleClient.OraclePermissionAttribute?displayProperty=fullName> è stato deprecato.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="design"></a>   
### <a name="assembly-systemdesigndll"></a>Assembly: System.Design.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.ComponentModel.Design.LocalizationExtenderProvider?displayProperty=fullName>|Questa classe è stata deprecata. Usare invece <xref:System.ComponentModel.Design.Serialization.CodeDomLocalizationProvider?displayProperty=fullName>.|  
|<xref:System.Web.UI.Design.DataBindingCollectionConverter?displayProperty=fullName>|L'uso di questo tipo non è consigliato perché la modifica di DataBindings viene avviata tramite un oggetto <xref:System.ComponentModel.Design.DesignerActionList?displayProperty=fullName> invece che tramite la griglia delle proprietà.|  
|<xref:System.Web.UI.Design.DataBindingCollectionEditor?displayProperty=fullName>|L'uso di questo tipo non è consigliato perché la modifica di DataBindings viene avviata tramite un oggetto <xref:System.ComponentModel.Design.DesignerActionList?displayProperty=fullName> invece che tramite la griglia delle proprietà.|  
|<xref:System.Web.UI.Design.IControlDesignerBehavior?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Web.UI.Design.IControlDesignerTag?displayProperty=fullName> o <xref:System.Web.UI.Design.IControlDesignerView?displayProperty=fullName>.|  
|<xref:System.Web.UI.Design.IHtmlControlDesignerBehavior?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Web.UI.Design.IControlDesignerTag?displayProperty=fullName> o <xref:System.Web.UI.Design.IControlDesignerView?displayProperty=fullName>.|  
|<xref:System.Web.UI.Design.ITemplateEditingFrame?displayProperty=fullName>|L'uso di questo tipo non è consigliato perché la modifica dei modelli viene gestita in <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName>. Per supportare la modifica dei modelli, esporre i dati del modello nella proprietà <xref:System.Web.UI.Design.ControlDesigner.TemplateGroups%2A?displayProperty=fullName> e chiamare <xref:System.Web.UI.Design.ControlDesigner.SetViewFlags%2A?displayProperty=fullName>.|  
|<xref:System.Web.UI.Design.IWebFormReferenceManager?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Web.UI.Design.WebFormsReferenceManager?displayProperty=fullName>. <xref:System.Web.UI.Design.WebFormsReferenceManager> contiene funzionalità aggiuntive e permette una maggiore estensibilità. Per ottenere <xref:System.Web.UI.Design.WebFormsReferenceManager>, usare la proprietà `RootDesigner.ReferenceManager` da <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName>.|  
|<xref:System.Web.UI.Design.IWebFormsDocumentService?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Web.UI.Design.WebFormsRootDesigner?displayProperty=fullName>. <xref:System.Web.UI.Design.WebFormsRootDesigner> contiene funzionalità aggiuntive e permette una maggiore estensibilità. Per ottenere <xref:System.Web.UI.Design.WebFormsRootDesigner>, usare la proprietà <xref:System.Web.UI.Design.ControlDesigner.RootDesigner%2A> da <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName>.|  
|<xref:System.Web.UI.Design.ITemplateEditingService?displayProperty=fullName>|L'uso di questo tipo non è consigliato perché la modifica dei modelli viene gestita in <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName>. Per supportare la modifica dei modelli, esporre i dati del modello nella proprietà <xref:System.Web.UI.Design.ControlDesigner.TemplateGroups%2A?displayProperty=fullName> e chiamare <xref:System.Web.UI.Design.ControlDesigner.SetViewFlags%2A?displayProperty=fullName>.|  
|<xref:System.Web.UI.Design.ReadWriteControlDesigner?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Web.UI.Design.ContainerControlDesigner?displayProperty=fullName>, perché usa un oggetto <xref:System.Web.UI.Design.EditableDesignerRegion?displayProperty=fullName> per modificare il contenuto. Le aree della finestra di progettazione consentono un migliore controllo del contenuto da modificare.|  
|<xref:System.Web.UI.Design.TemplateEditingService?displayProperty=fullName>|L'uso di questo tipo non è consigliato perché la modifica dei modelli viene gestita in <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName>. Per supportare la modifica dei modelli, esporre i dati del modello nella proprietà <xref:System.Web.UI.Design.ControlDesigner.TemplateGroups%2A?displayProperty=fullName> e chiamare <xref:System.Web.UI.Design.ControlDesigner.SetViewFlags%2A?displayProperty=fullName>.|  
|<xref:System.Web.UI.Design.TemplateEditingVerb?displayProperty=fullName>|L'uso di questo tipo non è consigliato perché la modifica dei modelli viene gestita in <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName>. Per supportare la modifica dei modelli, esporre i dati del modello nella proprietà <xref:System.Web.UI.Design.ControlDesigner.TemplateGroups%2A?displayProperty=fullName> e chiamare <xref:System.Web.UI.Design.ControlDesigner.SetViewFlags%2A?displayProperty=fullName>.|  
|<xref:System.Web.UI.Design.WebControls.CalendarAutoFormatDialog?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto la finestra di dialogo Formattazione automatica viene avviata dall'host della finestra di progettazione. L'elenco dei formati automatici disponibili viene esposto in <xref:System.Web.UI.Design.ControlDesigner?displayProperty=fullName> nella proprietà <xref:System.Web.UI.Design.ControlDesigner.AutoFormats%2A?displayProperty=fullName>.|  
|<xref:System.Web.UI.Design.WebControls.PanelDesigner?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Web.UI.Design.WebControls.PanelContainerDesigner?displayProperty=fullName>, perché usa un oggetto <xref:System.Web.UI.Design.EditableDesignerRegion?displayProperty=fullName> per modificare il contenuto. Le aree della finestra di progettazione consentono un migliore controllo del contenuto da modificare.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="system"></a>   
### <a name="assembly-systemdll"></a>Assembly: System.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.ComponentModel.IComNativeDescriptorHandler?displayProperty=fullName>|Questa interfaccia è stata deprecata. Aggiungere invece un oggetto <xref:System.ComponentModel.TypeDescriptionProvider?displayProperty=fullName> per gestire <xref:System.ComponentModel.TypeDescriptor.ComObjectType%2A?displayProperty=fullName> del tipo.|  
|<xref:System.ComponentModel.RecommendedAsConfigurableAttribute?displayProperty=fullName>|Usare invece <xref:System.ComponentModel.SettingsBindableAttribute?displayProperty=fullName> invece del nuovo modello di impostazioni.|  
|<xref:System.ComponentModel.Design.Serialization.RootDesignerSerializerAttribute?displayProperty=fullName>|Questo attributo è stato deprecato. Usare invece <xref:System.ComponentModel.Design.Serialization.DesignerSerializerAttribute?displayProperty=fullName>. Per specificare ad esempio una finestra di progettazione radice per CodeDom, usare `DesignerSerializerAttribute\(...,typeof\(TypeCodeDomSerializer\)\)`.|  
|<xref:System.Diagnostics.DiagnosticsConfigurationHandler?displayProperty=fullName>|Questa classe è stata deprecata.|  
|<xref:System.Diagnostics.PerformanceCounterManager?displayProperty=fullName>|Questa classe è stata deprecata. Usare invece i contatori delle prestazioni tramite la classe <xref:System.Diagnostics.PerformanceCounter?displayProperty=fullName>.|  
|<xref:System.Net.GlobalProxySelection?displayProperty=fullName>|Questa classe è stata deprecata. Usare invece <xref:System.Net.WebRequest.DefaultWebProxy%2A?displayProperty=fullName> per accedere al proxy globale predefinito e impostarlo. Usare "null" invece di <xref:System.Net.GlobalProxySelection.GetEmptyWebProxy%2A?displayProperty=fullName>.|  
|<xref:System.Net.Sockets.SocketClientAccessPolicyProtocol?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> L'utilizzo di questo tipo genera un errore del compilatore.<br /><br /> Questa API supporta l'infrastruttura .NET Framework e non deve essere usata direttamente dal codice.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="enterpriseservices"></a>   
### <a name="assembly-systementerpriseservicesdll"></a>Assembly: System.EnterpriseServices.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.EnterpriseServices.RegistrationHelperTx?displayProperty=fullName>|La classe <xref:System.EnterpriseServices.RegistrationHelperTx> è stata deprecata.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="net"></a>   
### <a name="assembly-systemnetdll"></a>Assembly: System.Net.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.Net.INetworkProgress?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> L'utilizzo di questo tipo genera un errore del compilatore.<br /><br /> Questa API supporta l'infrastruttura .NET Framework e non deve essere usata direttamente dal codice.|  
|<xref:System.Net.IUnsafeWebRequestCreate?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> L'utilizzo di questo tipo genera un errore del compilatore.<br /><br /> Questa API supporta l'infrastruttura .NET Framework e non deve essere usata direttamente dal codice.|  
|<xref:System.Net.NetworkProgressChangedEventArgs?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> L'utilizzo di questo tipo genera un errore del compilatore.<br /><br /> Questa API supporta l'infrastruttura .NET Framework e non deve essere usata direttamente dal codice.|  
|<xref:System.Net.UiSynchronizationContext?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> L'utilizzo di questo tipo genera un errore del compilatore.<br /><br /> Questa API supporta l'infrastruttura .NET Framework e non deve essere usata direttamente dal codice.|  
|<xref:System.Net.Sockets.HttpPolicyDownloaderProtocol?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> L'utilizzo di questo tipo genera un errore del compilatore.<br /><br /> Questa API supporta l'infrastruttura .NET Framework e non deve essere usata direttamente dal codice.|  
|<xref:System.Net.Sockets.SecurityCriticalAction?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> L'utilizzo di questo tipo genera un errore del compilatore.<br /><br /> Questa API supporta l'infrastruttura .NET Framework e non deve essere usata direttamente dal codice.|  
|<xref:System.Net.Sockets.SocketPolicy?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> L'utilizzo di questo tipo genera un errore del compilatore.<br /><br /> Questa API supporta l'infrastruttura .NET Framework e non deve essere usata direttamente dal codice.|  
|<xref:System.Net.Sockets.UdpAnySourceMulticastClient?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> L'utilizzo di questo tipo genera un errore del compilatore.<br /><br /> Questa API supporta l'infrastruttura .NET Framework e non deve essere usata direttamente dal codice.|  
|<xref:System.Net.Sockets.UdpSingleSourceMulticastClient?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> L'utilizzo di questo tipo genera un errore del compilatore.<br /><br /> Questa API supporta l'infrastruttura .NET Framework e non deve essere usata direttamente dal codice.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="servicemodel"></a>   
### <a name="assembly-systemservicemodeldll"></a>Assembly: System.ServiceModel.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.ServiceModel.NetPeerTcpBinding?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> La funzionalità del canale peer è obsoleta e verrà rimossa in futuro.|  
|<xref:System.ServiceModel.Channels.HttpCookieContainerBindingElement?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> Questo tipo è obsoleto. Per abilitare <xref:System.Net.CookieContainer> HTTP, usare la proprietà `AllowCookies` nell'associazione HTTP o in <xref:System.ServiceModel.Channels.HttpTransportBindingElement>.|  
|<xref:System.ServiceModel.Channels.PeerCustomResolverBindingElement?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> La funzionalità del canale peer è obsoleta e verrà rimossa in futuro.|  
|<xref:System.ServiceModel.Channels.PeerTransportBindingElement?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> La funzionalità del canale peer è obsoleta e verrà rimossa in futuro.|  
|<xref:System.ServiceModel.Configuration.NetPeerTcpBindingCollectionElement?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> La funzionalità del canale peer è obsoleta e verrà rimossa in futuro.|  
|<xref:System.ServiceModel.Configuration.NetPeerTcpBindingElement?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> La funzionalità del canale peer è obsoleta e verrà rimossa in futuro.|  
|<xref:System.ServiceModel.Configuration.PeerTransportElement?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> La funzionalità del canale peer è obsoleta e verrà rimossa in futuro.|  
|<xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> La funzionalità del canale peer è obsoleta e verrà rimossa in futuro.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="web"></a>   
### <a name="assembly-systemwebdll"></a>Assembly: System.Web.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.Web.Configuration.PassportAuthentication?displayProperty=fullName>|Questo tipo è obsoleto. Il prodotto di autenticazione Passport non è più supportato ed è stato sostituito dall'[account Microsoft](http://go.microsoft.com/fwlink/?LinkId=733413)|  
|<xref:System.Web.Mail.MailAttachment?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Net.Mail.Attachment?displayProperty=fullName>.|  
|<xref:System.Web.Mail.MailEncoding?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Net.Mime.TransferEncoding?displayProperty=fullName>.|  
|<xref:System.Web.Mail.MailFormat?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Net.Mail.MailMessage.IsBodyHtml%2A?displayProperty=fullName>.|  
|<xref:System.Web.Mail.MailMessage?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Net.Mail.MailMessage?displayProperty=fullName>.|  
|<xref:System.Web.Mail.MailPriority?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Net.Mail.MailPriority?displayProperty=fullName>.|  
|<xref:System.Web.Mail.SmtpMail?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Net.Mail.SmtpClient?displayProperty=fullName>.|  
|<xref:System.Web.Security.PassportAuthenticationEventArgs?displayProperty=fullName>|Questo tipo è obsoleto. Il prodotto di autenticazione Passport non è più supportato ed è stato sostituito dall'[account Microsoft](http://go.microsoft.com/fwlink/?LinkId=733413)|  
|<xref:System.Web.Security.PassportAuthenticationEventHandler?displayProperty=fullName>|Questo tipo è obsoleto. Il prodotto di autenticazione Passport non è più supportato ed è stato sostituito dall'[account Microsoft](http://go.microsoft.com/fwlink/?LinkId=733413)|  
|<xref:System.Web.Security.PassportAuthenticationModule?displayProperty=fullName>|Questo tipo è obsoleto. Il prodotto di autenticazione Passport non è più supportato ed è stato sostituito dall'[account Microsoft](http://go.microsoft.com/fwlink/?LinkId=733413)|  
|<xref:System.Web.Security.PassportIdentity?displayProperty=fullName>|Questo tipo è obsoleto. Il prodotto di autenticazione Passport non è più supportato ed è stato sostituito dall'[account Microsoft](http://go.microsoft.com/fwlink/?LinkId=733413)|  
|<xref:System.Web.Security.PassportPrincipal?displayProperty=fullName>|Questo tipo è obsoleto. Il prodotto di autenticazione Passport non è più supportato ed è stato sostituito dall'[account Microsoft](http://go.microsoft.com/fwlink/?LinkId=733413)|  
|<xref:System.Web.UI.ObjectConverter?displayProperty=fullName>|L'alternativa consigliata è <xref:System.Convert?displayProperty=fullName> o <xref:System.String.Format%2A?displayProperty=fullName>.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="mobile"></a>   
### <a name="assembly-systemwebmobiledll"></a>Assembly: System.Web.Mobile.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.Web.Mobile.CookielessData?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.Mobile.DeviceFilterElement?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.Mobile.DeviceFilterElementCollection?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.Mobile.DeviceFiltersSection?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.Mobile.ErrorHandlerModule?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.Mobile.MobileCapabilities?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.Mobile.MobileDeviceCapabilitiesSectionHandler?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.Mobile.MobileErrorInfo?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.Mobile.MobileFormsAuthentication?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.Design.MobileControls.IMobileDesigner?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.Design.MobileControls.IMobileWebFormServices?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.Design.MobileControls.MobileResource?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.Design.MobileControls.Converters.DataFieldConverter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.Design.MobileControls.Converters.DataMemberConverter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.AdRotator?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Alignment?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ArrayListCollectionBase?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.BaseValidator?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.BooleanOption?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Calendar?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Command?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.CommandFormat?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.CompareValidator?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Constants?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ControlElement?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ControlElementCollection?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ControlPager?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.CustomValidator?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.DesignerAdapterAttribute?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.DeviceElement?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.DeviceElementCollection?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.DeviceOverridableAttribute?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.DeviceSpecific?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoice?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoiceCollection?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoiceControlBuilder?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoiceTemplateBuilder?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.DeviceSpecificChoiceTemplateContainer?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.DeviceSpecificControlBuilder?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ErrorFormatterPage?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.FontInfo?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.FontSize?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Form?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.FormControlBuilder?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.FormMethod?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.IControlAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Image?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.IObjectListFieldCollection?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.IPageAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ItemPager?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ITemplateable?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Label?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Link?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.List?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ListCommandEventArgs?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ListCommandEventHandler?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ListControlBuilder?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ListDataBindEventArgs?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ListDataBindEventHandler?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ListDecoration?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ListSelectType?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.LiteralLink?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.LiteralText?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.LiteralTextContainerControlBuilder?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.LiteralTextControlBuilder?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.LoadItemsEventArgs?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.LoadItemsEventHandler?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.MobileControl?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.MobileControlBuilder?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.MobileControlsSection?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.MobileControlsSectionHandler?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.MobileListItem?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.MobileListItemCollection?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.MobileListItemType?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.MobilePage?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.MobileTypeNameConverter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.MobileUserControl?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectList?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListCommand?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListCommandCollection?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListCommandEventArgs?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListCommandEventHandler?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListControlBuilder?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListDataBindEventArgs?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListDataBindEventHandler?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListField?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListFieldCollection?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListItem?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListItemCollection?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListSelectEventArgs?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListSelectEventHandler?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListShowCommandsEventArgs?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListShowCommandsEventHandler?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListTitleAttribute?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ObjectListViewMode?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.PagedControl?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.PagerStyle?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Panel?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.PanelControlBuilder?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.PersistNameAttribute?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.PhoneCall?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.RangeValidator?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.RegularExpressionValidator?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.RequiredFieldValidator?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.SelectionList?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Style?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.StyleSheet?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.StyleSheetControlBuilder?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.TemplateContainer?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.TextBox?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.TextBoxControlBuilder?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.TextControl?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.TextView?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.TextViewElement?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.ValidationSummary?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Wrapping?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlCalendarAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlCommandAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlFormAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlImageAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlLinkAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlMobileTextWriter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlPageAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlPhoneCallAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlSelectionListAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.ChtmlTextBoxAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.ControlAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlCalendarAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlCommandAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlControlAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlFormAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlImageAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlLabelAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlLinkAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlListAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlLiteralTextAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlMobileTextWriter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlObjectListAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlPageAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlPanelAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlPhoneCallAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlSelectionListAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlTextBoxAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlTextViewAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlValidationSummaryAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.HtmlValidatorAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.MobileTextWriter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.MultiPartWriter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.UpWmlMobileTextWriter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.UpWmlPageAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlCalendarAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlCommandAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlControlAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlFormAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlImageAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlLabelAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlLinkAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlListAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlLiteralTextAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlMobileTextWriter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlObjectListAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlPageAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlPanelAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlPhoneCallAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlPostFieldType?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlSelectionListAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlTextBoxAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlTextViewAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlValidationSummaryAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.WmlValidatorAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.Doctype?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.StyleSheetLocation?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlCalendarAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlCommandAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlControlAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlCssHandler?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlFormAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlImageAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlLabelAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlLinkAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlListAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlLiteralTextAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlMobileTextWriter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlObjectListAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlPageAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlPanelAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlPhoneCallAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlSelectionListAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlTextBoxAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlTextViewAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlValidationSummaryAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
|<xref:System.Web.UI.MobileControls.Adapters.XhtmlAdapters.XhtmlValidatorAdapter?displayProperty=fullName>|L'assembly System.Web.Mobile.dll è stato deprecato e non deve più essere usato. Per informazioni su come sviluppare applicazioni ASP.NET per dispositivi mobili, vedere la pagina su [ASP.NET per dispositivi mobili](http://go.microsoft.com/fwlink/?LinkId=157231).|  
  
 [Torna all'inizio](#introduction)  
  
<a name="workflow_activities"></a>   
### <a name="assembly-systemworkflowactivitiesdll"></a>Assembly: System.Workflow.Activities.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|Tutti i tipi nello spazio dei nomi <xref:System.Workflow.Activities?displayProperty=fullName>|Deprecati inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|<xref:System.Workflow.Activities.Configuration.ActiveDirectoryRoleFactoryConfiguration?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|<xref:System.Workflow.Activities.Rules.RuleActionTrackingEvent?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|<xref:System.Workflow.Activities.Rules.RuleConditionReference?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|<xref:System.Workflow.Activities.Rules.RuleSetReference?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="workflow_componentmodel"></a>   
### <a name="assembly-systemworkflowcomponentmodeldll"></a>Assembly: System.Workflow.ComponentModel.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|Tutti i tipi nello spazio dei nomi <xref:System.Workflow.ComponentModel> ad eccezione di <xref:System.Workflow.ComponentModel.GetValueOverride?displayProperty=fullName> e <xref:System.Workflow.ComponentModel.SetValueOverride?displayProperty=fullName>|Deprecati inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|Tutti i tipi nello spazio dei nomi <xref:System.Workflow.ComponentModel.Compiler> ad eccezione di <xref:System.Workflow.ComponentModel.Compiler.ValidationError?displayProperty=fullName> e <xref:System.Workflow.ComponentModel.Compiler.ValidationErrorCollection?displayProperty=fullName>|Deprecati inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|Tutti i tipi nello spazio dei nomi <xref:System.Workflow.ComponentModel.Design> ad eccezione di <xref:System.Workflow.ComponentModel.Design.ConnectorEventHandler>|Deprecati inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|<xref:System.Workflow.ComponentModel.Serialization.ActivityCodeDomSerializationManager?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|<xref:System.Workflow.ComponentModel.Serialization.ActivityCodeDomSerializer?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|<xref:System.Workflow.ComponentModel.Serialization.ActivityMarkupSerializer?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|<xref:System.Workflow.ComponentModel.Serialization.ActivitySurrogateSelector?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|<xref:System.Workflow.ComponentModel.Serialization.ActivityTypeCodeDomSerializer?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|<xref:System.Workflow.ComponentModel.Serialization.CompositeActivityMarkupSerializer?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|<xref:System.Workflow.ComponentModel.Serialization.DependencyObjectCodeDomSerializer?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="workflow_runtime"></a>   
### <a name="assembly-systemworkflowruntimedll"></a>Assembly: System.Workflow.Runtime.dll  
  
|Tipo|Messaggio|  
|----------|-------------| 
|System.Activities.Statements.Interop](assetId:///T:System.Activities.Statements.Interop)|Deprecato inizialmente in .NET Framework 4.5.<br /><br />I tipi di Workflow Foundation 3.0 sono stati deprecati. Usare invece i tipi di Workflow 4.0 da <xref:System.Activities>.\*.|  
|<xref:System.Activities.Tracking.InteropTrackingRecord>|Deprecato inizialmente in .NET Framework 4.5.<br /><br />I tipi di Workflow Foundation 3.0 sono stati deprecati. Usare invece i tipi di Workflow 4.0 da <xref:System.Activities>.\*.|   
|Tutti i tipi nello spazio dei nomi <xref:System.Workflow.Runtime>|Deprecati inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|Tutti i tipi nello spazio dei nomi <xref:System.Workflow.Runtime.Configuration>|Deprecati inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|Tutti i tipi nello spazio dei nomi <xref:System.Workflow.Runtime.DebugEngine> ad eccezione di <xref:System.Workflow.Runtime.DebugEngine.DebugEngineCallback>|Deprecati inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|Tutti i tipi nello spazio dei nomi <xref:System.Workflow.Runtime.Hosting> ad eccezione di <xref:System.Workflow.Runtime.Hosting.WorkflowCommitWorkBatchService.CommitWorkBatchCallback>|Deprecati inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
|Tutti i tipi nello spazio dei nomi <xref:System.Workflow.Runtime.Tracking>|Deprecati inizialmente in .NET Framework 4.5.<br /><br /> I tipi System.Workflow.\* sono stati deprecati. Usare invece i nuovi tipi da <xref:System.Activities>.\*.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="workflowservices"></a>   
### <a name="assembly-systemworkflowservicesdll"></a>Assembly: System.WorkflowServices.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.ServiceModel.WorkflowServiceHost?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Activation.WorkflowServiceHostFactory?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Activities.Description.WorkflowRuntimeEndpoint?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Configuration.ExtendedWorkflowRuntimeServiceElementCollection?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Configuration.PersistenceProviderElement?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Configuration.WorkflowRuntimeElement?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Description.DurableOperationAttribute?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Description.DurableServiceAttribute?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Description.PersistenceProviderBehavior?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Description.UnknownExceptionAction?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Description.WorkflowRuntimeBehavior?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Dispatcher.DurableOperationContext?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Persistence.InstanceLockException?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Persistence.InstanceNotFoundException?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Persistence.LockingPersistenceProvider?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Persistence.PersistenceException?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Persistence.PersistenceProvider?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Persistence.PersistenceProviderFactory?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.ServiceModel.Persistence.SqlPersistenceProviderFactory?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|Tutti i tipi nello spazio dei nomi <xref:System.Workflow.Activities?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
|<xref:System.Workflow.Runtime.Hosting.ChannelManagerService?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> I tipi di WF 3 sono deprecati. Usare invece i nuovi tipi di WF 4 da <xref:System.Activities>.\*.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="xaml"></a>   
### <a name="assembly-systemxamldll"></a>Assembly: System.Xaml.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.Windows.Markup.AcceptedMarkupExtensionExpressionTypeAttribute?displayProperty=fullName>|Non viene usato dal parser XAML. Vedere <xref:System.Windows.Markup.XamlSetMarkupExtensionAttribute?displayProperty=fullName>.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="xml"></a>   
### <a name="assembly-systemxmldll"></a>Assembly: System.Xml.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.Xml.IApplicationResourceStreamResolver?displayProperty=fullName>|Deprecato inizialmente in .NET Framework 4.5.<br /><br /> L'utilizzo di questo tipo genera un errore del compilatore.<br /><br /> Questa API supporta l'infrastruttura .NET Framework e non deve essere usata direttamente dal codice.|  
|<xref:System.Xml.Schema.XmlSchemaCollection?displayProperty=fullName>|Usare <xref:System.Xml.Schema.XmlSchemaSet?displayProperty=fullName> per la compilazione e la convalida dello schema.|  
|<xref:System.Xml.XmlValidatingReader?displayProperty=fullName>|Usare invece un oggetto <xref:System.Xml.XmlReader?displayProperty=fullName> creato dal metodo <xref:System.Xml.XmlReader.Create%2A?displayProperty=fullName> tramite l'oggetto <xref:System.Xml.XmlReaderSettings?displayProperty=fullName> appropriato.|  
|<xref:System.Xml.XmlXapResolver?displayProperty=fullName>|L'utilizzo di questo tipo genera un errore del compilatore. Questa API supporta l'infrastruttura .NET Framework e non deve essere usata direttamente dal codice.|  
|<xref:System.Xml.Xsl.XslTransform?displayProperty=fullName>|Questa classe è stata deprecata. Usare invece <xref:System.Xml.Xsl.XslCompiledTransform?displayProperty=fullName>.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="WindowsBase"></a>   
### <a name="assembly-windowsbasedll"></a>Assembly: WindowsBase.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:System.Windows.Markup.IReceiveMarkupExtension?displayProperty=fullName>|<xref:System.Windows.Markup.IReceiveMarkupExtension?displayProperty=fullName> è stato deprecato. Questa interfaccia non è più usata.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="obsolete_types_in_microsoft_assemblies"></a>   
## <a name="obsolete-types-in-microsoft-assemblies"></a>Tipi obsoleti negli assembly Microsoft  
 Nelle seguenti sezioni sono elencati i tipi obsoleti contenuti negli assembly Microsoft. Questi ultimi sono assembly speciali, ad esempio assembly destinati a un unico linguaggio (es. Microsoft.JScript.dll o Microsoft.VisualC.dll).  
  
<a name="IEHost"></a>   
### <a name="assembly-iehostdll-and-ieexecexe"></a>Assembly: IEHost.dll e IEExec.exe  
 Gli assembly IEHost.dll e IEExec.dll sono stati rimossi da .NET Framework. Tutti i loro tipi e i membri sono obsoleti e non sono supportati da [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]. Questi assembly sono usati per eseguire l'hosting dei controlli Windows Form ed eseguire i file eseguibili in Internet Explorer. Le alternative consigliate includono ClickOnce, le applicazioni browser XAML (XBAP) e Microsoft Silverlight.  
  
 [Torna all'inizio](#introduction)  
  
<a name="Engine"></a>   
### <a name="assembly-microsoftbuildenginedll"></a>Assembly: Microsoft.Build.Engine.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:Microsoft.Build.BuildEngine.Engine?displayProperty=fullName>|Questa classe è stata deprecata. Usare invece <xref:Microsoft.Build.Evaluation.ProjectCollection?displayProperty=fullName> dall'assembly <!--zz <xref:Microsoft.Build?displayProperty=fullName> --> Microsoft.Build.|  
|<xref:Microsoft.Build.BuildEngine.Project?displayProperty=fullName>|Questa classe è stata deprecata. Usare invece <xref:Microsoft.Build.Evaluation.ProjectCollection?displayProperty=fullName> dall'assembly <xref:Microsoft.Build?displayProperty=fullName>.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="jscript"></a>   
### <a name="assembly-microsoftjscriptdll"></a>Assembly: Microsoft.JScript.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:Microsoft.JScript.Vsa.BaseVsaEngine?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.BaseVsaSite?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.BaseVsaStartup?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.IJSVsaCodeItem?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.IJSVsaEngine?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.IJSVsaError?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.IJSVsaGlobalItem?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.IJSVsaItem?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.IJSVsaItems?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.IJSVsaPersistSite?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.IJSVsaReferenceItem?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.IJSVsaSite?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.JSVsaError?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.JSVsaException?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.JSVsaItemFlag?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.JSVsaItemType?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.ResInfo?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
|<xref:Microsoft.JScript.Vsa.VsaEngine?displayProperty=fullName>|Non è consigliabile usare questo tipo in quanto deprecato in Visual Studio 2005; la funzionalità non sarà sostituita. Per altre informazioni, vedere la documentazione di <xref:System.CodeDom.Compiler.ICodeCompiler?displayProperty=fullName>.|  
  
 [Torna all'inizio](#introduction)  
  
<a name="VBCompat"></a>   
### <a name="assembly-microsoftvisualbasiccompatibilitydll"></a>Assembly: Microsoft.VisualBasic.Compatibility.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.BaseControlArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.BaseOcxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ButtonArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.CheckBoxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.CheckedListBoxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ColorDialogArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ComboBoxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DirListBox?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DirListBoxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DriveListBox?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DriveListBoxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FileListBox?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FileListBoxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FixedLengthString?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FontDialogArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.FormShowConstants?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.GroupBoxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.HScrollBarArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ImageListArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.LabelArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ListBoxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ListBoxItem?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ListViewArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.LoadResConstants?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MaskedTextBoxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MenuItemArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MouseButtonConstants?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.OpenFileDialogArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.PanelArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.PictureBoxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.PrintDialogArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ProgressBarArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.RadioButtonArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.RichTextBoxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.SaveFileDialogArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ScaleMode?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ShiftConstants?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.StatusBarArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.StatusStripArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.Support?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.TabControlArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.TextBoxArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.TimerArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ToolBarArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ToolStripArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ToolStripMenuItemArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.TreeViewArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.VScrollBarArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebBrowserArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClass?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassContainingClassNotOptional?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassCouldNotFindEvent?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassNextItemCannotBeCurrentWebItem?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassNextItemRespondNotFound?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassUserWebClassNameNotOptional?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassWebClassFileNameNotOptional?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebClassWebItemNotValid?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItem?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemAssociatedWebClassNotOptional?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemClosingTagNotFound?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemCouldNotLoadEmbeddedResource?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemCouldNotLoadTemplateFile?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemNameNotOptional?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemNoTemplateSpecified?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemTooManyNestedTags?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.WebItemUnexpectedErrorReadingTemplateFile?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ZOrderConstants?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
  
 [Torna all'inizio](#introduction)  
  
<a name="VBCompatData"></a>   
### <a name="assembly-microsoftvisualbasiccompatibilitydatadll"></a>Assembly: Microsoft.VisualBasic.Compatibility.Data.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.BOFActionEnum?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.EndOfRecordsetDelegate?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.EOFActionEnum?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.ErrorDelegate?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.FetchCompleteDelegate?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.FetchProgressDelegate?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.FieldChangeCompleteDelegate?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.MoveCompleteDelegate?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.OrientationEnum?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.RecordChangeCompleteDelegate?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.RecordsetChangeCompleteDelegate?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.WillChangeFieldDelegate?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.WillChangeRecordDelegate?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.WillChangeRecordsetDelegate?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODC.WillMoveDelegate?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.ADODCArray?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.BaseDataEnvironment?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.BindingCollectionEnumerator?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.CONNECTDATA?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBBINDING?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBCOLUMNINFO?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBID?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBinding?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBindingCollection?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBKINDENUM?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.DBPROPIDSET?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IAccessor?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IChapteredRowset?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IColumnsInfo?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IConnectionPoint?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IConnectionPointContainer?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IDataFormat?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IDataFormatDisp?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IEnumConnectionPoints?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IEnumConnections?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowPosition?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowPositionChange?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowset?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowsetChange?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowsetIdentity?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowsetInfo?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.IRowsetNotify?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MBinding?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.MBindingCollection?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.SRDescriptionAttribute?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.UGUID?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.UNAME?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
|<xref:Microsoft.VisualBasic.Compatibility.VB6.UpdateMode?displayProperty=fullName>|Vedere [Microsoft.VisualBasic.Compatibility.VB6.\<membro> è obsoleto e supportato solo all'interno di processi a 32 bit](https://msdn.microsoft.com/library/ee839621.aspx).|  
  
 [Torna all'inizio](#introduction)  
  
<a name="visualc"></a>   
### <a name="assembly-microsoftvisualcdll"></a>Assembly: Microsoft.VisualC.dll  
  
|Tipo|Messaggio|  
|----------|-------------|  
|<xref:Microsoft.VisualC.DebugInfoInPDBAttribute?displayProperty=fullName>|Microsoft.VisualC.dll è un assembly obsoleto e viene mantenuto ai soli fini della compatibilità con le versioni precedenti.|  
|<xref:Microsoft.VisualC.DecoratedNameAttribute?displayProperty=fullName>|Microsoft.VisualC.dll è un assembly obsoleto e viene mantenuto ai soli fini della compatibilità con le versioni precedenti.|  
|<xref:Microsoft.VisualC.IsConstModifier?displayProperty=fullName>|Microsoft.VisualC.dll è un assembly obsoleto e viene mantenuto ai soli fini della compatibilità con le versioni precedenti.|  
|<xref:Microsoft.VisualC.IsCXXReferenceModifier?displayProperty=fullName>|Microsoft.VisualC.dll è un assembly obsoleto e viene mantenuto ai soli fini della compatibilità con le versioni precedenti.|  
|<xref:Microsoft.VisualC.IsLongModifier?displayProperty=fullName>|Microsoft.VisualC.dll è un assembly obsoleto e viene mantenuto ai soli fini della compatibilità con le versioni precedenti.|  
|<xref:Microsoft.VisualC.IsSignedModifier?displayProperty=fullName>|Microsoft.VisualC.dll è un assembly obsoleto e viene mantenuto ai soli fini della compatibilità con le versioni precedenti.|  
|<xref:Microsoft.VisualC.IsVolatileModifier?displayProperty=fullName>|Microsoft.VisualC.dll è un assembly obsoleto e viene mantenuto ai soli fini della compatibilità con le versioni precedenti.|  
|<xref:Microsoft.VisualC.MiscellaneousBitsAttribute?displayProperty=fullName>|Microsoft.VisualC.dll è un assembly obsoleto e viene mantenuto ai soli fini della compatibilità con le versioni precedenti.|  
|<xref:Microsoft.VisualC.NeedsCopyConstructorModifier?displayProperty=fullName>|Microsoft.VisualC.dll è un assembly obsoleto e viene mantenuto ai soli fini della compatibilità con le versioni precedenti.|  
|<xref:Microsoft.VisualC.NoSignSpecifiedModifier?displayProperty=fullName>|Microsoft.VisualC.dll è un assembly obsoleto e viene mantenuto ai soli fini della compatibilità con le versioni precedenti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Elementi obsoleti nella libreria di classi](../../../docs/framework/whats-new/whats-obsolete.md)   
 [Membri obsoleti](../../../docs/framework/whats-new/obsolete-members.md)
