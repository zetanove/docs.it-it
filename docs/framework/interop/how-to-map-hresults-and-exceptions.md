---
title: "How to: Map HRESULTs and Exceptions | Microsoft Docs"
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
  - "interoperation with unmanaged code, HRESULTs"
  - "exceptions, HRESULTs"
  - "interoperation with unmanaged code, exceptions"
  - "HRESULTs"
  - "COM interop, HRESULTs"
  - "COM interop, exceptions"
ms.assetid: 610b364b-2761-429d-9c4a-afbc3e66f1b9
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Map HRESULTs and Exceptions
Per segnalare il verificarsi di un errore, i metodi COM restituiscono un HRESULT. I metodi .NET, invece, generano un'eccezione.  Il runtime gestisce la transizione tra i due.  Ogni classe che identifica un'eccezione in .NET Framework è associata a un HRESULT.  
  
 Le classi di eccezione definite dall'utente possono specificare un HRESULT appropriato.  Impostando il campo **HResult** dell'oggetto di eccezione, tali classi di eccezione possono modificare dinamicamente l'HRESULT che deve essere restituito quando viene generata l'eccezione.  Informazioni aggiuntive sull'eccezione vengono fornite al client tramite l'interfaccia **IErrorInfo**, che è implementata dall'oggetto .NET nel processo non gestito.  
  
 Se si crea una classe che estende **System.Exception**, sarà necessario impostare il campo HRESULT durante la costruzione.  In caso contrario, sarà la classe base a assegnare il valore di HRESULT.  È possibile associare nuove classi di eccezione a un HRESULT esistente fornendo il valore nel costruttore dell'eccezione.  
  
 Si noti che talvolta un `HRESULT` può essere ignorato dal runtime quando è presente un'interfaccia `IErrorInfo` sul thread.  Questo comportamento può verificarsi nei casi in cui l'`HRESULT` e l'interfaccia `IErrorInfo` non rappresentano lo stesso errore.   ``  
  
### Per creare una nuova classe di eccezione e mapparla a un HRESULT  
  
1.  Utilizzare il codice seguente per creare una nuova classe di eccezione denominata `NoAccessException` e mapparla al HRESULT `E_ACCESSDENIED`.  
  
    ```cpp  
    Class NoAccessException : public ApplicationException  
    {  
        NoAccessException () {  
        HResult = E_ACCESSDENIED;   
    }  
    }  
    CMyClass::MethodThatThrows  
    {  
    throw new NoAccessException();  
    }  
    ```  
  
 È possibile imbattersi in un programma \(in qualsiasi linguaggio di programmazione\) che utilizza contemporaneamente codice gestito e codice non gestito.  Il gestore di marshalling personalizzato illustrato nel codice che segue utilizza ad esempio il metodo **Marshal.ThrowExceptionForHR\(int HResult\)** per generare un'eccezione con uno specifico valore di HRESULT.  Il metodo esamina l'HRESULT e genera il tipo di eccezione appropriato.  L'HRESULT del frammento di codice riportato di seguito genera ad esempio **ArgumentException**.  
  
```cpp  
CMyClass::MethodThatThrows  
{  
    Marshal.ThrowExceptionForHR(COR_E_ARGUMENT);  
}  
```  
  
 Nella tabella che segue viene fornita la mappa completa delle associazioni tra ciascun HRESULT e la classe di eccezione di .NET Framework ad esso paragonabile.  
  
