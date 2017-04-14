---
title: "Protocollo PNRP (Peer Name Resolution Protocol) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 11940511-c124-4d91-ae31-d4ed6e81ee58
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Protocollo PNRP (Peer Name Resolution Protocol)
In ambienti peer\-to\-peer, campo specifici di risoluzione dei nomi di utilizzo dei peer per risolvere percorsi di rete \(ognuno degli indirizzi, porte e protocolli\) i nomi o altri tipi di identificatori.  In passato, la risoluzione dei nomi peer è stata complicata dalla connettività implicitamente temporanea e da altri difetti nel Domain Name System \(DNS\).  
  
 La piattaforma peer\-to\-peer di rete di Microsoft® Windows® risolve il problema con il protocollo peer \(PNRP\) di risoluzione dei nomi, una registrazione di nome e un protocollo sicuri, scalabili e dinamici di risoluzione dei nomi innanzitutto elaborato per Windows XP e quindi aggiornato in Windows Vista™.  Funzionamento di PNRP molto in modo diverso dai sistemi tradizionali di risoluzione dei nomi, aprenti le nuove funzionalità emozionanti per gli sviluppatori di applicazioni.  
  
 Con PNRP, i nomi peer possono essere applicate al computer, o singole applicazioni o servizi sul computer.  Risoluzione dei nomi peer include un indirizzo, la porta e possibilmente un payload esteso.  I vantaggi del sistema non includono la tolleranza di errore, bottiglia e le risoluzioni dei nomi che non restituiscono mai gli indirizzi non aggiornati; rendere il protocollo una soluzione eccellente per l'individuazione di utente mobili.  
  
 In termini di sicurezza, i nomi peer possono essere generati come protetto \(protetto\) o non sicuro \(sprotetto\).  Crittografia a chiave pubblica di utilizzo di PNRP per proteggere i nomi sicuri del peer lo spoofing, i computer che i servizi possono essere denominati con PNRP.  
  
-   Il protocollo peer di risoluzione dei nomi vengono illustrate le seguenti proprietà:  
  
-   Distribuito e quasi completamente serverless.  I server sono necessari solo per il processo di avvio.  
  
-   Verificare la pubblicazione di nome senza la partecipazione di terze parti.  A differenza della pubblicazione del nome DNS, la pubblicazione del nome di PNRP è controllo e senza costo finanziarie.  
  
-   Aggiornamenti di PNRP in tempo reale, che impedisce la risoluzione degli indirizzi non aggiornati.  
  
-   La risoluzione dei nomi tramite PNRP estende oltre i computer anche consentendo la risoluzione dei nomi per i servizi.  
  
## Lo spazio dei nomi di System.Net.PeerToPeer  
  
-   La funzionalità di PNRP è definita dallo spazio dei nomi <xref:System.Net.PeerToPeer> in.NET Framework versione 3.5.  Fornisce un insieme di tipi che possono essere utilizzati per registrare e risolvere i nomi del peer tramite un servizio disponibile di PNRP.  
  
-   \(PNRP e i Peer resolver personalizzati possono essere creati e crearne un'istanza utilizzando i tipi forniti nello spazio dei nomi <xref:System.ServiceModel.PeerResolvers> \).  
  
-   I tipi di base utilizzati per registrare e risolvere i nomi con un servizio disponibile di PNRP sono:  
  
-   <xref:System.Net.PeerToPeer.Cloud>: Definisce le informazioni che descrivono un cloud disponibile di PNRP, incluso il relativo ambito.  
  
-   <xref:System.Net.PeerToPeer.PeerName>: Definisce un nome peer che può essere utilizzato per la registrazione e successivamente risolvere un peer all'interno di un cloud.  
  
-   <xref:System.Net.PeerToPeer.PeerNameRecord>: Definisce il record di cloud di PNRP contenente le informazioni di registrazione per un peer, che include gli endpoint di rete per il quale il peer è possibile contattare.  
  
-   <xref:System.Net.PeerToPeer.PeerNameRegistration>: Definisce il processo di registrazione per un peer nome, compresi i metodi per avviare e interrompere la registrazione peer del nome.  
  
-   <xref:System.Net.PeerToPeer.PeerNameResolver>: Definisce il processo per risolvere un nome al peer endpoint di rete, inclusi metodi sincroni e asincroni per la risoluzione.  
  
## Vedere anche  
 <xref:System.ServiceModel.PeerResolvers>   
 <xref:System.Net.PeerToPeer>   
 [Esempi di programmazione di rete](../../../docs/framework/network-programming/network-programming-samples.md)   
 [esempio peer\-to\-peer di tecnologia](http://go.microsoft.com/fwlink/?LinkID=179571)