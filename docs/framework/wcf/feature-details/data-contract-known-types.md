---
title: "Tipi conosciuti di contratto dati | Microsoft Docs"
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
  - "contratti dati [WCF], tipi sconosciuti"
  - "KnownTypeAttribute [WCF]"
  - "KnownTypes [WCF]"
ms.assetid: 1a0baea1-27b7-470d-9136-5bbad86c4337
caps.latest.revision: 42
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 42
---
# Tipi conosciuti di contratto dati
La classe <xref:System.Runtime.Serialization.KnownTypeAttribute> consente di specificare, in anticipo, i tipi che devono essere presi in considerazione durante la deserializzazione. Per un esempio pratico, vedere l'esempio [Tipi conosciuti](../../../../docs/framework/wcf/samples/known-types.md).  
  
 In genere, quando si passano parametri e valori restituiti tra un client e un servizio, entrambi gli endpoint condividono tutti i contratti dati dei dati da trasmettere. Nelle circostanze seguenti, tuttavia, la situazione è diversa:  
  
-   Il contratto dati inviato deriva dal contratto dati previsto.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la sezione sull'ereditarietà in [Equivalenza dei contratti dati](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md). In tale caso, i dati trasmessi non hanno lo stesso contratto dati previsto dall'endpoint di destinazione.  
  
-   Il tipo dichiarato per le informazioni da trasmettere è un'interfaccia, anziché una classe, una struttura o un'enumerazione. Non è pertanto possibile conoscere in anticipo quale tipo che implementa l'interfaccia viene effettivamente inviato e, di conseguenza, l'endpoint di destinazione non è in grado di determinare, in anticipo, il contratto dati per i dati trasmessi.  
  
-   Il tipo dichiarato per le informazioni da trasmettere è <xref:System.Object>. Dato che ogni tipo eredita da <xref:System.Object> e che non è possibile sapere in anticipo qual è il tipo effettivamente inviato, l'endpoint di destinazione non è in grado di determinare in anticipo il contratto dati per i dati trasmessi. Questo è un caso speciale del primo elemento: ogni contratto dati deriva dall'impostazione predefinita, un contratto dati vuoto generato per <xref:System.Object>.  
  
-   Alcuni tipi, tra cui i tipi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], dispongono di membri che rientrano in una delle tre categorie precedenti.<xref:System.Collections.Hashtable>, ad esempio, utilizza <xref:System.Object> per memorizzare gli oggetti effettivi nella tabella hash. Durante la serializzazione di questi tipi, il lato di destinazione non è in grado di determinare in anticipo il contratto dati per questi membri.  
  
## Classe KnownTypeAttribute  
 Quando i dati arrivano a un endpoint di destinazione, il runtime di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tenta di deserializzarli in un'istanza di un tipo Common Language Runtime \(CLR\). Il tipo di cui viene creata l'istanza per la deserializzazione viene scelto controllando innanzitutto il messaggio in arrivo per determinare il contratto dati al quale è compatibile con il contenuto del messaggio. Il motore di deserializzazione tenta quindi di trovare un tipo CLR che implementi un contratto dati conforme al contenuto del messaggio. Il set di tipi di candidato consentiti dal motore di deserializzazione durante questo processo viene chiamato set di "tipi noti" del deserializzatore.  
  
 Un modo per consentire al motore di deserializzazione di conoscere un tipo consiste nell'utilizzare <xref:System.Runtime.Serialization.KnownTypeAttribute>. L'attributo non può essere applicato a membri dati singoli, ma solo a tutti i tipi di contratto dati. L'attributo viene applicato a un *tipo esterno* che può essere una classe o una struttura. Nell'utilizzo più elementare, l'applicazione dell'attributo specifica un tipo come "tipo conosciuto". Ciò fa sì che il tipo conosciuto sia parte di questo set di tipi noti ogni volta che viene deserializzato un oggetto del tipo esterno o un qualsiasi oggetto a cui si faccia riferimento tramite i suoi membri. Allo stesso tipo è possibile applicare più di un attributo <xref:System.Runtime.Serialization.KnownTypeAttribute>.  
  
## Tipi conosciuti e primitivi  
 I tipi primitivi, così come certi tipi trattati come primitivi \(ad esempio, <xref:System.DateTime> e <xref:System.Xml.XmlElement>\) sono sempre "conosciuti" e non è mai necessario aggiungerli tramite questo meccanismo. Le matrici di tipi primitivi, tuttavia, devono essere aggiunte in modo esplicito. La maggior parte delle raccolte è considerata equivalente alle matrici. \(La raccolte non generiche sono considerate equivalenti alle matrici di <xref:System.Object>\). Per un esempio di utilizzo di primitivi, matrici di primitivi e raccolte di primitivi, vedere l'esempio 4.  
  
