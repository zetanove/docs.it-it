---
title: "Attivit&#224; personalizzata SendMail | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 947a9ae6-379c-43a3-9cd5-87f573a5739f
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Attivit&#224; personalizzata SendMail
In questo esempio viene illustrato come creare un'attività personalizzata che deriva da <xref:System.Activities.AsyncCodeActivity> per inviare messaggi di posta elettronica tramite il protocollo SMTP da utilizzare in un'applicazione flusso di lavoro.Nell'attività personalizzata vengono utilizzate le funzionalità di <xref:System.Net.Mail.SmtpClient> per inviare messaggi di posta elettronica in modo asincrono e con autenticazione.Nell'attività sono inoltre disponibili funzionalità per l'utente finale, ad esempio la modalità test, la sostituzione dei token, i modelli di file e il percorso di destinazione di prova.  
  
 Nella tabella seguente vengono indicati in dettaglio gli argomenti per l'attività `SendMail`.  
  
||||  
|-|-|-|  
|Nome|Tipo|Descrizione|  
|Host|String|Indirizzo dell'host del server SMTP.|  
|Port|String|Porta del servizio SMTP nell'host.|  
|EnableSsl|bool|Specifica se la classe <xref:System.Net.Mail.SmtpClient> utilizza il protocollo SSL \(Secure Sockets Layer\) per crittografare la connessione.|  
|UserName|String|Nome utente per configurare le credenziali per l'autenticazione della proprietà <xref:System.Net.Mail.SmtpClient.Credentials%2A> del mittente.|  
|Password|String|Password per configurare le credenziali per l'autenticazione della proprietà <xref:System.Net.Mail.SmtpClient.Credentials%2A> del mittente.|  
|Subject|<xref:System.Activities.InArgument%601>\<string\>|Oggetto del messaggio.|  
|Body|<xref:System.Activities.InArgument%601>\<string\>|Corpo del messaggio.|  
|Attachments|<xref:System.Activities.InArgument%601>\<string\>|Raccolta di allegati utilizzati per memorizzare i dati allegati al messaggio di posta elettronica.|  
|From|<xref:System.Net.Mail.MailAddress>|Indirizzo del mittente per il messaggio di posta elettronica.|  
|To|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>\>|Raccolta di indirizzi contenente i destinatari del messaggio di posta elettronica.|  
|CC|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>\>|Raccolta di indirizzi contenente i destinatari della copia per conoscenza \(CC\) del messaggio di posta elettronica.|  
|BCC|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>\>|Raccolta di indirizzi contenente i destinatari della copia per conoscenza nascosta \(CCN\) del messaggio di posta elettronica.|  
|Tokens|<xref:System.Activities.InArgument%601>\<IDictionary\<string, string\>\>|Token da sostituire nel corpo del messaggio.Questa funzionalità consente agli utenti di specificare alcuni valori nel corpo del messaggio che possono essere sostituiti in un secondo momento dai token specificati utilizzando questa proprietà.|  
|BodyTemplateFilePath|String|Percorso di un modello per il corpo del messaggio.L'attività `SendMail` copia il contenuto di questo file nella relativa proprietà del corpo.<br /><br /> Il modello può contenere token sostituiti dal contenuto della proprietà Token.|  
|TestMailTo|<xref:System.Net.Mail.MailAddress>|Quando viene impostata questa proprietà, tutti messaggi di posta elettronica vengono inviati all'indirizzo specificato.<br /><br /> Questa proprietà deve essere utilizzata quando si esegue il test di flussi di lavoro,ad esempio quando si desidera verificare che tutti i messaggi di posta elettronica vengano inviati in modo corretto senza tuttavia effettuare l'invio ai destinatari effettivi.|  
|TestDropPath|String|Quando viene impostata questa proprietà, tutti messaggi di posta elettronica vengono salvati nel file specificato.<br /><br /> Questa proprietà deve essere utilizzata quando si esegue il test o il debug di flussi di lavoro per verificare che il formato e il contenuto dei messaggi di posta elettronica in uscita siano corretti.|  
  
## Contenuto della soluzione  
 Nella soluzione sono contenuti due progetti.  
  
|Progetto|Descrizione|File importanti|  
|--------------|-----------------|---------------------|  
|SendMail|Attività SendMail|1.  SendMail.cs: implementazione dell'attività principale<br />2.  SendMailDesigner.xaml e SendMailDesigner.xaml.cs: finestra di progettazione per l'attività SendMail<br />3.  MailTemplateBody.htm: modello per il messaggio di posta elettronica da inviare.|  
|SendMailTestClient|Client in cui eseguire il test dell'attività SendMail.In questo progetto l'attività viene richiamata in due modi diversi, ovvero in modo dichiarativo e a livello di codice.|1.  Sequence1.xaml: flusso di lavoro che richiama l'attività SendMail.<br />2.  Program.cs: richiama Sequence1 e crea un flusso di lavoro a livello di codice che utilizza SendMail.|  
  
