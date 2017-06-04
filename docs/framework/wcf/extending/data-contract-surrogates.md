---
title: "Surrogati del contratto dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contratti dati [WCF], surrogati"
ms.assetid: 8c31134c-46c5-4ed7-94af-bab0ac0dfce5
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Surrogati del contratto dati
Il *surrogato* del contratto dati è una funzionalità avanzata basata sul modello del contratto dati.È progettata per la personalizzazione e la sostituzione dei tipi nelle situazioni in cui gli utenti desiderano modificare il modo in cui un tipo viene serializzato, deserializzato o proiettato nei metadati.Un surrogato può essere utilizzato, ad esempio, quando un contratto dati non è stato specificato per il tipo, i campi e le proprietà non sono contrassegnati con l'attributo <xref:System.Runtime.Serialization.DataMemberAttribute> o gli utenti desiderano creare dinamicamente variazioni dello schema.  
  
 La serializzazione e la deserializzazione vengono eseguite con il surrogato del contratto dati quando si utilizza <xref:System.Runtime.Serialization.DataContractSerializer> per convertire da .NET Framework in un formato adatto, ad esempio XML.Il surrogato del contratto dati può essere utilizzato inoltre per modificare i metadati esportati per i tipi, durante la produzione di rappresentazioni dei metadati, ad esempio XSD \(XML Schema Documents\).In fase di importazione viene creato codice dai metadati e in questo caso il surrogato può essere utilizzato per personalizzare anche il codice generato.  
  