> [!NOTE]
>  A differenza di altri tipi di primitivi, la struttura <xref:System.DateTimeOffset> non è un tipo conosciuto per impostazione predefinita, pertanto deve essere aggiunta manualmente all'elenco dei tipi noti.  
  
## Esempi  
 Negli esempi seguenti viene illustrata la classe <xref:System.Runtime.Serialization.KnownTypeAttribute> utilizzata.  
  
#### Esempio 1  
 Esistono tre classi con una relazione di ereditarietà.  
  
 [!code-csharp[C_KnownTypeAttribute#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#1)]
 [!code-vb[C_KnownTypeAttribute#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#1)]  
  
 La classe `CompanyLogo` seguente può essere serializzata, ma non può essere deserializzata se il membro `ShapeOfLogo` è impostato su un `CircleType` o su un oggetto `TriangleType`, perché il motore di deserializzazione non riconosce alcun tipo con i nomi del contratto dati "Circle" o "Triangle".  
  
 [!code-csharp[C_KnownTypeAttribute#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#2)]
 [!code-vb[C_KnownTypeAttribute#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#2)]  
  
 La modalità corretta per scrivere il tipo `CompanyLogo` è illustrata nel codice seguente.  
  
 [!code-csharp[C_KnownTypeAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#3)]
 [!code-vb[C_KnownTypeAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#3)]  
  
 Ogni volta che il tipo esterno `CompanyLogo2` viene deserializzato, il motore di deserializzazione viene a conoscenza di `CircleType` e `TriangleType` e, pertanto, è in grado di cercare i tipi corrispondenti per i contratti dati "Circle" e "Triangle".  
  
#### Esempio 2  
 Nell'esempio seguente, anche se sia `CustomerTypeA` che `CustomerTypeB` hanno il contratto dati `Customer`, viene creata un'istanza di `CustomerTypeB` ogni volta che viene deserializzato un `PurchaseOrder`, perché solo `CustomerTypeB` è conosciuto al motore di deserializzazione.  
  
 [!code-csharp[C_KnownTypeAttribute#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#4)]
 [!code-vb[C_KnownTypeAttribute#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#4)]  
  
#### Esempio 3  
 Nell'esempio seguente, un <xref:System.Collections.Hashtable> memorizza internamente il contenuto come <xref:System.Object>. Per deserializzare correttamente una tabella hash, il motore di deserializzazione deve conoscere il set dei tipi possibili che possono verificarsi. In questo caso, si sa in anticipo che solo gli oggetti `Book` e `Magazine` vengono memorizzati in `Catalog`, pertanto vengono aggiunti utilizzando l'attributo <xref:System.Runtime.Serialization.KnownTypeAttribute>.  
  
 [!code-csharp[C_KnownTypeAttribute#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#5)]
 [!code-vb[C_KnownTypeAttribute#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#5)]  
  
#### Esempio 4  
 Nell'esempio seguente, un contratto dati memorizza un numero e un'operazione da eseguire sul numero. Il membro dati `Numbers` può essere un numero Integer, una matrice di numeri Integer o un oggetto <xref:System.Collections.Generic.List%601> che contiene numeri Integer.  
  
> [!CAUTION]
>  Questo funzionerà sul lato client solo se SVCUTIL.EXE è utilizzato per generare un proxy WCF. SVCUTIL.EXE recupera metadati dal servizio inclusi tutti i tipi noti. Senza queste informazioni un client non sarà in grado di deserializzare i tipi.  
  
 [!code-csharp[C_KnownTypeAttribute#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#6)]
 [!code-vb[C_KnownTypeAttribute#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#6)]  
  
 Questo è il codice dell'applicazione.  
  
 [!code-csharp[C_KnownTypeAttribute#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#7)]
 [!code-vb[C_KnownTypeAttribute#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#7)]  
  
## Tipi conosciuti, ereditarietà e interfacce  
 Quando un tipo conosciuto è associato a un particolare tipo utilizzando l'attributo `KnownTypeAttribute`, il tipo conosciuto viene associato anche a tutti i tipi derivati di quel tipo. Si consideri, ad esempio, il codice seguente.  
  
 [!code-csharp[C_KnownTypeAttribute#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#8)]
 [!code-vb[C_KnownTypeAttribute#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#8)]  
  
 La classe `DoubleDrawing` non richiede l'attributo `KnownTypeAttribute` per utilizzare `Square` e `Circle` nel campo `AdditionalShape`, perché nella classe di base \(`Drawing`\) questi attributi sono già applicati.  
  
 I tipi noti possono essere associati solo a classi e strutture, non a interfacce.  
  
## Tipi conosciuti che utilizzano metodi generici aperti  
 Potrebbe essere necessario aggiungere un tipo generico come tipo conosciuto. Non è tuttavia possibile passare un tipo generico aperto come parametro all'attributo `KnownTypeAttribute`.  
  
 Questo problema può essere risolto utilizzando un meccanismo alternativo, ovvero scrivere un metodo che restituisca un elenco di tipi da aggiungere alla raccolta di tipi noti. Specificare quindi il nome del metodo come argomento di tipo stringa per l'attributo `KnownTypeAttribute`, per far fronte ad alcune restrizioni.  
  
 Il metodo deve esistere nel tipo al quale è applicato l'attributo `KnownTypeAttribute`, deve essere statico, non deve accettare parametri e deve restituire un oggetto che possa essere assegnato a <xref:System.Collections.IEnumerable> di <xref:System.Type>.  
  
 Non è possibile combinare l'attributo `KnownTypeAttribute` con un nome di metodo e attributi `KnownTypeAttribute` con i tipi effettivi sullo stesso tipo. Non è inoltre possibile applicare più di un `KnownTypeAttribute` con un nome di metodo allo stesso tipo.  
  
 Fare riferimento alla classe seguente.  
  
 [!code-csharp[C_KnownTypeAttribute#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#9)]
 [!code-vb[C_KnownTypeAttribute#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#9)]  
  
 Il campo `theDrawing` contiene istanze di una classe `ColorDrawing` generica e una classe `BlackAndWhiteDrawing`generica, che ereditano entrambe da una classe `Drawing` generica. In genere, è necessario aggiungerle entrambe a tipi noti, ma quella che segue non è una sintassi valida per gli attributi.  
  
```csharp  
// Invalid syntax for attributes:  
// [KnownType(typeof(ColorDrawing<T>))]  
// [KnownType(typeof(BlackAndWhiteDrawing<T>))]  
```  
  
```vb  
' Invalid syntax for attributes:  
' <KnownType(GetType(ColorDrawing(Of T))), _  
' KnownType(GetType(BlackAndWhiteDrawing(Of T)))>  
```  
  
 Per restituire questi tipi, è pertanto necessario creare un metodo. Nel codice seguente viene illustrato il modo corretto per scrivere questo tipo.  
  
 [!code-csharp[C_KnownTypeAttribute#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#10)]
 [!code-vb[C_KnownTypeAttribute#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#10)]  
  
## Altri modi per aggiungere tipi noti.  
 I tipi noti possono essere aggiunti anche tramite un file di configurazione. Ciò è utile quando non si controlla il tipo che richiede tipi noti per una deserializzazione corretta, ad esempio quando si utilizzano librerie dei tipi di terze parti con [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
 Nel file di configurazione seguente viene illustrato come specificare un tipo conosciuto in un file di configurazione.  
  
 `<configuration>`  
  
 `<system.runtime.serialization>`  
  
 `<dataContractSerializer>`  
  
 `<declaredTypes>`  
  
 `<add type="MyCompany.Library.Shape,`  
  
 `MyAssembly, Version=2.0.0.0, Culture=neutral,`  
  
 `PublicKeyToken=XXXXXX, processorArchitecture=MSIL">`  
  
 `<knownType type="MyCompany.Library.Circle,`  
  
 `MyAssembly, Version=2.0.0.0, Culture=neutral,`  
  
 `PublicKeyToken=XXXXXX, processorArchitecture=MSIL"/>`  
  
 `</add>`  
  
 `</declaredTypes>`  
  
 `</dataContractSerializer>`  
  
 `</system.runtime.serialization>`  
  
 `</configuration>`  
  
 Nel file di configurazione precedente è stato dichiarato che un tipo di contratto dati chiamato `MyCompany.Library.Shape` ha `MyCompany.Library.Circle` come tipo conosciuto.  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.KnownTypeAttribute>   
 <xref:System.Collections.Hashtable>   
 <xref:System.Object>   
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Runtime.Serialization.DataContractSerializer.KnownTypes%2A>   
 [Tipi conosciuti](../../../../docs/framework/wcf/samples/known-types.md)   
 [Equivalenza dei contratti dati](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)   
 [Progettazione dei contratti di servizio](../../../../docs/framework/wcf/designing-service-contracts.md)