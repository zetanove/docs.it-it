---
title: "Servizi di crittografia | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "crittografia [.NET Framework]"
  - "modello di ereditarietà della classe derivata"
  - "firme digitali"
  - "algoritmi crittografici asimmetrici"
  - "firme digitali, sistemi di chiavi pubbliche"
  - "chiavi pubbliche"
  - "decrittografia [.NET Framework]"
  - "chiavi private"
  - "MAC (algoritmi)"
  - "algoritmi di crittografia"
  - "chiavi private, informazioni generali"
  - "crittografia [.NET Framework]"
  - "sicurezza [.NET Framework], crittografia"
  - "servizi crittografici"
  - "algoritmi crittografici simmetrici"
  - "hash"
  - "codici di autenticazione dei messaggi"
  - "ereditarietà della classe derivata"
  - "crittografia [.NET Framework], informazioni"
  - "generazione casuale di numeri"
ms.assetid: f96284bc-7b73-44b5-ac59-fac613ad09f8
caps.latest.revision: 34
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 34
---
# Servizi di crittografia
<a name="top"></a> Le reti pubbliche, ad esempio Internet, non offrono comunicazioni sicure tra entità. Le comunicazioni su tali reti possono essere lette o addirittura modificate da terze parti non autorizzate. La crittografia aiuta a proteggere i dati dalla visualizzazione, offre modalità per rilevare se i dati sono stati modificati e aiuta a offrire una modalità di comunicazione sicura su canali altrimenti non sicuri. Ad esempio, è possibile crittografare i dati usando un algoritmo di crittografia, trasmesso in stato crittografato e quindi decrittografato dal destinatario designato. Se una terza parte intercetta i dati crittografati, la decrittografia risulterà difficile.  
  
 In .NET Framework le classi dello spazio dei nomi <xref:System.Security.Cryptography?displayProperty=fullName> gestiscono automaticamente molti dettagli della crittografia. In alcuni casi si tratta di wrapper presenti nelle CryptoAPI di Microsoft non gestite, in altri semplicemente di implementazioni gestite. Non è necessario essere esperti di crittografia per usare queste classi. Quando si crea una nuova istanza di una delle classi dell'algoritmo di crittografia, le chiavi vengono generate automaticamente per semplificare l'uso e le proprietà predefinite offrono la maggiore sicurezza possibile.  
  
 Questa panoramica offre un riepilogo dei metodi e delle procedure di crittografia supportati da .NET Framework, inclusi i manifesti ClickOnce, Suite B e il supporto per Cryptography Next Generation \(CNG\) introdotto in [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)].  
  
 In questa panoramica sono incluse le sezioni seguenti:  
  