## Ulteriore configurazione dell'attività SendMail  
 Sebbene non illustrato nell'esempio, gli utenti possono configurare ulteriormente l'attività SendMail.Nelle tre sezioni successive viene illustrato come eseguire questa operazione.  
  
### Invio di un messaggio di posta elettronica utilizzando token specificati nel corpo del messaggio  
 In questo frammento di codice viene illustrato come è possibile inviare messaggi di posta elettronica nel cui corpo sono presenti token.Si noti il modo in cui i token vengono specificati nella proprietà Body.I valori per tali token vengono specificati nella proprietà Token.  
  
```html  
IDictionary<string, string> tokens = new Dictionary<string, string>();  
tokens.Add("@name", "John Doe");  
tokens.Add("@date", DateTime.Now.ToString());  
tokens.Add("@server", "localhost");  
  
new SendMail  
{  
    From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
    To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
    Subject = "Test email",  
    Body = "Hello @name. This is a test email sent from @server. Current date is @date",  
    Host = "localhost",  
    Port = 25,  
    Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens)  
};  
  
```  
  
### Invio di un messaggio di posta elettronica tramite un modello  
 In questo frammento di codice viene illustrato come inviare un messaggio di posta elettronica utilizzando un token del modello nel corpo.Si noti che quando si imposta la proprietà `BodyTemplateFilePath` non è necessario specificare il valore per la proprietà Body \(il contenuto del file modello verrà copiato nel corpo\).  
  
```  
new SendMail  
{    
    From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
    To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
    Subject = "Test email",  
    Host = "localhost",  
    Port = 25,  
    Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens),  
    BodyTemplateFilePath = @"..\..\..\SendMail\Templates\MailTemplateBody.htm",   
};  
  
```  
  
### Invio di messaggi di posta elettronica in modalità test  
 In questo frammento di codice viene illustrato come impostare le due proprietà di test. Se si imposta `TestMailTo`, tutti i messaggi verranno inviati a john.doe@contoso.con, indipendentemente dai valori impostati per il destinatario effettivo e i destinatari in copia.Se si imposta TestDropPath, tutti i messaggi di posta elettronica in uscita verranno inoltre salvati nel percorso specificato.È possibile impostare queste proprietà in modo indipendente l'una dall'altra perché non sono correlate.  
  
```  
new SendMail  
{    
   From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
   To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
   Subject = "Test email",  
   Host = "localhost",  
   Port = 25,  
   Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens),  
   BodyTemplateFilePath = @"..\..\..\SendMail\Templates\MailTemplateBody.htm",  
   TestMailTo= new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
   TestDropPath = @"c:\Samples\SendMail\TestDropPath\",  
};  
  
```  
  
## Istruzioni di configurazione  
 Per eseguire l'esempio, è necessario disporre dell'accesso a un server SMTP.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] configurazione di un server SMTP, vedere i collegamenti seguenti.  
  
-   [Microsoft TechNet](http://go.microsoft.com/fwlink/?LinkId=166060)  
  
-   [Configurazione del servizio SMTP \(IIS 6.0\)](http://go.microsoft.com/fwlink/?LinkId=150456)  
  
-   [IIS 7.0: Configurare la posta elettronica SMTP](http://go.microsoft.com/fwlink/?LinkId=150457)  
  
-   [Installazione del servizio SMTP](http://go.microsoft.com/fwlink/?LinkId=150458)  
  
 Per eseguire il download, sono disponibili emulatori SMTP forniti da terze parti.  
  
##### Per eseguire l'esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione SendMail.sln.  
  
2.  Verificare di disporre dell'accesso a un server SMTP valido.Vedere le istruzioni di configurazione.  
  
3.  Configurare il programma con l'indirizzo del server e gli indirizzi di posta elettronica del mittente e del destinatario.  
  
     Per eseguire correttamente l'esempio, potrebbe essere necessario configurare il valore degli indirizzi di posta elettronica del mittente e del destinatario e l'indirizzo del server SMTP in Program.cs e in Sequence.xaml.Poiché i messaggi di posta elettronica vengono inviati in due modalità diverse, sarà necessario modificare l'indirizzo in entrambi i percorsi.  
  
4.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
5.  Per eseguire la soluzione, premere CTRL\+F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\SendMail`  
  
## Vedere anche