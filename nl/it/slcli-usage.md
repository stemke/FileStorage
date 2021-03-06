---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-05"

keywords: File Storage, NSF, SLCLI, API

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:codeblock: .codeblock}

# Comandi SLCLI per {{site.data.keyword.filestorage_short}}
{: #SLCLIcommands}

Puoi utilizzare la SLCLI per eseguire delle azioni che vengono normalmente gestite tramite il [{{site.data.keyword.slportal}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/){:new_window}. Ad esempio, con la SLCLI puoi inserire degli ordini per nuovi volumi, replica e spazio di instantanea, aggiornare le autorizzazioni, eliminare i volumi e così via.

Per ulteriori informazioni su come installare e utilizzare la SLCLI, vedi [Python API Client ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://softlayer-python.readthedocs.io/en/latest/cli.html){:new_window}.
{:tip}

## Comandi SLCLI correlati all'accesso 
* [Gestione di {{site.data.keyword.filestorage_short}}](/docs/infrastructure/FileStorage?topic=FileStorage-managingstorage)  
  ```
  slcli file access-authorize
  slcli file access-list
  slcli file access-revoke
  ```

## Comandi SLCLI correlati alla replica 

* [Comandi SLCLI correlati alla replica ](/docs/infrastructure/FileStorage?topic=FileStorage-replication#clicommands)
  ```
  slcli file replica-failback
  slcli file replica-failover
  slcli file replica-locations
  slcli file replica-order
  slcli file replica-partners
  ```

## Comandi SLCLI correlati alle istantanee 

* [Ordinazione di istantanee](/docs/infrastructure/FileStorage?topic=FileStorage-ordering-snapshots)
  ```
  slcli file snapshot-order
  ```

* [Gestione delle istantanee](/docs/infrastructure/FileStorage?topic=FileStorage-managingSnapshots)
  ```
  slcli file snapshot-cancel
  slcli file snapshot-create
  slcli file snapshot-delete
  slcli file snapshot-disable
  slcli file snapshot-enable
  slcli file snapshot-list
  slcli file snapshot-restore
  ```

## Comandi SLCLI correlati al volume 

* [Ordinazione di un volume {{site.data.keyword.filestorage_short}} ](/docs/infrastructure/FileStorage?topic=FileStorage-orderingSLCLI)
* [Creazione di un volume duplicato](/docs/infrastructure/FileStorage?topic=FileStorage-duplicatevolume)
  ```
  slcli file volume-duplicate
  ```
* [Regolazione dell'IOPS](/docs/infrastructure/FileStorage?topic=FileStorage-adjustingIOPS#adjustingsteps)
  ```
  slcli file volume-modify
  ```
* [Espansione della capacità](/docs/infrastructure/FileStorage?topic=FileStorage-expandCapacity#resizingsteps)
  ```
  slcli file volume-modify
  ```
* [Gestione di {{site.data.keyword.filestorage_short}}](/docs/infrastructure/FileStorage?topic=FileStorage-managingstorage)
  ```
  slcli file volume-cancel
  slcli file volume-count
  slcli file volume-detail
  slcli file volume-duplicate
  slcli file volume-list
  slcli file volume-order
  ```
* [Gestione dei limiti di archiviazione](/docs/infrastructure/FileStorage?topic=FileStorage-managinglimits)
  ```
  slcli file volume-count
  ```
