---
title: "FindPrivateKey | Microsoft Docs"
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
  - "FindPrivateKey"
ms.assetid: 16b54116-0ceb-4413-af0c-753bb2a785a6
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# FindPrivateKey
Può essere difficile individuare il percorso e il nome del file di chiave privata associati a un certificato X.509 specifico nell'archivio certificati.Lo strumento FindPrivateKey.exe facilita questo processo.  
  
> [!IMPORTANT]
>  FindPrivateKey è un esempio che deve essere compilato prima dell'utilizzo.Vedere la sezione "Per compilare il progetto FindPrivateKey" riportata di seguito per istruzioni su come compilare lo strumento FindPrivateKey.  
  
 I certificati X.509 vengono installati da un amministratore o da qualsiasi utente nel computer.Tuttavia è possibile accedere al certificato da un servizio in esecuzione con un account diverso \(ad esempio, ASPNET su [!INCLUDE[wxp](../../../../includes/wxp-md.md)] o gli account Servizio di rete su [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]\).  
  
 Questo account può non avere accesso al file di chiave privata se il certificato non è stato originariamente installato.Lo strumento FindPrivateKey fornisce il percorso del file di chiave privata di un determinato certificato X.509.È possibile aggiungere o rimuovere autorizzazioni quando si conosce il percorso del file di chiave privata degli specifici certificati X.509.  
  
 Negli esempi in cui vengono utilizzati i certificati per la sicurezza, si adopera lo strumento FindPrivateKey nel file Setup.bat.Dopo aver individuato il file di chiave privata, è possibile utilizzare gli altri strumenti quali Cacls.exe per impostare i diritti di accesso appropriati sul file.  
  
 Quando si esegue un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] con un account utente, ad esempio un file eseguibile indipendente, accertarsi che l'account utente dispone dell'accesso in sola lettura al file.Se si esegue servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in Internet Information Services \(IIS\), gli account predefiniti utilizzati per eseguire il servizio sono ASPNET in [!INCLUDE[wxp](../../../../includes/wxp-md.md)] o Servizio di rete su [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)], che per impostazione predefinita non ha accesso al file di chiave privata.  
  
## Esempi  
 Quando si accede a un certificato per il quale il processo dispone del privilegio di lettura, viene visualizzato un messaggio di eccezione simile all'esempio seguente.  
  
```  
System.ArgumentException was unhandled  
Message="The certificate 'CN=localhost' must have a private key that is capable of key exchange.  The process must have access rights for the private key."  
Source="System.ServiceModel"  
```  
  
 Quando si verifica questo problema, utilizzare lo strumento FindPrivateKey per cercare il file di chiave privata e quindi impostare il diritto di accesso per il processo in cui è in esecuzione il servizio.Ad esempio, questa operazione può essere eseguita con lo strumento Cacls.exe, come illustrato nell'esempio seguente.  
  
```  
cacls.exe "C:\Documents and Settings\All Users\Application Data\Microsoft\Crypto\RSA\MachineKeys\8aeda5eb81555f14f8f9960745b5a40d_38f7de48-5ee9-452d-8a5a-92789d7110b1" /E /G "NETWORK SERVICE":R  
```  
  
#### Per compilare il progetto FindPrivateKey  
  
1.  Aprire [!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)], quindi spostarsi nella sottodirectory specifica del linguaggio del percorso della directory in cui si è installato l'esempio.  
  
2.  Fare doppio clic sull'icona del file con estensione sln per aprirlo in Visual Studio.  
  
3.  Scegliere **Ricompila soluzione** dal menu **Compila**.I file di programma client vengono compilati su client\\bin e i file del programma del servizio vengono compilati su service\\bin.  
  
4.  La compilazione della soluzione genera il file FindPrivateKey.exe.  
  
## Convenzioni: voci della riga di comando  
 "\[*option*\]" rappresenta un set di parametri facoltativo.  
  
 "{*option*}" rappresenta un set di parametri obbligatorio.  
  
 "*option1* &#124; *option2*" rappresenta una scelta tra i set di opzioni.  
  
 "\<*value*\>" rappresenta un valore di parametro da immettere.  
  
## Utilizzo  
  
```  
FindPrivateKey <storeName> <storeLocation> [{ {-n <subjectName>} | {-t <thumbprint>} } [-f | -d | -a]]  
```  
  
 Dove:  
  
```  
       <subjectName> The subject name of the certificate  
       <thumbprint>  The thumbprint of the certificate (You can use the Certmgr.exe tool to find this)  
       -f            output file name only  
       -d            output directory only  
       -a            output absolute file name  
```  
  
 Se non è specificato alcun parametro nel prompt dei comandi, viene visualizzato questo testo della Guida.  
  
## Esempi  
 In questo esempio viene ricercato il nome del file del certificato con un nome soggetto "CN\=localhost", nell'archivio Personale di Current User.FindPrivateKey My CurrentUser \- n "CN\=localhost".  
  
 In questo esempio viene ricercato il nome del file del certificato con un nome soggetto "CN\=localhost", nell'archivio Personale dell'utente corrente e viene generato il percorso completo.  
  
```  
User.FindPrivateKey My CurrentUser -n "CN=localhost" -a  
  
```  
  
 In questo esempio viene ricercato il nome del file del certificato con un'identificazione digitale di "03 33 98 63 d0 47 e7 48 71 33 62 64 76 5c 4c 9d 42 1d 6b 52", nell'archivio Personale del computer locale.  
  
```  
FindPrivateKey My LocalMachine -t "03 33 98 63 d0 47 e7 48 71 33 62 64 76 5c 4c 9d 42 1d 6b 52" –c  
```  
  
## Vedere anche