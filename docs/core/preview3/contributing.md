# <a name="using-the-cli-preview3-folder-and-sub-folders"></a>Uso della cartella cli-preview3 e delle relative sottocartelle

Questa cartella è il nodo di primo livello corrispondente alla cartella degli strumenti, ma contiene elementi differenziali per la versione di anteprima 3 degli strumenti di .NET Core.

L'obiettivo di questa struttura di cartelle parallele separate è fornire un'area per i contenuti della versione di anteprima 3 che possono essere uniti in modo relativamente semplice nella struttura principale nel passaggio da una versione all'altra nel sito pubblicato.

Il contenuto di questo nodo deve essere un set di documenti di dimensioni inferiori che rappresenta gli elementi differenziali tra la versione LTS (Long Term Support) e quella corrente. 

## <a name="structure"></a>Struttura

L'aggiunta di nuovo contenuto a questa versione si verifica in due casi:

* Modifiche ai documenti esistenti
    - Copiare il contenuto esistente in una cartella parallela in questa struttura. Apportare le modifiche e aggiungere il file modificato al sommario della versione di anteprima 3.
* Nuovi documenti
    - Inserire il nuovo documento nella posizione appropriata e aggiungerlo al sommario sotto il nodo della versione di anteprima 3. 

Tutti i file di rilascio correnti devono aggiungere quanto segue nella parte superiore dell'argomento:

[!include[current release track](../includes/warning.md)]

È stato creato un frammento di codice da includere nella sintassi seguente:

```markdown
[!include[current release track](../../includes/warning.md)]
```

### <a name="link-instructions"></a>Istruzioni di collegamento

In entrambi i casi, vengono forniti collegamenti dalla versione corrente alla pagina LTS (o index.md padre) a scopo di navigazione.
Si consiglia di fornire i collegamenti dalla pagina LTS (o index.md padre) alla nuova pagina dei contenuti della versione corrente.

## <a name="future-considerations"></a>Considerazioni

L'obiettivo finale consiste nel trattare le diverse versioni come rami nel [repository dei documenti](https://github.com/dotnet/docs). Finché non sarà disponibile il supporto per questo scenario di pubblicazione, verranno usate cartelle di livello superiore per ognuna delle versioni correnti. 

Al momento opportuno, sarà possibile unire ogni versione corrente nella cartella [documenti](../docs) principale, unire i nodi del sommario e pubblicare come set di documenti separati. Può essere utile unire le modifiche apportate alla versione LTS di un file e alla versione corrente di un file, ma è necessario che si tratti di modifiche di facile individuazione.


<!--HONumber=Nov16_HO3-->