## Funzionamento del surrogato  
 Un surrogato funziona eseguendo il mapping di un tipo \(l'"originale"\) a un altro tipo \(il "surrogato"\).Negli esempi seguenti sono mostrati il tipo originale `Inventory` e un nuovo tipo surrogato `InventorySurrogated`.Il tipo `Inventory` non è serializzabile diversamente dal tipo `InventorySurrogated`:  
  
 [!code-csharp[C_IDataContractSurrogate#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#1)]  
  
 Poiché per questa classe non è stato definito un contratto dati, è necessario convertire la classe in una classe surrogata con un contratto dati.La classe surrogata è illustrata nell'esempio seguente:  
  
 [!code-csharp[C_IDataContractSurrogate#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#2)]  
  
## Implementazione di IDataContractSurrogate  
 Per utilizzare il surrogato del contratto dati, implementare l'interfaccia <xref:System.Runtime.Serialization.IDataContractSurrogate>.  
  
 Di seguito è fornita una panoramica di ogni metodo dell'interfaccia <xref:System.Runtime.Serialization.IDataContractSurrogate> con una possibile implementazione.  
  
### GetDataContractType  
 Il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%2A> esegue il mapping di un tipo all'altro.È necessario per la serializzazione, la deserializzazione, l'importazione e l'esportazione.  
  
 La prima attività consiste nel definire i tipi che verranno mappati ad altri tipi.Ad esempio:  
  
 [!code-csharp[C_IDataContractSurrogate#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#3)]  
  
-   Nel caso della serializzazione, il mapping restituito da questo metodo viene successivamente utilizzato per trasformare l'istanza originale in un'istanza surrogata chiamando il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%2A>.  
  
-   Nel caso della deserializzazione, il mapping restituito da questo metodo viene utilizzato dal serializzatore per deserializzare in un'istanza del tipo surrogato.Viene quindi chiamato il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDeserializedObject%2A> per trasformare l'istanza surrogata in un'istanza del tipo originale.  
  
-   Nel caso dell'esportazione, viene eseguita la riflessione del tipo surrogato restituito da questo metodo per ottenere il contratto dati da utilizzare per la generazione dei metadati.  
  
-   Nel caso dell'importazione, il tipo iniziale viene modificato in un tipo surrogato di cui viene eseguita la riflessione per ottenere il contratto dati da utilizzare per scopi come il supporto di riferimento.  
  
 Il parametro <xref:System.Type> è il tipo dell'oggetto in fase di serializzazione, deserializzazione, importazione o esportazione.Il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%2A> deve restituire il tipo di input se il surrogato non gestisce il tipo.In caso contrario restituisce il tipo surrogato appropriato.Se esistono vari tipi surrogati, è possibile definire vari mapping in questo metodo.  
  
 Il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%2A> non viene chiamato per primitivi del contratto dati incorporati, ad esempio <xref:System.Int32> o <xref:System.String>.Per gli altri tipi, ad esempio matrici, tipi definiti dall'utente e altre strutture di dati, questo metodo verrà chiamato per ogni tipo.  
  
 Nell'esempio precedente il metodo verifica se il parametro `type` e `Inventory` sono confrontabili.In tal caso, il metodo lo mappa a `InventorySurrogated`.Ogni volta che viene chiamata una serializzazione, una deserializzazione, uno schema di importazione o di esportazione, questa funzione viene chiamata per prima per determinare il mapping tra tipi.  
  
### Metodo GetObjectToSerialize  
 Il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%2A> converte l'istanza del tipo originale nell'istanza del tipo surrogato.È necessario per la serializzazione.  
  
 Il passaggio successivo consiste nel definire il modo in cui i dati fisici verranno mappati dall'istanza originale al surrogato implementando il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%2A>.Ad esempio:  
  
 [!code-csharp[C_IDataContractSurrogate#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#4)]  
  
 Il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%2A> viene chiamato quando un oggetto viene serializzato.Questo metodo trasferisce dati dal tipo originale ai campi del tipo surrogato.I campi possono essere mappati direttamente ai campi surrogati oppure è possibile archiviare le modifiche dei dati originali nel surrogato.Gli utilizzi possibili comprendono: mapping diretto dei campi, esecuzione di operazioni sui dati da archiviare nei campi surrogati, archiviazione dell'XML del tipo originale nel campo surrogato.  
  
 Il parametro `targetType` fa riferimento al tipo dichiarato del membro.Questo parametro è il tipo surrogato restituito dal metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%2A>.Il serializzatore non implica che l'oggetto restituito possa essere assegnato a questo tipo.Il parametro `obj`  è l'oggetto da serializzare e verrà convertito nel surrogato, se necessario.Questo metodo deve restituire l'oggetto di input se il surrogato non gestisce l'oggetto.In caso contrario, verrà restituito il nuovo oggetto surrogato.Il surrogato non viene chiamato se l'oggetto è null.In questo metodo è possibile definire numerosi mapping surrogati per istanze diverse.  
  
 Quando si crea una classe <xref:System.Runtime.Serialization.DataContractSerializer>, è possibile fare in modo che conservi i riferimenti all'oggetto.\([!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Serializzazione e deserializzazione](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md).\) A tale scopo, impostare il parametro `preserveObjectReferences` nel costruttore su `true`.In questo caso, il surrogato viene chiamato solo una volta per un oggetto dal momento che tutte le serializzazioni successive scrivono il riferimento nel flusso.Se il parametro `preserveObjectReferences` è impostato su `false`, il surrogato viene chiamato ogni volta che si verifica un'istanza.  
  
 Se il tipo dell'istanza serializzata differisce dal tipo dichiarato, le informazioni sul tipo vengono scritte nel flusso, ad esempio `xsi:type`, per consentire la deserializzazione dell'istanza all'altra estremità.Questo processo ha luogo a prescindere dalla circostanza che l'oggetto sia surrogato o no.  
  
 Nell'esempio precedente i dati dell'istanza di `Inventory` vengono convertiti nei dati di `InventorySurrogated`.Viene verificato il tipo dell'oggetto e vengono eseguite le manipolazioni necessarie per la conversione al tipo surrogato.In questo caso, i campi della classe `Inventory` vengono copiati direttamente sui campi della classe `InventorySurrogated`.  
  
### Metodo GetDeserializedObject  
 Il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDeserializedObject%2A> converte l'istanza del tipo surrogato nell'istanza del tipo originale.È obbligatorio per la deserializzazione.  
  
 L'attività successiva consiste nel definire il modo in cui i dati fisici verranno mappati dall'istanza surrogata all'originale.Ad esempio:  
  
 [!code-csharp[C_IDataContractSurrogate#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#5)]  
  
 Questo metodo viene chiamato solo durante la deserializzazione di un oggetto.Fornisce il mapping dei dati inverso per la deserializzazione dal tipo surrogato al tipo originale.Analogamente al metodo `GetObjectToSerialize`, alcuni possibili utilizzi sono lo scambio diretto dei dati del campo, l'esecuzione di operazioni sui dati e l'archiviazione di dati XML.Quando si deserializza, non sempre è possibile ottenere dall'originale i valori dei dati esatti a causa di modifiche intervenute durante la conversione dei dati.  
  
 Il parametro `targetType` fa riferimento al tipo dichiarato del membro.Questo parametro è il tipo surrogato restituito dal metodo `GetDataContractType`.Il parametro `obj`  fa riferimento all'oggetto deserializzato.Se surrogato, l'oggetto può essere convertito di nuovo nel tipo originale.Questo metodo restituisce l'oggetto di input se il surrogato non gestisce l'oggetto.In caso contrario l'oggetto deserializzato verrà restituito dopo il completamento della conversione.Se esistono molti tipi surrogati, è possibile fornire per ognuno la conversione dei dati da surrogato a tipo originale indicando ogni tipo e la relativa conversione.  
  
 Durante la restituzione di un oggetto, le tabelle degli oggetti interni vengono aggiornate con l'oggetto restituito da questo surrogato.Qualsiasi riferimento successivo a un'istanza otterrà l'istanza del surrogato dalle tabelle degli oggetti.  
  
 Nell'esempio precedente gli oggetti di tipo `InventorySurrogated` vengono nuovamente convertiti nel tipo `Inventory`iniziale.In questo caso, i dati sono trasferiti direttamente da `InventorySurrogated` ai campi corrispondenti in `Inventory`.Poiché non sussistono modifiche dei dati, ogni campo membro conterrà gli stessi valori esistenti prima della serializzazione.  
  
### Metodo GetCustomDataToExport  
 Durante l'esportazione di uno schema, il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetCustomDataToExport%2A> è facoltativo.Viene utilizzato per inserire dati aggiuntivi o suggerimenti nello schema esportato.I dati aggiuntivi possono essere inseriti a livello di membro o a livello di tipo.Ad esempio:  
  
 [!code-csharp[C_IDataContractSurrogate#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#6)]  
  
 Questo metodo \(con due overload\) consente l'inclusione di informazioni aggiuntive nei metadati a livello di membro o di tipo.È possibile includere suggerimenti sulla qualità pubblica o privata di un membro e commenti che vengono conservati per tutta la durata dell'esportazione e dell'importazione dello schema.Tali informazioni andrebbero perse senza questo metodo.Il metodo non provoca l'inserimento o l'eliminazione di membri o tipi, piuttosto inserisce dati aggiuntivi negli schemi in corrispondenza di uno di questi livelli.  
  
 Il metodo è sottoposto a overload e può assumere un `Type` \(il parametro `clrtype`\) o <xref:System.Reflection.MemberInfo> \(il parametro `memberInfo`\).Il secondo parametro è sempre un `Type` \(il parametro `dataContractType`\).Questo metodo viene chiamato per ogni membro e tipo del tipo `dataContractType` surrogato.  
  
 Uno dei due overload deve restituire `null` o un oggetto serializzabile.Un oggetto diverso da null verrà serializzato come annotazione nello schema esportato.Per l'overload di `Type`, ogni tipo esportato nello schema viene inviato al metodo nel primo parametro unitamente al tipo surrogato come parametro `dataContractType`.Per l'overload di `MemberInfo`, ogni membro esportato nello schema invia le rispettive informazioni come parametro `memberInfo` con il tipo surrogato nel secondo parametro.  
  
#### Metodo GetCustomDataToExport \(Type, Type\)  
 Il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetCustomDataToExport%28System.Type%2CSystem.Type%29?displayProperty=fullName> viene chiamato durante l'esportazione dello schema per ogni definizione del tipo.Il metodo aggiunge informazioni ai tipi all'interno dello schema durante l'esportazione.Ogni tipo definito viene inviato a questo metodo per determinare se esistono dati aggiuntivi da includere nello schema.  
  
#### Metodo GetCustomDataToExport \(MemberInfo, Type\)  
 Il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetCustomDataToExport%28System.Reflection.MemberInfo%2CSystem.Type%29?displayProperty=fullName> viene chiamato durante l'esportazione per ogni membro esistente nei tipi esportati.Questa funzione consente di personalizzare eventuali commenti per i membri che verranno inclusi nello schema in fase di esportazione.Le informazioni relative a ogni membro della classe vengono inviate al metodo per appurare se è necessario aggiungere altri dati allo schema.  
  
 Nell'esempio precedente viene analizzato `dataContractType` alla ricerca di ogni membro del surrogato.Viene quindi restituito il modificatore di accesso appropriato per ogni campo.Senza questa personalizzazione, il valore predefinito dei modificatori di accesso è pubblico.Pertanto, tutti i membri verrebbero definiti come pubblici nel codice generato utilizzando lo schema esportato, indipendentemente dalle effettive restrizioni di accesso.Se non si utilizza questa implementazione, il membro `numpens` sarebbe pubblico nello schema esportato anche se definito come privato nel surrogato.Con l'utilizzo di questo metodo nello schema esportato, il modificatore di accesso può essere generato come privato.  
  
### Metodo GetReferencedTypeOnImport  
 Questo metodo mappa la classe<xref:System.Type> del surrogato al tipo originale.È facoltativo per l'importazione dello schema.  
  
 In caso di creazione di un surrogato che importa uno schema e genera codice appositamente, l'attività successiva consiste nel definire il tipo di un'istanza surrogata rispetto al tipo originale.  
  
 Se per il codice generato è necessario fare riferimento a un tipo utente esistente, questa operazione è possibile implementando il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetReferencedTypeOnImport%2A>.  
  
 In caso di importazione di uno schema, questo metodo viene chiamato per ogni dichiarazione di tipo per mappare il contratto dati surrogato a un tipo.I parametri di stringa `typeName` e `typeNamespace` definiscono il nome e lo spazio dei nomi del tipo surrogato.Il valore restituito per <xref:System.Runtime.Serialization.IDataContractSurrogate.GetReferencedTypeOnImport%2A> viene utilizzato per determinare l'esigenza di generare un tipo nuovo.Questo metodo deve restituire un tipo valido o null.Per i tipi validi, il tipo restituito verrà utilizzato nel codice generato come tipo a cui viene fatto riferimento.Se viene restituito null, non verrà fatto riferimento ad alcun tipo e verrà creato un tipo nuovo.Se esistono molti surrogati, è possibile eseguire di nuovo il mapping di ogni tipo surrogato al tipo iniziale.  
  
 Il parametro `customData` è l'oggetto derivato in origine da <xref:System.Runtime.Serialization.IDataContractSurrogate.GetCustomDataToExport%2A>.Il parametro `customData` viene utilizzato quando gli autori di surrogati desiderano inserire dati aggiuntivi\/suggerimenti nei metadati da utilizzare durante l'importazione per generare codice.  
  
### Metodo ProcessImportedType  
 Il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.ProcessImportedType%2A> personalizza qualsiasi tipo creato dall'importazione dello schema.È facoltativo.  
  
 In caso di importazione di uno schema, questo metodo consente la personalizzazione di qualsiasi tipo importato e di qualsiasi informazione di compilazione.Ad esempio:  
  
 [!code-csharp[C_IDataContractSurrogate#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#7)]  
  
 Durante l'importazione, questo metodo viene chiamato per ogni tipo generato.Modificare la classe <xref:System.CodeDom.CodeTypeDeclaration> specificata o la classe <xref:System.CodeDom.CodeCompileUnit>.Tale operazione include la modifica del nome, dei membri, degli attributi e di molte altre proprietà di `CodeTypeDeclaration`.Elaborando `CodeCompileUnit`, è possibile modificare le direttive, gli spazi dei nomi, gli assembly di riferimento e molti altri aspetti.  
  
 Il parametro `CodeTypeDeclaration` contiene la dichiarazione del tipo code DOM.Il parametro `CodeCompileUnit` consente le modifiche per l'elaborazione del codice.La restituzione di `null` sfocia nell'eliminazione della dichiarazione del tipo.Per contro, la restituzione di `CodeTypeDeclaration` comporta il mantenimento delle modifiche.  
  
 Se i dati personalizzati vengono inseriti durante l'esportazione dei metadati, è necessario che vengano forniti all'utente durante l'importazione perché possano essere utilizzati.I dati personalizzati possono essere utilizzati per suggerimenti dei modello di programmazione o altri commenti.Ogni istanza di `CodeTypeDeclaration` e di <xref:System.CodeDom.CodeTypeMember> comprende dati personalizzati, come la proprietà <xref:System.CodeDom.CodeObject.UserData%2A>, di cui è eseguito il cast al tipo `IDataContractSurrogate`.  
  
 Nell'esempio precedente vengono eseguite alcune modifiche sullo schema importato.Il codice mantiene membri privati del tipo originale utilizzando un surrogato.Il modificatore di accesso predefinito durante l'importazione di uno schema è `public`.Pertanto, tutti i membri dello schema surrogato saranno pubblici a meno che non vengano modificati, come in questo esempio.Durante l'esportazione, vengono inseriti nei metadati dati personalizzati relativi ai membri privati.Nell'esempio vengono cercati i dati personalizzati, viene verificato se il modificatore di accesso è privato e il membro appropriato viene quindi cambiato in privato mediante l'impostazione dei relativi attributi.Senza questa personalizzazione, il membro `numpens` verrebbe definito pubblico anziché privato.  
  
### Metodo GetKnownCustomDataTypes  
 Questo metodo ottiene dallo schema tipi di dati personalizzati definiti.È facoltativo per l'importazione dello schema.  
  
 Il metodo  viene chiamato all'inizio dell'esportazione e dell'importazione dello schema.Restituisce i tipi di dati personalizzati utilizzati nello schema esportato o importato.Viene passato a <xref:System.Collections.ObjectModel.Collection%601> \(il parametro `customDataTypes`\), che è una raccolta di tipi.Il metodo aggiunge ulteriori tipi conosciuti a questa raccolta.I tipi di dati personalizzati conosciuti sono indispensabili per attivare la serializzazione e la deserializzazione dei dati personalizzati utilizzando la classe <xref:System.Runtime.Serialization.DataContractSerializer>.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Tipi conosciuti di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md).  
  
## Implementazione di un surrogato  
 Per utilizzare il surrogato del contratto dati all'interno di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], è necessario attenersi a una procedura speciale.  
  
### Per utilizzare un surrogato per serializzazione e deserializzazione  
 Utilizzare la classe <xref:System.Runtime.Serialization.DataContractSerializer> per eseguire serializzazione e deserializzazione di dati con il surrogato.L'elemento <xref:System.Runtime.Serialization.DataContractSerializer> viene creato da <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>.È necessario specificare anche il surrogato.  
  
##### Per implementare serializzazione e deserializzazione  
  
1.  Creare un'istanza di <xref:System.ServiceModel.ServiceHost> per il servizio.Per istruzioni complete, vedere [Programmazione WCF di base](../../../../docs/framework/wcf/basic-wcf-programming.md).  
  
2.  Per ogni <xref:System.ServiceModel.Description.ServiceEndpoint> dell'host del servizio specificato, cercare il rispettivo elemento <xref:System.ServiceModel.Description.OperationDescription>.  
  
3.  Esaminare i comportamenti dell'operazione per stabilire se viene trovata un'istanza di <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>.  
  
4.  Se viene trovato un elemento <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>, impostarne la proprietà <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.DataContractSurrogate%2A> su un'istanza nuova del surrogato.Se non viene trovato alcun elemento <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>, creare un'istanza nuova e impostare il membro <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.DataContractSurrogate%2A> del nuovo comportamento su una nuova istanza del surrogato.  
  
5.  Infine, aggiungere questo nuovo comportamento ai comportamenti dell'operazione correnti, come nell'esempio seguente:  
  
     [!code-csharp[C_IDataContractSurrogate#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#8)]  
  
### Per utilizzare un surrogato per l'importazione dei metadati  
 Durante l'importazione di metadati come WSDL e XSD per la generazione di codice del lato client, è necessario aggiungere il surrogato al componente responsabile della generazione di codice dallo schema XSD, <xref:System.Runtime.Serialization.XsdDataContractImporter>.A questo scopo, modificare direttamente l'elemento <xref:System.ServiceModel.Description.WsdlImporter> utilizzato per importare i metadati.  
  
##### Per implementare un surrogato per l'importazione dei metadati  
  
1.  Importare i metadati utilizzando la classe <xref:System.ServiceModel.Description.WsdlImporter>.  
  
2.  Utilizzare il metodo <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> per verificare se è stato definito un elemento <xref:System.Runtime.Serialization.XsdDataContractImporter>.  
  
3.  Se il metodo <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> restituisce `false`, creare un nuovo elemento <xref:System.Runtime.Serialization.XsdDataContractImporter> e impostarne la proprietà <xref:System.Runtime.Serialization.XsdDataContractImporter.Options%2A> su una nuova istanza della classe <xref:System.Runtime.Serialization.ImportOptions>.In caso contrario, utilizzare l'unità di importazione restituita dal parametro `out` del metodo <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A>.  
  
4.  Se per l'elemento <xref:System.Runtime.Serialization.XsdDataContractImporter> non sono definite istanze della classe <xref:System.Runtime.Serialization.ImportOptions>, impostare la proprietà affinché sia una nuova istanza della classe <xref:System.Runtime.Serialization.ImportOptions>.  
  
5.  Impostare la proprietà <xref:System.Runtime.Serialization.ImportOptions.DataContractSurrogate%2A> di <xref:System.Runtime.Serialization.ImportOptions> dell'elemento <xref:System.Runtime.Serialization.XsdDataContractImporter> su una nuova istanza del surrogato.  
  
6.  Aggiungere l'elemento <xref:System.Runtime.Serialization.XsdDataContractImporter> alla raccolta restituita dalla proprietà <xref:System.ServiceModel.Description.MetadataExporter.State%2A> di <xref:System.ServiceModel.Description.WsdlImporter> \(ereditato dalla classe <xref:System.ServiceModel.Description.MetadataExporter>\).  
  
7.  Utilizzare il metodo <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A> di <xref:System.ServiceModel.Description.WsdlImporter> per importare tutti i contratti dati all'interno dello schema.Durante l'ultimo passaggio, viene generato codice dagli schemi caricati chiamando il surrogato.  
  
     [!code-csharp[C_IDataContractSurrogate#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#9)]  
  
### Per utilizzare un surrogato per l'esportazione dei metadati  
 Per impostazione predefinita, quando si esportano metadati da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per un servizio, è necessario che vengano generati sia schemi WSDL che XSD.È necessario che il surrogato venga aggiunto al componente responsabile della generazione di schema XSD per i tipi di contratto dati, <xref:System.Runtime.Serialization.XsdDataContractExporter>.A tale scopo, utilizzare un comportamento che implementi <xref:System.ServiceModel.Description.IWsdlExportExtension> per modificare l'elemento <xref:System.ServiceModel.Description.WsdlExporter> oppure modificare direttamente l'elemento <xref:System.ServiceModel.Description.WsdlExporter> utilizzato per esportare metadati.  
  
##### Per utilizzare un surrogato per l'esportazione dei metadati  
  
1.  Creare un nuovo elemento <xref:System.ServiceModel.Description.WsdlExporter> oppure utilizzare il parametro `wsdlExporter` passato al metodo <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportContract%2A>.  
  
2.  Utilizzare la funzione <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> per verificare se è stato definito un elemento <xref:System.Runtime.Serialization.XsdDataContractExporter>.  
  
3.  Se <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> restituisce `false`, creare un nuovo elemento <xref:System.Runtime.Serialization.XsdDataContractExporter> con gli schemi XML generati da <xref:System.ServiceModel.Description.WsdlExporter> e aggiungerlo alla raccolta restituita dalla proprietà <xref:System.ServiceModel.Description.MetadataExporter.State%2A> dell'elemento <xref:System.ServiceModel.Description.WsdlExporter>.In caso contrario, utilizzare l'unità di esportazione restituita dal parametro `out` del metodo <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A>.  
  
4.  Se per l'elemento <xref:System.Runtime.Serialization.XsdDataContractExporter> non sono definite istanze della classe <xref:System.Runtime.Serialization.ExportOptions>, impostare la proprietà <xref:System.Runtime.Serialization.XsdDataContractExporter.Options%2A> su una nuova istanza della classe <xref:System.Runtime.Serialization.ExportOptions>.  
  
5.  Impostare la proprietà <xref:System.Runtime.Serialization.ExportOptions.DataContractSurrogate%2A> di <xref:System.Runtime.Serialization.ExportOptions> dell'elemento <xref:System.Runtime.Serialization.XsdDataContractExporter> su una nuova istanza del surrogato.I passaggi successivi per l'esportazione dei metadati non richiedono modifiche.  
  
     [!code-csharp[C_IDataContractSurrogate#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#10)]  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Runtime.Serialization.IDataContractSurrogate>   
 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>   
 <xref:System.Runtime.Serialization.ImportOptions>   
 <xref:System.Runtime.Serialization.ExportOptions>   
 [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)