-   [Primitive di crittografia](#primitives)  
  
-   [Crittografia a chiave segreta](#secret_key)  
  
-   [Crittografia a chiave pubblica](#public_key)  
  
-   [Firme digitali](#digital_signatures)  
  
-   [Valore hash](#hash_values)  
  
-   [Generazione di numeri casuali](#random_numbers)  
  
-   [Manifesti ClickOnce](#clickonce)  
  
-   [Supporto per Suite B](#suite_b)  
  
-   [Argomenti correlati](#related_topics)  
  
 Per altre informazioni sulla crittografia e sui servizi, i componenti e gli strumenti Microsoft che permettono l'aggiunta di sicurezza crittografica alle applicazioni, vedere la sezione di questo documento relativa allo sviluppo e alla sicurezza Win32 e COM.  
  
<a name="primitives"></a>   
## Primitive di crittografia  
 In una situazione tipica in cui si usa la crittografia, due parti \(Alice e Bob\) comunicano su un canale non sicuro. Alice e Bob vogliono assicurare che le comunicazioni risultino incomprensibili a eventuali ascoltatori. Poiché, inoltre, Alice e Bob si trovano in posizioni remote, Alice deve assicurarsi che le informazioni ricevute da Bob non siano state modificate da altri durante la trasmissione. Deve inoltre assicurarsi che le informazioni provengano effettivamente da Bob e non da qualcuno che lo sta rappresentando.  
  
 La crittografia permette di realizzare gli obiettivi seguenti:  
  
-   Riservatezza: aiuta a proteggere l'identità o i dati di un utente dalla lettura.  
  
-   Integrità dei dati: aiuta a proteggere i dati dalla modifica.  
  
-   Autenticazione: assicura che i dati provengano da una parte specifica.  
  
-   Non ripudio: impedisce a una parte specifica di negare di avere inviato un messaggio.  
  
 Per realizzare questi obiettivi, è possibile usare una combinazione di algoritmi e procedure nota come primitive di crittografia per creare uno schema crittografico. La tabella seguente elenca le primitive di crittografia e il rispettivo uso.  
  
|Primitiva di crittografia|Usa|  
|-------------------------------|---------|  
|Crittografia a chiave segreta \(crittografia simmetrica\)|Esegue una trasformazione sui dati per impedirne la lettura da terze parti. Questo tipo di crittografia usa una singola chiave segreta condivisa per crittografare e decrittografare i dati.|  
|Crittografia a chiave pubblica \(crittografia asimmetrica\)|Esegue una trasformazione sui dati per impedirne la lettura da terze parti. Questo tipo di crittografia usa una coppia di chiavi pubblica\/privata per crittografare e decrittografare i dati.|  
|Firme di crittografia|Aiuta a verificare che i dati provengano da una parte specifica, tramite la creazione di una firma digitale univoca per tale parte. Questo processo usa anche funzioni hash.|  
|Hash di crittografia|Mappa i dati di qualsiasi lunghezza a una sequenza di byte a lunghezza fissa. Gli hash sono statisticamente univoci. Una sequenza di due byte diversa non avrà come risultato hash con lo stesso valore.|  
  
 [Torna all'inizio](#top)  
  
<a name="secret_key"></a>   
## Crittografia a chiave segreta  
 Gli algoritmi di crittografia a chiave segreta usano una singola chiave segreta per crittografare e decrittografare i dati. È necessario proteggere la chiave dall'accesso da parte di agenti non autorizzati, poiché chiunque sia in possesso della chiave la potrà usare per decrittografare i dati o crittografare i propri dati, affermando che sono stati originati dall'utente.  
  
 La crittografia a chiave segreta è definita anche crittografia simmetrica, poiché si usa la stessa chiave per la crittografia e la decrittografia. Gli algoritmi di crittografia a chiave segreta sono molto veloci, rispetto agli algoritmi a chiave pubblica e sono ottimali per l'esecuzione di trasformazioni crittografiche su grandi flussi di dati. Gli algoritmi di crittografia asimmetrica, ad esempio RSA, sono matematicamente limitati a livello di quantità di dati che sono in grado di crittografare. Gli algoritmi di crittografia simmetrica non presentano in genere questi problemi.  
  
 Un tipo di algoritmo a chiave segreta, denominato crittografia a blocchi, viene usato per crittografare un blocco di dati alla volta. Tramite la crittografia a blocchi, come Data Encryption Standard \(DES\), TripleDES e Advanced Encryption Standard \(AES\), un blocco di input di *n* byte viene trasformato a livello di crittografia in un blocco di output di byte crittografati. Se si vuole crittografare o decrittografare una sequenza di byte, è necessario eseguire tale operazione blocco per blocco. Poiché la dimensione di *n* è limitata \(8 byte per DES e TripleDES, 16 byte come valore predefinito, 24 o 32 byte per AES\), i valori di dati superiori a *n* devono essere crittografati un blocco alla volta. I valori di dati inferiori a *n* devono essere espansi a *n* per essere elaborati.  
  
 Una forma semplice di crittografia a blocchi viene definita modalità ECB \(Electronic Codebook\). La modalità ECB non è considerata sicura, poiché non usa un vettore di inizializzazione per inizializzare il primo blocco di testo normale. Per una determinata chiave segreta *k*, tramite una semplice crittografia a blocchi in cui non viene usato un vettore di inizializzazione lo stesso blocco di input di testo non crittografato verrà crittografato nello stesso blocco di output di testo crittografato. Se sono quindi presenti blocchi duplicati nel flusso di testo normale di input, saranno presenti blocchi duplicati nel flusso di testo crittografato di output. Questi blocchi di output duplicati segnalano agli utenti non autorizzati la crittografia debole usata, gli algoritmi usati e le possibili modalità di attacco. La modalità ECB è quindi abbastanza vulnerabile all'analisi e quindi all'individuazione delle chiavi.  
  
 Le classi d crittografia a blocchi fornite nella libreria di classi base usano una modalità di concatenamento predefinita denominata CBC \(Cipher\-Block Chaining\), ma se si vuole è possibile modificare questa impostazione predefinita.  
  
 La crittografia CBC supera i problemi associati alla crittografia ECB usando un vettore di inizializzazione per crittografare il primo blocco di testo normale. Ogni blocco successivo di testo normale viene sottoposto a un'operazione Bitwise\-OR esclusiva \(`XOR`\) con il blocco di testo crittografato precedente prima della crittografia. Ogni blocco di testo crittografato dipende prima da tutti i blocchi precedenti. Quando viene usato questo sistema, le intestazioni di messaggio comuni che potrebbero essere note a un utente non autorizzato non potranno essere usate per decodificare una chiave.  
  
 Un modo per compromettere dati crittografati con la modalità CBC consiste nell'eseguire una ricerca completa di ogni chiave possibile. In base alle dimensioni della chiave usata per eseguire la crittografia, questo tipo di ricerca richiede molto tempo anche nei computer più veloci ed è quindi irrealizzabile. Le dimensioni di chiave più elevate sono più difficili da decifrare. Benché la crittografia non renda teoricamente impossibile a un utente malintenzionato il recupero di dati crittografati, aumenta il costo di tale operazione. Se sono necessari tre mesi per eseguire una ricerca completa per recuperare dati che risultano significativi solo per alcuni giorni, il metodo di ricerca completa risulta poco pratico.  
  
 Lo svantaggio della crittografia a chiave segreta consiste nel fatto che presuppone che le due parti si siano accordate su una chiave e un vettore di inizializzazione e che abbiano comunicato i rispettivi valori. Il vettore di inizializzazione non è considerato segreto e può essere trasmesso in testo normale con il messaggio. La chiave deve essere tuttavia mantenuta segreta agli utenti non autorizzati. A causa di questi problemi, la crittografia a chiave segreta viene usata spesso insieme alla crittografia a chiave pubblica per comunicare in modo privato i valori della chiave e del vettore di inizializzazione.  
  
 Supponendo che Alice e Bob siano due parti che vogliono comunicare su un canale non sicuro, potranno usare la crittografia a chiave segreta nel modo seguente: Alice e Bob decidono di usare un algoritmo specifico, ad esempio AES, con una chiave e un vettore di inizializzazione specifici. Alice compone un messaggio e crea un flusso di rete \(forse una named pipe o posta elettronica di rete\) su cui inviare il messaggio. In seguito crittografa il testo usando la chiave e il vettore di inizializzazione e invia il messaggio crittografato e il vettore di inizializzazione a Bob tramite Intranet. Bob riceve il testo crittografato e lo decrittografa usando il vettore di inizializzazione e la chiave precedentemente concordata. Se la trasmissione viene intercettata, l'intercettore non può recuperare il messaggio originale, poiché non conosce la chiave. In questo scenario, solo la chiave deve rimanere segreta. In uno scenario reale Alice o Bob genera una chiave segreta e usa la crittografia a chiave pubblica \(asimmetrica\) per trasferire la chiave segreta \(simmetrica\) all'altra parte. Per altre informazioni sulla crittografia a chiave pubblica, vedere la sezione successiva.  
  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fornisce le classi seguenti che implementano algoritmi di crittografia a chiave segreta:  
  
-   <xref:System.Security.Cryptography.AesManaged> \(introdotto in [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)]\).  
  
-   <xref:System.Security.Cryptography.DESCryptoServiceProvider>.  
  
-   <xref:System.Security.Cryptography.HMACSHA1>: si tratta tecnicamente di un algoritmo a chiave segreta in quanto rappresenta il codice di autenticazione del messaggio calcolato usando una funzione hash di crittografia combinata con una chiave segreta. Vedere [Valori hash](#hash_values) più avanti in questo argomento.  
  
-   <xref:System.Security.Cryptography.RC2CryptoServiceProvider>.  
  
-   <xref:System.Security.Cryptography.RijndaelManaged>.  
  
-   <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider>.  
  
 [Torna all'inizio](#top)  
  
<a name="public_key"></a>   
## Crittografia a chiave pubblica  
 a crittografia a chiave pubblica usa una chiave privata che deve essere tenuta segreta agli utenti non autorizzati e una chiave pubblica che può essere resa pubblica a tutti. La chiave pubblica e la chiave privata sono collegate matematicamente. I dati crittografati con la chiave pubblica possono essere decrittografati solo con la chiave privata e i dati firmati con la chiave privata possono essere verificati solo con la chiave pubblica. La chiave pubblica può essere distribuita a tutti in quanto viene usata per crittografare i dati da inviare a chi detiene la chiave privata. Gli algoritmi di crittografia a chiave pubblica sono noti anche come algoritmi asimmetrici, poiché per crittografare e successivamente decrittografare i dati è necessario usare due chiavi diverse. Una regola di crittografia di base proibisce il riutilizzo di chiavi ed entrambe le chiavi devono essere univoche per ogni sessione di comunicazione. In pratica, tuttavia, le chiavi asimmetriche sono in genere di lunga durata.  
  
 Le due parti, Alice e Bob, possono usare la crittografia a chiave pubblica come illustrato di seguito. Alice genera prima di tutto una coppia di chiavi pubblica\/privata. Se Bob vuole inviare ad Alice un messaggio crittografato, le chiede la chiave pubblica. Alice invia a Bob la chiave pubblica su una rete non sicura e Bob la usa per crittografare un messaggio. Bob invia il messaggio crittografato ad Alice, che lo decrittografa usando la sua chiave privata. Se Bob ha ricevuto la chiave di Alice su un canale non sicuro, ad esempio una rete pubblica, sarà esposto a un attacco di tipo man\-in\-the\-middle. Bob deve quindi verificare con Alice che la copia a sua disposizione della chiave pubblica sia corretta.  
  
 Durante la trasmissione della chiave pubblica di Alice, una persona non autorizzata potrebbe intercettare la chiave. La stessa persona potrebbe intercettare anche il messaggio crittografato da Bob. Tale persona, tuttavia, non potrà decrittografare il messaggio con la chiave pubblica. Il messaggio può essere decrittografato solo con la chiave privata di Alice che non è stata trasmessa. Alice non usa la propria chiave privata per crittografare un messaggio di risposta a Bob, poiché chiunque sia in possesso della chiave pubblica potrebbe decrittografare il messaggio. Se Alice vuole inviare un messaggio a Bob, gli chiede la chiave pubblica e crittografa il suo messaggio usando quella chiave. Bob decrittografa quindi il messaggio usando la sua chiave privata associata.  
  
 In questo scenario Alice e Bob usano la crittografia a chiave pubblica \(asimmetrica\) per trasferire una chiave segreta \(simmetrica\) e usano la crittografia a chiave segreta per il resto della sessione.  
  
 L'elenco seguente offre un confronto tra algoritmi di crittografia a chiave pubblica e a chiave segreta:  
  
-   Gli algoritmi di crittografia a chiave pubblica usano una dimensione fissa del buffer, mentre gli algoritmi di crittografia a chiave segreta usano un buffer a lunghezza variabile.  
  
-   Gli algoritmi di crittografia a chiave pubblica non possono essere usati per il concatenamento di dati in flussi come gli algoritmi di crittografia a chiave segreta, poiché è possibile crittografare solo piccole quantità di dati. Le operazioni asimmetriche non usano quindi lo stesso modello di streaming delle operazioni simmetriche.  
  
-   La crittografia a chiave pubblica ha uno spazio delle chiavi \(intervallo dei valori possibili\) molto più ampio rispetto alla crittografia a chiave segreta, pertanto è meno esposta a tecniche esaustive per scoprire la chiave.  
  
-   Le chiavi pubbliche possono essere distribuite in modo semplice poiché non è necessario proteggerle, purché sia possibile verificare l'identità del mittente.  
  
-   Alcuni algoritmi a chiave pubblica, ad esempio RSA e DSA, ma non Diffie\-Hellman, possono essere usati per creare firme digitali per la verifica dell'identità del mittente dei dati.  
  
-   Gli algoritmi a chiave pubblica sono molto lenti rispetto a quelli a chiave segreta e non sono destinati alla crittografia di grandi quantità di dati. Risultano utili solo per il trasferimento di piccole quantità di dati. Generalmente la crittografia a chiave pubblica viene usata per crittografare una chiave e un vettore di inizializzazione utilizzabili da un algoritmo a chiave segreta. Dopo il trasferimento della chiave e del vettore di inizializzazione, la crittografia a chiave segreta viene usata per il resto della sessione.  
  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] offre le classi seguenti che implementano gli algoritmi della crittografia a chiave pubblica:  
  
-   <xref:System.Security.Cryptography.DSACryptoServiceProvider>  
  
-   <xref:System.Security.Cryptography.RSACryptoServiceProvider>  
  
-   <xref:System.Security.Cryptography.ECDiffieHellman> \(classe base\)  
  
-   <xref:System.Security.Cryptography.ECDiffieHellmanCng>  
  
-   <xref:System.Security.Cryptography.ECDiffieHellmanCngPublicKey> \(classe base\)  
  
-   <xref:System.Security.Cryptography.ECDiffieHellmanKeyDerivationFunction> \(classe base\)  
  
-   <xref:System.Security.Cryptography.ECDsaCng>  
  
 RSA consente sia la crittografia sia la firma, mentre DSA può essere usato solo per la firma e Diffie\-Hellman solo per la generazione di chiavi. In genere, gli algoritmi a chiave pubblica sono più limitati nell'utilizzo rispetto a quelli a chiave privata.  
  
 [Torna all'inizio](#top)  
  
<a name="digital_signatures"></a>   
## Firme digitali  
 Gli algoritmi a chiave pubblica possono essere usati per formare firme digitali, il cui obiettivo è l'autenticazione dell'identità di un mittente, se la chiave pubblica di quest'ultimo viene considerata attendibile, e la protezione dell'integrità dei dati. Attraverso una chiave pubblica generata da Alice, il destinatario dei suoi dati può verificare che siano stati inviati effettivamente da lei confrontando la firma digitale sui dati e la chiave pubblica di Alice.  
  
 Per apporre una firma digitale a un messaggio usando la crittografia a chiave pubblica, Alice applica prima di tutto un algoritmo hash al messaggio per creare un digest del messaggio. Il digest è una rappresentazione dei dati compatta e univoca. Alice quindi crittografa il digest del messaggio con la sua chiave privata per creare la sua firma personale. Alla ricezione del messaggio e della firma, Bob decrittografa la firma con la chiave pubblica di Alice per recuperare il digest del messaggio e genera un hash mediante lo stesso algoritmo hash inviato da Alice. Se il digest del messaggio calcolato da Bob corrisponde esattamente al digest del messaggio ricevuto da Alice, Bob ha la certezza che il messaggio provenga dal possessore della chiave privata e che i dati non siano stati modificati. Se Bob ha la certezza che Alice sia il possessore della chiave privata, saprà che il messaggio proviene solo da Alice.  
  
> [!NOTE]
>  Chiunque può verificare una firma, poiché la chiave pubblica del mittente è di pubblico dominio e generalmente viene inclusa nel formato della firma digitale. Questo metodo non mantiene la segretezza del messaggio. Perché possa essere segreto, anche il messaggio deve essere crittografato.  
  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] offre le classi seguenti che implementano gli algoritmi della firma digitale:  
  
-   <xref:System.Security.Cryptography.DSACryptoServiceProvider>  
  
-   <xref:System.Security.Cryptography.RSACryptoServiceProvider>  
  
-   <xref:System.Security.Cryptography.ECDsa> \(classe base\)  
  
-   <xref:System.Security.Cryptography.ECDsaCng>  
  
 [Torna all'inizio](#top)  
  
<a name="hash_values"></a>   
## Valore hash  
 Gli algoritmi hash associano valori binari di lunghezza arbitraria a piccoli valori binari di lunghezza fissa, noti come valori hash. Per valore hash si intende una rappresentazione numerica di una porzione di dati. Se si inserisce un hash in un paragrafo di testo non crittografato e si modifica anche una sola lettera del paragrafo, un hash successivo produrrà un valore diverso. Se l'hash è basato su una crittografia avanzata, il relativo valore verrà modificato in modo significativo. Se ad esempio viene modificato un singolo bit di un messaggio, una funzione hash sicura può produrre un output che si differenzia del 50%. Molti valori di input possono avere hash dello stesso valore di output. Dal punto di vista del calcolo, tuttavia, è impossibile trovare due input di versi che forniscono come risultato un hash con lo stesso valore.  
  
 Due parti \(Alice e Bob\) sono riuscite a usare una funzione hash per garantire l'integrità del messaggio. Hanno selezionato un algoritmo di hash per firmare i messaggi. Alice ha scritto un messaggio, quindi ha creato un hash di tale messaggio tramite l'algoritmo selezionato. Hanno quindi seguito uno dei metodi seguenti:  
  
-   Alice invia il messaggio come testo normale e il messaggio con hash \(firma digitale\) a Bob. Bob riceve il messaggio, ne esegue l'hashing, quindi confronta il proprio valore hash con quello che ha ricevuto da Alice. Se i valori hash corrispondono, il messaggio non è stato alterato. Se invece i valori non corrispondono, il messaggio è stato alterato dopo essere stato scritto da Alice.  
  
     Purtroppo, questo metodo non consente di stabilire l'autenticità del mittente. Chiunque può rappresentare Alice e inviare un messaggio a Bob. Possono usare lo stesso algoritmo hash per firmare il messaggio e tutto ciò che Bob è in grado di determinare è che il messaggio corrisponde alla relativa firma. Si tratta di una forma di attacco di tipo man\-in\-the\-middle. Per altre informazioni, vedere l'[esempio di comunicazioni protette con Cryptography Next Generation \(CNG\) in NIB](http://msdn.microsoft.com/it-it/8048e94e-054a-417b-87c6-4f5e26710e6e).  
  
-   Alice invia il messaggio come testo normale a Bob tramite un canale pubblico non protetto. Invia il messaggio con hash a Bob su un canale privato protetto. Bob riceve il messaggio in testo normale, ne esegue l'hashing, quindi confronta il valore hash con quello scambiato privatamente. Se i valori corrispondono, Bob può accertare quanto segue:  
  
    -   Il messaggio non è stato modificato.  
  
    -   Il mittente del messaggio \(Alice\) è autentico.  
  
     Perché il sistema funzioni, Alice deve nascondere il valore hash originale a tutte le parti ad eccezione di Bob.  
  
-   Alice invia il messaggio in testo normale a Bob tramite un canale pubblico non protetto e inserisce il messaggio con hash sul proprio sito Web pubblico.  
  
     Questo metodo consente di evitare la manomissione del messaggio impedendo a chiunque di modificare il valore hash. Anche se chiunque può leggere il messaggio e il relativo hash, il valore hash può essere modificato solo da Alice. Un utente non autorizzato che vuole rappresentare Alice necessita di accesso al sito Web di Alice.  
  
 Nessuno dei metodi precedenti impedisce la lettura dei messaggi di Alice, perché vengono trasmessi come testo normale. Una soluzione di sicurezza completa richiede le firme digitali \(firma dei messaggi\) e la crittografia.  
  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] offre le classi seguenti che implementano che implementano gli algoritmi di hash:  
  
-   <xref:System.Security.Cryptography.HMACSHA1>.  
  
-   <xref:System.Security.Cryptography.MACTripleDES>.  
  
-   <xref:System.Security.Cryptography.MD5CryptoServiceProvider>.  
  
-   <xref:System.Security.Cryptography.RIPEMD160>.  
  
-   <xref:System.Security.Cryptography.SHA1Managed>.  
  
-   <xref:System.Security.Cryptography.SHA256Managed>.  
  
-   <xref:System.Security.Cryptography.SHA384Managed>.  
  
-   <xref:System.Security.Cryptography.SHA512Managed>.  
  
-   Varianti HMAC di tutti gli algoritmi SHA \(Secure Hash Algorithm\), MD5 \(Message Digest 5\) e RIPEMD\-160.  
  
-   Implementazioni CryptoServiceProvider \(wrapper del codice gestito\) di tutti gli algoritmi SHA.  
  
-   Implementazioni CNG \(Cryptography Next Generation\) di tutti gli algoritmi MD5 e SHA.  
  
> [!NOTE]
>  I difetti di progettazione di MD5 sono stati individuati nel 1996 e SHA\-1 è stato consigliato in sostituzione. Nel 2004 sono stati individuati altri difetti e l'algoritmo MD5 non è più considerato sicuro. Anche l'algoritmo SHA\-1 si è rivelato non sicuro e attualmente è consigliato l'algoritmo SHA\-2.  
  
 [Torna all'inizio](#top)  
  
<a name="random_numbers"></a>   
## Generazione di numeri casuali  
 La generazione di numeri casuali è integrata in molte operazioni di crittografia. Le chiavi di crittografia, ad esempio, devono essere il più casuali possibile in modo che non sia possibile riprodurle. I generatori di numeri casuali di crittografia devono generare output che sia impossibile da prevedere con una probabilità superiore al 50%. Pertanto, qualsiasi metodo di previsione del bit di output successivo non deve avere una prestazione migliore della previsione casuale. Le classi in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] usano i generatori di numeri casuali per generare chiavi di crittografia.  
  
 La classe <xref:System.Security.Cryptography.RNGCryptoServiceProvider> è un'implementazione di un algoritmo di generazione di numeri casuali.  
  
 [Torna all'inizio](#top)  
  
<a name="clickonce"></a>   
## Manifesti ClickOnce  
 In [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] sono disponibili le classi di crittografia seguenti che consentono di ottenere e verificare informazioni sulle firme del manifesto per applicazioni distribuite con la [tecnologia ClickOnce](../Topic/ClickOnce%20Security%20and%20Deployment.md):  
  
-   La classe <xref:System.Security.Cryptography.ManifestSignatureInformation> ottiene informazioni su una firma del manifesto quando si usano i relativi overload del metodo <xref:System.Security.Cryptography.ManifestSignatureInformation.VerifySignature%2A>.  
  
-   È possibile usare l'enumerazione <xref:System.Security.ManifestKinds> per specificare i manifesti da verificare. Il risultato della verifica è uno dei valori di enumerazione <xref:System.Security.Cryptography.SignatureVerificationResult>.  
  
-   La classe <xref:System.Security.Cryptography.ManifestSignatureInformationCollection> fornisce una raccolta di sola lettura di oggetti <xref:System.Security.Cryptography.ManifestSignatureInformation> delle firme verificate.  
  
 Le classi seguenti forniscono inoltre informazioni specifiche sulla firma:  
  
-   <xref:System.Security.Cryptography.StrongNameSignatureInformation> contiene informazioni sulla firma con nome sicuro per un manifesto.  
  
-   <xref:System.Security.Cryptography.X509Certificates.AuthenticodeSignatureInformation> rappresenta le informazioni sulla firma Authenticode per un manifesto.  
  
-   <xref:System.Security.Cryptography.X509Certificates.TimestampInformation> contiene informazioni sul timestamp di una firma Authenticode.  
  
-   <xref:System.Security.Cryptography.X509Certificates.TrustStatus> fornisce un modo semplice per controllare se una firma Authenticode è attendibile.  
  
 [Torna all'inizio](#top)  
  
<a name="suite_b"></a>   
## Supporto per Suite B  
 [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] supporta l'insieme di algoritmi di crittografia Suite B pubblicati da National Security Agency \(NSA\). Per altre informazioni su Suite B, vedere la pagina relativa alla [scheda descrittiva della crittografia Suite B dell'agenzia NSA](http://go.microsoft.com/fwlink/?LinkId=100111).  
  
 Sono inclusi gli algoritmi seguenti:  
  
-   Algoritmo AES \(Advanced Encryption Standard\) con dimensioni della chiave di 128, 192 e 256 bit per la crittografia.  
  
-   Algoritmi SHA\-1, SHA\-256, SHA\-384 e SHA\-512 \(Secure Hash Algorithm\) per l'hashing. Gli ultimi tre sono in genere raggruppati e noti come SHA\-2.  
  
-   Algoritmo ECDSA \(Elliptic Curve Digital Signature Algorithm\) che usa curve di coefficienti di numeri primi di 256, 384 e 521 bit per la generazione della firma. La documentazione NSA definisce in modo specifico queste curve e le chiama P\-256, P\-384 e P\-521. Questo algoritmo viene fornito dalla classe <xref:System.Security.Cryptography.ECDsaCng>. e consente di firmare con una chiave privata e verificare la firma con una chiave pubblica.  
  
-   Algoritmo ECDH \(Elliptic Curve Diffie\-Hellman\) che usa curve di coefficienti di numeri primi di 256, 384 e 521 bit per lo scambio di chiave e la generazione della chiave privata. Questo algoritmo viene fornito dalla classe <xref:System.Security.Cryptography.ECDiffieHellmanCng>.  
  
 Nelle nuove classi <xref:System.Security.Cryptography.AesCryptoServiceProvider>, <xref:System.Security.Cryptography.SHA256CryptoServiceProvider>, <xref:System.Security.Cryptography.SHA384CryptoServiceProvider> e <xref:System.Security.Cryptography.SHA512CryptoServiceProvider> sono disponibili wrapper del codice gestito per le implementazioni certificate da FIPS \(Federal Information Processing Standard\) delle implementazioni AES, SHA\-256, SHA\-384 e SHA\-512.  
  
 [Torna all'inizio](#top)  
  
<a name="cng"></a>   
## Classi Cryptography Next Generation \(CNG\)  
 Le classi Cryptography Next Generation \(CNG\) forniscono un wrapper gestito intorno alle funzioni CNG native. CNG sostituisce CryptoAPI. Il nome di queste classi contiene "Cng". Elemento centrale delle classi wrapper CNG è la classe del contenitore di chiavi <xref:System.Security.Cryptography.CngKey> che astrae l'archiviazione e l'utilizzo delle chiavi CNG. Questa classe consente di archiviare in modo sicuro una coppia di chiavi o una chiave pubblica e fare riferimento a tale chiave usando un semplice nome di stringa. La classe di firma basata su curva ellittica <xref:System.Security.Cryptography.ECDsaCng> e la classe di crittografia <xref:System.Security.Cryptography.ECDiffieHellmanCng> possono usare oggetti <xref:System.Security.Cryptography.CngKey>.  
  
 La classe <xref:System.Security.Cryptography.CngKey> viene usata per una varietà di operazioni aggiuntive, incluse l'apertura, la creazione, l'eliminazione e l'esportazione di chiavi. Fornisce inoltre l'accesso all'handle di chiave sottostante da usare quando le funzioni native vengono chiamate direttamente.  
  
 [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] include anche varie classi CNG di supporto, quali le seguenti:  
  
-   <xref:System.Security.Cryptography.CngProvider> gestisce un provider di archiviazione chiavi.  
  
-   <xref:System.Security.Cryptography.CngAlgorithm> gestisce un algoritmo CNG.  
  
-   <xref:System.Security.Cryptography.CngProperty> gestisce proprietà di chiave usate frequentemente.  
  
 [Torna all'inizio](#top)  
  
<a name="related_topics"></a>   
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Cryptography Model](../../../docs/standard/security/cryptography-model.md)|Illustra il modo in cui la crittografia viene implementata nella libreria delle classi base.|  
|[Walkthrough: Creating a Cryptographic Application](../../../docs/standard/security/walkthrough-creating-a-cryptographic-application.md)|Illustra le attività di base di crittografia e decrittografia.|  
|[Configurazione di classi di crittografia](../../../docs/framework/configure-apps/configure-cryptography-classes.md)|Illustra come associare i nomi degli algoritmi a classi di crittografia e come associare identificatori di oggetti a un algoritmo di crittografia.|