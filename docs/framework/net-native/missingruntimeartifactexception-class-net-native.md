---
title: "Classe MissingRuntimeArtifactException (.NET Native) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d5b3d13e-689f-4584-8ba6-44f5167a8590
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Classe MissingRuntimeArtifactException (.NET Native)
**.NET per app di Windows per Windows 10, solo per [!INCLUDE[net_native](../../../includes/net-native-md.md)]**  
  
 L'eccezione generata quando i metadati per un tipo o un membro del tipo sono disponibili ma ne è stata rimossa l'implementazione.  
  
 **Spazio dei nomi:** System.Reflection  
  
> [!IMPORTANT]
>  La classe `MissingRuntimeArtifactException` è destinata esclusivamente all'uso interno da parte della catena di strumenti [!INCLUDE[net_native](../../../includes/net-native-md.md)].  La classe non può essere usata in codice di terze parti ed è preferibile evitare di gestire l'eccezione nel codice dell'applicazione.  Al contrario, eliminare l'eccezione aggiungendo le voci al [file delle direttive di runtime](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md).  Per altre informazioni, vedere la sezione Osservazioni.  
  
## Sintassi  
 [!code-csharp[ProjectN#22](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/missingruntimeartifactexception_syntax1.cs#22)]  
  
 Si noti che la classe `MissingRuntimeArtifactException` deriva da <xref:System.MemberAccessException>.  
  
 La classe `MissingRuntimeArtifactException` include i membri seguenti:  
  
## Costruttori  
  
|Costruttore|Descrizione|  
|-----------------|-----------------|  
|`public MissingRuntimeArtifactException()`|Inizializza una nuova istanza della classe `MissingRuntimeArtifactException` usando un messaggio fornito dal sistema che descrive l'errore.<br /><br /> Questo costruttore è destinato a un uso interno da parte della sola catena di strumenti del [!INCLUDE[net_native](../../../includes/net-native-md.md)].|  
|`public MissingRuntimeArtifactException(String message)`|Inizializza una nuova istanza della classe `MissingRuntimeArtifactException` con un messaggio di errore specificato.<br /><br /> Questo costruttore è destinato a un uso interno da parte della sola catena di strumenti del [!INCLUDE[net_native](../../../includes/net-native-md.md)].|  
  
## Proprietà  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|`public IDictionary Data { get; }`|Ottiene una raccolta di coppie chiave\-valore che fornisce informazioni aggiuntive definite dall'utente relative all'eccezione.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public string HelpLink { get; set; }`|Ottiene o imposta un collegamento al file della Guida associato all'eccezione.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public int HResult { get; protected set; }`|Ottiene o imposta `HRESULT`, un valore numerico codificato che viene assegnato a un'eccezione specifica.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public Exception InnerException { get; }`|Ottiene l'eccezione che ha causato l'eccezione corrente.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public string Message { get; }`|Ottiene un messaggio che descrive l'eccezione corrente.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public string Source { get; set; }`|Ottiene o imposta il nome dell'applicazione o dell'oggetto che ha causato l'errore.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public string StackTrace { get; }`|Ottiene una rappresentazione di stringa dei frame immediati nello stack di chiamate.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public MethodBase TargetSite { get; }`|Ottiene il metodo che ha generato l'eccezione corrente.  Ereditato da <xref:System.Exception?displayProperty=fullName>.|  
  
## Metodi  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|`public bool Equals(Object obj)`|Determina se l'oggetto specificato equivale all'oggetto corrente.  Ereditata da <xref:System.Object>.|  
|`protected void Finalize()`|Consente a un oggetto di effettuare un tentativo di liberare risorse ed eseguire altre operazioni di pulizia prima che venga recuperato da Garbage Collection.  Ereditata da <xref:System.Object>.|  
|`public Exception GetBaseException()`|Restituisce l'eccezione che rappresenta la causa principale di una o più eccezioni successive.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public int GetHashCode()`|Restituisce un codice hash per un'istanza `MissingRuntimeArtifactException`.  Ereditata da <xref:System.Object>.|  
|`public void GetObjectData(SerializationInfo info, StreamingContext context)`|Imposta un oggetto <xref:System.Runtime.Serialization.SerializationInfo> con informazioni sull'eccezione.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`public Type GetType()`|Ottiene il tipo di runtime dell'istanza corrente.  Ereditata da <xref:System.Exception?displayProperty=fullName>.|  
|`protected Object MemberwiseClone()`|Crea una copia superficiale dell'oggetto corrente.  Ereditata da <xref:System.Object>.|  
|`public string ToString()`|Restituisce la rappresentazione di stringa dell'eccezione corrente.  Ereditato da <xref:System.Exception?displayProperty=fullName>.|  
  
## Eventi  
  
|Evento|Descrizione|  
|------------|-----------------|  
|`protected event EventHandler<SafeSerializationEventArgs> SerializeObjectState`|Si verifica quando un'eccezione viene serializzata per creare un oggetto di stato eccezione contenente i dati serializzati relativi all'eccezione.  Ereditato da <xref:System.Exception?displayProperty=fullName>.|  
  
## Dettagli sull'uso  
 L'eccezione `MissingRuntimeArtifactException` viene generata quando si tenta di creare un'istanza di un tipo o di richiamare un membro del tipo la cui implementazione sia stata rimossa, sebbene i metadati del tipo o del membro siano presenti.  
  
 La disponibilità dei metadati e del codice di implementazione per l'esecuzione dinamica di un metodo nell'app al runtime viene definita dal file di direttive di runtime \(configurazione XML\), \*.rd.xml.  Per evitare che l'app generi questa eccezione, è necessario modificare il file \*.rd.xml per assicurarsi che i metadati necessari a un tipo o a un membro del tipo siano presenti al runtime.  Per informazioni sul formato del file \*.rd.xml, vedere [Riferimento a file di configurazione di direttive di runtime \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md).  
  
> [!IMPORTANT]
>  L'eccezione indica che il codice di implementazione richiesto dall'applicazione non è disponibile al runtime; per questo motivo, l'eccezione non va gestita in un blocco `try`\/`catch`.  È invece necessario diagnosticare la causa dell'eccezione ed eliminarla usando un file di direttive di runtime.  In genere, l'eccezione viene eliminata specificando i criteri `Activate` o `Dynamic` appropriati per un elemento di programma nel file di direttive di runtime \(file \*.rd.xml\).  Per ottenere la voce che è possibile aggiungere al file di direttive di runtime che elimina l'eccezione, è possibile usare uno dei due strumenti di risoluzione dei problemi:  
>   
>  -   Lo [strumento di risoluzione dei problemi MissingMetadataException](http://dotnet.github.io/native/troubleshooter/type.html) per i tipi.  
> -   Lo [strumento di risoluzione dei problemi MissingMetadataException](http://dotnet.github.io/native/troubleshooter/method.html) per i metodi.  
  
 La classe `MissingRuntimeArtifactException` non contiene membri univoci. Tutti i membri sono ereditati dalla relativa classe base, <xref:System.MemberAccessException>.  
  
## Vedere anche  
 [Riferimento a file di configurazione di direttive di runtime \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [Impostazioni dei criteri della direttiva di runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md)