---
title: "Classe MissingMetadataException (.NET Native) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 408f25c4-6d60-475c-92b1-7b52b777c6db
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Classe MissingMetadataException (.NET Native)
**.NET per app di Windows per Windows 10, solo per [!INCLUDE[net_native](../../../includes/net-native-md.md)]**  
  
 Eccezione generata quando la reflection viene usata per recuperare i metadati che non sono presenti.  
  
 **Spazio dei nomi:** System.Reflection  
  
> [!IMPORTANT]
>  La classe `MissingMetadataException` è destinata esclusivamente all'uso interno da parte della catena di strumenti [!INCLUDE[net_native](../../../includes/net-native-md.md)].  La classe non può essere usata in codice di terze parti ed è preferibile evitare di gestire l'eccezione nel codice dell'applicazione.  Al contrario, eliminare l'eccezione aggiungendo le voci al [file delle direttive di runtime](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md).  Per altre informazioni, vedere la sezione Osservazioni.  
  
## Sintassi  
 [!code-csharp[ProjectN#4](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/missingmetadataexception_syntax1.cs#4)]  
  
 Si noti che la classe `MissingMetadataException` deriva da <xref:System.TypeAccessException>.  
  
 La classe `MissingMetadataException` include i membri seguenti:  
  
## Costruttori  
  
|Costruttore|Descrizione|  
|-----------------|-----------------|  
|`public MissingMetadataException()`|Inizializza una nuova istanza della classe `MissingMetadataException` usando un messaggio fornito dal sistema che descrive l'errore.<br /><br /> Questo costruttore è destinato a un uso interno da parte della sola catena di strumenti del [!INCLUDE[net_native](../../../includes/net-native-md.md)].|  
|`public MissingMetadataException(String message)`|Inizializza una nuova istanza della classe `MissingMetadataException` con un messaggio di errore specificato.<br /><br /> Questo costruttore è riservato all'uso interno da parte della catena di strumenti [!INCLUDE[net_native](../../../includes/net-native-md.md)].|  
  
## Proprietà  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|`public IDictionary Data { get; }`|Ottiene una raccolta di coppie chiave\-valore che fornisce informazioni aggiuntive definite dall'utente relative all'eccezione.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public string HelpLink { get; set; }`|Ottiene o imposta un collegamento al file della Guida associato all'eccezione.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public int HResult { get; protected set; }`|Ottiene o imposta `HRESULT`, un valore numerico codificato che viene assegnato a un'eccezione specifica.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public Exception InnerException { get; }`|Ottiene l'eccezione che ha causato l'eccezione corrente.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public string Message { get; }`|Ottiene un messaggio che descrive l'eccezione corrente.  Ereditata da <xref:System.TypeLoadException>.|  
|`public string Source { get; set; }`|Ottiene o imposta il nome dell'applicazione o dell'oggetto che ha causato l'errore.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public string StackTrace { get; }`|Ottiene una rappresentazione di stringa dei frame immediati nello stack di chiamate.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public MethodBase TargetSite { get; }`|Ottiene il metodo che ha generato l'eccezione corrente.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public string TypeName { get; ]`|Ottiene il nome completo del tipo i cui metadati non sono presenti.  Ereditato da <xref:System.TypeLoadException>.|  
  
## Metodi  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|`public bool Equals(Object obj)`|Determina se l'oggetto specificato equivale all'oggetto corrente.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`protected void Finalize()`|Consente a un oggetto di effettuare un tentativo di liberare risorse ed eseguire altre operazioni di pulizia prima che venga recuperato da Garbage Collection.  Ereditata da <xref:System.Object>.|  
|`public Exception GetBaseException()`|Restituisce l'eccezione che rappresenta la causa principale di una o più eccezioni successive.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public int GetHashCode()`|Restituisce un codice hash per un'istanza `MissingMetadataException`.  Ereditata da <xref:System.Object>.|  
|`public void GetObjectData(SerializationInfo info, StreamingContext context)`|Imposta un oggetto <xref:System.Runtime.Serialization.SerializationInfo> con informazioni sull'eccezione.  Ereditata da <xref:System.TypeLoadException>.|  
|`public Type GetType()`|Ottiene il tipo di runtime dell'istanza corrente.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`protected Object MemberwiseClone()`|Crea una copia superficiale dell'oggetto corrente.  Ereditata da <xref:System.Object>.|  
|`public string ToString()`|Restituisce la rappresentazione di stringa dell'eccezione corrente.  Ereditato da <xref:System.Exception?displayProperty=fullName>.|  
  
## Eventi  
  
|Evento|Descrizione|  
|------------|-----------------|  
|`protected event EventHandler<SafeSerializationEventArgs> SerializeObjectState`|Si verifica quando un'eccezione viene serializzata per creare un oggetto di stato eccezione contenente i dati serializzati relativi all'eccezione.  Ereditato da <xref:System.Exception?displayProperty=fullName>.|  
  
## Dettagli sull'uso  
 Eccezione `MissingMetadataException` generata quando la reflection viene usata per accedere ai metadati che non sono disponibili in un assembly.  
  
 I metadati disponibili in un'app al runtime sono definiti dal file di direttive di runtime \(configurazione XML\), \*.rd.xml.  Per evitare che l'app generi questa eccezione, è necessario modificare il file \*.rd.xm per definire i metadati che devono essere presenti al runtime.  Per informazioni sul formato del file \*.rd.xml, vedere [Riferimento a file di configurazione di direttive di runtime \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md).  
  
> [!IMPORTANT]
>  L'eccezione indica che i metadati richiesti dall'applicazione non sono disponibili al runtime; per questo motivo, l'eccezione non va gestita in un blocco `try`\/`catch`.  È invece necessario diagnosticare la causa dell'eccezione ed eliminarla usando un file di direttive di runtime.  Per ottenere la voce che è possibile aggiungere al file di direttive di runtime che elimina l'eccezione, è possibile usare uno dei due strumenti di risoluzione dei problemi:  
>   
>  -   Lo [strumento di risoluzione dei problemi MissingMetadataException](http://dotnet.github.io/native/troubleshooter/type.html) per i tipi.  
> -   Lo [strumento di risoluzione dei problemi MissingMetadataException](http://dotnet.github.io/native/troubleshooter/method.html) per i metodi.  
  
 La classe `MissingMetadataException` non contiene membri univoci. Tutti i membri sono ereditati dalla relativa classe base, <xref:System.TypeAccessException>.  
  
## Vedere anche  
 <xref:System.Exception?displayProperty=fullName>   
 <xref:System.TypeAccessException>   
 [Classe MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md)   
 [Classe MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md)   
 [Riferimento a file di configurazione di direttive di runtime \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)