---

copyright:
  years: 2014, 2019
lastupdated: "2019-03-26"

keywords: File Storage, encryption, security, provisioning, limitations, NFS

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:faq: data-hd-content-type='faq'}

# FAQ (Foire aux questions)
{: #faqs}

## Comment savoir si tel ou tel volume {{site.data.keyword.filestorage_short}} est chiffré ?
{: faq}

Consultez la liste de volumes {{site.data.keyword.filestorage_short}} dans le portail client. Une icône en forme de verrou figure à droite du nom de volume des volumes qui sont chiffrés.

## Si j'ai acquis un stockage {{site.data.keyword.filestorage_short}} non chiffré dans un centre de données qui a été mis à jour pour le chiffrement, puis-je chiffrer mon stockage {{site.data.keyword.filestorage_short}} ?
{: faq}

Le stockage {{site.data.keyword.filestorage_short}} qui a été mis à disposition avant la mise à niveau d'un centre de données ne peut pas être chiffré. Un nouveau stockage {{site.data.keyword.filestorage_short}} mis à disposition dans des centres de données mis à niveau est automatiquement chiffré. Cette opération est automatique ; ce n'est pas un paramètre de mise à disposition que vous pouvez sélectionner ou ignorer. Il est possible de chiffrer les données figurant sur un stockage non chiffré en créant un nouveau volume, puis en copiant les données sur ce nouveau volume chiffré en procédant à une migration basée sur l'hôte. Pour plus d'informations, voir [Migration de stockage de fichier](/docs/infrastructure/FileStorage?topic=FileStorage-migratestorage).

## Comment savoir si je mets à disposition un stockage {{site.data.keyword.filestorage_short}} dans un centre de données mis à niveau ?
{: faq}

Dans le formulaire de commande {{site.data.keyword.filestorage_short}}, tous les centres de données mis à niveau sont signalés par un astérisque (`*`). Durant la commande, le système vous indique que vous mettez à disposition du stockage avec chiffrement. Une fois le stockage mis à disposition, une icône apparaît dans la liste de stockage pour indiquer que le volume est chiffré.

Tous les volumes et partages de fichiers chiffrés sont mis à disposition uniquement dans des centres de données mis à niveau. Vous trouverez la liste complète des centres de données mis à niveau et des fonctionnalités disponibles [ici](/docs/infrastructure/FileStorage?topic=FileStorage-news).

## Pourquoi un stockage {{site.data.keyword.filestorage_short}} de type Endurance avec un niveau de 10 IOPS doit-il être mis à disposition dans certains centres de données et pas dans d'autres ?
{: faq}

Le type de stockage {{site.data.keyword.filestorage_short}} Endurance avec un niveau de 10 IOPS/Go est disponible dans des centres de données sélectionnés, auxquels s'ajouteront bientôt de nouveaux centres de données. Vous trouverez la liste complète des centres de données mis à niveau et des fonctionnalités disponibles [ici](/docs/infrastructure/FileStorage?topic=FileStorage-news).

## Comment faire pour trouver le point de montage correct de mon stockage {{site.data.keyword.filestorage_short}} ?
{: faq}

Tous les volumes {{site.data.keyword.filestorage_short}} chiffrés mis à disposition dans les centres de données améliorés ont un point de montage différent de celui des volumes non chiffrés. Pour vérifier que vous utilisez le bon point de montage, vous pouvez afficher les informations sur le point de montage sur la page **Détails du volume** de l'interface utilisateur. Vous pouvez également accéder au point de montage correct via un appel d'API : `SoftLayer_Network_Storage::getNetworkMountAddress()`.

## Combien de volumes puis-je mettre à disposition ?
{: faq}

Par défaut, vous pouvez mettre à disposition un total combiné de 250 volumes de bloc et de stockage de fichier. Pour augmenter votre limite, contactez votre commercial. Pour plus d'informations, voir [Gestion des limites de stockage](/docs/infrastructure/FileStorage?topic=FileStorage-managinglimits).

## Combien d'instances peuvent partager l'utilisation d'un volume {{site.data.keyword.filestorage_short}} mis à disposition ?
{: faq}

Le nombre d'autorisations par volume de fichier est limité par défaut à 64. Pour augmenter cette limite, contactez votre commercial.

## Combien de volumes {{site.data.keyword.filestorage_short}} peuvent être connectés à un seul hôte ?
{: faq}

Le nombre dépend de ce que le système d'exploitation hôte est capable de gérer, il ne s'agit pas d'un paramètre limité par {{site.data.keyword.BluSoftlayer_full}}. Consultez la documentation de votre système d'exploitation pour connaître les limites relatives au nombre de partages de fichiers pouvant être montés.

## Combien de partages de fichiers sont-ils autorisés par taille de volume de fichier ? Quelle est la taille maximale de partage de fichiers autorisée par taille de volume ?
{: faq}

<table>
  <caption>Le tableau 1 présente le nombre maximal d'i-nodes autorisés en fonction de la taille de volume. Les tailles de volume sont indiquées dans la colonne de gauche. Le nombre d'i-nodes et de partages de fichiers est indiqué à droite.</caption>
  <thead>
    <tr>
      <th>Taille de volume</th>
      <th>I-nodes et partages de fichiers</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>20 Go - 39 Go</td>
      <td>622 484</td>
    </tr>
    <tr>
      <td>40 Go - 79 Go</td>
      <td>1 245 084</td>
    </tr>          
    <tr>
      <td>80 Go - 99 Go</td>
      <td>2 490 263</td>
    </tr>          
    <tr>
      <td>100 Go - 249 Go</td>
      <td>3 112 863</td>
    </tr>          
    <tr>
      <td>250 Go - 499 Go</td>
      <td>7 782 300</td>
    </tr>          
    <tr>
      <td>500 Go - 999 Go</td>
      <td>15 564 695</td>
    </tr>
    <tr>
      <td>1 To</td>
      <td>31 876 593</td>
    </tr>
    <tr>
      <td>2 To</td>
      <td>63,753,186</td>
    </tr>
    <tr>
      <td>3 To</td>
      <td>95,629,970</td>
    </tr>
    <tr>
      <td>4 To - 12 To</td>
      <td>127,506,359</td>
    </tr>
   </tbody>
</table>

## Mesure des IOPS
{: faq}

Les IOPS sont mesurées en fonction d'un profil de chargement de blocs de 16 Ko avec une répartition aléatoire de 50 % de lectures et 50 % d'écritures. Les charges de travail qui diffèrent de ce profil sont susceptibles de connaître des performances moins élevées.

## Que se passe-t-il si j'utilise une taille de bloc plus petite pour mesurer les performances ?
{: faq}

Le nombre maximal d'IOPS peut être obtenu même si vous utilisez des tailles de bloc plus petites. Toutefois, le débit sera plus lent. Par exemple, un volume doté de 6 000 IOPS présente les débits suivants en fonction des tailles de bloc :

- 16 ko * 6 000 IOPS == ~93,75 Mo/sec
- 8 ko * 6 000 IOPS == ~46,88 Mo/sec
- 4 ko * 6 000 IOPS == ~23,44 Mo/sec


## Les opérations d'entrées-sorties par seconde (IOPS) sont-elles allouées par instance ou par volume ?
{: faq}

Les IOPS sont appliquées au niveau volume. Autrement dit, deux hôtes connectés à un volume doté de 6 000 IOPS partagent ces 6 000 IOPS.

## Le volume doit-il être préchauffé pour obtenir le débit prévu ?
{: faq}

Il n'est pas nécessaire de préchauffer le volume. Le débit indiqué peut être observé immédiatement après la mise à disposition du volume.

## Est-il possible d'atteindre un débit plus élevé si une connexion Ethernet plus rapide est utilisée ?
{: faq}

Les limites de débit sont configurées par volume. Une connexion Ethernet plus rapide ne permet pas d'augmenter la limite définie. Une connexion Ethernet plus lente risque toutefois de générer un goulot d'étranglement.

## Les pare-feu et groupes de sécurité ont-ils un impact sur les performances ?
{: faq}

Il est recommandé d'exécuter le trafic de stockage sur un réseau local virtuel qui ignore le pare-feu. L'exécution du trafic de stockage via des pare-feu logiciels augmente le temps d'attente et a un impact négatif sur les performances de stockage.

## Quel temps d'attente lié aux performances puis-je attendre de mon stockage {{site.data.keyword.filestorage_short}} ?   
{: faq}

Le temps d'attente cible du stockage est inférieur à 1 ms. Le stockage est connecté à des instances de calcul sur un réseau partagé ; le temps d'attente exact des performances dépend donc du trafic réseau sur une période donnée.

## Qu'advient-il des données en cas de suppression des volumes {{site.data.keyword.filestorage_short}} ?
{: faq}

{{site.data.keyword.filestorage_full}} présente des partages de fichiers aux clients sur un stockage physique avant toute réutilisation. Les clients ayant des exigences particulières en matière de conformité (par exemple, NIST 800-88 Guidelines for Media Sanitization) doivent exécuter une procédure d'expurgation des données avant de supprimer leur stockage.

## Quelles sont les versions NFS prises en charge ?
{: faq}

NFS version 3 et NFS version 4.1 sont pris en charge dans l'environnement {{site.data.keyword.BluSoftlayer_full}}. 

NFS version 3 est recommandé car il s'agit d'un protocole sans état plus résilient lorsque des événements de réseau se produisent. 

NFS v3 prend en charge en natif `no_root_squash` qui permet aux clients root de conserver les droits root sur le partage NFS. Vous pouvez activer cette fonctionnalité dans NFS v4.1 en éditant les informations sur le domaine et en exécutant `rpcidmapd` ou un service similaire. Pour plus d'informations, voir [Implémentation de no_root_squash pour NFS](/docs/infrastructure/FileStorage?topic=FileStorage-mountingLinux#norootsquash).

Lorsqu'il s'agit de vSphere Solutions, NFS version 3 prend en charge plus de fonctionnalités que la version 4.1. Par exemple, Storage DRS et Site Recovery Manager.


## Qu'advient-il des unités déclassées du centre de données de cloud ?
{: faq}

Lorsque des unités sont déclassées, IBM les détruit avant de les supprimer. Elles sont ainsi inutilisables. Toutes les données écrites sur ces unités deviennent inaccessibles.
