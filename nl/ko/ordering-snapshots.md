---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-05"

keywords: File Storage, file storage, NFS, snapshot, ordering snapshot, snapshot space

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}


# 스냅샷 구매
{: #ordering-snapshots}

자동으로 또는 수동으로 스토리지 볼륨의 스냅샷을 작성하려면 이를 보관하기 위한 영역을 구매해야 합니다. 최대 스토리지 볼륨 양까지 용량을 구매할 수 있습니다(초기 볼륨 구매 중에 또는 해당 단계를 사용하여 나중에).

## 주문할 스냅샷 영역의 양 결정

일반적으로 스냅샷 영역은 스냅샷에서 두 가지 핵심 요인에 따라 사용됩니다.
- 시간 경과에 따라 활성 파일 시스템이 변경되는 양
- 스냅샷을 보존할 기간  

필요한 영역의 양을 계산하는 방법은 **(변경 비율)** x **(데이터 보존 시간/일/주/월 수)**입니다.  

활성 파일 시스템 블록을 표시하는 메타데이터의 사본(포인터)에 불과하므로, 첫 번째 스냅샷은 매우 소량의 영역을 사용합니다.
{:note}

변경량이 많고 보존 기간이 긴 볼륨은 변경량과 보존 스케줄이 중간 정도인 볼륨보다 더 많은 영역을 필요로 합니다. 첫 번째 유형의 예로는 변경 비율이 높은 데이터베이스가 있습니다. 두 번째 유형의 예로는 VMware 데이터 저장소가 있습니다.

500GB의 실제 데이터에 대해 12개의 시간별 스냅샷을 작성하며 각 스냅샷 간의 변경량이 1퍼센트인 경우에는 스냅샷에 60GB를 사용하게 됩니다.

*(5GB의 변경 비율) x (12개의 시간별 스냅샷) = (60GB의 사용 영역)*

반면 실제 데이터가 500GB이고 시간별 스냅샷 수가 12개이며 시간당 10퍼센트의 변경량이 관찰된 경우 사용되는 스냅샷 영역은 600GB입니다.

*(50GB의 변경 비율) x (12개의 시간별 스냅샷) = (600GB의 사용 영역)*

따라서 필요한 스냅샷 영역의 양을 결정할 때는 변경 비율을 신중하게 고려하십시오. 이는 필요한 스냅샷 영역의 양에 중대한 영향을 줍니다. 볼륨이 클수록 자주 변경될 가능성이 높습니다. 그러나 변경량이 5GB인 500GB 볼륨과 변경량이 5GB인 10TB 볼륨은 동일한 양의 스냅샷 영역을 사용합니다.

또한 대부분의 워크로드에서는 볼륨이 클수록 초기에 확보해야 하는 영역이 더 작아집니다. 이는 주로 기본 데이터 효율성과 환경에서 스냅샷이 작동하는 방식에 기인합니다.

## {{site.data.keyword.cloud_notm}} 콘솔을 통해 스냅샷 영역 주문

1. [IBM Cloud 콘솔](https://{DomainName}/){:new_window}에 로그인하여 왼쪽 상단의 메뉴 아이콘을 클릭하십시오. **일반 인프라**를 선택하십시오.

   또는 [{{site.data.keyword.slportal}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){:new_window}에 로그인할 수 있습니다.
2. **스토리지** > **{{site.data.keyword.filestorage_short}}**를 통해 스토리지에 액세스하십시오.
3. 스냅샷 프레임에서 **스냅샷 영역 변경**을 클릭하십시오.
4. 필요한 영역의 양과 지불 방법을 선택하십시오.
5. **계속**을 클릭하십시오.
6. 보유한 프로모션 코드를 입력하고 **재계산**을 클릭하십시오. **이 주문의 비용** 및 **주문 검토**에는 기본값이 있습니다.

   주문을 처리할 때 할인이 적용됩니다.
   {:note}
7. **마스터 서비스 계약을 읽었으며 해당 이용 약관에 동의합니다** 상자를 선택하고 **주문하기**를 클릭하십시오. 잠시 후에 스냅샷 영역이 프로비저닝됩니다.

## SLCLI를 통해 스냅샷 영역 주문

```
# slcli file snapshot-order --help
Usage: slcli file snapshot-order [OPTIONS] VOLUME_ID

Options:
  --capacity INTEGER    Size of snapshot space to create in GB  [required]
  --tier [0.25|2|4|10]  Endurance Storage Tier (IOPS per GB) of the file
                        volume for which space is ordered [optional, and only
                        valid for endurance storage volumes]
  --upgrade             Flag to indicate that the order is an upgrade
  -h, --help            Show this message and exit.
```
