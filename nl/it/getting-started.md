---

copyright:
  years: 2014, 2019
lastupdated: "2019-03-07"

keywords: File Storage, file storage, NFS, provisioning, setup, configuration, mounting storage

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
 {:shortdesc: .shortdesc}


# Esercitazione introduttiva
{: #getting-started}

{{site.data.keyword.filestorage_full}} è {{site.data.keyword.filestorage_short}} persistente, veloce, flessibile, basato su NFS e collegato alla rete. In questo ambiente NAS (Network Attached Storage), hai il controllo totale sulle prestazioni e la funzione di condivisioni dei tuoi file. Le condivisioni di {{site.data.keyword.filestorage_short}} possono essere connesse a un massimo di 64 dispositivi autorizzati su connessioni TCP/IP instradate per la resilienza.
{:shortdesc}

## Prima di iniziare
{: #prereqs}

È possibile eseguire il provisioning di volumi {{site.data.keyword.filestorage_short}} da 20 GB a 12 TB con due opzioni: <br/>
- Esegui il provisioning di livelli **Endurance** che offrono livelli di prestazioni predefiniti e funzioni quali le istantanee e la replica.
- Crea un ambiente **Performance** molto potente con IOPS (input/output operations per second) allocato.

Per ulteriori informazioni sull'offerta {{site.data.keyword.filestorage_short}}, consulta [Informazioni su {{site.data.keyword.filestorage_short}}](/docs/infrastructure/FileStorage?topic=FileStorage-about)

## Considerazioni sul provisioning

### Dimensione blocco 

IOPS sia per Endurance che per Performance è basato su una dimensione di blocco di 16-KB con un carico di lavoro casuale/sequenziale al 50/50 e con lettura/scrittura al 50/50. Un blocco di 16-KB è l'equivalente di una scrittura sul volume.
{:important}

La dimensione del blocco utilizzata dalla tua applicazione influisce direttamente sulle prestazioni dell'archiviazione. Se la dimensione del blocco utilizzata dalla tua applicazione è inferiore a 16 KB, il limite IOPS si realizza prima del limite di velocità effettiva. Viceversa, se la dimensione del blocco utilizzata dalla tua applicazione è superiore a 16 KB, il limite di velocità effettiva si realizza prima del limite di IOPS.

<table>
  <caption>La tabella 4 mostra degli esempi di come la dimensione del blocco e IOPS influiscono sulla velocità effettiva.</caption>
        <colgroup>
          <col/>
          <col/>
          <col/>
        </colgroup>
        <thead>
          <tr>
            <th>Dimensione blocco (KB)</th>
            <th>IOPS</th>
            <th>Velocità effettiva (MB/s)</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>4 (tipica per Linux)</td>
            <td>1.000</td>
            <td>4</td>
          </tr>
          <tr>
            <td>8 (tipica per Oracle)</td>
            <td>1.000</td>
            <td>8</td>
          </tr>
          <tr>
            <td>16</td>
            <td>1.000</td>
            <td>16</td>
          </tr>
          <tr>
            <td>32 (tipica per SQL Server)</td>
            <td>500</td>
            <td>16</td>
          </tr>          
          <tr>
            <td>64</td>
            <td>250</td>
            <td>16</td>
          </tr>
          <tr>
            <td>128</td>
            <td>128</td>
            <td>16</td>
          </tr>
          <tr>
            <td>512</td>
            <td>32</td>
            <td>16</td>
          </tr>
        </tbody>
</table>

### Host autorizzati 

Un altro fattore da considerare è il numero di host che sta utilizzando il tuo volume. Se c'è un singolo host che sta accedendo al volume, potrebbe essere difficile realizzare l'IOPS massimo disponibile, soprattutto a conteggi IOPS estremi (nell'ordine delle decine di migliaia). Se il tuo carico di lavoro richiede una velocità effettiva elevata, sarebbe meglio configurare almeno un paio di server che accedono al tuo volume per evitare un collo di bottiglia di un singolo server.

### Connessione di rete 

La velocità della tua connessione Ethernet deve essere superiore a quella effettiva massima prevista dal tuo volume. In generale, non prevedere di saturare la tua connessione Ethernet oltre il 70% della larghezza di banda disponibile. Ad esempio, se hai 6.000 IOPS e stai utilizzando una dimensione del blocco di 16-KB, il volume può gestire una velocità effettiva di circa 94-MBps. Se hai una connessione Ethernet da 1-Gbps al tuo LUN, diventa un collo di bottiglia quando i tuoi server provano a utilizzare la velocità effettiva massima disponibile. Ciò è dovuto al fatto che il 70 percento del limite teorico di una connessione Ethernet da 1-Gbps (125 MB al secondo) consentirebbe solo 88 MB al secondo.

Per raggiungere l'IOPS massimo, è necessario che siano implementate delle risorse di rete adeguate. Altre considerazioni includono l'utilizzo della rete privata esternamente al lato archiviazione e host e le regolazioni specifiche per le applicazioni (stack di IP o [profondità di coda](/docs/infrastructure/FileStorage?topic=FileStorage-hostqueuesettings) e altre impostazioni).

Il traffico di archiviazione viene incluso nell'utilizzo di rete totale dei server virtuali pubblici. Per ulteriori informazioni sui limiti che potrebbero essere imposti dal servizio, vedi la [documentazione del Virtual Server](/docs/vsi?topic=virtual-servers-about-public-virtual-servers).

### Versione NFS 

Nell'ambiente {{site.data.keyword.BluSoftlayer_full}} sono supportati sia NFS v3 che NFS v4.1. Tuttavia, NFS v3 è preferito perché NFS v4.1 è un protocollo con stato (non senza stato come NFSv3) e durante gli eventi di rete potrebbero verificarsi dei problemi di protocollo. NFS v4.1 deve disattivare tutte le operazioni e quindi completare un recupero del blocco. Su un server di file NFS relativamente occupato, l'aumentata latenza può causare interruzioni del servizio. La mancanza di multipercorso e trunking NFS v4.1 può anche estendere il ripristino di uno stato normale delle operazioni NFS.

## Inoltro del tuo ordine

Quando sei pronto a inviare il tuo ordine, puoi effettuarlo tramite la [Console](/docs/infrastructure/FileStorage?topic=FileStorage-orderingConsole) o la [SLCLI](/docs/infrastructure/FileStorage?topic=FileStorage-orderingSLCLI). Per il File Storage Provisioning con VMware, fai clic [qui](/docs/infrastructure/FileStorage?topic=FileStorage-architectureguide)

## Connessione della tua nuova archiviazione
{: #mountingstorage}

Dopo che la tua richiesta di provisioning è stata completata, autorizza i tuoi host ad accedere alla nuova archiviazione e configura la tua connessione. A seconda del sistema operativo del tuo host, segui il link appropriato.
- [Accesso a {{site.data.keyword.filestorage_short}} su Linux](/docs/infrastructure/FileStorage?topic=FileStorage-mountingLinux)
- [Montaggio di {{site.data.keyword.filestorage_short}} in CentOS](/docs/infrastructure/FileStorage?topic=FileStorage-mountingCentOS)
- [Montaggio di {{site.data.keyword.filestorage_short}} su CoreOS](/docs/infrastructure/FileStorage?topic=FileStorage-mountingCoreOS)
- [Configurazione di {{site.data.keyword.filestorage_short}} per il backup con cPanel](/docs/infrastructure/FileStorage?topic=FileStorage-cPanelBackups)
- [Configurazione di {{site.data.keyword.filestorage_short}} per il backup con Plesk](/docs/infrastructure/FileStorage?topic=FileStorage-PleskBackup)
- [Montaggio del volume {{site.data.keyword.filestorage_short}} sugli host ESXi](/docs/infrastructure/FileStorage?topic=FileStorage-architectureguide)

## Gestione della tua nuova archiviazione

Tramite il portale o la SLCLI, puoi gestire molti aspetti del tuo {{site.data.keyword.filestorage_short}} come ad esempio gli annullamenti e le autorizzazioni host. Per ulteriori informazioni, consulta [Gestione di {{site.data.keyword.filestorage_short}}](/docs/infrastructure/FileStorage?topic=FileStorage-managingstorage).
