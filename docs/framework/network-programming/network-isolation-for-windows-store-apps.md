---
title: "Isolamento rete per app di Windows Store | Microsoft Docs"
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
ms.assetid: b064497c-d956-46b8-838d-7a0223c7e200
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# Isolamento rete per app di Windows Store
Le classi in <xref:System.Net>, in <xref:System.Net.Http>negli spazi dei nomi <xref:System.Net.Http.Headers> possono essere utilizzate per compilare applicazioni dell'archivio di Windows o applicazioni desktop.  Se utilizzate in un'applicazione di archivio di Windows, le classi negli spazi dei nomi sono interessate da isolamento rete, parte del modello di sicurezza dell'applicazione utilizzati da [!INCLUDE[win8](../../../includes/win8-md.md)].  Le funzionalità appropriate della rete devono essere abilitati nel manifesto dell'app per un'applicazione di archivio di Windows per il sistema consentono l'accesso alla rete.  
  
## Elenco di controllo per l'isolamento rete  
 Utilizzare questo elenco di controllo per accertarsi che l'isolamento rete è configurato per l'applicazione dell'archivio di Windows.  
  
1.  Determinare la direzione delle richieste di accesso alla rete necessarie dall'applicazione.  Ciò può essere o richieste client avviate in uscita o le richieste non sollecitate in ingresso o potrebbe essere una combinazione di entrambi i tipi di rete.  
  
2.  Determinare il tipo di risorse di rete cui l'applicazione comunicherà con.  Un'applicazione può essere necessario comunicare con le soluzioni attendibili su Home o di eseguire la rete.  Un'applicazione potrebbe essere necessario comunicare con le risorse in Internet.  Un'applicazione potrebbe essere necessario accedere a entrambi i tipi di risorse di rete.  
  
3.  Configurare le funzionalità minimo\- necessari per l'isolamento della rete nel manifesto dell'app.  
  
4.  Implementare ed eseguire l'applicazione per verificare mediante gli strumenti di isolamento rete forniti per risolvere.  
  
 Per informazioni dettagliate su come configurare gli strumenti di funzionalità e di isolamento di rete utilizzati per l'isolamento rete per la risoluzione dei problemi, vedere [Come configurare la funzionalità di isolamento rete](http://go.microsoft.com/fwlink/?LinkID=228265) la documentazione per sviluppatori [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].  
  
## Vedere anche  
 [Connessione a un servizio web](http://go.microsoft.com/fwlink/?LinkID=245696)   
 [Linee guida e un elenco di controllo per l'isolamento rete](http://go.microsoft.com/fwlink/?LinkID=228265)   
 [guida rapida: Connessione utilizzando HttpClient](http://go.microsoft.com/fwlink/?LinkId=245697)   
 [come utilizzare i gestori di HttpClient](http://go.microsoft.com/fwlink/?LinkId=245699)   
 [Come proteggere le connessioni di HttpClient](http://go.microsoft.com/fwlink/?LinkId=245698)   
 [esempio di HttpClient](http://go.microsoft.com/fwlink/?LinkId=242550)