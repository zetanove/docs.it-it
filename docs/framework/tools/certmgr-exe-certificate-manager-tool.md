---
title: "Certmgr.exe (Certificate Manager Tool) | Microsoft Docs"
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
  - "certificates, managing"
  - "CRLs"
  - "certificate trust lists"
  - "Certmgr.exe"
  - "Certificate Manager tool"
  - "CTLs"
  - "certificate revocation lists"
ms.assetid: 7e953b43-1374-4bbc-814f-53ca1b6b52bb
caps.latest.revision: 27
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 27
---
# Certmgr.exe (Certificate Manager Tool)
Lo strumento di gestione certificati \(Certmgr.exe\) gestisce certificati, elenchi di scopi consentiti ai certificati ed elenchi di revoche di certificati \(CRL, Certificate Revocation List\).  
  
 Lo strumento viene installato automaticamente insieme a Visual Studio.  Per avviare lo strumento, utilizzare il [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
> [!NOTE]
>  Lo strumento di gestione dei certificati \(Certmgr.exe\) è un'utilità da riga di comando, da non confondere con lo snap\-in certificati \(Certmgr.msc\) di Microsoft Management Console \(MMC\).  Poiché Certmgr.msc in genere si trova nella directory di sistema di Windows, l'immissione di `certmgr` nella riga di comando potrebbe caricare lo snap\-in anche se è stato aperto il prompt dei comandi di Visual Studio.  Questo accade perché il percorso dello snap\-in precede il percorso dello strumento di gestione dei certificati nella variabile di ambiente PATH.  Se si verifica questo problema, è possibile eseguire i comandi Certmgr.exe specificando il percorso dell'eseguibile.  
  
 Viene installato automaticamente con Visual Studio.  Per eseguire lo strumento, utilizzare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7.  Per altre informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Per una panoramica dei certificati X.509, vedere [Utilizzo dei certificati](../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
 Al prompt dei comandi digitare quanto segue:  
  
## Sintassi  
  
```  
  
certmgr [/add | /del | /put] [options] [/s[/r registryLocation]] [sourceStorename] [/s[/r registryLocation]] [destinationStorename]  
```  
  
#### Parametri  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|*sourceStorename*|Archivio certificati contenente certificati, elenchi di scopi consentiti ai certificati o CRL da aggiungere, eliminare, salvare o visualizzare.  Può trattarsi di un file di archivio o di un archivio di sistema.|  
|*destinationStorename*|File o archivio certificati di output.|  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/add**|Aggiunge certificati, elenchi di scopi consentiti ai certificati e CRL a un archivio certificati.|  
|**\/all**|Aggiunge tutte le voci se utilizzata con **\/add**,  le elimina se utilizzata con **\/del** e le visualizza se utilizzata senza le opzioni **\/add** o **\/del**.  Non è possibile usare l'opzione **\/all** con **\/put**.|  
|**\/c**|Aggiunge i certificati se utilizzata con **\/add**,  li elimina se utilizzata con **\/del** e li salva se utilizzata con **\/put**.  Visualizza certificati quando utilizzata senza le opzioni **\/add**, **\/del** o **\/put**.|  
|**\/CRL**|Aggiunge i CRL se utilizzati con **\/add**,  li elimina se utilizzati con **\/del** e li salva se utilizzata con **\/put**.  Visualizza CRL quando utilizzata senza le opzioni **\/add**, **\/del** o **\/put**.|  
|**\/CTL**|Aggiunge gli elenchi di scopi consentiti se utilizzata con **\/add**,  li elimina se utilizzata con **\/del** e li salva se utilizzata con **\/put**.  Visualizza gli elenchi di scopi consentiti quando utilizzata senza le opzioni **\/add**, **\/del** o **\/put**.|  
|**\/del**|Elimina certificati, elenchi di scopi consentiti e CRL da un archivio certificati.|  
|**\/e** *encodingType*|Specifica il tipo di codifica dei certificati.  Il valore predefinito è `X509_ASN_ENCODING`.|  
|**\/f** *dwFlags*|Specifica il flag di archivio aperto.  Si tratta del parametro *dwFlags* passato a **CertOpenStore**.  Il valore predefinito è CERT\_SYSTEM\_STORE\_CURRENT\_USER.  Questa opzione viene considerata solo se viene utilizzata l'opzione **\/y**.|  
|**\/h**\[**elp**\]|Visualizza la sintassi e le opzioni di comando dello strumento.|  
|**\/n** *nam*|Specifica il nome comune del certificato da aggiungere, eliminare o salvare.  È possibile usare questa opzione solo con certificati, non con elenchi di scopi consentiti o CRL.|  
|**\/put**|Salva su file un certificato X.509, un elenco di scopi consentiti o un CRL da un archivio certificati.  Il file viene salvato nel formato X.509.  È possibile usare l'opzione **\/7** con l'opzione **\/put** per salvare il file nel formato PKCS \#7.  L'opzione **\/put** deve essere seguita da **\/c**, **\/CTL** o **\/CRL**.  Non è possibile usare l'opzione **\/all** con **\/put**.|  
|**\/r** *location*|Identifica la posizione dell'archivio di sistema all'interno del Registro di sistema.  Questa opzione viene considerata solo se viene specificata l'opzione **\/s**.  *location* deve essere uno degli elementi seguenti:<br /><br /> -   `currentUser` indica che l'archivio certificati si trova sotto la chiave HKEY\_CURRENT\_USER.  Questa è l'impostazione predefinita.<br />-   `localMachine` indica che l'archivio certificati si trova sotto la chiave HKEY\_LOCAL\_MACHINE.|  
|**\/s**|Indica che l'archivio certificati è un archivio di sistema.  Se non si specifica questa opzione, l'archivio viene considerato come **StoreFile**.|  
|**\/sha1** *sha1Hash*|Specifica l'hash SHA1 del certificato, dell'elenco di scopi consentiti o del CRL da aggiungere, eliminare o salvare.|  
|**\/v**|Specifica la modalità dettagliata. Visualizza informazioni dettagliate su certificati, elenchi di scopi consentiti e CRL.  Non è possibile usare questa opzione con le opzioni **\/add**, **\/del** o **\/put**.|  
|**\/y** *provider*|Specifica il nome del provider dell'archivio.|  
|**\/7**|Salva l'archivio di destinazione come oggetto PKCS \#7.|  
|**\/?**|Visualizza la sintassi e le opzioni di comando dello strumento.|  
  
## Note  
 Certmgr.exe svolge le seguenti funzioni di base:  
  
-   Visualizza certificati, elenchi di scopi consentiti e CRL sulla console.  
  
-   Aggiunge certificati, elenchi di scopi consentiti ai certificati e CRL a un archivio certificati.  
  
-   Elimina certificati, elenchi di scopi consentiti e CRL da un archivio certificati.  
  
-   Salva su file un certificato X.509, un elenco di scopi consentiti o un CRL da un archivio certificati.  
  
 Certmgr.exe funziona con due tipi di archivi certificati: **StoreFile** e archivi di sistema.  Non è necessario specificare il tipo di archivio certificati: Certmgr.exe è infatti in grado di identificare il tipo di archivio e di eseguire le operazioni appropriate.  
  
 Se Certmgr.exe viene eseguito senza specificare alcuna opzione, verrà avviato lo snap\-in certmgr.msc, che comprende una GUI che assisterà l'utente nell'esecuzione delle attività di gestione dei certificati disponibili anche dalla riga di comando.  La GUI fornisce una procedura guidata di importazione che consente di copiare certificati, elenchi di scopi consentiti e CRL dal disco a un archivio certificati.  
  
 È possibile trovare i nomi degli archivi X509Certificate per i parametri `destinationStorename` e `sourceStorename` compilando ed eseguendo il codice seguente.  
  
 [!code-csharp[Tools.CertMgr#1](../../../samples/snippets/csharp/VS_Snippets_CLR/tools.certmgr/cs/storenames1.cs#1)]
 [!code-vb[Tools.CertMgr#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/tools.certmgr/vb/storenames1.vb#1)]  
  
 Per altre informazioni sui certificati, vedere [Utilizzo dei certificati](../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
## Esempi  
 Il comando che segue visualizza un archivio di sistema predefinito denominato `my` con output dettagliato.  
  
```  
certmgr /v /s my  
```  
  
 Il comando che segue aggiunge tutti i certificati contenuti in un file denominato `myFile.ext` in un nuovo file denominato `newFile.ext`.  
  
```  
certmgr /add /all /c myFile.ext newFile.ext  
```  
  
 Il comando che segue aggiunge il certificato contenuto in un file denominato `testcert.cer` all'archivio di sistema `my`.  
  
```  
certmgr /add /c testcert.cer /s my  
```  
  
 Il comando che segue aggiunge il certificato contenuto in un file denominato `TrustedCert.cer` all'archivio certificati radice.  
  
```  
certmgr /c /add TrustedCert.cer /s root  
```  
  
 Il comando che segue salva un certificato con il nome comune `myCert` contenuto nell'archivio di sistema `my` in un file denominato `newCert.cer`.  
  
```  
certmgr /add /c /n myCert /s my newCert.cer  
```  
  
 Il comando che segue elimina tutti gli elenchi di scopi consentiti contenuti nell'archivio di sistema `my` e salva l'archivio ottenuto in un file denominato `newStore.str`.  
  
```  
certmgr /del /all /ctl /s my newStore.str  
```  
  
 Il comando che segue salva nel file `newFile` un certificato contenuto nell'archivio di sistema `my`.  Verrà chiesto di inserire il numero del certificato presente in `my` per inserirlo in `newFile`.  
  
```  
certmgr /put /c /s my newFile  
```  
  
## Vedere anche  
 [Tools](../../../docs/framework/tools/index.md)   
 [Makecert.exe \(Certificate Creation Tool\)](../Topic/Makecert.exe%20\(Certificate%20Creation%20Tool\).md)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)