---
title: "Utilizzo dei contratti di messaggio | Microsoft Docs"
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
  - "contratti di messaggio [WCF]"
ms.assetid: 1e19c64a-ae84-4c2f-9155-91c54a77c249
caps.latest.revision: 46
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 46
---
# Utilizzo dei contratti di messaggio
In genere, quando creano applicazioni [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], gli sviluppatori prestano particolare attenzione alle strutture dei dati e alle problematiche di serializzazione. Non è invece necessario che si preoccupino della struttura dei messaggi in cui sono trasportati i dati.Per queste applicazioni, la creazione dei contratti dati per i parametri o dei valori restituiti è semplice.\([!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Specifica del trasferimento di dati nei contratti di servizio](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md).\)  
  
 Talvolta, tuttavia, il controllo completo della struttura di un messaggio SOAP è importante quanto quello del suo contenuto.Questo è particolarmente vero quando l'interoperabilità è importante o per controllare in modo specifico problemi di sicurezza a livello di messaggio o di parte di esso.In questi casi, è possibile creare un *contratto di messaggio* che consente di specificare la struttura del messaggio SOAP preciso richiesto.  
  
 In questo argomento viene illustrato come utilizzare i vari attributi del contratto di messaggio per creare un contratto di messaggio specifico per l'operazione.  
  
## Utilizzo dei contratti di messaggio nelle operazioni  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta operazioni modellate sullo *stile delle chiamate a una procedura remota \(RPC\)* o sullo *stile di messaggistica*.In un'operazione in stile RPC, è possibile utilizzare qualsiasi tipo serializzabile e si ha accesso alle funzionalità disponibili per le chiamate locali, ad esempio più parametri e parametri `ref` e `out`.In questo stile, la forma di serializzazione scelta controlla la struttura dei dati nei messaggi sottostanti e il runtime di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] crea i messaggi per supportare l'operazione.Ciò consente agli sviluppatori che non hanno dimestichezza con SOAP e messaggi SOAP di creare rapidamente e facilmente applicazioni di servizio e di utilizzarle.  
  
 Nell'esempio di codice seguente viene illustrata un'operazione di servizio modellata sullo stile RPC.  
  
```csharp  
[OperationContract]  
public BankingTransactionResponse PostBankingTransaction(BankingTransaction bt);  
```  
  
 Un contratto dati è in genere sufficiente per definire lo schema per i messaggi.Nell'esempio precedente, è sufficiente per la maggior parte delle applicazioni se `BankingTransaction` e `BankingTransactionResponse` hanno contratti dati per definire il contenuto dei messaggi SOAP sottostanti.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sui contratti dati, vedere [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md).  
  
 Talvolta è tuttavia necessario controllare esattamente la modalità di trasmissione in rete della struttura del messaggio SOAP.Lo scenario più comune è l'inserimento di intestazioni SOAP personalizzate.Un altro scenario comune è quello della definizione di proprietà di sicurezza per le intestazioni e il corpo del messaggio, ovvero, quando è necessario decidere se questi elementi devono essere firmati digitalmente e crittografati.Infine, alcuni stack SOAP di terze parti richiedono che i messaggi abbiano un formato specifico.Questo controllo è fornito da operazioni in stile messaggistica.  
  
 Un'operazione in stile messaggistica ha al massimo un parametro e un valore restituito in cui entrambi i tipi sono tipi di messaggio, ovvero, vengono serializzati direttamente in una struttura del messaggio SOAP specificata.Può trattarsi di un qualsiasi tipo contrassegnato con <xref:System.ServiceModel.MessageContractAttribute> o del tipo <xref:System.ServiceModel.Channels.Message>.Nell'esempio di codice seguente viene illustrata un'operazione simile allo stile RCP precedente, ma in cui viene utilizzato lo stile di messaggistica.  
  
 Se, ad esempio, `BankingTransaction` e `BankingTransactionResponse` sono entrambi tipi relativi a contratti di messaggio, il codice nelle operazioni seguenti è valido.  
  
```csharp  
[OperationContract]  
BankingTransactionResponse Process(BankingTransaction bt);  
[OperationContract]  
void Store(BankingTransaction bt);  
[OperationContract]  
BankingTransactionResponse GetResponse();  
```  
  
 Il codice seguente, tuttavia, non è valido.  
  
