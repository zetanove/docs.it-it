---
title: "Sn.exe (Strong Name Tool) | Microsoft Docs"
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
  - "public keys, signing files"
  - "Strong Name tool"
  - "Sn.exe"
  - "assemblies [.NET Framework], signing"
  - "signing files"
  - "strong-named assemblies, signing files"
  - "key pairs for signing files"
ms.assetid: c1d2b532-1b8e-4c7a-8ac5-53b801135ec6
caps.latest.revision: 44
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 44
---
# Sn.exe (Strong Name Tool)
Lo strumento Nome sicuro \(Sn.exe\) consente di firmare assembly con [nomi sicuri](../../../docs/framework/app-domains/strong-named-assemblies.md).  Lo strumento offre diverse opzioni per la gestione delle chiavi e la generazione e la verifica delle firme.  
  
 Per altre informazioni sui nomi sicuri e sugli assembly con nomi sicuri, vedere [Assembly con nomi sicuri](../../../docs/framework/app-domains/strong-named-assemblies.md) e [Procedura: firmare un assembly con un nome sicuro](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md).  
  
 Lo strumento Nome Sicuro viene installato automaticamente con Visual Studio.  Per avviare lo strumento, usare il prompt dei comandi per lo sviluppatore \(o il prompt dei comandi di Visual Studio in Windows 7\).  Per altre informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
> [!NOTE]
>  Nei computer a 64 bit, eseguire la versione a 32 bit di Sn.exe tramite il prompt dei comandi di Visual Studio e la versione a 64 bit tramite il prompt dei comandi di Visual Studio x64 Win64.  
  
 Al prompt dei comandi digitare quanto segue:  
  
## Sintassi  
  
```  
  
sn [-quiet][option [parameter(s)]]  
```  
  