|HRESULT|Eccezione .NET|  
|-------------|--------------------|  
|**MSEE\_E\_APPDOMAINUNLOADED**|**AppDomainUnloadedException**|  
|**COR\_E\_APPLICATION**|**ApplicationException**|  
|**COR\_E\_ARGUMENT o E\_INVALIDARG**|**ArgumentException**|  
|**COR\_E\_ARGUMENTOUTOFRANGE**|**ArgumentOutOfRangeException**|  
|**COR\_E\_ARITHMETIC o ERROR\_ARITHMETIC\_OVERFLOW**|**ArithmeticException**|  
|**COR\_E\_ARRAYTYPEMISMATCH**|**ArrayTypeMismatchException**|  
|**COR\_E\_BADIMAGEFORMAT o ERROR\_BAD\_FORMAT**|**BadImageFormatException**|  
|**COR\_E\_COMEMULATE\_ERROR**|**COMEmulateException**|  
|**COR\_E\_CONTEXTMARSHAL**|**ContextMarshalException**|  
|**COR\_E\_CORE**|**CoreException**|  
|**NTE\_FAIL**|**CryptographicException**|  
|**COR\_E\_DIRECTORYNOTFOUND o ERROR\_PATH\_NOT\_FOUND**|**DirectoryNotFoundException**|  
|**COR\_E\_DIVIDEBYZERO**|**DivideByZeroException**|  
|**COR\_E\_DUPLICATEWAITOBJECT**|**DuplicateWaitObjectException**|  
|**COR\_E\_ENDOFSTREAM**|**EndOfStreamException**|  
|**COR\_E\_TYPELOAD**|**EntryPointNotFoundException**|  
|**COR\_E\_EXCEPTION**|**Eccezione**|  
|**COR\_E\_EXECUTIONENGINE**|**ExecutionEngineException**|  
|**COR\_E\_FIELDACCESS**|**FieldAccessException**|  
|**COR\_E\_FILENOTFOUND o ERROR\_FILE\_NOT\_FOUND**|**FileNotFoundException**|  
|**COR\_E\_FORMAT**|**FormatException**|  
|**COR\_E\_INDEXOUTOFRANGE**|**IndexOutOfRangeException**|  
|**COR\_E\_INVALIDCAST o E\_NOINTERFACE**|**InvalidCastException**|  
|**COR\_E\_INVALIDCOMOBJECT**|**InvalidComObjectException**|  
|**COR\_E\_INVALIDFILTERCRITERIA**|**InvalidFilterCriteriaException**|  
|**COR\_E\_INVALIDOLEVARIANTTYPE**|**InvalidOleVariantTypeException**|  
|**COR\_E\_INVALIDOPERATION**|**InvalidOperationException**|  
|**COR\_E\_IO**|**IOException**|  
|**COR\_E\_MEMBERACCESS**|**AccessException**|  
|**COR\_E\_METHODACCESS**|**MethodAccessException**|  
|**COR\_E\_MISSINGFIELD**|**MissingFieldException**|  
|**COR\_E\_MISSINGMANIFESTRESOURCE**|**MissingManifestResourceException**|  
|**COR\_E\_MISSINGMEMBER**|**MissingMemberException**|  
|**COR\_E\_MISSINGMETHOD**|**MissingMethodException**|  
|**COR\_E\_MULTICASTNOTSUPPORTED**|**MulticastNotSupportedException**|  
|**COR\_E\_NOTFINITENUMBER**|**NotFiniteNumberException**|  
|**E\_NOTIMPL**|**NotImplementedException**|  
|**COR\_E\_NOTSUPPORTED**|**NotSupportedException**|  
|**COR\_E\_NULLREFERENCE o E\_POINTER**|**NullReferenceException**|  
|**COR\_E\_OUTOFMEMORY o**<br /><br /> **E\_OUTOFMEMORY**|**OutOfMemoryException**|  
|**COR\_E\_OVERFLOW**|**OverflowException**|  
|**COR\_E\_PATHTOOLONG o ERROR\_FILENAME\_EXCED\_RANGE**|**PathTooLongException**|  
|**COR\_E\_RANK**|**RankException**|  
|**COR\_E\_REFLECTIONTYPELOAD**|**ReflectionTypeLoadException**|  
|**COR\_E\_REMOTING**|**RemotingException**|  
|**COR\_E\_SAFEARRAYTYPEMISMATCH**|**SafeArrayTypeMismatchException**|  
|**COR\_E\_SECURITY**|**SecurityException**|  
|**COR\_E\_SERIALIZATION**|**SerializationException**|  
|**COR\_E\_STACKOVERFLOW o ERROR\_STACK\_OVERFLOW**|**StackOverflowException**|  
|**COR\_E\_SYNCHRONIZATIONLOCK**|**SynchronizationLockException**|  
|**COR\_E\_SYSTEM**|**SystemException**|  
|**COR\_E\_TARGET**|**TargetException**|  
|**COR\_E\_TARGETINVOCATION**|**TargetInvocationException**|  
|**COR\_E\_TARGETPARAMCOUNT**|**TargetParameterCountException**|  
|**COR\_E\_THREADABORTED**|**ThreadAbortException**|  
|**COR\_E\_THREADINTERRUPTED**|**ThreadInterruptedException**|  
|**COR\_E\_THREADSTATE**|**ThreadStateException**|  
|**COR\_E\_THREADSTOP**|**ThreadStopException**|  
|**COR\_E\_TYPELOAD**|**TypeLoadException**|  
|**COR\_E\_TYPEINITIALIZATION**|**TypeInitializationException**|  
|**COR\_E\_VERIFICATION**|**VerificationException**|  
|**COR\_E\_WEAKREFERENCE**|**WeakReferenceException**|  
|**COR\_E\_VTABLECALLSNOTSUPPORTED**|**VTableCallsNotSupportedException**|  
|**Tutti gli altri HRESULT**|**COMException**|  
  
 Per recuperare informazioni sull'errore, il client gestito deve esaminare i campi dell'oggetto di eccezione generato.  Affinché l'oggetto di eccezione fornisca informazioni utili su un errore, è necessario che l'oggetto COM implementi l'interfaccia **IErrorInfo**.  Il runtime utilizza le informazioni fornite da **IErrorInfo** per inizializzare l'oggetto di eccezione.  
  
 Se l'oggetto COM non supporta **IErrorInfo**, il runtime inizializzerà un oggetto di eccezione con i valori predefiniti.  Nella tabella che segue vengono elencati tutti i campi associati a un oggetto di eccezione e viene identificata l'origine delle informazioni predefinite adottata quando l'oggetto COM supporta **IErrorInfo**.  
  
 Si noti che talvolta un `HRESULT` può essere ignorato dal runtime quando è presente un'interfaccia `IErrorInfo` sul thread.  Questo comportamento può verificarsi nei casi in cui l'`HRESULT` e l'interfaccia `IErrorInfo` non rappresentano lo stesso errore.   ``  
  
