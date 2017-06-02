---
title: "Strumenti | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 89c907f9-313f-408c-992a-631f1eadf1da
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Strumenti
In questo argomento vengono elencate tutte le eccezioni generate dagli strumenti di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  
  
## Elenco delle eccezioni  
  
|Codice sorgente|Stringa di risorsa|  
|---------------------|------------------------|  
|ParametersTarget|\<enum\>|  
|ParametersToolConfig|\<file config\>|  
|ErrInvalidPath|Il percorso specificato non è valido.Controllare l'argomento specificato.|  
|ParametersReference|\<percorso file\>|  
|WrnCannotLoadConfigFileForValidation|Si è verificato un errore durante l'elaborazione del file di configurazione caricato dal percorso specificato.Non è possibile convalidare i servizi definiti in questo file di configurazione.|  
|MoreHelp|Per ulteriori informazioni, digitare "svcutil" con gli argomenti specificati.|  
|HelpMergeConfig|Determina l'incorporazione della configurazione generata in un file esistente anziché la sovrascrittura del file esistente.|  
|ErrCannotWriteFile|Non è possibile scrivere in un file di output.|  
|ErrInvalidNamespaceArgument|Il valore non valido specificato è stato passato all'opzione indicata.Specificare una coppia spazio dei nomi di destinazione e spazio dei nomi CLR delimitata da virgole.|  
|HelpImportXmlType|Configura il serializzatore DataContract per l'importazione di tipi diversi da DataContract come tipi IXmlSerializable.|  
|ErrExclusiveOptionsSpecified|È impossibile utilizzare l'opzione specificata se è stata indicata un'altra opzione.|  
|WrnHttpGetFailed|Error GET HTTP con l'URI specificato.|  
|ErrInputFileNotAssemblyOrMetadata|Il file nel percorso specificato letto tramite l'argomento di input indicato non sembra essere un file di metadati XML né un assembly valido.|  
|WrnUnknownMetadataFound|È impossibile salvare un documento dei metadati non riconosciuto del tipo specificato.|  
|ErrDirectoryContainsInvalidCharacters|Il valore non valido specificato è stato passato all'opzione indicata.Il carattere indicato non è consentito in un percorso.|  
|WrnCannotResolveServiceForValidation|È impossibile caricare un servizio con il configName specificato.Per convalidare un servizio, specificare l'assembly contenente il tipo di servizio e un eseguibile con la configurazione per questo servizio.|  
|ErrUnexpectedValue|L'opzione specificata non supporta valori.|  
|\#InvalidArg|Nell'oggetto specificato è contenuto un argomento non valido.|  
|ParametersExcludeType|\<tipo\>|  
|HelpXmlSerializer|Generare tipi di dati che utilizzano XmlSerializer per la serializzazione e la deserializzazione.|  
|\#|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\=|  
|ErrUnexpectedError|Si è verificato un errore nello strumento.|  
|HelpNologo|Le informazioni di copyright e il messaggio di avvio non sono visualizzati.|  
|ErrInputConflictsWithTarget|Il tipo di input letto dall'opzione specificata non è supportato con l'opzione indicata impostata sul valore dato.|  
|WrnCannotLoadServiceForExport|Si è verificato un errore durante il caricamento del tipo di servizio da esportare.|  
|HelpMetadataDownloadCategory|\- \= DOWNLOAD DEI METADATI \= \-|  
|WrnNoServiceContractTypes|È impossibile generare tipi XmlSerializer per l'assembly specificato.Nessun tipo di contratto di servizio trovato.|  
|WrnCouldNotLoadTypesFromReferenceAssemblyAt|Si è verificato un errore durante il caricamento di tipi in un assembly caricato dal percorso specificato.Alcuni tipi contenuti nell'assembly non sono stati caricati e non sono disponibli per lo strumento.|  
|ErrDirectoryPointsToAFile|Il valore non valido specificato è stato passato all'opzione specificata.Il valore specificato è un percorso a un file.|  
|Errore|Errore:|  
|ErrDuplicateReferenceValues|L'assembly specificato è stato caricato due volte utilizzando l'opzione indicata.Un assembly può essere usato come riferimento solo una volta.|  
|WrnNoXmlSerializerOperationBehavior|È impossibile generare XmlSerializer per l'assembly specificato.Nessun contratto di servizio nell'assembly dispone di un'operazione con XmlSerializerOperationBehavior.|  
|ErrCannotCreateDirectory|È impossibile creare la directory specificata.|  
|ErrCouldNotLoadTypesFromAssemblyAt|È impossibile caricare tutti i tipi nell'assembly specificato.|  
|ErrUnknownSwitch|L'opzione specificata non è riconosciuta.|  
|Logo|Il logo dello strumento è "Microsoft ® Servizio Modello Metadati Strumento" con numero di versione.|  
|NoCodeWasGenerated|Il codice non è stato generato.<br /><br /> Se si stava tentando di creare un client, ciò può essere dovuto al fatto che i documenti dei metadati non contengono contratti o servizi validi<br /><br /> oppure tutti i contratti\/servizi sono presenti negli assembly di riferimento.Verificare di aver passato tutti i documenti dei metadati allo strumento.|  
|WrnUnableToLoadContractForSGen|Si è verificato un errore durante il caricamento di un tipo di contratto.È impossibile generare il tipo XmlSerializer per questo contratto.Il tipo e i dettagli sono specificati.|  
|WrnOptionConflictsWithInput|È impossibile utilizzare l'opzione specificata con più assembly di input.L'opzione specificata viene ignorata.|  
|ErrUnableToImportMetadata|Si è verificato un errore critico durante il tentativo di importazione dei metadati.|  
|ErrInvalidSerializer|Un valore non valido del serializzatore è stato passato all'opzione specificata.I serializzatori supportati sono specificati.|  
|SavingDownloadedMetadata|Salvataggio dei file di metadati scaricati in corso.|  
|WrnNoConfigForServices|Nessuno degli assembly passati sono file eseguibili con file di configurazione oppure nessuno dei file di configurazione contiene servizi con il nome di configurazione specificato.|  
|ErrInputConflictsWithOption|L'input letto dall'opzione specificata non può essere utilizzato con l'opzione indicata perché implica modalità diverse di funzionamento dello strumento.|  
|ErrUnableToExportEndpoints|Si è verificato un errore durante l'esportazione del tipo di servizio specificato.|  
|ErrInputSchemaParseError|Si è verificato un errore di analisi dell'XML Schema durante la lettura dell'elemento specificato.Verificare che il formato del file XML sia corretto e valido.|  
|ErrInputPolicyParseError|Si è verificato un errore di analisi WS\-Policy durante la lettura dell'elemento specificato.Verificare che il formato del file XML sia corretto e valido.|  
|ErrUnableToLoadReferenceType|Si è verificato un errore durante il caricamento di un tipo di contratto di riferimento.Il tipo specificato viene ignorato.|  
|WrnCannotLoadServiceForValidation|Si è verificato un errore durante il caricamento del servizio da convalidare.Il tipo e i dettagli sono specificati.|  
|HelpCodeGenerationCategory|\-\= GENERAZIONE DI CODICE \=\-|  
|RetreivingMetadataWithMexAndDisco|Tentativo di download dei metadati dalla posizione specificata utilizzando WS\-Metadati Exchange o DISCO.|  
|ErrGeneralSchemaValidation|Si è verificato un errore durante la verifica di schemi XML generati durante l'esportazione.|  
|ParametersDirectory|\<directory\>|  
|ErrCannotLoadSpecifiedType|Nessun tipo può essere caricato per il valore specificato passato all'opzione indicata.Assicurarsi che l'assembly al quale appartiene questo tipo venga specificato utilizzando l'opzione indicata.|  
|ErrOptionModeConflict|L'opzione specificata non può essere utilizzata con l'altra opzione perché implicano tipi di output diversi.|  
|ErrIsNotAnAssembly|È stato impossibile caricare l'elemento specificato come assembly.Verificare che il file sia un assembly .NET.|  
|ErrInputConflictsWithMode|L'input letto dall'elemento specificato non è coerente con le altre opzioni.|  
|ErrDuplicateValuePassedToTypeArg|Il valore specificato è stato passato più volte all'opzione indicata.Ogni tipo può essere specificato una sola volta.|  
|ErrInputEPRFileParseError|È impossibile leggere il riferimento all'endpoint dall'elemento specificato.Verificare che il formato del file XML sia corretto e valido.|  
|ErrCouldNotCreateCodeProvider|È impossibile creare un provider di codice per il valore specificato, passato all'argomento \/{1}.Verificare che il provider di codice sia installato e configurato correttamente.|  
|ErrPathTooLongDirOnly|Il percorso risultante specificato è troppo lungo.Controllare l'argomento specificato.|  
|HelpDataContractSerializer|Generare tipi di dati che utilizzano DataContract Serializer per la serializzazione e la deserializzazione.|  
|ErrUnableToExportEndpoint|Si è verificato un errore durante l'esportazione del nome dell'endpoint specificato nello spazio dei nomi indicato nel tipo di servizio specificato trovato nel file di configurazione caricato per l'assembly.|  
|HelpUsage1|Visualizza l'utilizzo della Guida.|  
|HelpUsage2|Visualizza l'utilizzo della Guida.|  
|HelpUsage3|Visualizza l'utilizzo della Guida.|  
|HelpUsage4|Visualizza l'utilizzo della Guida.|  
|HelpUsage5|Visualizza l'utilizzo della Guida.|  
|ErrDirectoryNotFound|Non è possibile trovare la directory specificata.Verificare che la directory esista e che si disponga delle autorizzazioni appropriate per accedervi.|  
|ErrUnableToLoadFile|È impossibile leggere il file specificato.|  
|ErrNoFilesFound|Il percorso di input specificato non sembra fare riferimento ad alcun file esistente.|  
|ParametersConfig|\<file config\>|  
|ErrDirectoryInsteadOfFile|Il percorso di input specificato sembra essere una directory.Deve essere un URL o un percorso di file.|  
|HelpConfig|Indica agli strumenti di generare un file di configurazione con il nome fornito.Impostazione predefinita: output.config.|  
|ErrSingleUseSwitch|L'opzione specificata non può essere indicata più volte.|  
|Warning|Avviso:|  
|WrnAmbiguousServiceConfig|Sono state trovate più configurazioni del servizio con il nome di configurazione specificato e vengono specificati gli assembly seguenti.|  
|ErrInvalidInputPath|Il percorso di input specificato non sembra fare riferimento ad alcun file esistente e non sembra essere un URI valido.|  
|ErrUnableToLoadInputs|Si è verificato un errore durante la lettura dei metadati caricati.|  
|GeneratingSerializer|Creazione di serializzatori XML in corso.|  
|HelpToolConfig|File di configurazione personalizzato da utilizzare al posto del file di configurazione dell'applicazione.Può essere utilizzato per modificare la configurazione dei metadati o registrare estensioni di configurazione senza alterare il file di configurazione dello strumento.|  
|ErrValidateInvalidUse|Non è possibile utilizzare l'opzione specificata con l'opzione indicata.|  
|WrnWSMExFailed|Errore WS\-Metadati Exchange con l'URI specificato.|  
|HelpNoconfig|Non generare la configurazione.|  
|HelpCodeGenerationDescription|L'elemento specificato è in grado di generare contratti di servizio, client e tipi di dati dai documenti dei metadati.|  
|HelpTargetMetadata|Metadati di output.Se l'input è un URL, Svcutil.exe salva i metadati su disco e non genera codice.Se l'input è uno o più assembly, Svcutil.exe genera metadati dai tipi negli assembly.|  
|ErrAmbiguousOptionModeConflict|L'opzione specificata è in conflitto con altre opzioni.Rivedere l'utilizzo dello strumento.|  
|ErrNotLanguageOrCodeDomType|Il valore specificato passato all'argomento indicato non rappresenta un linguaggio definito e non può essere caricato come tipo CLR completo.|  
|ErrUnableToUniquifyFilename|È impossibile creare il nome del file di output.Vengono creati troppi file con il prefisso specificato.|  
|ErrCannotCreateFile|È impossibile creare il file di output specificato.|  
|ErrExpectedValue|L'opzione specificata richiede l'indicazione di un valore.|  
|ErrCannotDisambiguateSpecifiedTypes|Più di un tipo con lo stesso nome esiste nel set di assembly di riferimento.Utilizzare nomi completi di assembly per distinguere tra i tipi specificati per l'opzione indicata.|  
|RetreivingMetadataWithMexOnly|Tentativo di download dei metadati dalla posizione specificata utilizzando WS\-Metadati Exchange.L'URL non supporta DISCO.|  
|ErrInvalidTarget|La destinazione indicata è non valida se specificata con l'opzione indicata.Le destinazioni supportate sono specificate.|  
|ErrPathTooLong|Il percorso risultante è troppo lungo.Rivedere gli argomenti specificati.|  
|HelpCommonOptionsCategory|\- \= OPZIONI COMUNI \= \-|  
|ParametersServiceName|\<NomeConfServizio\>|  
|ErrNoValidInputFilesSpecified|Non è stato specificato alcun file di input valido.Specificare documenti di metadati o file di assembly.|  
|ParametersLanguage|\<language\>|  
|ErrUnableToLoadMetadataDocument|Si è verificato un errore durante la lettura dei metadati da uno dei documenti caricati.L'identificatore del documento è specificato.|  
|ErrConflictingInputs|L'argomento di input specificato è in conflitto con l'elemento indicato perché implica modalità diverse di funzionamento dello strumento.|  
|WrnUnableToLoadContractForValidation|Si è verificato un errore durante il caricamento di un tipo di contratto.Il tipo e i dettagli sono specificati.|  
|WrnAttributeReflectionErrors|La riflessione dell'attributo non è riuscita per alcuni tipi contenuti nell'assembly caricato dalla posizione specificata.Verificare che l'assembly possa essere caricato da questo percorso con i privilegi di sicurezza corretti.|  
|HelpMetadataExportCategory|\- \= ESPORTAZIONE DEI METADATI \= \-|  
|HelpValidationCategory|\- \= CONVALIDA DEL SERVIZIO \= \-|  
|ValidationError|Errore di convalida:|  
|GeneratingFiles|Generazione di file in corso.|  
|ErrCannotSpecifyMultipleMappingsForNamespace|Un valore non valido è stato passato all'opzione specificata.Non è possibile mappare lo spazio dei nomi di destinazione specificato a più spazi dei nomi CLR come indicato.|  
|ErrCouldNotLoadReferenceAssemblyAt|È impossibile caricare l'assembly di riferimento specificato.|  
|ParametersOut|\<file\>|  
|NoCodeWasGeneratedSuggestDCOnly|Per generare contratti per gli schemi, utilizzare l'opzione specificata.|  
|ErrUnableToLoadInputConfig|È impossibile caricare il file di configurazione specificato.|  
|ErrUnexpectedDelimiter|Un delimitatore di argomento non valido \(':' o '\='\) non può avviare l'opzione.|  
|ErrMergeConfigUsedWithoutConfig|È impossibile utilizzare l'opzione specificata senza specificare anche l'altra opzione.|  
|ErrUnableToExportContract|Si è verificato un errore durante l'esportazione del contratto caricato dal tipo specificato.|  
|GeneratingMetadata|Generazione di file di metadati in corso.|  
|ErrNotCodeDomType|Il tipo specificato passato all'argomento indicato non appartiene alla classe derivata specificata.|  
|WrnNoTypeForServices|Nessuno degli assembly passati contenevano tipi di servizio con il nome di configurazione specificato.|  
|ErrAssemblyLoadFailed|È impossibile caricare il file specificato come assembly.Per ulteriori informazioni, verificare FusionLogs.|  
|NoMetadataWasGenerated|I file dei metadati non sono stati generati.Nessun contratto di servizio è stato esportato.<br /><br /> Per esportare un servizio, utilizzare l'opzione specificata.Per esportare contratti di dati, specificare l'opzione.|  
|WrnCannotResolveServiceForExport|È impossibile caricare un servizio con il configName specificato.Per esportare un servizio, specificare l'assembly contenente il tipo di servizio e un eseguibile con la configurazione per questo servizio.|  
|ParametersCollectionType|\<tipo\>|  
|ErrOptionConflictsWithTarget|L'utilizzo dell'opzione specificata non è supportato con l'opzione indicata impostata sul valore specificato.|  
|ErrCodegenError|Si è verificato un errore durante la generazione di codice nel linguaggio specificato.<br /><br /> Il linguaggio non supporta tutti gli elementi di codice generati.È necessario utilizzare un altro linguaggio.|  
|ErrInputWsdlParseError|Si è verificato un errore di analisi WSDL durante la lettura dell'elemento specificato.Verificare che il formato del file XML sia corretto e valido.|  
|ErrCouldNotCreateInstance|È impossibile creare un'istanza del tipo specificato passato all'argomento indicato.|  
|ParametersNamespace|\<stringa,stringa\>|  
|HelpNostdlib|Non fare riferimento a librerie standard \(per impostazione predefinita viene fatto riferimento a mscorlib.dll e system.servicemodel.dll\).|  
|WrnCannotLoadConfigFileForExport|Si è verificato un errore durante l'elaborazione del file di configurazione caricato dal percorso indicato.È impossibile caricare servizi definiti in questo file di configurazione.|  
|WrnUnableToLoadContractForExport|Si è verificato un errore durante il caricamento di un tipo di contratto.È impossibile esportare il tipo specificato.|