#### Parametri  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\-a** *identityKeyPairFile* *signaturePublicKeyFile*|Genera dati <xref:System.Reflection.AssemblySignatureKeyAttribute> per eseguire la migrazione della chiave di identità alla chiave di firma da un file.|  
|**\-ac** *identityPublicKeyFile* *identityKeyPairContainer* *signaturePublicKeyFile*|Genera dati <xref:System.Reflection.AssemblySignatureKeyAttribute> per eseguire la migrazione della chiave di identità alla chiave di firma da un contenitore di chiavi.|  
|**\-c** \[*csp*\]|Imposta il provider del servizio di crittografia \(CSP\) predefinito da usare per la firma con nome sicuro.  Questa impostazione ha effetto sull'intero computer.  Se non si specifica alcun nome CSP, l'impostazione corrente viene cancellata.|  
|**\-d** *container*|Elimina dal CSP del nome sicuro il contenitore delle chiavi specificato.|  
|**\-D**  *assembly1 assembly2*|Verifica che due assembly differiscano solo nella firma.  Questa opzione è spesso usata come controllo dopo che un assembly è stato nuovamente firmato con una coppia di chiavi differente.|  
|**\-e**  *assembly outfile*|Estrae la chiave pubblica da *assembly* e la archivia in *outfile.*|  
|**\-h**|Visualizza la sintassi e le opzioni di comando dello strumento.|  
|**\-i** *infile container*|Installa la coppia di chiavi da *infile*nel contenitore delle chiavi specificato.  Il contenitore delle chiavi si trova nel CSP del nome sicuro.|  
|**\-k** \[*keysize*\] *outfile*|Genera una nuova chiave <xref:System.Security.Cryptography.RSACryptoServiceProvider> con la dimensione indicata e la scrive nel file specificato.  Nel file vengono scritte sia la chiave pubblica sia la chiave privata.<br /><br /> Se non si specifica una dimensione per la chiave, verrà generata una chiave a 1024 bit se è installato Microsoft Enhanced Cryptographic Provider; in caso contrario, verrà generata una chiave a 512 bit.<br /><br /> Se è installato Microsoft Enhanced Cryptographic Provider, il parametro *keysize* supporta lunghezze di chiave da 384 a 16.384 bit con incrementi di 8 bit.  Se è stato installato Microsoft Base Cryptographic Provider, supporta lunghezze di chiave da 384 a 512 bit per incrementi di 8 bit.|  
|**\-m** \[**y** *&#124;* **n**\]|Indica se i contenitori delle chiavi sono specifici del computer o dell'utente.  Se si specifica *y*, i contenitori delle chiavi sono specifici del computer.  Se si specifica *n*, i contenitori delle chiavi sono specifici dell'utente.<br /><br /> Se non si specifica né y né n, questa opzione visualizzerà l'impostazione corrente.|  
|**\-o**  *infile* \[*outfile*\]|Estrae la chiave pubblica da *infile* e la archivia in un file .csv.  I byte della chiave pubblica sono separati da virgole.  Questo formato è utile per gestire i riferimenti hardcoded alle chiavi sotto forma di matrici inizializzate nel codice sorgente.  Se non si specifica *outfile*, questa opzione inserirà l'output negli Appunti. **Note:**  Questa opzione non verifica che l'input sia solo una chiave pubblica.  Se in `infile` è contenuta una coppia di chiavi con una chiave privata, verrà estratta anche la chiave privata.|  
|**\-p** *infile outfile* \[*hashalg*\]|Estrae la chiave pubblica dalla coppia di chiavi in *infile* e la archivia in *outfile*, eventualmente usando l'algoritmo RSA specificato da *hashalg*.  È possibile usare questa chiave pubblica per ritardare la firma di un assembly mediante le opzioni **\/delaysign\+** and **\/keyfile** di [Assembly Linker \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md).  Quando per un assembly è impostata la firma ritardata, in fase di compilazione viene impostata solo la chiave pubblica e nel file viene riservato spazio per la firma che verrà aggiunta in un secondo momento, quando sarà nota la chiave privata.|  
|**\-pc**  *container* *outfile* \[*hashalg*\]|Estrae la chiave pubblica dalla coppia di chiavi in *container* e la archivia in *outfile*.  Se si usa l'opzione *hashalg*, l'algoritmo RSA viene usato per estrarre la chiave pubblica.|  
|**\-Pb** \[**y** *&#124;* **n**\]|Specifica se sono applicati i criteri per ignorare i nomi sicuri.  Se si specifica *y*, i nomi sicuri per gli assembly con attendibilità totale non vengono convalidati se caricati in <xref:System.AppDomain> con attendibilità totale.  Se si specifica *n*, i nomi sicuri vengono convalidati per verificare se sono corretti, ma non per individuare un nome sicuro specifico.  <xref:System.Security.Permissions.StrongNameIdentityPermission> non ha effetto sugli assembly con attendibilità totale.  È necessario eseguire un controllo manuale per rilevare una corrispondenza di nomi sicuri.<br /><br /> Se non si specifica né `y` né `n`, questa opzione visualizzerà l'impostazione corrente.  Il valore predefinito è `y`. **Note:**  Nei computer a 64 bit è necessario impostare questo parametro sia nell'istanza di Sn.exe a 32 bit che in quella a 64 bit.|  
|**\-q**\[**uiet**\]|Specifica la modalità non interattiva. Evita la visualizzazione dei messaggi di esito positivo.|  
|**\-R**\[**a**\] *assembly* *infile*|Firma nuovamente un assembly firmato in precedenza o con firma ritardata con la coppia di chiavi presente in *infile*.<br /><br /> Se si usa **\-Ra**, vengono ricalcolati gli hash per tutti i file nell'assembly.|  
|**\-Rc**\[**a**\] *assembly container*|Firma nuovamente un assembly firmato in precedenza o con firma ritardata con la coppia di chiavi presente in*container*.<br /><br /> Se si usa **\-Rca**, vengono ricalcolati gli hash per tutti i file nell'assembly.|  
|**\-Rh** *assembly*|Ricalcola gli hash per tutti i file dell'assembly.|  
|**\-t**\[**p**\] *infile*|Visualizza il token per la chiave pubblica archiviata in *infile*.  Il contenuto di *infile* deve essere una chiave pubblica generata in precedenza da un file di coppia di chiavi usando **\-p**.  Non usare l'opzione **\-t\[p\]** per estrarre il token direttamente dal file di coppia di chiavi.<br /><br /> Sn.exe calcola il token usando una funzione hash tratta dalla chiave pubblica.  Per risparmiare spazio, Common Language Runtime archivia i token di chiave pubblica nel manifesto come parte di un riferimento a un altro assembly quando registra una dipendenza in un assembly con nome sicuro.  L'opzione **\-tp** visualizza anche la chiave pubblica, oltre al token.  Se all'assembly è stato applicato l'attributo <xref:System.Reflection.AssemblySignatureKeyAttribute>, il token è per la chiave di identità e viene visualizzato il nome dell'algoritmo hash e della chiave di identità.<br /><br /> Questa opzione non verifica la firma dell'assembly e non deve essere usata per prendere decisioni sull'attendibilità.  Serve solo a visualizzare i dati non elaborati del token della chiave pubblica.|  
|**\-T**\[**p**\] *assembly*|Visualizza il token della chiave pubblica per *assembly.*  *assembly*  deve corrispondere al nome di un file contenente un manifesto dell'assembly.<br /><br /> Sn.exe calcola il token usando una funzione hash tratta dalla chiave pubblica.  Per risparmiare spazio, il runtime archivia i token di chiave pubblica nel manifesto come parte di un riferimento a un altro assembly quando registra una dipendenza in un assembly con nome sicuro.  L'opzione **\-Tp** visualizza anche la chiave pubblica, oltre al token.  Se all'assembly è stato applicato l'attributo <xref:System.Reflection.AssemblySignatureKeyAttribute>, il token è per la chiave di identità e viene visualizzato il nome dell'algoritmo hash e della chiave di identità.<br /><br /> Questa opzione non verifica la firma dell'assembly e non deve essere usata per prendere decisioni sull'attendibilità.  Serve solo a visualizzare i dati non elaborati del token della chiave pubblica.|  
|`-TS`  `assembly` `infile`|Applica la firma di test all'`assembly` firmato o parzialmente firmato con la coppia di chiavi presente in `infile`.|  
|\-`TSc` `assembly` `container`|Applica la firma di test all'`assembly` firmato o parzialmente firmato con la coppia di chiavi presente nel contenitore di chiavi `container`.|  
|**\-v** *assembly*|Verifica il nome sicuro di *assembly*, dove *assembly* è il nome di un file contenente un manifesto dell'assembly.|  
|**\-vf**  *assembly*|Verifica il nome sicuro in *assembly.* A differenza dall'opzione **\-v**, **\-vf** forza la verifica, anche se questa è stata disabilitata mediante l'opzione **\-Vr**.|  
|**\-Vk**  *regfile.reg* *assembly* \[*userlist*\] \[*infile*\]|Crea un file con voci di registrazione \(.reg\) che è possibile usare per registrare l'assembly specificato e poter saltare la verifica.  Le regole di denominazione dell'assembly che si applicano all'opzione **\-Vr** si applicano anche a **\-Vk**.  Per informazioni sulle opzioni *userlist* e *infile*, vedere l'opzione **\-Vr**.|  
|**\-Vl**|Elenca le impostazioni correnti per la verifica del nome sicuro nel computer.|  
|**\-Vr**  *assembly* \[*userlist*\] \[*infile*\]|Registra *assembly* per saltare la verifica.  Facoltativamente, è possibile specificare un elenco delimitato da virgole di nomi utente a cui applicare il salto della verifica.  Se si specifica *infile*, la verifica resta abilitata, ma nelle operazioni di verifica verrà usata la chiave pubblica contenuta in *infile*.  È possibile specificare *assembly* nel formato *\*, strongname* per registrare tutti gli assembly con il nome sicuro specificato.  *strongname* deve essere specificato come stringa di cifre esadecimali che rappresenta la chiave pubblica in formato token.  Vedere le opzioni **\-t** e **\-T** per visualizzare il token della chiave pubblica. **Caution:**  Usare questa opzione solo durante lo sviluppo.  L'aggiunta di un assembly all'elenco di omissione della verifica rende vulnerabile il sistema di sicurezza.  Un assembly dannoso potrebbe usare il nome completamente specificato \(nome assembly, versione, impostazioni cultura e token della chiave pubblica\) dell'assembly aggiunto all'elenco di omissione della verifica per camuffare la propria identità.  La verifica verrebbe omessa quindi anche per l'assembly dannoso.|  
|||  
|**\-Vu**  *assembly*|Annulla la registrazione di *assembly* per saltare la verifica.  Per **\-Vu** valgono le stesse regole di denominazione dell'assembly applicate per **\-Vr**.|  
|**\-Vx**|Rimuove tutte le voci di salto della verifica.|  
|**\-?**|Visualizza la sintassi e le opzioni di comando dello strumento.|  
  
> [!NOTE]
>  Per essere valide, le opzioni di Sn.exe devono essere digitate esattamente come indicato, rispettando con precisione la combinazione di maiuscole e minuscole.  
  
## Note  
 Le opzioni **\-R** e **\-Rc** sono utili con gli assembly per i quali è stata impostata la firma ritardata.  In questo scenario solo la chiave pubblica viene impostata in fase di compilazione e la firma viene apposta in un secondo tempo, quando sarà nota la chiave privata.  
  
> [!NOTE]
>  Per i parametri \(ad esempio, –**Vr\)** che scrivono in risorse protette quali il Registro di sistema, eseguire il comando SN.exe come amministratore.  
  
## Esempi  
 Il comando che segue crea una nuova coppia casuale di chiavi e la archivia in `keyPair.snk`.  
  
```  
sn -k keyPair.snk  
```  
  
 Il comando che segue archivia la chiave presente in `keyPair.snk` all'interno del contenitore `MyContainer` nel CSP del nome sicuro.  
  
```  
sn -i keyPair.snk MyContainer  
```  
  
 Il comando che segue estrae la chiave pubblica da `keyPair.snk` e la archivia in `publicKey.snk`.  
  
```  
sn -p keyPair.snk publicKey.snk  
```  
  
 Il comando che segue visualizza la chiave pubblica e il token per la chiave pubblica contenuti in `publicKey.snk`.  
  
```  
sn -tp publicKey.snk  
```  
  
 Il comando che segue verifica l'assembly `MyAsm.dll`.  
  
```  
sn -v MyAsm.dll  
```  
  
 Il comando che segue elimina `MyContainer` dal CSP predefinito.  
  
```  
sn -d MyContainer  
```  
  
## Vedere anche  
 [Tools](../../../docs/framework/tools/index.md)   
 [Al.exe \(Assembly Linker\)](../../../docs/framework/tools/al-exe-assembly-linker.md)   
 [Assembly con nomi sicuri](../../../docs/framework/app-domains/strong-named-assemblies.md)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)