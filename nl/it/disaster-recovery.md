---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

keywords: File Storage, file storage, NFS, disaster recovery, duplicate volume, replica volume, failover, failback,

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}


# Ripristino di emergenza - Failover con un volume primario inaccessibile
{: #dr-inaccessible}

Se un errore catastrofico o un'emergenza causano un'interruzione sul sito primario, i clienti possono eseguire le seguenti azioni per accedere rapidamente ai loro dati sul sito secondario.

## Failover con un duplicato di un volume di replica sul sito secondario

1. Accedi [Alla console IBM Cloud ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/){:new_window} e fai clic sull'icona **menu** nell'angolo superiore sinistro. Seleziona **Infrastruttura classica**.

   In alternativa, puoi accedere al [{{site.data.keyword.slportal}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/){:new_window}.
2. Fai clic su **Storage** > **{{site.data.keyword.filestorage_short}}**.
3. Fai clic sulla replica della condivisione file per visualizzarne la pagina **Details**.
4. Nella pagina **Details**, scorri verso il basso, seleziona un'istantanea esistente e fai clic su **Actions** > **Duplicate**.
5. Apporta tutti gli aggiornamenti necessari alla capacità (per aumentare la dimensione) o IOPs per il nuovo volume.
6. Puoi aggiornare lo spazio di istantanea per il nuovo volume, se necessario.
7. Fai clic su **Continue** per effettuare il tuo ordine per il duplicato.

Non appena viene creato il volume, puoi collegarlo a un host ed eseguire le operazioni di lettura/scrittura su tale volume. Mentre i dati vengono copiati dal volume originale al duplicato, vedi un stato nella pagina dei dettagli che mostra che la duplicazione è in corso. Una volta completato il processo di duplicazione, il nuovo volume diventa indipendente dall'originale e può essere gestito con le istantanee e la replica normalmente.

## Esegui il failback al sito primario originale

Se vuoi far tornare la produzione al sito primario originale, devi completare le seguenti istruzioni.

1. Accedi [Alla console IBM Cloud ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/){:new_window} e fai clic sull'icona **menu** nell'angolo superiore sinistro. Seleziona **Infrastruttura classica**.

   In alternativa, puoi accedere al [{{site.data.keyword.slportal}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/){:new_window}.
2. Fai clic su **Storage** > **{{site.data.keyword.filestorage_short}}**.
3. Fai clic sul nome del LUN e crea una pianificazione delle istantanee (se non ne esiste già una).

   Per ulteriori informazioni sulle pianificazioni delle istantanee, consulta [Gestione delle istantanee](/docs/infrastructure/FileStorage?topic=FileStorage-managingSnapshots#addschedule).
   {:tip}
4. Fai clic su **Replica** e fai clic su **Purchase a replication**.
5. Seleziona la pianificazione delle istantanee esistente che vuoi venga seguita dalla replica. L'elenco contiene tutte le pianificazioni delle istantanee attive.
6. Fai clic su **Location** e seleziona il data center che era il sito di produzione originale.
7. Fai clic su **Continue**.
8. Fai clic sulla casella di spunta **I have read the Master Service Agreement…** e fai clic su **Place Order**.

Dopo che la replica è completa, devi creare un volume duplicato della nuova replica.
{:important}

1. Torna a **Storage** > **{{site.data.keyword.filestorage_short}}**.
2. Fai clic sulla replica del LUN nell'elenco per visualizzare la relativa pagina **Details**.
3. Nella pagina **Details**, scorri verso il basso, seleziona un'istantanea esistente e fai clic su **Actions** > **Duplicate**.
4. Apporta tutti gli aggiornamenti necessari alla capacità (per aumentare la dimensione) o IOPs per il nuovo volume.
5. Aggiorna lo spazio di istantanea per il nuovo volume se necessario.
6. Fai clic su **Continue** per effettuare il tuo ordine per il duplicato.

Quando il processo di duplicazione è completo, puoi eliminare la replica e i volumi che sono stati utilizzati per richiamare i dati al sito primario originale. Il duplicato diventa l'archiviazione primaria e la replica al sito secondario originale può essere ristabilita.
