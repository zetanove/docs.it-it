---
title: "Walkthrough: Creating a Cryptographic Application | Microsoft Docs"
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
  - "cryptography [NET Framework], example"
  - "cryptography [NET Framework], cryptographic application example"
  - "cryptography [NET Framework], application example"
ms.assetid: abf48c11-1e72-431d-9562-39cf23e1a8ff
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# Walkthrough: Creating a Cryptographic Application
Questa procedura dettagliata illustra come crittografare e decrittografare il contenuto.  Gli esempi di codice sono progettati per un'applicazione Windows Forms.  Questa applicazione non illustra situazioni del mondo reale, come l'utilizzo di smart card.  Al contrario illustra gli aspetti fondamentali della crittografia e decrittografia.  
  
 Questa procedura dettagliata usa le linee guida seguenti per la crittografia:  
  
-   Usare la classe <xref:System.Security.Cryptography.RijndaelManaged>, un algoritmo simmetrico, per crittografare e decrittografare dati mediante le proprietà <xref:System.Security.Cryptography.SymmetricAlgorithm.Key%2A> e <xref:System.Security.Cryptography.SymmetricAlgorithm.IV%2A> generate automaticamente.  
  
-   Usare <xref:System.Security.Cryptography.RSACryptoServiceProvider>, un algoritmo generato automaticamente, per crittografare e decrittografare la chiave di dati crittografati da <xref:System.Security.Cryptography.RijndaelManaged>.  Gli algoritmi asimmetrici sono ideali per più piccole quantità di dati, come ad esempio una chiave.  
  
    > [!NOTE]
    >  Se si vogliono proteggere dati sul computer anziché scambiare contenuto crittografato con altri utenti, è possibile usare le classi <xref:System.Security.Cryptography.ProtectedData> o <xref:System.Security.Cryptography.ProtectedMemory>.  
  
 Nella seguente tabella sono riepilogate le attività crittografate in questo argomento.  
  
|Attività|Descrizione|  
|--------------|-----------------|  
|Creazione di un'applicazione Windows Form|Elenca i controlli necessari per l'esecuzione dell'applicazione.|  
|Dichiarazione di oggetti globali|Dichiara le variabili del percorso stringa, <xref:System.Security.Cryptography.CspParameters> e <xref:System.Security.Cryptography.RSACryptoServiceProvider> per avere il contenuto globale della classe <xref:System.Windows.Forms.Form>.|  
|Creazione di una chiave asimmetrica|Crea una coppia chiave\-valore pubblica e privata asimmetrica e le assegna un nome del contenitore di chiavi.|  
|Crittografia di un file|Visualizza una finestra di dialogo per selezionare un file per la crittografia e lo crittografa.|  
|Decrittografia di un file|Visualizza una finestra di dialogo per selezionare un file crittografato per la decrittografia e lo decrittografa.|  
|Recupero di una chiave privata|Ottiene una coppia di chiavi completa usando il nome del contenitore di chiavi.|  
|Esportazione di una chiave pubblica|Salva la chiave in un file XML con solo parametri pubblici.|  
|Importazione di una chiave pubblica|Carica la chiave da un file XML in un contenitore di chiavi.|  
|Test dell'applicazione|Elenca le procedure per il test di questa applicazione.|  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   Riferimenti agli spazi dei nomi <xref:System.IO> e <xref:System.Security.Cryptography>.  
  
## Creazione di un'applicazione Windows Form  
 La maggior parte degli esempi di codice in questa procedura dettagliata sono progettati per essere gestori di eventi per i controlli pulsante.  Nella tabella seguente sono elencati i controlli necessari per l'applicazione di esempio e i relativi nomi richiesti per la corrispondenza con gli esempi di codice.  
  
|Controllo|Nome|Proprietà di testo \(in base alle necessità\)|  
|---------------|----------|---------------------------------------------------|  
|<xref:System.Windows.Forms.Button>|`buttonEncryptFile`|Crittografa un file|  
|<xref:System.Windows.Forms.Button>|`buttonDecryptFile`|Decrittografa un file|  
|<xref:System.Windows.Forms.Button>|`buttonCreateAsmKeys`|Crea chiavi|  
|<xref:System.Windows.Forms.Button>|`buttonExportPublicKey`|Esporta una chiave pubblica|  
|<xref:System.Windows.Forms.Button>|`buttonImportPublicKey`|Importa una chiave pubblica|  
|<xref:System.Windows.Forms.Button>|`buttonGetPrivateKey`|Ottiene una chiave privata|  
|<xref:System.Windows.Forms.Label>|`label1`||  
|<xref:System.Windows.Forms.OpenFileDialog>|`openFileDialog1`||  
|<xref:System.Windows.Forms.OpenFileDialog>|`openFileDialog2`||  
  
 Fare doppio clic sul pulsante nella finestra di progettazione di Visual Studio per creare i relativi gestori eventi.  
  
