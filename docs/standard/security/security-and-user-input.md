---
title: "Security and User Input | Microsoft Docs"
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
  - "security [.NET Framework], user input"
  - "user input, security"
  - "secure coding, user input"
  - "code security, user input"
ms.assetid: 9141076a-96c9-4b01-93de-366bb1d858bc
caps.latest.revision: 7
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 5
---
# Security and User Input
I dati utente, ovvero tutti i tipi di input, ad esempio i dati di una richiesta Web o di un URL, gli input in controlli di un'applicazione Microsoft Windows Forms e così via, possono avere effetti negativi sul codice in quanto questi dati sono spesso utilizzati direttamente come parametri per chiamare altro codice.  Questa situazione è analoga a quella della chiamata del codice da parte di codice dannoso con parametri insoliti ed è necessario adottare le stesse precauzioni.  La sicurezza dell'input dell'utente è un'operazione difficile in quanto non è disponibile alcuno stack frame per registrare la presenza dei dati potenzialmente inattendibili.  
  
 Questi ultimi rappresentano i bug più difficili da rilevare in quanto, sebbene possano essere presenti in codice apparentemente non collegato alla sicurezza, costituiscono una porta tramite cui i dati dannosi possono essere passati ad altro codice.  Per ricercare bug di questo tipo, prendere in considerazione i vari tipi di dati di input, immaginare l'intervallo dei valori possibili e determinare se il codice relativo a questi dati è in grado di gestire tutti i casi.  Questi bug possono essere corretti tramite la verifica dell'intervallo e il rifiuto dell'input che non è possibile gestire tramite codice.  
  
 Tra gli aspetti importanti dei dati utente sono inclusi i seguenti:  
  
-   I dati utente in una risposta server sono eseguiti nel contesto del sito del server sul client.  Se il server Web accetta dati utente e li inserisce nella pagina Web restituita, può, ad esempio, includere un tag **\<script\>** e consentire l'esecuzione come se questa avvenisse dal server.  
  
-   Tenere presente che il client può richiedere qualsiasi URL.  
  
-   Prendere in considerazione i percorsi complessi o non validi:  
  
    -   ..\\ , percorsi estremamente lunghi.  
  
    -   Utilizzo di caratteri jolly \(\*\).  
  
    -   Espansione del token \(%token%\).  
  
    -   Forme insolite di percorsi con significati speciali.  
  
    -   Nomi di flusso del file system alternativi come `filename::$DATA`.  
  
    -   Versioni abbreviate dei nomi file come `longfi~1` per `longfilename`.  
  
-   Ricordare che Eval\(userdata\) consente di eseguire qualsiasi operazione.  
  
-   Tenere conto dell'associazione tardiva a un nome che include dati utente.  
  
-   Se si utilizzano dati Web, prendere in considerazione le varie forme di escape consentite, inclusi:  
  
    -   Escape esadecimali \(%nn\).  
  
    -   Escape Unicode \(%nnn\).  
  
    -   Escape lunghi UTF\-8 \(%nn%nn\).  
  
    -   Escape doppi \(%nn diviene %mmnn, dove %mm è il carattere di escape per '%'\).  
  
-   Prestare attenzione ai nomi utente che possono avere più di un formato canonico.  In Microsoft Windows 2000, ad esempio, è spesso possibile utilizzare la forma MYDOMAIN\\*nomeutente* o la forma *nomeutente*@mydomain.example.com.  
  
## Vedere anche  
 [Secure Coding Guidelines](../../../docs/standard/security/secure-coding-guidelines.md)