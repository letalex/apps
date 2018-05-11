---
copyright:

  years: 2018

lastupdated: "2018-03-17"

---

{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}  
{:screen: .screen}  
{:codeblock: .codeblock}  
{:pre: .pre}
{:tip: .tip}

# Distribuzione delle applicazioni
{: #deploy}

Puoi distribuire le tue applicazioni con una toolchain o un'interfaccia riga di comando. Una toolchain è un insieme di integrazioni dello strumento. L'interfaccia riga di comando è un modo semplice per distribuire le tue applicazioni e istanze del servizio.
{: shortdesc}

## Distribuzione delle applicazioni con le toolchain
{: #toolchains_getting_started}

Le toolchain aperte sono disponibili negli ambienti pubblico e dedicato in {{site.data.keyword.Bluemix}}. Puoi creare una toolchain in due modi: utilizzando un template o creandola da un'applicazione. Per ulteriori informazioni sulle toolchain, vedi [Creazione delle toolchain](../services/ContinuousDelivery/toolchains_working.html#toolchains_getting_started)

Con una toolchain correttamente configurata, la distribuzione della tua applicazione è banale: sarà automaticamente avviato un ciclo di creazione-distribuzione con ogni unione al ramo master nel tuo repository.

Tutte le toolchain create da un dashboard di sviluppo {{site.data.keyword.Bluemix}} saranno configurate per la distribuzione automatica.
{: tip}

## Distribuzione di applicazioni con l'interfaccia riga di comando
{: #cli}

IBM Cloud fornisce una solida CLI nonché i plug-in e le estensioni dello strumento per sviluppatori che si integrano con la CLI.

Utilizza l'interfaccia riga di comando {{site.data.keyword.Bluemix_notm}} per distribuire le tue applicazioni e istanze del servizio.
{:shortdesc}

Prima di iniziare, scarica e installa l'interfaccia di riga di comando {{site.data.keyword.Bluemix_notm}}.

<p>
<a class="xref" href="https://clis.ng.bluemix.net" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/btn_bx_commandline.svg" alt="Scarica l'interfaccia riga di comando Bluemix" /> </a>
</p>

**Limitazione:** lo strumento della riga di comando non è supportato da Cygwin. Utilizzalo in una finestra della riga di comando diversa da quella di Cygwin.
{:prereq}

Dopo aver installato l'interfaccia riga di comando, puoi iniziare:

  1. {: download} Scarica il codice per la tua applicazione in una nuova directory per configurare il tuo ambiente di sviluppo.

    <a class="xref" href="http://bluemix.net" target="_blank" title="(Si apre in una nuova scheda o finestra)"></a>

  2. Passa alla directory in cui si trova il codice.

  <pre class="pre"><code class="hljs">cd <var class="keyword varname">la_tua_nuova_directory</var></code></pre>

  3.  Apporta le modifiche al codice della tua applicazione. Ad esempio, se stai utilizzando un'applicazione di esempio {{site.data.keyword.Bluemix_notm}} che contiene il file `src/main/webapp/index.html`, puoi modificarlo con "Thanks for creating ..." per fare qualcosa di nuovo. Assicurati che l'applicazione sia in esecuzione localmente prima di distribuirla a {{site.data.keyword.Bluemix_notm}}.

    Prendi nota del file `manifest.yml`. Quando ridistribuisci la tua applicazione a {{site.data.keyword.Bluemix_notm}}, questo file viene utilizzato per determinare l'URL, l'allocazione di memoria, il numero di istanze e altri parametri fondamentali della tua applicazione.

    Presta inoltre attenzione al file `README.md`, che contiene dettagli come le istruzioni di creazione se applicabili.

    Nota: se la tua applicazione è un'applicazione Liberty, devi crearla prima di ridistribuirla.

  4. Collegati ed accedi a {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></code></pre>

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></code></pre>

  Se stai utilizzando un ID federato, usa l'opzione `-sso`.

  <pre class="pre"><code class="hljs">bluemix login  -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var> -sso</code></pre>

  **Nota**: se il valore contiene uno spazio, devi aggiungere singoli o doppi apostrofi intorno a `nomeutente`, `nome_org` e  `nome_spazio` se il valore contiene uno spazio, ad esempio, `-o "my org"`.

  5. Da <var class="keyword varname">la_tua_nuova_directory</var>, ridistribuisci la tua applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando il comando `bluemix app push`. Per ulteriori informazioni sul comando `bx app push`, vedi [Caricamento della tua applicazione](/docs/starters/upload_app.html).

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">nome_app</var></code></pre>

  6. Accedi alla tua applicazione andando all'indirizzo https://<var class="keyword varname" data-hd-keyref="app_url">url_app</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span>.