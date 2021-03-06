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


# Tutorial de introdução
{: #getting-started}

O {{site.data.keyword.filestorage_full}} é um {{site.data.keyword.filestorage_short}} baseado em NFS persistente, rápido e flexível, conectado à rede. Nesse ambiente de armazenamento conectado à rede (NAS), você tem controle total sobre sua função de compartilhamentos de arquivo e sobre o desempenho. Os compartilhamentos do {{site.data.keyword.filestorage_short}} podem ser conectados a até 64 dispositivos autorizados sobre conexões TCP/IP roteadas para resiliência.
{:shortdesc}

## Antes de Iniciar
{: #prereqs}

Os volumes do {{site.data.keyword.filestorage_short}} podem ser provisionados de 20 GB a 12 TB com duas opções: <br/>
- Provisiona camadas do **Endurance** que apresentam níveis de desempenho predefinidos e outros recursos, como capturas instantâneas e replicação.
- Construa um ambiente **Performance** de alta potência com input/output operations per second (IOPS) alocado.

Para obter mais informações sobre a oferta do {{site.data.keyword.filestorage_short}}, consulte [Sobre o {{site.data.keyword.filestorage_short}}](/docs/infrastructure/FileStorage?topic=FileStorage-about)

## Considerações de fornecimento

### Tamanho do Bloco

O IOPS para Endurance e Performance se baseia em um tamanho de bloco de 16 KB com uma carga de trabalho aleatória/sequencial 50/50 de leitura/gravação 50/50. Um bloco de 16 KB equivale a uma gravação no volume.
{:important}

O tamanho do bloco usado por seu aplicativo afetará diretamente o desempenho do armazenamento. Se o tamanho do bloco usado por seu aplicativo for menor que 16 KB, o limite do IOPS será realizado antes do limite do rendimento. Por outro lado, se o tamanho do bloco usado por seu aplicativo for maior que 16 KB, o limite de rendimento será realizado antes do limite do IOPS.

<table>
  <caption>A Tabela 4 mostra exemplos de como o tamanho do bloco e o IOPS afetam o rendimento.</caption>
        <colgroup>
          <col/>
          <col/>
          <col/>
        </colgroup>
        <thead>
          <tr>
            <th>Tamanho de bloco (KB)</th>
            <th>IOPS</th>
            <th>Rendimento (MB/s)</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>4 (típico para Linux)</td>
            <td>1.000</td>
            <td>4</td>
          </tr>
          <tr>
            <td>8 (típico para Oracle)</td>
            <td>1.000</td>
            <td>8</td>
          </tr>
          <tr>
            <td>16</td>
            <td>1.000</td>
            <td>16</td>
          </tr>
          <tr>
            <td>32 (típico para o SQL Server)</td>
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

### Hosts autorizados

Outro fator a ser considerado é o número de hosts que estão usando seu volume. Se houver um único host acessando o volume, poderá ser difícil realizar o IOPS máximo disponível, especialmente em contagens extremas de IOPS (10.000s). Se a sua carga de trabalho requerer alto rendimento, será melhor configurar pelo menos alguns servidores para acessar seu volume para evitar um gargalo de servidor único.

### Conexão da rede

A velocidade da sua conexão Ethernet deve ser mais rápida do que o rendimento máximo esperado de seu volume. Em geral, não espere saturar sua conexão Ethernet além de 70% da largura de banda disponível. Por exemplo, se você tiver 6.000 IOPS e estiver usando um tamanho de bloco de 16 KB, o volume poderá manipular o rendimento de aproximadamente 94 MBps. Se você tiver uma conexão Ethernet de 1 Gbps com seu LUN, ela se tornará um gargalo quando seus servidores tentarem usar o rendimento máximo disponível. Isso porque 70 por cento do limite teórico de uma conexão Ethernet de 1 Gbps (125 MB por segundo) permitiria 88 MB por segundo apenas.

Para alcançar o IOPS máximo, recursos de rede adequados precisam estar em vigor. Outras considerações incluem o uso de rede privada fora do armazenamento e do lado do host, além de ajustes específicos do aplicativo (pilha de IP ou [profundidades de fila](/docs/infrastructure/FileStorage?topic=FileStorage-hostqueuesettings) e outras configurações).

O tráfego de armazenamento é incluído no uso total de rede de Virtual Servers Públicos. Para obter mais informações sobre os limites que podem ser impostos pelo serviço, consulte a [Documentação do Virtual Server](/docs/vsi?topic=virtual-servers-about-public-virtual-servers).

### Versão de NFS

O NFS v3 e NFS v4.1 são suportados no ambiente do {{site.data.keyword.BluSoftlayer_full}}. No entanto, o NFS v3 é preferencial porque o NFS v4.1 é um protocolo stateful (não stateless como o NFSv3) e problemas de protocolo podem ocorrer durante eventos de rede. O NFS v4.1 deve colocar em modo quiesce todas as operações e, em seguida, concluir a recuperação de bloqueio. Em um servidor de arquivos NFS relativamente ocupado, a latência aumentada pode causar interrupções. A falta de caminhos múltiplos e entroncamento do NFS v4.1 também pode estender a recuperação das operações do NFS.

## Enviando sua Ordem

Quando você estiver pronto para enviar seu pedido, poderá fazer isso por meio
do [Console](/docs/infrastructure/FileStorage?topic=FileStorage-orderingConsole) ou da [SLCLI](/docs/infrastructure/FileStorage?topic=FileStorage-orderingSLCLI). Para ver Provisionando o File Storage com o VMware, clique [aqui](/docs/infrastructure/FileStorage?topic=FileStorage-architectureguide)

## Conectando seu novo armazenamento
{: #mountingstorage}

Quando sua solicitação de fornecimento estiver concluída, autorize seus hosts a acessar o novo armazenamento e configurar sua conexão. Dependendo do sistema operacional de seu host, siga o link apropriado.
- [Acessando o {{site.data.keyword.filestorage_short}} no Linux](/docs/infrastructure/FileStorage?topic=FileStorage-mountingLinux)
- [Montando o {{site.data.keyword.filestorage_short}} no CentOS](/docs/infrastructure/FileStorage?topic=FileStorage-mountingCentOS)
- [Montando o {{site.data.keyword.filestorage_short}} no CoreOS](/docs/infrastructure/FileStorage?topic=FileStorage-mountingCoreOS)
- [Configurando o {{site.data.keyword.filestorage_short}} para backup com o cPanel](/docs/infrastructure/FileStorage?topic=FileStorage-cPanelBackups)
- [Configurando o {{site.data.keyword.filestorage_short}} para backup com o Plesk](/docs/infrastructure/FileStorage?topic=FileStorage-PleskBackup)
- [Montando o volume do {{site.data.keyword.filestorage_short}} em hosts ESXi](/docs/infrastructure/FileStorage?topic=FileStorage-architectureguide)

## Gerenciando seu novo Armazenamento

Por meio do portal ou do SLCLI, é possível gerenciar vários aspectos de seu {{site.data.keyword.filestorage_short}}, tais como autorizações e cancelamentos de host. Para obter mais informações, consulte [Gerenciando o {{site.data.keyword.filestorage_short}}](/docs/infrastructure/FileStorage?topic=FileStorage-managingstorage).
