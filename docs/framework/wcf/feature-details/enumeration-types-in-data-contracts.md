---
title: "Tipi di enumerazioni nei contratti dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contratti dati [WCF], tipi di enumerazione"
ms.assetid: b5d694da-68cb-4b74-a5fb-75108a68ec3b
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Tipi di enumerazioni nei contratti dati
Le enumerazioni possono essere espresse nel modello del contratto dati.  In questo argomento vengono esaminati molti esempi che spiegano il modello di programmazione.  
  
## Nozioni fondamentali sull'enumerazione  
 Per usare i tipi di enumerazione nel modello del contratto dati, applicare l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> al tipo.  Applicare quindi l'attributo <xref:System.Runtime.Serialization.EnumMemberAttribute> a ogni membro che deve essere incluso nel contratto dati.  
  
 Nell'esempio che segue vengono illustrate due classi.  La prima usa l'enumerazione e la seconda definisce l'enumerazione.  
  
 [!code-csharp[c_DataContractEnumerations#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#1)]
 [!code-vb[c_DataContractEnumerations#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#1)]  
  
 Un'istanza della classe `Car` può essere inviata o ricevuta solo se il campo `condition` è impostato su uno dei valori `New`, `Used` o `Rental`.  Se `condition` è `Broken` o `Stolen`, viene generata un'eccezione <xref:System.Runtime.Serialization.SerializationException>.  
  
 È possibile usare come al solito le proprietà <xref:System.Runtime.Serialization.DataContractAttribute> \(<xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> e <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>\) per i contratti dati dell'enumerazione.  
  
### Valori membro dell'enumerazione  
 In genere il contratto dati include i nomi dei membri dell'enumerazione, non i valori numerici.  Tuttavia, quando si usa il modello del contratto dati, se il lato ricevente è un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], lo schema esportato mantiene i valori numerici.  La situazione è diversa quando si usa [Utilizzo della classe XmlSerializer](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md).  
  
 Nell'esempio precedente, se `condition` è impostato su `Used` e i dati vengono serializzati in XML, il codice XML risultante è `<condition>Used</condition>``<condition>1</condition>` e non .  Di conseguenza, il contratto dati seguente è equivalente al contratto dati di `CarConditionEnum`.  
  
 [!code-csharp[c_DataContractEnumerations#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#2)]
 [!code-vb[c_DataContractEnumerations#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#2)]  
  
 Ad esempio, è possibile usare `CarConditionEnum` sul lato mittente e `CarConditionWithNumbers` sul lato ricevente.  Sebbene il lato mittente usi il valore "1" per `Used` e il lato ricevente usi il valore "20", la rappresentazione XML è `<condition>Used</condition>` per entrambi i lati.  
  
 Per essere incluso nel contratto dati, è necessario applicare l'attributo <xref:System.Runtime.Serialization.EnumMemberAttribute>.  In [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], è sempre possibile applicare il valore speciale 0 \(zero\) a un'enumerazione che è anche il valore predefinito per qualsiasi enumerazione.  Tuttavia, anche il valore speciale zero non può essere serializzato a meno che sia contrassegnato con l'attributo <xref:System.Runtime.Serialization.EnumMemberAttribute>.  
  
 Esistono due eccezioni a questo contesto:  
  
-   Enumerazioni di flag \(esaminate più avanti in questo argomento\).  
  
-   Membri dati dell'enumerazione con la proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> impostata su `false` \(in tal caso l'enumerazione con valore zero viene omessa dai dati serializzati\).  
  
### Personalizzazione dei valori membro dell'enumerazione  
 È possibile personalizzare il valore del membro dell'enumerazione che costituisce una parte del contratto dati usando la proprietà <xref:System.Runtime.Serialization.EnumMemberAttribute.Value%2A> dell'attributo <xref:System.Runtime.Serialization.EnumMemberAttribute>.  
  
 Ad esempio, il contratto dati seguente è equivalente anche al contratto dati di `CarConditionEnum`.  
  
 [!code-csharp[c_DataContractEnumerations#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#3)]
 [!code-vb[c_DataContractEnumerations#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#3)]  
  
 Una volta serializzato, il valore di `PreviouslyOwned` contiene la rappresentazione XML `<condition>Used</condition>`.  
  
## Enumerazioni semplici  
 È anche possibile serializzare i tipi di enumerazione ai quali non è stato applicato l'attributo <xref:System.Runtime.Serialization.DataContractAttribute>.  Tali tipi di enumerazione vengono trattati esattamente come descritto in precedenza, con l'eccezione che ogni membro, a cui non è applicato l'attributo <xref:System.NonSerializedAttribute>, viene trattato come se fosse stato applicato l'attributo <xref:System.Runtime.Serialization.EnumMemberAttribute>.  Ad esempio, l'enumerazione seguente contiene implicitamente un contratto dati equivalente all'esempio `CarConditionEnum` precedente.  
  
 [!code-csharp[c_DataContractEnumerations#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#6)]
 [!code-vb[c_DataContractEnumerations#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#6)]  
  
 È possibile usare le enumerazioni semplici quando non è necessario personalizzare lo spazio dei nomi e il nome del contratto dati dell'enumerazione e i valori membro dell'enumerazione.  
  
#### Nota sulle enumerazioni semplici  
 L'applicazione dell'attributo <xref:System.Runtime.Serialization.EnumMemberAttribute> alle enumerazioni semplici non produce alcun effetto.  
  
 È indifferente se l'attributo <xref:System.SerializableAttribute> viene applicato o meno all'enumerazione.  
  
 Il fatto che la classe <xref:System.Runtime.Serialization.DataContractSerializer> si basa sull'applicazione dell'attributo <xref:System.NonSerializedAttribute> ai membri dell'enumerazione è diverso dal comportamento di <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> e <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>.  Entrambi i serializzatori ignorano l'attributo <xref:System.NonSerializedAttribute>.  
  
## Enumerazioni di flag  
 È possibile applicare l'attributo <xref:System.FlagsAttribute> alle enumerazioni.  In tal caso, è possibile inviare o ricevere simultaneamente un elenco di zero o più valori di enumerazione.  
  
 A tale scopo, applicare l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> all'enumerazione del flag e quindi contrassegnare tutti i membri che sono potenze di due con l'attributo <xref:System.Runtime.Serialization.EnumMemberAttribute>.  Si noti che per usare un'enumerazione del flag, la progressione deve essere una sequenza ininterrotta di potenze di 2 \(ad esempio, 1, 2, 4, 8, 16, 32, 64\).  
  
 I passaggi seguenti si applicano all'invio del valore dell'enumerazione di un flag:  
  
1.  Tentare di individuare un membro dell'enumerazione \(a cui è applicato l'attributo <xref:System.Runtime.Serialization.EnumMemberAttribute>\) associato al valore numerico.  Se disponibile, inviare un elenco che contenga solo quel membro.  
  
2.  Tentare di suddividere il valore numerico in una somma tale che vi siano membri dell'enumerazione \(ai quali è applicato l'attributo <xref:System.Runtime.Serialization.EnumMemberAttribute>\) associati a ogni parte della somma.  Inviare l'elenco di tutti questi membri.  Poiché viene usato l'*algoritmo di tipo greedy* per trovare tale somma, non è possibile garantire che tale somma venga trovata anche se è presente.  Per evitare questo problema, verificare che i valori numerici dei membri dell'enumerazione siano potenze di due.  
  
3.  Se i due passaggi precedenti hanno esito negativo e il valore numerico è diverso da zero, generare un'eccezione <xref:System.Runtime.Serialization.SerializationException>.  Se il valore numerico è zero, inviare l'elenco vuoto.  
  
### Esempio  
 L'esempio di enumerazione seguente può essere usato in un'operazione di flag.  
  
 [!code-csharp[c_DataContractEnumerations#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#4)]
 [!code-vb[c_DataContractEnumerations#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#4)]  
  
 I valori nell'esempio seguente vengono serializzati come indicato.  
  
 [!code-csharp[c_DataContractEnumerations#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#5)]
 [!code-vb[c_DataContractEnumerations#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#5)]  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)   
 [Specifica del trasferimento di dati nei contratti di servizio](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)