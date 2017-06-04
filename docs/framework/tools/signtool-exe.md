---
title: "SignTool.exe (Sign Tool) | Microsoft Docs"
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
  - "Sign tool"
  - "SignTool.exe"
ms.assetid: 0c25ff6c-bff3-422e-b017-146a3ee86cb9
caps.latest.revision: 33
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 33
---
# SignTool.exe (Sign Tool)
Lo strumento Firma è uno strumento da riga di comando per la firma digitale dei file, la verifica delle firme e l'aggiunta di timestamp nei file.  
  
 Viene installato automaticamente con Visual Studio.  Per eseguire lo strumento, usare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7.  Per altre informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Al prompt dei comandi digitare quanto segue:  
  
## Sintassi  
  
```  
  
signtool [command] [options] [file_name | ...]  
```  
  
#### Parametri  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|`command`|Uno dei quattro comandi \(`catdb`, `sign`, `Timestamp` o `Verify`\) che specifica l'operazione da eseguire su un file.  Per una descrizione di ogni comando, vedere la tabella successiva.|  
|`options`|Opzione che modifica un comando.  Oltre alle opzioni globali `/q` e `/v`, ciascun comando supporta un set univoco di opzioni.|  
|`file_name`|Il percorso di un file da firmare.|  
  
 Lo strumento Firma supporta i comandi seguenti.  Ogni comando è usato con set distinti di opzioni, elencati nelle rispettive sezioni.  
  
