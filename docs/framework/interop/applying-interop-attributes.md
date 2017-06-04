---
title: "Applying Interop Attributes | Microsoft Docs"
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
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "design-time attributes"
  - ".NET Framework, exposing components to COM"
  - "attributes [.NET Framework], design-time functionality"
  - "conversion-tool attributes"
  - "attributes [.NET Framework], interop-specific"
  - "attributes [.NET Framework], conversion-tool"
  - "interoperation with unmanaged code, applying attributes"
  - "interoperation with unmanaged code, exposing .NET Framework components"
  - "COM interop, exposing COM components"
  - "COM interop, applying attributes"
ms.assetid: b6014613-641c-4912-9e2f-83a99210a037
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Applying Interop Attributes
Lo spazio dei nomi <xref:System.Runtime.InteropServices> fornisce tre categorie di attributi specifici dell'interoperabilità: quelli da applicare manualmente in fase di progettazione, quelli che vengono applicati dalle API e dagli strumenti dell'interoperabilità COM durante il processo di conversione e quelli che vengono applicati nell'uno o nell'altro modo.  
  
 Per informazioni su come utilizzare gli attributi nel codice gestito, vedere [Estensione di metadati mediante attributi](../../../docs/standard/attributes/index.md).  Come per altri attributi personalizzati, è possibile applicare gli attributi specifici dell'interoperabilità a tipi, metodi, proprietà, parametri e altri membri.  
  
## Attributi della fase di progettazione  
 L'utilizzo di attributi della fase di progettazione consente di intervenire sul risultato del processo di conversione eseguito dalle API e dagli strumenti di interoperabilità COM.  Nella tabella che segue vengono descritti gli attributi che possono essere applicati al codice sorgente gestito.  Anche gli strumenti di interoperabilità COM possono in alcuni casi applicare gli attributi descritti di seguito.  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|<xref:System.Runtime.InteropServices.AutomationProxyAttribute>|Specifica se il marshalling del tipo deve essere eseguito utilizzando il gestore di marshalling di automazione oppure un proxy e uno stub personalizzati.|  