```csharp  
[OperationContract]  
bool Validate(BankingTransaction bt);  
// Invalid, the return type is not a message contract.  
[OperationContract]  
void Reconcile(BankingTransaction bt1, BankingTransaction bt2);  
// Invalid, there is more than one parameter.  
```  
  
 Per qualsiasi operazione che implica un tipo di contratto di messaggio e che non segue uno schema valido, viene generata un'eccezione.Le operazioni che non implicano tipi di contratto di messaggio non sono ovviamente soggette a queste restrizioni.  
  
 Se un tipo ha sia un contratto di messaggio che un contratto dati, quando viene utilizzato in un'operazione viene considerato solo il suo contratto di messaggio.  
  
## Definizione dei contratti di messaggio  
 Per definire un contratto di messaggio per un tipo, ovvero, per definire il mapping tra il tipo e una SOAP envelope, applicare <xref:System.ServiceModel.MessageContractAttribute> al tipo.Applicare quindi <xref:System.ServiceModel.MessageHeaderAttribute> ai membri del tipo che si desidera trasformare in intestazioni SOAP e applicare <xref:System.ServiceModel.MessageBodyMemberAttribute> ai membri che si desidera trasformare in parti del corpo SOAP del messaggio.  
  
 Nel codice seguente viene fornito un esempio dell'utilizzo di un contratto di messaggio.  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageHeader] public DateTime transactionDate;  
  [MessageBodyMember] private Account sourceAccount;  
  [MessageBodyMember] private Account targetAccount;  
  [MessageBodyMember] public int amount;  
}  
```  
  
 Quando si utilizza questo tipo come parametro delle operazioni, viene generata la seguente SOAP envelope:  
  
```xml  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:Header>  
    <h:operation xmlns:h="http://tempuri.org/" xmlns="http://tempuri.org/">Deposit</h:operation>  
    <h:transactionDate xmlns:h="http://tempuri.org/" xmlns="http://tempuri.org/">2012-02-16T16:10:00</h:transactionDate>  
  </s:Header>  
  <s:Body xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <BankingTransaction xmlns="http://tempuri.org/">  
      <amount>0</amount>  
      <sourceAccount xsi:nil="true"/>  
      <targetAccount xsi:nil="true"/>  
    </BankingTransaction>  
  </s:Body>  
</s:Envelope>  
  
```  
  
 Si noti che `operation` e `transactionDate` vengono visualizzati come intestazioni SOAP e il corpo SOAP è costituito da un elemento wrapper `BankingTransaction` che contiene `sourceAccount`, `targetAccount` e `amount`.  
  
 È possibile applicare <xref:System.ServiceModel.MessageHeaderAttribute> e <xref:System.ServiceModel.MessageBodyMemberAttribute> a tutti i campi, le proprietà e gli eventi, indipendentemente dal fatto che siano pubblici, privati, protetti o interni.  
  
 L'oggetto <xref:System.ServiceModel.MessageContractAttribute> consente di specificare gli attributi WrapperName e WrapperNamespace tramite cui viene controllato il nome dell'elemento wrapper nel corpo del messaggio SOAP.Per impostazione predefinita, il nome del tipo di contratto di messaggio viene utilizzato per il wrapper e lo spazio dei nomi in cui il contratto di messaggio viene definito. `http://tempuri.org/` viene utilizzato come spazio dei nomi predefinito.  
  
> [!NOTE]
>  Gli attributi <xref:System.Runtime.Serialization.KnownTypeAttribute> vengono ignorati nei contratti di messaggio.Se è richiesto un <xref:System.Runtime.Serialization.KnownTypeAttribute>, inserirlo nell'operazione in cui è utilizzato il contratto di messaggio interessato.  
  
## Controllo di intestazione, nomi di parti del corpo e spazi dei nomi  
 Nella rappresentazione SOAP di un contratto di messaggio, ogni intestazione e parte del corpo esegue il mapping a un elemento XML che ha un nome e uno spazio dei nomi.  
  
 Per impostazione predefinita, lo spazio dei nomi corrisponde allo spazio dei nomi del contratto di servizio al quale partecipa il messaggio e il nome è determinato dal nome del membro al quale vengono applicati gli attributi <xref:System.ServiceModel.MessageHeaderAttribute> o <xref:System.ServiceModel.MessageBodyMemberAttribute>.  
  
 È possibile cambiare queste impostazioni predefinite modificando <xref:System.ServiceModel.MessageContractMemberAttribute.Name%2A?displayProperty=fullName> e <xref:System.ServiceModel.MessageContractMemberAttribute.Namespace%2A?displayProperty=fullName> \(nella classe padre degli attributi <xref:System.ServiceModel.MessageHeaderAttribute> e <xref:System.ServiceModel.MessageBodyMemberAttribute>\).  
  
 Si consideri la classe nell'esempio di codice seguente.  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageHeader(Namespace="http://schemas.contoso.com/auditing/2005")] public bool IsAudited;  
  [MessageBodyMember(Name="transactionData")] public BankingTransactionData theData;  
}  
  