|Comando|Descrizione|  
|-------------|-----------------|  
|`catdb`|Aggiunge o rimuove un file di catalogo da un database di cataloghi.  I database dei cataloghi vengono usati per la ricerca automatica di file di catalogo e sono identificati dal GUID.  Per un elenco delle opzioni supportate dal comando `catdb`, vedere [Opzioni del comando catdb](../../../docs/framework/tools/signtool-exe.md#catdb).|  
|`sign`|Firma digitalmente i file.  Le firme digitali impediscono la manomissione dei file e consentono agli utenti di verificare il firmatario in base a un certificato di firma.  Per un elenco delle opzioni supportate dal comando `sign`, vedere [Opzioni del comando sign](../../../docs/framework/tools/signtool-exe.md#sign).|  
|`Timestamp`|Aggiunge un timestamp ai file.  Per un elenco delle opzioni supportate dal comando `TimeStamp`, vedere [Opzioni del comando TimeStamp](../../../docs/framework/tools/signtool-exe.md#TimeStamp).|  
|`Verify`|Verifica la firma digitale dei file determinando se il certificato di firma è stato emesso da un'autorità attendibile, se è stato revocato e, facoltativamente, se è valido per criteri specifici.  Per un elenco delle opzioni supportate dal comando `Verify`, vedere [Opzioni del comando Verify](../../../docs/framework/tools/signtool-exe.md#Verify).|  
  
 Le opzioni riportate di seguito si applicano a tutti i comandi dello strumento Firma.  
  
|Opzione globale|Descrizione|  
|---------------------|-----------------|  
|**\/q**|Non visualizza alcun output se il comando viene eseguito correttamente e visualizza un output minimo se il comando ha esito negativo.|  
|**\/v**|Visualizza un output dettagliato indipendentemente dall'esito del comando e visualizza messaggi di avviso.|  
|**\/debug**|Visualizza le informazioni di debug.|  
  
<a name="catdb"></a>   
## Opzioni del comando catdb  
 Nella tabella seguente vengono illustrate le opzioni utilizzabili con il comando `catdb`.  
  
|Opzione catdb|Descrizione|  
|-------------------|-----------------|  
|`/d`|Specifica che il database dei cataloghi predefinito viene aggiornato.  Se non si usa né l'opzione `/d` né l'opzione `/g`, viene aggiornato il database dei driver e dei componenti del sistema.|  
|`/g` *GUID*|Specifica che il database dei cataloghi identificato dall'identificatore univoco globale *GUID* viene aggiornato.|  
|`/r`|Rimuove i cataloghi specificati dal database dei cataloghi.  Se questa opzione non è specificata, i cataloghi specificati vengono aggiunti al database dei cataloghi.|  
|`/u`|Specifica che un nome univoco viene generato automaticamente per i file di catalogo aggiunti.  Se necessario, i file di catalogo vengono rinominati per evitare conflitti con i nomi dei file di catalogo esistenti.  Se questa opzione non è specificata, i cataloghi esistenti che hanno lo stesso nome dei cataloghi aggiunti vengono sovrascritti.|  
  
<a name="sign"></a>   
## Opzioni del comando sign  
 Nella tabella seguente vengono illustrate le opzioni utilizzabili con il comando `sign`.  
  
|Opzioni del comando sign|Descrizione|  
|------------------------------|-----------------|  
|`/a`|Seleziona automaticamente il miglior certificato di firma.  Verranno trovati tutti i certificati validi che soddisfano tutte le condizioni specificate e verrà selezionato quello valido per il periodo più lungo.  Se questa opzione non è presente, è prevista la presenza di un solo certificato di firma valido.|  
|`/ac`  *file*|Aggiunge un altro certificato dal *file* al blocco di firme.|  
|`/as`|Aggiunge questa firma.  Se non è presente alcuna firma primaria, questa firma viene impostata come primaria.|  
|`/c`  *NomeModCertificato*|Specifica un'estensione Microsoft, Certificate Template Name, per il certificato di firma.|  
|`/csp`  *NomeCSP*|Specifica il provider del servizio di crittografia \(CSP\) che contiene il contenitore di chiavi private.|  
|`/d`  *Desc*|Specifica una descrizione del contenuto firmato.|  
|`/du`  *URL*|Specifica un URL \(Uniform Resource Locator\) per la descrizione estesa del contenuto firmato.|  
|`/f`  *FileCertFirma*|Specifica il certificato di firma in un file.  Se il file è nel formato PFX \(Personal Information Exchange\) ed è protetto da una password, usare l'opzione `/p` per specificare la password.  Se il file non contiene chiavi private, usare le opzioni `/csp` e `/k` per specificare il CSP e il nome del contenitore delle chiavi private.|  
|`/fd`|Specifica l'algoritmo digest file da usare per creare le firme del file.  Il valore predefinito è SHA1.|  
|`/i`  *NomeAutEmittente*|Specifica il nome dell'emittente del certificato di firma.  Questo valore può essere una sottostringa dell'intero nome dell'emittente.|  
|`/kc`  *NomeContChiaviPriv*|Specifica il nome del contenitore delle chiavi private.|  
|`/n`  *NomeSoggetto*|Specifica il nome del soggetto del certificato di firma.  Questo valore può essere una sottostringa dell'intero nome del soggetto.|  
|`/nph`|Se supportato, sopprime gli hash delle pagine per i file eseguibili.  Il valore predefinito è determinato dalla variabile di ambiente SIGNTOOL\_PAGE\_HASHES e dalla versione di wintrust.dll.  Questa opzione viene ignorata per i file non PE.|  
|`/p`  *Password*|Specifica la password da usare all'apertura di un file PFX  \(usare l'opzione `/f` per specificare un file PFX\).|  
|`/p7` *Percorso*|Specifica di produrre un file PKCS \(Public Key Cryptography Standards\) \#7 per ogni file di contenuto specificato.  I file PKCS \#7 sono denominati *percorso*\\*nomefile*.p7.|  
|`/p7ce` *Valore*|Specifica le opzioni per il contenuto PKCS \#7 firmato.  Impostare *Valore* su "Embedded" per incorporare il contenuto firmato nel file PKCS \#7 o su "DetachedSignedData" per generare la parte di dati firmati di un file PKCS \#7 scollegato.  Se non si usa l'opzione `/p7ce`, il contenuto firmato è incorporato per impostazione predefinita.|  
|`/p7co` *\<OID\>*|Specifica l'identificatore di oggetto \(OID\) tramite cui viene identificato il contenuto PKCS \#7 firmato.|  
|`/ph`|Se supportato, genera gli hash delle pagine per i file eseguibili.|  
|`/r`  *NomeSoggRadice*|Specifica il nome del soggetto del certificato radice cui deve essere concatenato il certificato di firma.  Questo valore può essere una sottostringa dell'intero nome del soggetto del certificato radice.|  
|`/s`  *NomeArchivio*|Specifica l'archivio da aprire durante la ricerca del certificato.  Se questa opzione non è specificata, viene aperto l'archivio `My`.|  
|`/sha1`  *Hash*|Specifica l'hash SHA1 del certificato di firma.  Il valore hash SHA1 viene specificato in genere quando più certificati soddisfano i criteri specificati dalle opzioni rimanenti.|  
|`/sm`|Specifica di usare un archivio del computer anziché un archivio utente.|  
|`/t`  *URL*|Specifica l'URL del server di timestamp.  Se questa opzione \(o `/tr`\) non è presente, al file firmato non verrà aggiunto il timestamp.  Se l'aggiunta del timestamp non riesce, viene generato un avviso.  Non è possibile usare questa opzione con l'opzione `/tr`.|  
|`/td`  *alg*|Usata con l'opzione `/tr` per richiedere un algoritmo digest usato dal server di timestamp RFC 3161.|  
|`/tr`  *URL*|Specifica l'URL del server di timestamp RFC 3161.  Se questa opzione \(o `/t`\) non è presente, al file firmato non verrà aggiunto il timestamp.  Se l'aggiunta del timestamp non riesce, viene generato un avviso.  Non è possibile usare questa opzione con l'opzione `/t`.|  
|`/u`  *Utilizzo*|Specifica l'utilizzo chiavi avanzato \(EKU\) che deve essere presente nel certificato di firma.  Il valore di utilizzo può essere specificato tramite OID o stringa.  L'utilizzo predefinito è "Firma codice" \(1.3.6.1.5.5.7.3.3\).|  
|`/uw`|Specifica l'utilizzo di "Verifica dei componenti di sistema Windows" \(1.3.6.1.4.1.311.10.3.6\).|  
  
 Per esempi di utilizzo, vedere [Uso di SignTool per firmare un File](http://msdn.microsoft.com/library/windows/desktop/aa388170.aspx).  
  
<a name="TimeStamp"></a>   
## Opzioni del comando TimeStamp  
 Nella tabella seguente vengono illustrate le opzioni utilizzabili con il comando `TimeStamp`.  
  
|Opzione TimeStamp|Descrizione|  
|-----------------------|-----------------|  
|`/p7`|Aggiunge un timestamp ai file PKCS \#7.|  
|`/t` *URL*|Specifica l'URL del server di timestamp.  È necessario che il file a cui viene aggiunto il timestamp sia stato precedentemente firmato.  È richiesta l'opzione `/t` o `/tr`.|  
|`/td` *alg*|Richiede un algoritmo digest usato dal server di timestamp RFC 3161.  `/td` viene usata insieme all'opzione `/tr`.|  
|`/tp` *Indice*|Aggiunge un timestamp alla firma in corrispondenza di *indice*.|  
|`/tr` *URL*|Specifica l'URL del server di timestamp RFC 3161.  È necessario che il file a cui viene aggiunto il timestamp sia stato precedentemente firmato.  È richiesta l'opzione `/tr` o `/t`.|  
  
 Per un esempio di utilizzo, vedere [Aggiunta timestamp a file firmati in precedenza](http://msdn.microsoft.com/library/windows/desktop/aa375542.aspx).  
  
<a name="Verify"></a>   
## Opzioni del comando Verify  
  
|Opzione Verify|Descrizione|  
|--------------------|-----------------|  
|`/a`|Specifica che tutti i metodi possono essere usati per verificare il file.  Innanzitutto, viene effettuata una ricerca nei database dei cataloghi per determinare se il file è firmato in un catalogo.  Se non risulta firmato in alcun catalogo, viene effettuato un tentativo di verifica della firma incorporata del file.  Questa opzione è consigliata per la verifica di file che possono risultare firmati o non firmati all'interno di un catalogo.  Gli esempi di questi file includono i file o i driver di Windows.|  
|`/ad`|Trova il catalogo usando il database dei cataloghi predefinito.|  
|`/ag` *CatDBGUID*|Trova il catalogo nel database dei cataloghi identificato da *CatDBGUID*.|  
|`/all`|Verifica tutte le firme in un file che include più firme.|  
|`/as`|Trova il catalogo usando il database dei cataloghi \(driver\) dei componenti del sistema.|  
|`/c` *FileCat*|Specifica il file di catalogo in base al nome.|  
|`/d`|Specifica che lo strumento Firma deve visualizzare la descrizione e l'URL della descrizione.|  
|`/ds` *Indice*|Verifica la firma in una posizione specificata.|  
|`/hash` \(`SHA1` &#124;`SHA256`\)|Specifica un algoritmo hash facoltativo da usare quando si cerca un file in un catalogo.|  
|`/kp`|Specifica che la verifica deve essere eseguita con i criteri di firma del driver in modalità kernel.|  
|`/ms`|Usa semantica di verifica multipla.  Si tratta del comportamento predefinito di una chiamata [WinVerifyTrust](http://msdn.microsoft.com/library/windows/desktop/aa388208.aspx) in [!INCLUDE[win8](../../../includes/win8-md.md)] e versioni successive.|  
|`/o` *Versione*|Verifica il file in base alla versione del sistema operativo.  *Versione* ha il formato seguente: *IDPiattaforma*:*VersPrinc*.*VersSecond*.*NumeroBuild*.  *IDPiattaforma* rappresenta il valore sottostante di un membro dell'enumerazione <xref:System.PlatformID>. **Important:**  L'utilizzo dell'opzione `/o` è consigliato.  Se `/o` non è specificata, è possibile che vengano restituiti risultati imprevisti.  Ad esempio, se non si include l'opzione `/o`, i cataloghi di sistema che vengono convalidati correttamente in un sistema operativo precedente potrebbero non essere convalidati correttamente in un sistema operativo più nuovo.|  
|`/p7`|Verifica i file PKCS \#7.  Non viene usato alcun criterio esistente per la convalida PKCS \#7.  La firma viene controllata e viene creata una catena per il certificato di firma.|  
|`/pa`|Specifica che devono essere usati i criteri di verifica Authenticode predefiniti.  Se l'opzione `/pa` non è specificata, vengono usati i criteri di verifica dei driver di Windows.  Non è possibile usare questa opzione con le opzioni `catdb`.|  
|`/pg` *CriteriGUID*|Specifica i criteri di verifica in base al GUID.  *CriteriGUID* corrisponde all'IDAzione dei criteri di verifica.  Non è possibile usare questa opzione con le opzioni `catdb`.|  
|`/ph`|Specifica che lo strumento Firma deve visualizzare e verificare i valori hash delle pagine.|  
|`/r` *NomeSoggRadice*|Specifica il nome del soggetto del certificato radice cui deve essere concatenato il certificato di firma.  Questo valore può essere una sottostringa dell'intero nome del soggetto del certificato radice.|  
|`/tw`|Specifica che, se la firma non contiene un timestamp, deve essere generato un avviso.|  
  
 Per esempi di utilizzo, vedere [Uso di SignTool per verificare la firma di un file](http://msdn.microsoft.com/library/windows/desktop/aa388171.aspx).  
  
## Valore restituito  
 Lo strumento Firma restituisce uno dei seguenti codici di uscita quando termina.  
  
|Codice di uscita|Descrizione|  
|----------------------|-----------------|  
|0|Esecuzione completata correttamente.|  
|1|Esecuzione non riuscita.|  
|2|Esecuzione completata con avvisi.|  
  
## Esempi  
 Il seguente comando aggiunge il file di catalogo MyCatalogFileName.cat al database dei driver e dei componenti di sistema.  L'opzione `/v` genera un nome univoco, se necessario, per impedire la sostituzione di un file di catalogo esistente denominato `MyCatalogFileName.cat`.  
  
```  
signtool catdb /v /u MyCatalogFileName.cat  
```  
  
 Il comando seguente firma automaticamente un file usando il certificato migliore.  
  
```  
signtool sign /a MyFile.exe  
```  
  
 Il comando seguente appone una firma digitale a un file usando un certificato archiviato in un file PFX protetto da password.  
  
```  
signtool sign /f MyCert.pfx /p MyPassword MyFile.exe  
```  
  
 Il comando seguente appone una firma digitale e un timestamp a un file.  Il certificato usato per firmare il file è memorizzato in un file PFX.  
  
```  
signtool sign /f MyCert.pfx /t http://timestamp.verisign.com/scripts/timstamp.dll MyFile.exe  
```  
  
 Il comando seguente firma un file usando un certificato contenuto nell'archivio `My` con nome soggetto `My Company Certificate`.  
  
```  
signtool sign /n "My Company Certificate" MyFile.exe  
```  
  
 Il comando seguente firma un controllo ActiveX e fornisce le informazioni visualizzate da Internet Explorer quando viene richiesto all'utente di installare il controllo.  
  
```  
Signtool sign /f MyCert.pfx /d: "MyControl" /du http://www.example.com/MyControl/info.html MyControl.exe  
```  
  
 Il comando seguente appone un timestamp a un file a cui è già stata apposta una firma digitale.  
  
```  
signtool timestamp /t http://timestamp.verisign.com/scripts/timstamp.dll MyFile.exe  
```  
  
 Il comando seguente verifica che un file sia stato firmato.  
  
```  
signtool verify MyFile.exe  
```  
  
 Il comando seguente verifica un file di sistema che può essere firmato in un catalogo.  
  
```  
signtool verify /a SystemFile.dll  
```  
  
 Il comando seguente verifica un file di sistema firmato in un catalogo denominato `MyCatalog.cat`.  
  
```  
signtool verify /c MyCatalog.cat SystemFile.dll  
```  
  
## Vedere anche  
 [Tools](../../../docs/framework/tools/index.md)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)