|Campo di eccezione|Origine delle informazioni da COM|  
|------------------------|---------------------------------------|  
|**ErrorCode**|HRESULT restituito dalla chiamata.|  
|**HelpLink**|Se **IErrorInfo\-\>HelpContext** è diverso da zero, la stringa viene formata concatenando **IErrorInfo\-\>GetHelpFile** e "\#" e **IErrorInfo\-\>GetHelpContext**.  In caso contrario, la stringa viene restituita da **IErrorInfo\-\>GetHelpFile**.|  
|**InnerException**|Sempre un riferimento Null \(**Nothing** in Visual Basic\).|  
|**Messaggio**|Stringa restituita da **IErrorInfo\-\>GetDescription**.|  
|**Origine**|Stringa restituita da **IErrorInfo\-\>GetSource**.|  
|**StackTrace**|La traccia dello stack.|  
|**TargetSite**|Il nome del metodo che ha restituito l'HRESULT di errore.|  
  
 I campi di eccezione, quali **Message**, **Source** e **StackTrace**, non sono disponibili per **StackOverflowException**.  
  
## Vedere anche  
 [Advanced COM Interoperability](http://msdn.microsoft.com/it-it/3ada36e5-2390-4d70-b490-6ad8de92f2fb)   
 [Eccezioni](../../../docs/standard/exceptions/index.md)