## Dichiarazione di oggetti globali  
 Aggiungere il seguente codice al costruttore del form:  Modificare le variabili di stringa per l'ambiente e le preferenze.  
  
 [!code-csharp[CryptoWalkThru#1](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#1)]
 [!code-vb[CryptoWalkThru#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#1)]  
  
## Creazione di una chiave asimmetrica  
 Questa attività crea una chiave asimmetrica che crittografa e decrittografa la chiave <xref:System.Security.Cryptography.RijndaelManaged>.  Questa chiave era usata per crittografare il contenuto e visualizza il nome del contenitore di chiavi nel controllo etichetta.  
  
 Aggiungere il codice seguente come gestore eventi `Click` per il pulsante `Create Keys` \(`buttonCreateAsmKeys_Click`\).  
  
 [!code-csharp[CryptoWalkThru#2](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#2)]
 [!code-vb[CryptoWalkThru#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#2)]  
  
## Crittografia di un file  
 Per questa attività vengono usati due metodi: il metodo gestore eventi per il pulsante `Encrypt File` \(`buttonEncryptFile_Click`\) e il metodo `EncryptFile`.  Il primo metodo visualizza una finestra di dialogo per la selezione di un file e passa il nome file al secondo metodo, che esegue la crittografia.  
  
 Il contenuto, la chiave e il vettore di inizializzazione \(IV\) crittografati vengono tutti salvati in un <xref:System.IO.FileStream>, a cui si fa riferimento come pacchetto di crittografia.  
  
 Il metodo `EncryptFile` esegue le operazioni seguenti:  
  
1.  Crea un algoritmo simmetrico <xref:System.Security.Cryptography.RijndaelManaged> per crittografare il contenuto.  
  
2.  Crea un oggetto <xref:System.Security.Cryptography.RSACryptoServiceProvider> per crittografare la chiave <xref:System.Security.Cryptography.RijndaelManaged>.  
  
3.  Usa un oggetto <xref:System.Security.Cryptography.CryptoStream> per leggere e crittografare <xref:System.IO.FileStream> del file di origine, in blocchi di byte, in un oggetto <xref:System.IO.FileStream> di destinazione per il file crittografato.  
  
4.  Determina le lunghezze della chiave e del vettore di inizializzazione \(IV\) crittografati e crea matrici di byte dei valori delle relative lunghezze.  
  
5.  Scrive la chiave, il vettore di inizializzazione \(IV\) e i valori delle relative lunghezze nel pacchetto di crittografia.  
  
 Il pacchetto di crittografia usa il seguente formato:  
  
-   Lunghezza chiave, byte 0 \- 3  
  
-   Lunghezza vettore di inizializzazione, byte 4 \- 7  
  
-   Chiave crittografata  
  
-   Vettore di inizializzazione \(IV\)  
  
-   Testo crittografato  
  
 È possibile usare le lunghezze della chiave e del vettore di inizializzazione \(IV\) per determinare i punti iniziali e lunghezze di tutte le parti del pacchetto di crittografia, che quindi può essere usato per decrittografare il file.  
  
 Aggiungere il codice seguente come gestore eventi `Click` per il pulsante `Encrypt File` \(`buttonEncryptFile_Click`\).  
  
 [!code-csharp[CryptoWalkThru#3](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#3)]
 [!code-vb[CryptoWalkThru#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#3)]  
  
 Aggiungere il metodo `EncryptFile` seguente al form.  
  
 [!code-csharp[CryptoWalkThru#5](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#5)]
 [!code-vb[CryptoWalkThru#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#5)]  
  
## Decrittografia di un file  
 Per questa attività vengono usati due metodi: il metodo gestore eventi per il pulsante `Decrypt File` \(`buttonEncryptFile_Click`\) e il metodo `DecryptFile`.  Il primo metodo visualizza una finestra di dialogo per la selezione di un file e passa il nome file al secondo metodo, che esegue la decrittografia.  
  
 Il metodo `Decrypt` esegue le operazioni seguenti:  
  
1.  Crea un algoritmo simmetrico <xref:System.Security.Cryptography.RijndaelManaged> per decrittografare il contenuto.  
  
2.  Legge i primi otto byte del pacchetto crittografato <xref:System.IO.FileStream> in matrici di byte per ottenere le lunghezze della chiave e del vettore di inizializzazione crittografati.  
  
3.  Estrae la chiave e il vettore di inizializzazione dal pacchetto di crittografia in matrici di byte.  
  
4.  Crea un oggetto <xref:System.Security.Cryptography.RSACryptoServiceProvider> per decrittografare la chiave <xref:System.Security.Cryptography.RijndaelManaged>.  
  
5.  Usa un oggetto <xref:System.Security.Cryptography.CryptoStream> per leggere e decrittografare la sezione del testo crittografato del pacchetto di crittografia <xref:System.IO.FileStream>, in blocchi di byte, nell'oggetto <xref:System.IO.FileStream> per il file decrittografato.  Quando questa operazione è terminata, la decrittografia è completata.  
  
 Aggiungere il codice seguente come gestore eventi `Click` per il pulsante `Decrypt File`.  
  
 [!code-csharp[CryptoWalkThru#4](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#4)]
 [!code-vb[CryptoWalkThru#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#4)]  
  
 Aggiungere il metodo `DecryptFile` seguente al form.  
  
 [!code-csharp[CryptoWalkThru#6](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#6)]
 [!code-vb[CryptoWalkThru#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#6)]  
  
## Esportazione di una chiave pubblica  
 Questa attività salva la chiave creata dal pulsante `Create Keys` in un file.  Esporta solo i parametri pubblici.  
  
 Questa attività simula lo scenario in cui Alice fornisce a Bob la sua chiave pubblica affinché egli possa crittografare i file per Alice.  Bob e altri utenti che dispongono di quella chiave pubblica non saranno in grado di decrittografarli poiché non possiedono la coppia di chiavi completa con i parametri privati.  
  
 Aggiungere il codice seguente come gestore eventi `Click` per il pulsante `Export Public Key` \(`buttonExportPublicKey_Click`\).  
  
 [!code-csharp[CryptoWalkThru#8](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#8)]
 [!code-vb[CryptoWalkThru#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#8)]  
  
## Importazione di una chiave pubblica  
 Questa attività carica la chiave con solo parametri pubblici, come creati dal pulsante `Export Public Key` e la imposta come nome del contenitore di chiavi.  
  
 Questa attività simula lo scenario di Bob che carica la chiave di Alice con solo parametri pubblici in modo che possa crittografare file per conto di Alice.  
  
 Aggiungere il codice seguente come gestore eventi `Click` per il pulsante `Import Public Key` \(`buttonImportPublicKey_Click`\).  
  
 [!code-csharp[CryptoWalkThru#9](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#9)]
 [!code-vb[CryptoWalkThru#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#9)]  
  
## Recupero di una chiave privata  
 Questa attività imposta il nome del contenitore di chiavi sul nome della chiave creata mediante il pulsante `Create Keys`.  Il contenitore di chiavi conterrà la coppia di chiavi completa con parametri privati.  
  
 Questa attività simula lo scenario di Alice che usa la propria chiave privata per decrittografare file crittografati da Bob.  
  
 Aggiungere il codice seguente come gestore eventi `Click` per il pulsante `Get Private Key` \(`buttonGetPrivateKey_Click`\).  
  
 [!code-csharp[CryptoWalkThru#7](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#7)]
 [!code-vb[CryptoWalkThru#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#7)]  
  
## Verifica dell'applicazione  
 Dopo aver compilato l'applicazione, eseguire gli scenari di test seguenti.  
  
#### Per creare chiavi, crittografare e decrittografare  
  
1.  Fare clic sul pulsante `Create Keys`.  L'etichetta visualizza il nome della chiave e mostra che è una coppia di chiavi completa.  
  
2.  Fare clic sul pulsante `Export Public Key`.  Si noti che l'esportazione dei parametri della chiave pubblica non modifica la chiave corrente.  
  
3.  Fare clic sul pulsante `Encrypt File` e selezionare un file.  
  
4.  Fare clic sul pulsante `Decrypt File`e selezionare il file appena crittografato.  
  
5.  Esaminare il file appena decrittografato.  
  
6.  Chiudere l'applicazione e riavviarla per testare il recupero dei contenitori di chiavi persistenti nello scenario successivo.  
  
#### Per crittografare mediante la chiave pubblica  
  
1.  Fare clic sul pulsante `Import Public Key`.  L'etichetta visualizza il nome della chiave e mostra che è solo pubblica.  
  
2.  Fare clic sul pulsante `Encrypt File` e selezionare un file.  
  
3.  Fare clic sul pulsante `Decrypt File`e selezionare il file appena crittografato.  Questa operazione avrà esito negativo perché si deve avere a disposizione la chiave privata per decrittografare.  
  
 Questo scenario illustra una situazione in cui si possiede solo la chiave pubblica per crittografare un file per un'altra persona.  In genere quella persona potrebbe mettere a disposizione solo la chiave pubblica e mantenere quella privata per la decrittografia.  
  
#### Per decrittografare mediante la chiave privata  
  
1.  Fare clic sul pulsante `Get Private Key`.  L'etichetta visualizza il nome della chiave e mostra se è la coppia di chiavi completa.  
  
2.  Fare clic sul pulsante `Decrypt File` e selezionare il file appena crittografato.  Questa operazione avrà esito positivo perché si possiede la coppia di chiavi completa per decrittografare.  
  
## Vedere anche  
 [Servizi di crittografia](../../../docs/standard/security/cryptographic-services.md)