```  
  
 In questo esempio, l'intestazione `IsAudited` è nello spazio dei nomi specificato nel codice e la parte del corpo che rappresenta il membro `theData` è rappresentata da un elemento XML con il nome `transactionData`.Di seguito è riportato il codice XML generato per il contratto di messaggio.  
  
```  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:Header>  
    <h:IsAudited xmlns:h="http://schemas.contoso.com/auditing/2005" xmlns="http://schemas.contoso.com/auditing/2005">false</h:IsAudited>  
    <h:operation xmlns:h="http://tempuri.org/" xmlns="http://tempuri.org/">Deposit</h:operation>  
  </s:Header>  
  <s:Body xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <AuditedBankingTransaction xmlns="http://tempuri.org/">  
      <transactionData/>  
    </AuditedBankingTransaction>  
  </s:Body>  
</s:Envelope>  
  
```  
  
## Controllo dell'incapsulamento di parti di corpo SOAP  
 Per impostazione predefinita, le parti di corpo SOAP vengono serializzate in un elemento incapsulato.Nel codice seguente, ad esempio, viene illustrato l'elemento wrapper `HelloGreetingMessage` generato dal nome del tipo <xref:System.ServiceModel.MessageContractAttribute> nel contratto di messaggio per il messaggio `HelloGreetingMessage`.  
  
 [!code-csharp[MessageHeaderAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/messageheaderattribute/cs/services.cs#3)]
 [!code-vb[MessageHeaderAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/messageheaderattribute/vb/services.vb#3)]  
  
 Per sopprimere l'elemento wrapper, impostare la proprietà <xref:System.ServiceModel.MessageContractAttribute.IsWrapped%2A> su `false`.Per controllare il nome e lo spazio dei nomi dell'elemento wrapper, utilizzare le proprietà <xref:System.ServiceModel.MessageContractAttribute.WrapperName%2A> e <xref:System.ServiceModel.MessageContractAttribute.WrapperNamespace%2A>.  
  
> [!NOTE]
>  La presenza di più di una parte del corpo del messaggio in messaggi non incapsulati non è conforme a WS\-I Basic Profile 1.1 e non è consigliata quando si progettano nuovi contratti di messaggio.In certi scenari di interoperabilità, può tuttavia essere necessario avere più di una parte del corpo del messaggio non incapsulato.Se si ha intenzione di trasmettere più di un pezzo di dati in un corpo del messaggio, è consigliato utilizzare la modalità predefinita \(incapsulata\).La presenza di più di un'intestazione del messaggio nei messaggi non incapsulati è completamente accettabile.  
  
## Utilizzo di tipi personalizzati nei contratti di messaggio  
 Ogni singola intestazione del messaggio e parte del corpo del messaggio viene serializzata \(trasformata in XML\) utilizzando il motore di serializzazione scelto per il contratto di servizio in cui il messaggio è utilizzato.Il motore di serializzazione predefinito, `XmlFormatter`, è in grado di gestire qualsiasi tipo che abbia un contratto dati, in modo esplicito \(con <xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=fullName>\) o implicito \(se si tratta di un tipo primitivo, con <xref:System.SerializableAttribute?displayProperty=fullName> e così via\).[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md).  
  
 Nell'esempio precedente, i tipi `Operation` e `BankingTransactionData` devono avere un contratto dati e `transactionDate` è serializzabile perché <xref:System.DateTime> è un primitivo e, di conseguenza, ha un contratto dati implicito.  
  
 È tuttavia possibile passare a un diverso motore di serializzazione, `XmlSerializer`.Se si sceglie di cambiare motore, è necessario assicurarsi che tutti i tipi utilizzati per le intestazioni dei messaggi e le parti del corpo siano serializzabili utilizzando `XmlSerializer`.  
  
## Utilizzo di matrici nei contratti di messaggio  
 È possibile utilizzare matrici di elementi ripetuti nei contratti di messaggio in due modi.  
  
 Il primo consiste nell'utilizzare un <xref:System.ServiceModel.MessageHeaderAttribute> o un <xref:System.ServiceModel.MessageBodyMemberAttribute> direttamente nella matrice.In questo caso, l'intera matrice viene serializzata come un solo elemento, ovvero, come un'unica intestazione o un'unica parte del corpo, con in più elementi figlio.Si consideri la classe nell'esempio seguente.  
  
```csharp  
[MessageContract]  
public class BankingDepositLog  
{  
  [MessageHeader] public int numRecords;  
  [MessageHeader] public DepositRecord[] records;  
  [MessageHeader] public int branchID;  
}  
```  
  
 Il risultato nelle intestazioni SOAP è simile al seguente.  
  
```  
<BankingDepositLog>  
<numRecords>3</numRecords>  
<records>  
  <DepositRecord>Record1</DepositRecord>  
  <DepositRecord>Record2</DepositRecord>  
  <DepositRecord>Record3</DepositRecord>  
