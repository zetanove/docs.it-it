---
title: "Controllo delle versioni dei contratti dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "contratti dati [WCF], controllo delle versioni"
  - "controllo delle versioni [WCF]"
  - "controllo delle versioni [WCF], contratti dati"
ms.assetid: 4a0700cb-5f5f-4137-8705-3a3ecf06461f
caps.latest.revision: 35
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 35
---
# Controllo delle versioni dei contratti dati
Lo sviluppo delle applicazioni implica la modifica dei contratti dati utilizzati dai servizi.  In questo argomento viene illustrato come controllare le versioni dei contratti dati.  Vengono descritti i meccanismi di controllo delle versioni dei contratti dati.  Per una panoramica completa e per istruzioni sul controllo delle versioni, vedere [Procedure consigliate: controllo delle versioni del contratto dati](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md).  
  
## Modifiche che causano interruzione e modifiche chenon causano interruzione  
 Le modifiche a un contratto dati possono determinare interruzioni oppure no.  Quando un contratto dati viene modificato in modo che non determini interruzioni, un'applicazione che utilizza la versione precedente del contratto può comunicare con un'applicazione che utilizza la versione più recente e viceversa.  Una modifica che determina interruzioni, invece, può impedire la comunicazione in una o in entrambe le direzioni.  
  
 Qualsiasi modifica a un tipo che non influisce sulla modalità con cui viene trasmessa e ricevuta non determina interruzioni.  Tali modifiche non cambiano il contratto dati ma solo il tipo sottostante.  È possibile, ad esempio, modificare il nome di un campo in modo che non determini interruzioni se si imposta la proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A> di <xref:System.Runtime.Serialization.DataMemberAttribute> sul nome della versione precedente.  Nel codice seguente viene illustrata la versione 1 di un contratto dati.  
  
 [!code-csharp[C_DataContractVersioning#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractversioning/cs/source.cs#1)]
 [!code-vb[C_DataContractVersioning#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractversioning/vb/source.vb#1)]  
  
 Nel codice seguente viene illustrata una modifica che non determina interruzioni.  
  
 [!code-csharp[C_DataContractVersioning#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractversioning/cs/source.cs#2)]
 [!code-vb[C_DataContractVersioning#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractversioning/vb/source.vb#2)]  
  
 Alcune modifiche cambiano i dati trasmessi ma possono determinare interruzioni oppure no.  Le modifiche seguenti determinano sempre interruzioni:  
  
-   Modifica del valore <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> o <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A> di un contratto dati.  
  
-   Modifica dell'ordine di membri dati tramite la proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> di <xref:System.Runtime.Serialization.DataMemberAttribute>.  
  
-   Ridenominazione di un membro dati.  
  
-   Modifica del contratto dati di un membro dati.  La modifica, ad esempio, del tipo di membro dati da un numero intero a una stringa o da un tipo con un contratto dati denominato "Customer" a un tipo con un contratto dati denominato "Person".  
  
 Sono possibili inoltre le modifiche seguenti.  
  
## Aggiunta e rimozione di membri dati  
 Nella maggior parte dei casi, l'aggiunta o la rimozione di un membro dati non è una modifica che determina interruzioni, a meno che non venga richiesta una rigorosa conformità allo schema \(convalide di nuove istanze a fronte dello schema precedente\).  
  
 Quando un tipo con un campo aggiuntivo viene deserializzato in un tipo con un campo mancante, le informazioni aggiuntive vengono ignorate.  Può essere archiviato anche a fini di sequenze di andata e ritorno. Per ulteriori informazioni, vedere [Contratti dati compatibili con versioni successive](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md).  
  
 Quando un tipo con un campo mancante viene deserializzato in un tipo con un campo aggiuntivo, il campo aggiuntivo viene lasciato con il valore predefinito, generalmente zero o `null`.  Il valore predefinito può essere modificato. Per ulteriori informazioni, vedere [Callback di serializzazione a tolleranza di versione](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md).  
  
 È possibile, ad esempio, utilizzare la classe `CarV1` in un client e la classe `CarV2` in un servizio o è possibile utilizzare la classe `CarV1` in un servizio e la classe `CarV2` in un client.  
  
 [!code-csharp[C_DataContractVersioning#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractversioning/cs/source.cs#3)]
 [!code-vb[C_DataContractVersioning#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractversioning/vb/source.vb#3)]  
  
 L'endpoint della versione 2 può inviare correttamente dati all'endpoint della versione 1.  La serializzazione della versione 2 del contratto dati `Car` restituisce un XML simile all'esempio seguente.  
  
```  
<Car>  
    <Model>Porsche</Model>  
    <HorsePower>300</HorsePower>  
</Car>  
```  
  
 Il motore di deserializzazione nella versione 1 non trova un membro dati corrispondente al campo `HorsePower` e ignora quei dati.  
  
 L'endpoint della versione 1 può, inoltre, inviare dati all'endpoint della versione 2.  La serializzazione della versione 1 del contratto dati `Car` restituisce un XML simile all'esempio seguente.  
  
```  
<Car>  
    <Model>Porsche</Model>  
</Car>  
```  
  
 Il deserializzatore della versione 2 non sa su quale valore impostare il campo `HorsePower`, poiché non ci sono dati corrispondenti nel codice XML in ingresso.  Il campo viene impostato sul valore predefinito 0.  
  
## Membri dati obbligatori  
 Un membro dati può essere contrassegnato come obbligatorio impostando la proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> di <xref:System.Runtime.Serialization.DataMemberAttribute> su `true`.  Se dati obbligatori vanno persi durante la deserializzazione, anziché impostare il membro dati sul valore predefinito, viene generata un'eccezione.  
  
 L'aggiunta di un membro dati obbligatorio è una modifica che determina interruzioni,  ovvero il tipo più recente può essere ancora inviato agli endpoint con il tipo precedente ma non viceversa.  La rimozione di un membro dati contrassegnato come obbligatorio in qualsiasi versione precedente è una modifica che determina interruzioni.  
  
 La modifica del valore della proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> da `true` a `false` non determina interruzioni ma la modifica di quest'ultima da `false` a `true` può determinare interruzioni se eventuali versioni precedenti del tipo non dispongono del membro dati in questione.  
  
> [!NOTE]
>  Sebbene la proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> sia impostata su `true`, i dati in ingresso potrebbero essere Null o zero e per gestire questa possibilità è necessario predisporre un tipo.  Non utilizzare <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> come meccanismo di sicurezza contro dati in ingresso non validi.  
  
## Valori predefiniti omessi  
 È possibile, sebbene non consigliato, impostare la proprietà `EmitDefaultValue` nell'attributo DataMemberAttribute su `false`, come descritto in [Valori predefiniti dei membri dati](../../../../docs/framework/wcf/feature-details/data-member-default-values.md).  Se questa impostazione è `false`, il membro dati non verrà creato se è impostato sul valore predefinito \(generalmente Null o zero\).  L'incompatibilità con i membri dati obbligatori in versioni diverse è dovuta a due motivi:  
  
-   Un contratto dati con un membro dati obbligatorio in una versione non può ricevere dati predefiniti \(Null o zero\) da una versione diversa nella quale il valore del membro dati `EmitDefaultValue` è impostato su `false`.  
  
-   Un membro dati obbligatorio con il valore `EmitDefaultValue` impostato su `false` non può essere utilizzato per serializzare il valore predefinito \(Null o zero\) ma può ricevere tale valore nella deserializzazione.  Questo crea un problema di sequenze di andata e ritorno \(i dati possono essere letti in ingresso ma non possono essere scritti in uscita\).  Se, pertanto, `IsRequired` è `true` e `EmitDefaultValue` è `false` in una versione, la stessa combinazione deve applicarsi a tutte le altre versioni in modo che nessuna versione del contratto dati sia in grado di produrre un valore che non comporti sequenze di andata e ritorno.  
  
## Considerazioni sugli schemi  
 Per una spiegazione sugli schemi prodotti per i tipi di contratto dati, vedere [Riferimento allo schema del contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md).  
  
 Lo schema prodotto da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per i tipi di contratto dati non fornisce il controllo delle versioni.  Ovvero, lo schema esportato da una certa versione di un tipo contiene solo i membri dati presenti in quella versione.  L'implementazione dell'interfaccia <xref:System.Runtime.Serialization.IExtensibleDataObject> non modifica lo schema per un tipo.  
  
 Per impostazione predefinita, i membri dati vengono esportati nello schema come elementi facoltativi,  quindi il valore di `minOccurs` \(attributo XML\) è impostato su 0.  I membri dati obbligatori vengono esportati con `minOccurs` impostato su 1.  
  
 Molte delle modifiche che si ritiene non determinino interruzioni, di fatto le provocano nel caso in cui sia richiesta una stretta osservanza dello schema.  Nell'esempio precedente, un'istanza `CarV1` con il solo elemento `Model` eseguirebbe la convalida a fronte dello schema `CarV2` che dispone degli elementi `Model` e `Horsepower`, entrambi facoltativi.  Non è tuttavia vero il contrario, ovvero un'istanza `CarV2` non riuscirebbe a eseguire la convalida a fronte dello schema `CarV1`.  
  
 Le sequenze di andata e ritorno comportano inoltre alcune considerazioni aggiuntive.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la sezione "Considerazioni sugli schemi" in [Contratti dati compatibili con versioni successive](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md).  
  
### Altre modifiche consentite  
 L'implementazione dell'interfaccia <xref:System.Runtime.Serialization.IExtensibleDataObject> è una modifica che non determina interruzioni.  Il supporto delle sequenze di andata e ritorno, tuttavia, non esiste per versioni del tipo precedenti alla versione nella quale <xref:System.Runtime.Serialization.IExtensibleDataObject> è stato implementato.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Contratti dati compatibili con versioni successive](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md).  
  
## Enumerazioni  
 L'aggiunta o la rimozione di un membro di enumerazione è una modifica che determina interruzioni.  La modifica del nome di un membro di enumerazione determina interruzioni, a meno che il nome del contratto non sia identico a quello della versione precedente utilizzando l'attributo `EnumMemberAtttribute`.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Tipi di enumerazioni nei contratti dati](../../../../docs/framework/wcf/feature-details/enumeration-types-in-data-contracts.md).  
  
## Raccolte  
 La maggior parte delle modifiche di raccolte non determina interruzioni poiché la maggior parte dei tipi di raccolta sono intercambiabili tra loro nel modello del contratto dati.  La trasformazione di una raccolta non personalizzata in una personalizzata e viceversa è, tuttavia, una modifica che determina interruzioni.  Inoltre, modificare le impostazioni di personalizzazione della raccolta è una modifica sostanziale che implica il cambiamento del nome del contratto dati e dello spazio dei nomi, del nome dell'elemento ripetuto, del nome dell'elemento key e del nome dell'elemento value.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lla personalizzazione delle raccolte, vedere [Tipi di raccolta nei contratti dati](../../../../docs/framework/wcf/feature-details/collection-types-in-data-contracts.md).    
Ovviamente, la modifica del contratto dati del contenuto di una raccolta, ad esempio il passaggio da un elenco di numeri interi a un elenco di stringhe, è sostanziale.  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A>   
 <xref:System.Runtime.Serialization.DataMemberAttribute>   
 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>   
 <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>   
 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>   
 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A>   
 <xref:System.Runtime.Serialization.SerializationException>   
 <xref:System.Runtime.Serialization.IExtensibleDataObject>   
 [Callback di serializzazione a tolleranza di versione](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)   
 [Procedure consigliate: controllo delle versioni del contratto dati](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)   
 [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)   
 [Equivalenza dei contratti dati](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)   
 [Contratti dati compatibili con versioni successive](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)