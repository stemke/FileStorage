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


# 재해 복구 - 액세스할 수 없는 1차 볼륨으로 장애 복구
{: #dr-inaccessible}

파국적 장애나 재해 때문에 1차 사이트에서 가동 중단이 발생하는 경우 고객은 다음의 조치를 취하여 2차 사이트의 데이터에 빠르게 액세스할 수 있습니다.

## 2차 사이트에서 복제본 볼륨의 중복으로 장애 복구

1. [IBM Cloud 콘솔 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/){:new_window}에 로그인하고 왼쪽 상단의 **메뉴** 아이콘을 클릭하십시오. **일반 인프라**를 선택하십시오.

   또는 [{{site.data.keyword.slportal}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){:new_window}에 로그인할 수 있습니다.
2. **스토리지** > **{{site.data.keyword.filestorage_short}}**를 클릭하십시오.
3. 목록에서 파일 공유의 복제본을 클릭하여 해당 **세부사항** 페이지를 보십시오.
4. **세부사항** 페이지에서 아래로 스크롤하여 기존 스냅샷을 선택한 후에 **조치** > **중복**을 클릭하십시오.
5. 필요한 대로 새 볼륨의 IOP 또는 용량(크기 늘리기)을 업데이트하십시오.
6. 필요하면 새 볼륨의 스냅샷 영역을 업데이트할 수 있습니다.
7. **계속**을 클릭하여 복제를 주문하십시오.

볼륨이 작성되는 즉시 이를 호스트에 연결하여 해당 볼륨에 대한 읽기/쓰기 오퍼레이션을 수행할 수 있습니다. 데이터가 원래 볼륨에서 복제 볼륨으로 복사되는 동안 세부사항 페이지에는 복제가 진행 중임을 보여주는 상태가 표시됩니다. 복제 프로세스가 완료되면 새 볼륨은 원본으로부터 독립되며 정상적으로 스냅샷 및 복제의 관리가 가능합니다.

## 원래 1차 사이트로 장애 조치

프로덕션을 원래 1차 사이트로 리턴하려면 다음 단계를 수행해야 합니다.

1. [IBM Cloud 콘솔 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/){:new_window}에 로그인하고 왼쪽 상단의 **메뉴** 아이콘을 클릭하십시오. **일반 인프라**를 선택하십시오.

   또는 [{{site.data.keyword.slportal}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){:new_window}에 로그인할 수 있습니다.
2. **스토리지** > **{{site.data.keyword.filestorage_short}}**를 클릭하십시오.
3. LUN 이름을 클릭하고 스냅샷 스케줄을 작성하십시오(아직 존재하지 않는 경우).

   스냅샷 스케줄에 대한 자세한 정보는 [스냅샷 관리](/docs/infrastructure/FileStorage?topic=FileStorage-managingSnapshots#addschedule)를 참조하십시오.
   {:tip}
4. **복제본**을 클릭하고 **복제 구매**를 클릭하십시오.
5. 복제가 따라야 할 기존 스냅샷 스케줄을 선택하십시오. 목록에는 모든 활성 스냅샷 스케줄이 포함됩니다.
6. **위치**를 클릭하고 원래 프로덕션 사이트였던 데이터 센터를 선택하십시오.
7. **계속**을 클릭하십시오.
8. **마스터 서비스 계약을 읽었습니다…** 선택란을 클릭하고 **주문하기**를 클릭하십시오.

복제가 완료되면 새 복제본의 중복 볼륨을 작성해야 합니다.
{:important}

1. **스토리지** > **{{site.data.keyword.filestorage_short}}**로 되돌아가십시오.
2. 목록에서 LUN의 복제본을 클릭하여 해당 **세부사항** 페이지를 보십시오.
3. **세부사항** 페이지에서 아래로 스크롤하여 기존 스냅샷을 선택한 후에 **조치** > **중복**을 클릭하십시오.
4. 필요한 대로 새 볼륨의 IOP 또는 용량(크기 늘리기)을 업데이트하십시오.
5. 필요하면 새 볼륨의 스냅샷 영역을 업데이트하십시오.
6. **계속**을 클릭하여 복제를 주문하십시오.

복제 프로세스가 완료되면 데이터를 다시 원래 1차 사이트로 가져오는 데 사용된 볼륨 및 복제를 취소할 수 있습니다. 복제는 1차 스토리지가 되며, 원래 2차 사이트로의 복제가 다시 설정될 수 있습니다.
