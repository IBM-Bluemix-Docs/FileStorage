---

copyright:
  years: 2014, 2018
lastupdated: "2018-11-30"

---
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# SL CLI를 통해 {{site.data.keyword.filestorage_short}} 주문

일반적으로 [{{site.data.keyword.slportal}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){:new_window}을 통해 주문하는 제품을 주문하는 데 SL CLI를 사용할 수 있습니다. SL API에서, 주문은 여러 주문 컨테이너로 구성됩니다. 주문 CLI는 하나의 주문 컨테이너와만 작동합니다.

SL CLI 설치 및 사용 방법에 관한 자세한 정보는 [Python API 클라이언트](https://softlayer-python.readthedocs.io/en/latest/cli.html){:new_window}를 참조하십시오.
{:tip}

## 사용 가능한 {{site.data.keyword.filestorage_short}} 오퍼 검색

주문할 때 검색하는 첫 번째 컴포넌트가 패키지입니다. 패키지는 {{site.data.keyword.BluSoftlayer_full}}에서 주문하는 데 사용할 수 있는 다양한 최상위 레벨 제품으로 구분됩니다. 몇 가지 예제 패키지는 VSI의 경우 CLOUD_SERVER, Bare Metal Server의 경우 BARE_METAL_SERVER, {{site.data.keyword.filestorage_short}} 및 {{site.data.keyword.blockstorageshort}}의 경우 STORAGE_AS_A_SERVICE_STAAS입니다.

패키지에서 일부 항목은 카테고리로 분할됩니다. 일부 패키지에는 편의를 위한 사전 설정 세트가 있으며 다른 패키지에서는 항목을 개별적으로 지정해야 합니다. 패키지의 카테고리가 필요한 경우, 패키지를 주문하려면 해당 카테고리의 항목을 선택해야 합니다. 카테고리에 따라 카테고리에 있는 일부 항목은 상호 배타적일 수 있습니다.

각 주문에는 위치(데이터 센터)가 연관되어 있어야 합니다. {{site.data.keyword.filestorage_short}}를 주문할 때 컴퓨팅 인스턴스와 동일한 위치에서 프로비저닝되는지 확인하십시오.
{:important}

`slcli order package-list` 명령을 사용하여 주문할 패키지를 찾을 수 있습니다. `–keyword` 옵션은 단순 검색 및 필터링을 수행하도록 제공됩니다. 이 옵션을 사용하면 필요한 패키지를 찾기가 쉬워집니다.

```
$ slcli order package-list --help
사용법: slcli order package-list [OPTIONS]

  placeOrder API를 통해 주문할 수 있는 패키지를 나열합니다.

  예:
      # 주문 가능한 모든 패키지 나열
      slcli order package-list

  패키지를 더 쉽게 찾을 수 있도록 일부 간단한 필터링 기능에도 키워드에
  사용할 수 있습니다.

  예:
     # 이름에 "server"가 있는 모든 패키지 나열
      slcli order package-list --keyword server

옵션:
  --keyword TEXT  패키지 이름을 필터링하는 데 사용하는 단어(또는 문자열)입니다.
  -h, --help      이 메시지를 표시하고 종료합니다.
```

*Storage-as-a-Service Package 759를 찾는 방법에 관한 지시사항 필요*

```
$ slcli order package-list --keyword "Storage"
:.....................:.....................:
:         이름        :       keyName       :
:.....................:.....................:
: ???                 : ???                 :
: ???                 : ???                 :
:.....................:.....................:
```

```
$ slcli order category-list STORAGE_AS_A_SERVICE_STAAS --required
:..................................:...................:............:
:               이름               :    categoryCode   : isRequired :
:..................................:...................:............:
:              예제                :        ???        :     Y      :
:              예제                :        ???        :     Y      :
:              예제                :        ???        :     Y      :
:              예제                :        ???        :     Y      :
:..................................:...................:............:
```

`item-list` 명령을 사용하여 주문할 나머지 항목을 선택하십시오. 일반적으로 패키지에는 선택할 수 있는 항목이 많이 있으므로 `–category` 옵션을 사용하여 관심있는 카테고리에서만 항목을 검색하십시오.

```
$ slcli order item-list STORAGE_AS_A_SERVICE_STAAS --category ??
:..........................:..............................................:
:         keyName          :                설명                          :
:..........................:..............................................:
:           ???            :                    ????                      :
:           ???            :                    ????                      :
:           ???            :                    ????                      :
:           ???            :                    ????                      :
:..........................:..............................................:
```

API를 통해 {{site.data.keyword.filestorage_short}}를 주문하는 데 관한 자세한 정보는 [order_file_volume](https://softlayer-python.readthedocs.io/en/latest/api/managers/file.html#SoftLayer.managers.file.FileStorageManager.order_file_volume){:new_window}을 참조하십시오.
새 기능에 모두 액세스할 수 있으려면 `Storage-as-a-Service Package 759`를 주문하십시오.
{:tip}

## 주문 확인

주문에서 필수 카테고리가 누락되었는지 확신이 없으면 `place` 명령과 함께 `–verify` 플래그를 사용할 수 있습니다. 카테고리가 누락된 경우 화면에 인쇄됩니다.


```
$ slcli order place --verify blablabla
:..............................................:.................................................:......:
:                keyName                       :                   설명                          : 비용 :
:..............................................:.................................................:......:
:                  ???                         :                 yadi yadi yada                  :  0   :
:                  ???                         :                 yadi yadi yada                  :  0   :
:                  ???                         :                 yadi yadi yada                  :  0   :
:                  ???                         :                 yadi yadi yada                  :  0   :
:..............................................:.................................................:......:
```

출력에는 주문하는 각 항목 및 해당 항목과 관련된 비용이 표시됩니다. 주문이 검증을 통과하면 충돌하는 항목이 없고 모든 필수 카테고리에 주문에 지정된 항목이 있다는 의미입니다.

## 주문하기

다음 단계는 주문을 하는 것입니다.

```
$ slcli order place .....

이 조치를 수행하면 계정에 비용이 청구됩니다. 계속하시겠습니까? [y/N]: y

API 응답
```

기본적으로, 250개 {{site.data.keyword.filestorage_short}} 볼륨의 통합 총계를 프로비저닝할 수 있습니다. 볼륨 수를 늘리려면 영업 담당자에게 문의하십시오. 한계를 늘리는 데 관한 자세한 정보는 [스토리지 한계 관리](managing-storage-limits.html)를 참조하십시오.
{:important}

## 호스트에 새 스토리지에 액세스하는 권한 부여

TBD

호스트에서 API를 통해 {{site.data.keyword.filestorage_short}}에 액세스하는 권한을 부여하는 데 관한 자세한 정보는 [authorize_host_to_volume](https://softlayer-python.readthedocs.io/en/latest/api/managers/file.html#SoftLayer.managers.file.FileStorageManager.authorize_host_to_volume){:new_window}을 참조하십시오.
{:tip}

동시 권한 부여 한계에 관한 자세한 정보는 [FAQ](faqs.html)를 참조하십시오.
{:important}

## 새 스토리지 연결

호스트의 운영 체제에 따라 적절한 링크를 사용하십시오.
- [Linux의 {{site.data.keyword.filestorage_short}} 마운트](accessing-file-storage-linux.html)
- [CentOS의 {{site.data.keyword.filestorage_short}} 마운트](mounting-nsf-file-storage.html)
- [CoreOS의 {{site.data.keyword.filestorage_short}} 마운트](mounting-storage-coreos.html)
- [cPanel로 백업을 위한 {{site.data.keyword.filestorage_short}} 구성](configure-backup-cpanel.html)
- [Plesk로 백업을 위한 {{site.data.keyword.filestorage_short}} 구성](configure-backup-plesk.html)
- [ESXi 호스트에 {{site.data.keyword.filestorage_short}} 볼륨 마운트](architecture-guide-file-storage-vmware.html)
