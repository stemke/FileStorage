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

# 재해 복구 - 액세스 가능한 1차 볼륨으로 장애 복구
{: #dr-accessible}

1차 사이트에서 파국적 장애나 재해가 발생하고 1차 스토리지에는 여전히 액세스할 수 있는 경우 고객은 다음의 조치를 취하여 2차 사이트의 데이터에 빠르게 액세스할 수 있습니다.

장애 복구를 시작하기 전에 모든 호스트 권한 부여가 준비되어 있는지 확인하십시오.

권한 부여된 호스트 및 볼륨은 동일한 데이터 센터에 있어야 합니다. 예를 들어 복제본 볼륨은 런던에 두고 호스트는 암스테르담에 둘 수는 없습니다. 둘 다 런던에 있거나 둘 다 암스테르담에 있어야 합니다.
{:note}

1. [{{site.data.keyword.cloud}} 콘솔 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/catalog){:new_window}에 로그인하고 왼쪽 상단에서 **메뉴** 아이콘을 클릭하십시오. **일반 인프라**를 선택하십시오.

   또는 [{{site.data.keyword.slportal}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){:new_window}에 로그인할 수 있습니다.
1. **{{site.data.keyword.filestorage_short}}** 페이지에서 소스 또는 대상 볼륨을 클릭하십시오.
2. **복제본**을 클릭하십시오.
3. **호스트 권한 부여** 프레임으로 스크롤하여 오른쪽에 있는 **호스트 권한 부여**를 클릭하십시오.
4. 복제에 대해 권한 부여되는 호스트에 강조표시하십시오. 다수의 호스트를 선택하려면 CTRL 키를 사용하여 해당되는 호스트를 클릭하십시오.
5. **제출**을 클릭하십시오. 호스트가 없는 경우에는 동일한 데이터 센터의 컴퓨팅 리소스를 구매하라는 프롬프트가 표시됩니다.

## 볼륨에서 해당 복제본으로 장애 복구 시작

장애가 발생하는 경우에는 대상 볼륨으로 **장애 복구**를 시작할 수 있습니다. 대상 볼륨이 활성이 됩니다. 마지막으로 복제된 스냅샷이 활성화되며 볼륨이 마운트를 위해 활성화됩니다. 이전 복제 주기 이후 소스 볼륨에 기록된 데이터는 유실됩니다. 장애 복구가 시작되면 복제 관계가 반전됩니다. 대상 볼륨이 소스 볼륨이 되고, 이전 소스 볼륨은 **REP**가 뒤따르는 **LUN 이름**으로 표시되는 대상이 됩니다.

장애 복구는 [[{{site.data.keyword.slportal}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){:new_window}의 **스토리지**, **{{site.data.keyword.filestorage_short}}**에서 시작합니다.

이러한 단계를 진행하기 전에 볼륨의 연결을 끊으십시오. 그렇게 하지 못하면 손상 및 데이터 유실이 발생합니다.
{:important}

1. 활성 볼륨("소스")을 클릭하십시오.
2. 오른쪽 상단에서 **복제본**을 클릭하고 **조치**를 클릭하십시오.
3. **장애 복구**를 선택하십시오.

   장애 복구가 진행 중임을 알리는 메시지가 표시됩니다. 또한 **{{site.data.keyword.filestorage_short}}**의 볼륨 옆에 활성 트랜잭션이 진행 중임을 나타내는 아이콘이 표시됩니다. 아이콘 위로 마우스 커서를 이동하면 트랜잭션을 표시하는 창이 생성됩니다. 일단 트랜잭션이 완료되면 아이콘이 사라집니다. 장애 복구 프로세스 중에는 구성 관련 조치가 읽기 전용입니다. 사용자는 스냅샷 스케줄을 편집하거나 스냅샷 영역을 변경할 수 없습니다. 이벤트는 복제 히스토리에 로깅됩니다.<br/> 대상 볼륨이 작동 상태가 되면 다른 메시지가 수신됩니다. 원래 소스 볼륨의 LUN 이름이 "REP"로 끝나도록 업데이트되며 해당 상태가 비활성이 됩니다.
   {:note}
4. **모두 보기({{site.data.keyword.filestorage_short}})**를 클릭하십시오.
5. 활성 볼륨(이전 대상 볼륨)을 클릭하십시오. 이제는 이 볼륨의 상태가 **활성**입니다.
6. 스토리지 볼륨을 호스트에 마운트하고 이에 연결하십시오. 지시사항을 보려면 [여기](/docs/infrastructure/FileStorage?topic=FileStorage-orderingConsole)를 클릭하십시오.


## 볼륨에서 해당 복제본으로 장애 조치 시작

원래 소스 볼륨이 복구되면 원래 소스 볼륨으로 제어된 장애 조치를 시작할 수 있습니다. 제어된 장애 조치에서는 다음 항목이 적용됩니다.

- 활성 소스 볼륨이 오프라인 상태가 됩니다.
- 스냅샷이 작성됩니다.
- 복제 주기가 완료됩니다.
- 방금 작성된 데이터 스냅샷이 활성화됩니다.
- 소스 볼륨이 마운트를 위해 활성화됩니다.

장애 조치가 시작되면 복제 관계가 다시 반전됩니다. 소스 볼륨이 소스 볼륨으로 복원되고, 대상 볼륨이 다시 **REP**가 뒤따르는 **LUN 이름**으로 표시되는 대상 볼륨이 됩니다.

장애 조치는 [[{{site.data.keyword.slportal}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){:new_window}의 **스토리지**, **{{site.data.keyword.filestorage_short}}**에서 시작합니다.

1. 활성 볼륨("대상")을 클릭하십시오.
2. 오른쪽 상단에서 **복제본**을 클릭하고 **조치**를 클릭하십시오.
3. **장애 조치**를 선택하십시오.

   장애 복구가 진행 중임을 나타내는 메시지가 표시됩니다. 또한 **{{site.data.keyword.filestorage_short}}**의 볼륨 옆에 활성 트랜잭션이 진행 중임을 나타내는 아이콘이 표시됩니다. 아이콘 위로 마우스 커서를 이동하면 트랜잭션을 표시하는 창이 생성됩니다. 일단 트랜잭션이 완료되면 아이콘이 사라집니다. 장애 조치 프로세스 중에는 구성 관련 조치가 읽기 전용입니다. 사용자는 스냅샷 스케줄을 편집하거나 스냅샷 영역을 변경할 수 없습니다. 이벤트는 복제 히스토리에 로깅됩니다.
   {:note}
4. 오른쪽 상단에서 **모든 {{site.data.keyword.filestorage_short}} 보기** 링크를 클릭하십시오.
5. 활성 볼륨("소스")을 클릭하십시오.
6. 스토리지 볼륨을 호스트에 마운트하고 이에 연결하십시오. 지시사항을 보려면 [여기](/docs/infrastructure/FileStorage?topic=FileStorage-orderingConsole)를 클릭하십시오.