|<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>|Controlla il tipo di interfaccia generato per una classe.|  
|<xref:System.Runtime.InteropServices.CoClassAttribute>|Identifica il CLSID della coclasse originale importata da una libreria dei tipi.<br /><br /> Questo attributo viene in genere applicato dagli strumenti di interoperabilità COM.|  
|<xref:System.Runtime.InteropServices.ComImportAttribute>|Indica che una coclasse o una definizione di interfaccia è stata importata da una libreria dei tipi COM.  Il runtime utilizza questo flag per determinare come attivare il tipo e effettuarne il marshalling.  Questo attributo impedisce la riesportazione del tipo in una libreria dei tipi.<br /><br /> Questo attributo viene in genere applicato dagli strumenti di interoperabilità COM.|  
|<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute>|Indica che quando l'assembly viene registrato per l'utilizzo da COM deve essere chiamato un metodo specificato, in modo che possa essere eseguito codice utente durante il processo di registrazione.|  
|<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>|Identifica le interfacce che sono fonti di eventi per la classe.<br /><br /> Gli strumenti di interoperabilità COM possono applicare questo attributo.|  
|<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute>|Indica che quando la registrazione dell'assembly presso COM viene annullata deve essere chiamato un metodo specificato, in modo che possa essere eseguito codice utente durante il processo.|  
|<xref:System.Runtime.InteropServices.ComVisibleAttribute>|Rende i tipi invisibili a COM quando il valore dell'attributo è uguale a **false**.  Questo attributo può essere applicato a un tipo singolo o a un intero assembly per controllare la visibilità COM.  Tutti i tipi gestiti e pubblici sono visibili per impostazione predefinita. Non occorre utilizzare questo attributo per renderli visibili.|  
|<xref:System.Runtime.InteropServices.DispIdAttribute>|Specifica il DISPID COM di un metodo o di un campo.  Questo attributo contiene il DISPID per il metodo, per il campo o per la proprietà che descrive.<br /><br /> Gli strumenti di interoperabilità COM possono applicare questo attributo.|  
|<xref:System.Runtime.InteropServices.FieldOffsetAttribute>|Indica la posizione fisica di ciascun campo all'interno di una classe quando è utilizzato con l'attributo **StructLayoutAttribute** e **LayoutKind** è impostato su Explicit.|  
|<xref:System.Runtime.InteropServices.GuidAttribute>|Specifica l'identificatore univoco globale \(GUID, Globally Unique Identifier\) di una classe, un'interfaccia o un'intera libreria dei tipi.  La stringa di formato passata all'attributo deve costituire un argomento valido per il costruttore del tipo **System.Guid**.<br /><br /> Gli strumenti di interoperabilità COM possono applicare questo attributo.|  
|[IDispatchImpAttribute](frlrfsystemruntimeinteropservicesidispatchimplattributeclasstopic)|Indica quale implementazione dell'interfaccia **IDispatch** utilizza Common Language Runtime quando espone a COM interfacce duali e interfacce dispatch.|  
|<xref:System.Runtime.InteropServices.InAttribute>|Indica che è necessario effettuare il marshalling dei dati verso il chiamante.  Può essere utilizzato per i parametri.|  
|<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>|Controlla come una interfaccia gestita è esposta ai client COM \(Dual, derivata da IUnknown o soltanto IDispatch\).<br /><br /> Gli strumenti di interoperabilità COM possono applicare questo attributo.|  
|<xref:System.Runtime.InteropServices.LCIDConversionAttribute>|Indica che una firma del metodo non gestito accetta un parametro LCID.<br /><br /> Gli strumenti di interoperabilità COM possono applicare questo attributo.|  
|<xref:System.Runtime.InteropServices.MarshalAsAttribute>|Indica come deve essere effettuato il marshalling dei dati di campi o parametri tra codice gestito e codice non gestito.  Questo attributo è sempre facoltativo perché per ciascun tipo di dati è previsto un comportamento di marshalling predefinito.<br /><br /> Gli strumenti di interoperabilità COM possono applicare questo attributo.|  
|<xref:System.Runtime.InteropServices.OptionalAttribute>|Indica che un parametro è facoltativo.<br /><br /> Gli strumenti di interoperabilità COM possono applicare questo attributo.|  
|<xref:System.Runtime.InteropServices.OutAttribute>|Indica che è necessario effettuare il marshalling dei dati di un campo o parametro restituito da un oggetto chiamato al relativo chiamante.|  
|<xref:System.Runtime.InteropServices.PreserveSigAttribute>|Disattiva la trasformazione della firma retval o HRESULT che normalmente ha luogo durante le chiamate di interoperabilità.  L'attributo influisce sul marshalling, come pure sull'esportazione delle librerie dei tipi.<br /><br /> Gli strumenti di interoperabilità COM possono applicare questo attributo.|  
|<xref:System.Runtime.InteropServices.ProgIdAttribute>|Specifica il ProgID di una classe .NET Framework.  Può essere utilizzato per le classi.|  
|<xref:System.Runtime.InteropServices.StructLayoutAttribute>|Controlla il layout fisico dei campi di una classe.<br /><br /> Gli strumenti di interoperabilità COM possono applicare questo attributo.|  
  
## Attributi di strumenti di conversione  
 Nella tabella che segue vengono descritti gli attributi applicati dagli strumenti di interoperabilità COM durante il processo di conversione.  Questi attributi non vanno applicati in fase di progettazione.  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|<xref:System.Runtime.InteropServices.ComAliasNameAttribute>|Indica gli alias COM di un tipo campo o parametro.  Può essere utilizzato per parametri, campi o valori restituiti.|  
|<xref:System.Runtime.InteropServices.ComConversionLossAttribute>|Indica che informazioni relative a una classe o a un'interfaccia sono andate perdute durante l'importazione da una libreria dei tipi a un assembly.|  
|<xref:System.Runtime.InteropServices.ComEventInterfaceAttribute>|Identifica l'interfaccia di origine e la classe che implementa i metodi dell'interfaccia eventi.|  
|<xref:System.Runtime.InteropServices.ImportedFromTypeLibAttribute>|Indica che l'assembly è stato importato in origine da una libreria dei tipi COM.  Questo attributo contiene la definizione della libreria dei tipi di origine.|  
|<xref:System.Runtime.InteropServices.TypeLibFuncAttribute>|Contiene i **FUNCFLAGS** importati all'origine per questa funzione dalla libreria dei tipi COM.|  
|<xref:System.Runtime.InteropServices.TypeLibTypeAttribute>|Contiene i **TYPEFLAGS** importati all'origine per questo tipo dalla libreria dei tipi COM.|  
|<xref:System.Runtime.InteropServices.TypeLibVarAttribute>|Contiene i **VARFLAGS** importati all'origine per questa variabile dalla libreria dei tipi COM.|  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices>   
 [Exposing .NET Framework Components to COM](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)   
 [Attributi](../../../docs/standard/attributes/index.md)   
 [Qualifying .NET Types for Interoperation](../../../docs/framework/interop/qualifying-net-types-for-interoperation.md)   
 [Packaging an Assembly for COM](../../../docs/framework/interop/packaging-an-assembly-for-com.md)