---

copyright:
  years: 2014, 2017
lastupdated: "2017-12-14"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.filestorage_full_notm}} Encryption-At-Rest 

{{site.data.keyword.BluSoftlayer_full}} takes the need for security seriously, and understand the importance of being able to encrypt data to keep it safe. With provider managed encryption, {{site.data.keyword.filestorage_full}} provisioned with either Endurance or Performance are encrypted by default at no additional cost and no impact to performance.

The provider managed encryption-at-rest feature uses the following industry standard protocols:

* Industry-Standard AES-256 encryption
* Keys are managed in-house with industry standard Key Management Improbability Protocol (KMIP)
* Storage is Federal Information Processing Standard (FIPS) Publication 140-2 validated for Federal Information Security Management Act (FISMA), Health Insurance Portability and Accountability Act (HIPAA), Payment Card Industry (PCI), Basel II, California Security Breach Information Act (SB 1386) and EU Data Protection Directive 95/46/EC compliance

## Encryption-at-Rest for Snapshots or Replicated storage  

All snapshots and replicas of encrypted file storage are also encrypted by default. This feature cannot be turned off on a volume basis.

## Provisioning Storage with Encryption

The provider managed encryption-at-rest feature is only available for {{site.data.keyword.filestorage_short}} that is provisioned in select data centers with new data center availability being added regularly. All storage provisioned in these data centers is automatically provisioned with encryption for data-at-rest. Click [here](new-ibm-block-and-file-storage-location-and-features.html) to see the current list of data centers where {{site.data.keyword.filestorage_short}} encryption for data-at-rest is available.


When ordering your {{site.data.keyword.filestorage_short}}, select a data center noted with an asterisk (`*`) and message stating that encryption is available. You will see a lock icon to the right of the LUN/Volume Name field indicating that it is encrypted. See Figure 1.

![The lock icon indicates that the LUN is encrypted](/images/encryptedstorage.png)
<caption>Figure 1. Example of the lock icon indicating the volume is encrypted.</caption>



**Note** that non-encrypted storage provisioned prior to a data center upgrade will **not** be automatically encrypted. If you have non-encrypted storage in an upgraded data center, you will need to create a new volume and perform a data migration. The following article can provide guidance.

* [File Storage Migration in Upgraded Data Centers](migrate-file-storage-encrypted-file-storage.html)
