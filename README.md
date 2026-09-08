# NoSQL Database Comparison Service

Java ve Maven kullanılarak geliştirilen bu projede, **Redis, Hazelcast ve MongoDB** NoSQL teknolojileri kullanılarak aynı veri setine erişim sağlayan REST tabanlı bir servis geliştirilmiştir.

Projenin temel amacı, farklı NoSQL veri depolama teknolojilerinin kullanımını ve veri erişim performanslarını karşılaştırmalı olarak incelemektir.

## Proje Özellikleri

* Java ile REST tabanlı servis geliştirme
* Redis, Hazelcast ve MongoDB entegrasyonu
* Her veri tabanında **10.000 öğrenci kaydı** ile çalışma
* Her teknoloji için ayrı veri erişim katmanı
* Öğrenci numarası üzerinden doğrudan veri sorgulama
* JSON formatında veri sunumu
* Maven ile bağımlılık ve proje yönetimi
* Farklı NoSQL teknolojilerinin performans karşılaştırması

## Kullanılan Teknolojiler

* **Java 11**
* **Apache Maven**
* **Spark Java** – REST API geliştirme
* **Redis** – Key-Value veri depolama
* **Jedis** – Redis Java istemcisi
* **Hazelcast** – Dağıtık veri yapısı / In-Memory Data Grid
* **MongoDB** – Doküman tabanlı NoSQL veri tabanı
* **MongoDB Java Driver**
* **Gson** – JSON serileştirme ve deserileştirme

## Mimari Yapı

Proje, veri erişim sorumluluklarını ayrı sınıflara ayıracak şekilde yapılandırılmıştır.

```text
src/
└── main/
    └── java/
        └── app/
            ├── Main.java
            ├── model/
            │   └── Student.java
            └── store/
                ├── RedisStore.java
                ├── HazelcastStore.java
                └── MongoStore.java
```

`Student` modeli ortak veri yapısını temsil ederken, `RedisStore`, `HazelcastStore` ve `MongoStore` sınıfları ilgili veri tabanlarıyla gerçekleştirilen veri erişim işlemlerini yönetmektedir.

## REST Endpoint'leri

Her NoSQL teknolojisi için ayrı bir endpoint bulunmaktadır:

| Teknoloji | Endpoint                                 |
| --------- | ---------------------------------------- |
| Redis     | `/nosql-lab-rd/student_no={student_no}`  |
| Hazelcast | `/nosql-lab-hz/student_no={student_no}`  |
| MongoDB   | `/nosql-lab-mon/student_no={student_no}` |

Örnek:

```text
http://localhost:8080/nosql-lab-rd/student_no=2025000001
http://localhost:8080/nosql-lab-hz/student_no=2025000001
http://localhost:8080/nosql-lab-mon/student_no=2025000001
```

Her endpoint ilgili veri kaynağından öğrenci kaydını doğrudan sorgulayarak JSON formatında sonuç döndürmektedir.

## Performans Testleri

Veri erişim performanslarını karşılaştırmak amacıyla **Siege** kullanılarak yük testleri gerçekleştirilmiştir.

Test senaryosunda:

* **1000 toplam HTTP isteği**
* **10 eş zamanlı istemci**
* İstemci başına **100 istek**
* JSON response kontrolü

uygulanarak Redis, Hazelcast ve MongoDB endpoint'leri karşılaştırılmıştır.

Ayrıca eş zamanlı istekler altında endpoint'lerin çalışma sürelerini ölçmek amacıyla `curl`, `xargs` ve Linux `time` komutları kullanılmıştır.

## Projede Kazanımlar

Bu proje kapsamında:

* NoSQL veri tabanlarının farklı veri modelleriyle çalışma prensipleri incelendi.
* Redis ve Hazelcast gibi bellek tabanlı veri teknolojileriyle çalışıldı.
* MongoDB ile doküman tabanlı veri erişimi gerçekleştirildi.
* Java uygulamalarında farklı veri tabanlarına bağlantı ve veri erişim katmanları oluşturuldu.
* REST API üzerinden NoSQL veri kaynaklarına erişim sağlandı.
* Yük testi ve performans ölçümü gerçekleştirildi.
* Farklı NoSQL çözümlerinin veri erişim performanslarının karşılaştırılması deneyimlendi.

## Proje

[GitHub Repository](https://github.com/fthozkctn/NoSQL-lab)