</records>  
<branchID>20643</branchID>  
</BankingDepositLog>  
```  
  
 In alternativa, è possibile utilizzare <xref:System.ServiceModel.MessageHeaderArrayAttribute>.In questo caso, ogni elemento della matrice viene serializzato in modo indipendente affinché abbia un'intestazione, in modo simile all'esempio seguente.  
  
```  
  
<numRecords>3</numRecords>  
<records>Record1</records>  
<records>Record2</records>  
<records>Record3</records>  
<branchID>20643</branchID>  
```  
  
 Il nome predefinito per le voci della matrice è il nome del membro al quale vengono applicati gli attributi <xref:System.ServiceModel.MessageHeaderArrayAttribute>.  
  
 L'attributo <xref:System.ServiceModel.MessageHeaderArrayAttribute> eredita da <xref:System.ServiceModel.MessageHeaderAttribute>.Ha lo stesso set di funzionalità degli attributi non di matrice, ad esempio, è possibile impostare l'ordine, il nome e lo spazio dei nomi per una matrice di intestazioni nella stessa modalità utilizzata per una singola intestazione.Quando si utilizza la proprietà `Order` su una matrice, tale proprietà viene applicata alla matrice intera.  
  
 È possibile applicare <xref:System.ServiceModel.MessageHeaderArrayAttribute> solo alle matrici, non alle raccolte.  
  
## Utilizzo di matrici di byte nei contratti di messaggio  
 Le matrici di byte, quando sono utilizzate con attributi non di matrice \(<xref:System.ServiceModel.MessageBodyMemberAttribute> e <xref:System.ServiceModel.MessageHeaderAttribute>\), non vengono trattate come matrici ma come un tipo primitivo speciale rappresentato come dati con codifica Base64 nell'XML risultante.  
  
 Quando si utilizzano matrici di byte con l'attributo della matrice <xref:System.ServiceModel.MessageHeaderArrayAttribute>, i risultati dipendono dal serializzatore utilizzato.Con il serializzatore predefinito, la matrice è rappresentata sotto forma di singola voce per ogni byte.Quando, tuttavia, è selezionato `XmlSerializer`, \(utilizzando <xref:System.ServiceModel.XmlSerializerFormatAttribute> nel contratto di servizio\), le matrici di byte vengono trattate come dati Base64 indipendentemente dal fatto che siano utilizzati attributi di matrice o non di matrice.  
  
## Firma e crittografia di parti di messaggio  
 Un contratto di messaggio può indicare se le intestazioni e\/o il corpo del messaggio devono essere crittografati e firmati digitalmente.  
  
 A tal fine, impostare la proprietà <xref:System.ServiceModel.MessageContractMemberAttribute.ProtectionLevel%2A?displayProperty=fullName> sugli attributi <xref:System.ServiceModel.MessageHeaderAttribute> e <xref:System.ServiceModel.MessageBodyMemberAttribute>.La proprietà è un'enumerazione del tipo <xref:System.Net.Security.ProtectionLevel?displayProperty=fullName> e può essere impostata su <xref:System.Net.Security.ProtectionLevel> \(nessuna crittografia o firma\), <xref:System.Net.Security.ProtectionLevel> \(solo firma digitale\) o <xref:System.Net.Security.ProtectionLevel> \(sia crittografia che firma digitale\).Il valore predefinito è <xref:System.Net.Security.ProtectionLevel>.  
  
 Affinché queste funzionalità di sicurezza funzionino, è necessario configurare correttamente l'associazione e i comportamenti.Se vengono utilizzate senza la configurazione corretta, ad esempio se si tenta di firmare un messaggio senza fornire le proprie credenziali, al momento della convalida viene generata un'eccezione.  
  
 Nel caso delle intestazioni di messaggio, il livello di protezione viene determinato singolarmente per ogni intestazione.  
  
 Per le parti del corpo del messaggio, il livello di protezione può essere considerato come "livello minimo di protezione". Il corpo ha un solo livello di protezione, indipendentemente dal numero delle sue parti.Il livello di protezione del corpo è determinato dall'impostazione più alta della proprietà <xref:System.ServiceModel.MessageContractMemberAttribute.ProtectionLevel%2A> di tutte le parti del corpo.È tuttavia necessario impostare il livello di protezione di ogni parte del corpo sul livello di protezione minimo effettivo richiesto.  
  
 Si consideri la classe nell'esempio di codice seguente.  
  
```csharp  
[MessageContract]  
public class PatientRecord  
{  
   [MessageHeader(ProtectionLevel=None)] public int recordID;  
   [MessageHeader(ProtectionLevel=Sign)] public string patientName;  
   [MessageHeader(ProtectionLevel=EncryptAndSign)] public string SSN;  
   [MessageBodyMember(ProtectionLevel=None)] public string comments;  
   [MessageBodyMember(ProtectionLevel=Sign)] public string diagnosis;  
   [MessageBodyMember(ProtectionLevel=EncryptAndSign)] public string medicalHistory;  
}  
```  
  
 In questo esempio, l'intestazione `recordID` non è protetta, la parte `patientName` è `signed` e la parte `SSN` è crittografata e firmata.Ad almeno una parte del corpo, `medicalHistory`, è applicato <xref:System.Net.Security.ProtectionLevel>, pertanto tutto il corpo del messaggio è crittografato e firmato anche se i commenti e le parti del corpo di diagnosi specificano livelli di protezione inferiori.  
  
## Azione SOAP  
 SOAP e gli standard dei servizi Web correlati definiscono una proprietà chiamata `Action` che può essere presente per ogni messaggio SOAP inviato.Il valore di questa proprietà è controllato dalle proprietà <xref:System.ServiceModel.OperationContractAttribute.Action%2A?displayProperty=fullName> e <xref:System.ServiceModel.OperationContractAttribute.ReplyAction%2A?displayProperty=fullName> dell'operazione.  
  
## Attributi di intestazione SOAP  
 Lo standard SOAP definisce gli attributi che possono esistere in un'intestazione. Tali attributi sono:  
  
-   `Actor/Role` \(`Actor` in SOAP 1.1, `Role` in SOAP 1.2\)  
  
-   `MustUnderstand`  
  
-   `Relay`  
  
 L'attributo `Actor` o `Role` specifica l'URI \(Uniform Resource Identifier\) del nodo al quale è destinata una determinata intestazione.L'attributo `MustUnderstand` specifica se il nodo che elabora l'intestazione deve comprenderla.L'attributo `Relay` specifica se l'intestazione deve essere inoltrata ai nodi downstream.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non elabora in alcun modo questi attributi quando presenti nei messaggi in ingresso, ad eccezione di `MustUnderstand`, come specificato nella sezione "Controllo delle versioni dei contratti di messaggio" più avanti in questo argomento.Consente tuttavia di leggerli e scriverli come appropriato, come nella descrizione seguente.  
  
 Quando si invia un messaggio, per impostazione predefinita questi attributi non vengono creati.È possibile modificare l'impostazione in due modi.In primo luogo, è possibile impostare staticamente gli attributi su qualsiasi valore desiderato modificando le proprietà <xref:System.ServiceModel.MessageHeaderAttribute.Actor%2A?displayProperty=fullName>, <xref:System.ServiceModel.MessageHeaderAttribute.MustUnderstand%2A?displayProperty=fullName> e <xref:System.ServiceModel.MessageHeaderAttribute.Relay%2A?displayProperty=fullName>, come mostrato nell'esempio di codice che segue.Si noti che non esiste alcuna proprietà `Role`. Nel caso in cui si utilizzi SOAP 1.2, se si imposta la proprietà <xref:System.ServiceModel.MessageHeaderAttribute.Actor%2A> viene creato l'attributo `Role`.  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader(Actor="http://auditingservice.contoso.com", MustUnderstand=true)] public bool IsAudited;  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember] public BankingTransactionData theData;  
}  
```  
  
 La seconda modalità di controllo di questi attributi è dinamica, tramite codice.In questo caso, incapsulare il tipo di intestazione desiderato nel tipo <xref:System.ServiceModel.MessageHeader%601>, per essere certi di non confondere questo tipo con la versione non generica, e utilizzare il tipo insieme a <xref:System.ServiceModel.MessageHeaderAttribute>.Quindi, è possibile utilizzare proprietà in <xref:System.ServiceModel.MessageHeader%601> per impostare gli attributi SOAP, come illustrato nell'esempio di codice seguente.  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public MessageHeader<bool> IsAudited;  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember] public BankingTransactionData theData;  
}  
// application code:  
BankingTransaction bt = new BankingTransaction();  
bt.IsAudited = new MessageHeader<bool>();  
bt.IsAudited.Content = false; // Set IsAudited header value to "false"  
bt.IsAudited.Actor="http://auditingservice.contoso.com";  
bt.IsAudited.MustUnderstand=true;  
```  
  
 Se si utilizza sia il meccanismo di controllo dinamico sia quello statico, per impostazione predefinita vengono utilizzate le impostazioni statiche che, tuttavia, in seguito possono essere sottoposte a override utilizzando il meccanismo dinamico, come illustrato nel codice seguente.  
  
```  
[C#]  
[MessageHeader(MustUnderstand=true)] public MessageHeader<Person> documentApprover;  
// later on in the code:  
BankingTransaction bt = new BankingTransaction();  
bt.documentApprover = new MessageHeader<Person>();  
bt.documentApprover.MustUnderstand = false; // override the static default of 'true'  
```  
  
 È consentito creare intestazioni ripetute con il controllo dinamico degli attributi, come illustrato nel codice seguente.  
  
```csharp  
[MessageHeaderArray] public MessageHeader<Person> documentApprovers[];  
```  
  
 Sul lato ricevente, la lettura di questi attributi SOAP può essere eseguita solo se si utilizza la classe <xref:System.ServiceModel.MessageHeader%601> per l'intestazione nel tipo.Per individuare le impostazioni degli attributi del messaggio ricevuto è possibile esaminare le proprietà `Actor`, `Relay` o `MustUnderstand` di un'intestazione di tipo <xref:System.ServiceModel.MessageHeader%601>.  
  
 Quando si riceve un messaggio e quindi lo si invia nuovamente all'origine, il roundtrip delle impostazioni degli attributi SOAP viene eseguito solo per le intestazioni di tipo <xref:System.ServiceModel.MessageHeader%601>.  
  
## Ordine delle parti del corpo SOAP  
 In alcune circostanze, potrebbe essere necessario controllare l'ordine delle parti del corpo.Per impostazione predefinita, l'ordine degli elementi del corpo è alfabetico ma può essere controllato dalla proprietà <xref:System.ServiceModel.MessageBodyMemberAttribute.Order%2A?displayProperty=fullName>.Questa proprietà ha la stessa semantica della proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A?displayProperty=fullName>, a parte il comportamento negli scenari di ereditarietà. Nei contratti di messaggio, i membri del corpo di tipo base non sono ordinati prima dei membri del corpo di tipo derivato.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Ordine dei membri dati](../../../../docs/framework/wcf/feature-details/data-member-order.md).  
  
 Nell'esempio seguente, `amount` normalmente verrebbe per primo perché è primo alfabeticamente.La proprietà <xref:System.ServiceModel.MessageBodyMemberAttribute.Order%2A> l'inserisce tuttavia nella terza posizione.  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember(Order=1)] public Account sourceAccount;  
  [MessageBodyMember(Order=2)] public Account targetAccount;  
  [MessageBodyMember(Order=3)] public int amount;  
}  
```  
  
## Controllo delle versioni dei contratti di messaggio  
 Talvolta potrebbe essere necessario modificare contratti di messaggio.Una nuova versione dell'applicazione, ad esempio, potrebbe aggiungere un'altra intestazione a un messaggio.Quindi, in caso di invio dalla versione nuova a quella vecchia, il sistema deve gestire un'intestazione in più, mentre in direzione opposta deve gestirne una in meno.  
  
 Per il controllo delle versioni delle intestazioni, si applicano le regole seguenti:  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non obietta alle intestazioni mancanti. I membri corrispondenti vengono lasciati sui rispettivi valori predefiniti.  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ignora anche intestazioni aggiuntive impreviste.Fa eccezione a questa regola il caso di un'intestazione aggiuntiva il cui attributo `MustUnderstand` sia impostato su `true` nel messaggio SOAP in ingresso. Non essendo possibile elaborare un'intestazione che deve essere compresa, viene generata un'eccezione.  
  
 Per i corpi dei messaggi si applicano regole simili di controllo delle versioni, sia le parti di corpi dei messaggi mancanti che quelle aggiuntive vengono ignorate.  
  
## Considerazioni sull'ereditarietà  
 Un tipo di contratto di messaggio può ereditare da un altro tipo, a condizione che anche il tipo di base abbia un contratto di messaggio.  
  
 Quando si crea o si accede a un messaggio utilizzando un tipo di contratto di messaggio che eredita da altri tipi di contratto di messaggio, si applicano le regole seguenti:  
  
-   Tutte le intestazioni del messaggio nella gerarchia di ereditarietà sono raccolte insieme per formare il set completo di intestazioni per il messaggio.  
  
-   Tutte le parti del corpo del messaggio nella gerarchia di ereditarietà sono raccolte insieme per formare l'intero corpo del messaggio.Le parti del corpo sono ordinate in base alle normali regole di ordinamento \(in base alla proprietà <xref:System.ServiceModel.MessageBodyMemberAttribute.Order%2A?displayProperty=fullName> e quindi alfabeticamente\), senza considerare affatto la loro posizione nella gerarchia di ereditarietà.È assolutamente sconsigliato utilizzare l'eredità del contratto di messaggio nel caso in cui le parti del corpo del messaggio si trovino a più livelli della struttura di eredità.Se una classe di base e una classe derivata definiscono un'intestazione o una parte del corpo con lo stesso nome, per archiviare il valore di quell'intestazione o di quella parte del corpo viene utilizzato il membro della classe più di base.  
  
 Si considerino le classi nell'esempio di codice seguente.  
  
```csharp  
[MessageContract]  
public class PersonRecord  
{  
  [MessageHeader(Name="ID")] public int personID;  
  [MessageBodyMember] public string patientName;  
}  
  
[MessageContract]  
public class PatientRecord : PersonRecord  
{  
  [MessageHeader(Name="ID")] public int patientID;  
  [MessageBodyMember] public string diagnosis;  
}  
```  
  
 La classe `PatientRecord` descrive un messaggio con un'intestazione chiamata `ID`.L'intestazione corrisponde a `personID` e non al membro `patientID`, perché viene scelto il membro più di base.Pertanto, in questo caso il campo `patientID` è inutile.Il corpo del messaggio contiene l'elemento `diagnosis` seguito dall'elemento `patientName`, perché questo è l'ordine alfabetico.Si noti che nell'esempio viene illustrato uno schema assolutamente sconsigliato: sia il contratto di messaggio di base che quello del messaggio derivato hanno parti di corpo del messaggio.  
  
## Considerazioni su WSDL  
 Quando si genera un contratto Web Services Description Language \(WSDL\) da un servizio che utilizza contratti di messaggio, è importante ricordare che non tutte le funzionalità del contratto di messaggio vengono riflesse nel WSDL risultante.Si considerino i punti seguenti:  
  
-   WSDL non è in grado di esprimere il concetto di una matrice di intestazioni.Quando si creano messaggi con una matrice di intestazioni utilizzando <xref:System.ServiceModel.MessageHeaderArrayAttribute>, il WSDL risultante riflette solo un'intestazione anziché la matrice.  
  
-   Il documento WSDL risultante non può riflettere alcune informazioni del livello di protezione.  
  
-   Il tipo di messaggio generato in WSDL ha lo stesso nome della classe del tipo del contratto di messaggio.  
  
-   Quando si utilizza lo stesso contratto di messaggio in più operazioni, nel documento WSDL vengono generati più tipi di messaggio.I nomi sono resi univoci aggiungendo i numeri "2", "3" e così via, per gli utilizzi successivi.Al momento della reimportazione in WSDL, vengono creati più tipi di contratto di messaggio, che sono identici tranne che per il nome.  
  
## Considerazioni sulla codifica SOAP  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente di utilizzare lo stile di codifica SOAP legacy di XML. Non è tuttavia consigliato.Quando si utilizza questo stile, impostando la proprietà `Use` su `Encoded` nel <xref:System.ServiceModel.XmlSerializerFormatAttribute?displayProperty=fullName> applicato al contratto di servizio, si applicano le considerazioni aggiuntive seguenti:  
  
-   Le intestazioni del messaggio non sono supportate. Ciò significa che l'attributo <xref:System.ServiceModel.MessageHeaderAttribute> e l'attributo della matrice <xref:System.ServiceModel.MessageHeaderArrayAttribute> sono incompatibili con la codifica SOAP.  
  
-   Se il contratto di messaggio non viene incapsulato, ovvero se la proprietà <xref:System.ServiceModel.MessageContractAttribute.IsWrapped%2A> è impostata su `false`, può avere solo una parte del corpo.  
  
-   Il nome dell'elemento wrapper per il contratto di messaggio di richiesta deve corrispondere al nome dell'operazione.A tale scopo, utilizzare la proprietà `WrapperName` del contratto di messaggio.  
  
-   Il nome dell'elemento wrapper per il contratto di messaggio di risposta deve essere identico a quello del nome dell'operazione con il suffisso "Response".A tale scopo, utilizzare la proprietà <xref:System.ServiceModel.MessageContractAttribute.WrapperName%2A> del contratto di messaggio.  
  
-   La codifica SOAP mantiene i riferimenti all'oggetto.Si consideri, ad esempio, il codice seguente.  
  
    ```csharp  
    [MessageContract(WrapperName="updateChangeRecord")]  
    public class ChangeRecordRequest  
    {  
      [MessageBodyMember] Person changedBy;  
      [MessageBodyMember] Person changedFrom;  
      [MessageBodyMember] Person changedTo;  
    }  
  
    [MessageContract(WrapperName="updateChangeRecordResponse")]  
    public class ChangeRecordResponse  
    {  
      [MessageBodyMember] Person changedBy;  
      [MessageBodyMember] Person changedFrom;  
      [MessageBodyMember] Person changedTo;  
    }  
  
    // application code:  
    ChangeRecordRequest cr = new ChangeRecordRequest();  
    Person p = new Person("John Doe");  
    cr.changedBy=p;  
    cr.changedFrom=p;  
    cr.changedTo=p;  
    ```  
  
 Dopo aver serializzato il messaggio utilizzando la codifica SOAP, `changedFrom` e `changedTo` non contengono copie di `p`, ma puntano alla copia all'interno dell'elemento `changedBy`.  
  
## Considerazioni sulle prestazioni  
 Ogni intestazione del messaggio e ogni parte del corpo del messaggio viene serializzata indipendentemente dalle altre.È pertanto possibile dichiarare gli stessi spazi dei nomi per ogni intestazione e parte del corpo.Per migliorare le prestazioni, specie in termini di dimensioni del messaggio in transito, consolidare più intestazioni e parti del corpo in un'unica intestazione o parte del corpo.Anziché, ad esempio, il codice seguente:  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember] public Account sourceAccount;  
  [MessageBodyMember] public Account targetAccount;  
  [MessageBodyMember] public int amount;  
}  
```  
  
 Utilizzare questo codice.  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember] public OperationDetails details;  
}  
  
[DataContract]  
public class OperationDetails  
{  
  [DataMember] public Account sourceAccount;  
  [DataMember] public Account targetAccount;  
  [DataMember] public int amount;  
}  
```  
  
### Contratti client e di messaggio asincroni basati su eventi  
 Le linee guida di progettazione per il modello asincrono basato su eventi indicano che, se vengono restituiti più valori, un valore viene restituito come proprietà `Result` e i restanti valori sono restituiti come proprietà nell’oggetto  <xref:System.EventArgs>.Di conseguenza, è possibile che, se un client importa metadati utilizzando le opzioni di comando asincrone basate su eventi e l'operazione restituisce più valori, l'oggetto predefinito <xref:System.EventArgs> restituisce un valore come proprietà `Result` e i restanti valori come proprietà dell’oggetto <xref:System.EventArgs>.  
  
 Se si desidera ricevere l’oggetto del messaggio come proprietà `Result` e i valori restituiti come proprietà in quell’oggetto, utilizzare l’opzione di comando `/messageContract`.Questa operazione genera una firma che restituisce il messaggio di risposta come proprietà `Result` nell’oggetto <xref:System.EventArgs>.Pertanto, tutti i valori restituiti interni sono proprietà dell’oggetto del messaggio di risposta.  
  
## Vedere anche  
 [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)   
 [Progettazione e implementazione di servizi](../../../../docs/framework/wcf/designing-and-implementing-services.md)