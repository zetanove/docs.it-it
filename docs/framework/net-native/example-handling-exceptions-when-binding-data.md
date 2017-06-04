---
title: "Esempio: gestione delle eccezioni durante il data binding | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bd63ed96-9853-46dc-ade5-7bd1b0f39110
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Esempio: gestione delle eccezioni durante il data binding
> [!NOTE]
>  In questo argomento si fa riferimento a .NET Native Developer Preview, ovvero la versione preliminare del software,  che può essere scaricato dal [sito Web di Microsoft Connect](http://go.microsoft.com/fwlink/?LinkId=394611) \(è necessaria la registrazione\).  
  
 Nel seguente esempio viene illustrato come risolvere un'eccezione [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) generata quando un'app compilata con la catena di strumenti [!INCLUDE[net_native](../../../includes/net-native-md.md)] tenta di associare i dati.  Queste sono le informazioni sull'eccezione:  
  
```  
  
This operation cannot be carried out as metadata for the following type was removed for performance reasons:   
App.ViewModels.MainPageVM  
  
```  
  
 Questo è lo stack di chiamate associato:  
  
```  
  
Reflection::Execution::ReflectionDomainSetupImplementation.CreateNonInvokabilityException+0x238  
Reflection::Core::ReflectionDomain.CreateNonInvokabilityException+0x2e  
Reflection::Core::Execution::ExecutionEnvironment.+0x316  
System::Reflection::Runtime::PropertyInfos::RuntimePropertyInfo.GetValue+0x1cb  
System::Reflection::PropertyInfo.GetValue+0x22  
System::Runtime::InteropServices::WindowsRuntime::CustomPropertyImpl.GetValue+0x42  
App!$66_Interop::McgNative.Func_IInspectable_IInspectable+0x158  
App!$66_Interop::McgNative::__vtable_Windows_UI_Xaml_Data__ICustomProperty.GetValue__STUB+0x46  
Windows_UI_Xaml!DirectUI::PropertyProviderPropertyAccess::GetValue+0x3f   
Windows_UI_Xaml!DirectUI::PropertyAccessPathStep::GetValue+0x31   
Windows_UI_Xaml!DirectUI::PropertyPathListener::ConnectPathStep+0x113  
  
```  
  
## Che cosa stava eseguendo l'app?  
 Alla base dello stack, i frame dello spazio dei nomi [Windows.UI.Xaml](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.aspx) indicano che il motore di rendering XAML era in esecuzione.  L'uso del metodo <xref:System.Reflection.PropertyInfo.GetValue%2A?displayProperty=fullName> indica una ricerca basata su reflection del valore di una proprietà sul tipo di cui sono stati rimossi i metadati.  
  
 Il primo passaggio per la fornitura di una direttiva di metadati consiste nell'aggiunta di metadati `serialize` per il tipo che ne rende accessibili le proprietà:  
  
```  
<Type Name="App.ViewModels.MainPageVM" Serialize="Required Public" />  
```  
  
## Si tratta di un caso isolato?  
 In questo scenario, se il data binding contiene metadati incompleti per `ViewModel`, potrebbe contenerne anche per altri.  Se il codice è strutturato in modo che i modelli di visualizzazione dell'app siano tutti nello spazio dei nomi `App.ViewModels`, è possibile usare una direttiva di runtime più generale:  
  
```  
<Namespace Name="App.ViewModels " Serialize="Required Public" />  
```  
  
## Il codice può essere riscritto per escludere l'uso della reflection?  
 Il data binding ha un elevato livello di reflection, pertanto la modifica del codice per impedire la reflection non è consentita.  
  
 Tuttavia, sono disponibili dei metodi per specificare `ViewModel` nella pagina XAML in modo che la catena di strumenti possa associare le associazioni di proprietà al tipo corretto durante la compilazione e mantenere i metadati senza usare una direttiva di runtime.  Ad esempio, è possibile applicare l'attributo [Windows.UI.Xaml.Data.BindableAttribute](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.data.bindableattribute.aspx) sulle proprietà.  In questo modo il compilatore XAML genera le informazioni di ricerca necessarie ed evita la richiesta di una direttiva di runtime nel file Default.rd.xml.  
  
## Vedere anche  
 [Introduzione](../../../docs/framework/net-native/getting-started-with-net-native.md)   
 [Esempio: Risoluzione dei problemi di programmazione dinamica](../../../docs/framework/net-native/example-troubleshooting-dynamic-programming.md)