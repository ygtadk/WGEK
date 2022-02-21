---
title: Snap, Flatpak ve AppImage
layout: post
author:
  name: Yiğit Adak
  link: https://github.com/ygtadk
date: 2022-02-21 13:55 +0300
categories: [Linux]
tags: [snap, flatpak, appimage]
image:
  src: /media/posts/2022-02-21-snap-flatpak-ve-appimage/kapak.png
---

## "Dağıtımdan Bağımsız" Paketler

Son birkaç yılda *dağıtımdan bağımsız* (veya *konteynerize* veya *evrensel* &#x1f937;) paket biçimleri iyice yaygınlaştı. Peki nedir bu *dağıtımdan bağımsız* paket yöneticileri?

Dağıtımdan bağımsız paket biçimleri, bildiğimiz paket biçimlerinden farklı olarak, uygulamayı tek bir paket olarak kurmak ve çalıştırmak için tüm bağımlılıklarla uygulamaları bir araya getirir.

Tabi bu çok avantajlı görünebilir, sonuçta aynı bağımlılığın farklı sürümlerini kullanmak isteyen iki uygulamanın olması gibi birçok farklı sorunlarla karşılaşmazsınız. Her ne kadar günümüz Linux ve açık kaynak yazılım geliştirme topluluğunun büyümesiyle böyle sorunlarla sık karşılaşmasakta güncellemeleri en hızlı şekilde sunan dağıtımlarda (bleeding-edge) böyle sorunlarla karşılaşabiliyoruz. Birde şuan aklıma geldiği gibi stabil ve sık güncellenmeyen dağıtımınızda uygulamaları güncel şekilde kullanabilmeniz için de çok iyi bir buluş. Fakat bu paket biçimlerinin ve çalışma mantıklarının da kendi dezavantajları var;

 - Bir geliştirici, kendi uygulamasını veya başkasının uygulamasını dağıtmak için dağıtımdan bağımsız paket biçimi kullandığında, bağımlılıkların en son güvenlik önlemleriyle güncel olmasını sağlamaktan tamamen sorumlu olur. Göz ardı edildiğinde, paket sistem için bir güvenlik tehdidi oluşturabilir. Geleneksel yazılım paketleri, dağıtımın geliştiricileri tarafından servis edilir ve bağımlılıkların en son güvenlik güncellemeleriyle güncellenmesini sağlar.

 - Bu paket formatları ile oluşturulmuş uygulamalar geleneksel paket formatları ile kurduğumuz uygulamalardan daha az performans sergileyebilir.

 - Bu *dağıtımdan bağımsız* paketlerin çalışma mantığı bazı açılardan sorun çıkarabilir. Örneğin sisteminize Firefox'u snap pakedi olarak kurarsanız, snap uygulamalarının kum havuzunda (güvenli sanal depolama) çalışması nedeni ile Firefox sisteminiz ile doğrudan iletişim kurma becerisine sahip olamaz. Bu yüzden Gnome kabuk uzantıları için oluşturulan eklenti gibi sistem ile iletişim kuran bir eklenti yüklediğinizde çalışmayacaktır.

## Snap

Snap, [Canonical](https://canonical.com/) tarafından geliştirilen ve ilk olarak 2014'te piyasaya sürülen dağıtımdan bağımsız paket formatı/yöneticisidir. Başlangıçta Ubuntu için geliştirilmiştir ancak Arch, Linux Mint, CentOS, Gentoo ve Fedora gibi diğer Linux dağıtımlara da resmi şekilde uyarlanmıştır.

Bu paket sisteminin geliştirmesinin arkasındaki asıl amaç, uygulamaların IoT, Ubuntu Core ve farklı Ubuntu versiyonlarını çalıştıran çeşitli cihazlarda çalışması için tek bir format bulmaktı. Snap kurulu uygulamaları sanal güvenli alanda (sand-box) çalıştırmaktadır. Bu sayede kurulu uygulamalar sisteme zarar verememektedir.

Snap için kullanılan resmi uygulama mağazası [Snapcraft](https://snapcraft.io/)'dır. Dağıtımdan bağımsız paket yöneticileri arasında en büyük uygulama havuzuna sahiptir.

> Snapcraft, bizzat Canonical ekibi tarafından kontrol edilmektedir.
{: .prompt-note }

## Flatpak

Flatpak da Linux sistemlerinde genel uygulama dağıtımını ve kullanımını basitleştirmeyi amaçlayan dağıtımdan bağımsız başka bir paket biçimidir. Tıpkı snap gibi flatpak ile kurulmuş uygulamar da sanal güvenli alanda çalışmaktadır.

Flatpak, 2015 yılında Red Hat, Endless Computers ve Collabora'nın desteği ile resmi olarak piyasaya çıkmıştır. Yaygın bir şekilde kullanılan bir çok dağıtım Flatpak tarafından desteklenmektedir.

Flatpak sisteminin kendisi C programla dilinde geliştirildi ve LGPL lisansı altında yayınlandı. Baş geliştirici, bir Red Hat çalışanı olan Alexander Larsson'dur.

Flatpak, Snap'ın aksine tek bir şirket tarafından yönetilen tek bir depoya sahip değildir. Flatpak birden fazla depo kullanımını destekler. Flatpak için kullanılan resmi uygulama mağazası [Flathub](https://flathub.org/home)'dır.

> Başlangıçta Flathub, web sitesinde yalnızca açık kaynaklı uygulamaların paylaşımına izin vermişti ancak yakın zamanda tescilli uygulamaların da paylaşılmasını onayladı.
{: .prompt-note }

## AppImage

AppImage, ilk olarak 2004 yılında "Kik" adıyla piyasaya sürülen bir başka yaygın dağıtımdan bağımsız paket formatıdır. 

Taşınabilir bir dosya formatıdır. "Bir uygulama = bir dosya" konseptine sahiptir. Bunun anlamı uygulama ve gerekliliklerinin tek bir dosyayada toplandığıdır. Windows işletim sistemlerindeki `.exe` dosya formatına benzemektedir. AppImage formatındaki dosyaları çalıştırmak çok kolaydır, yürütülebilirlik (`chmod +x`) izni verildikten sonra dosyaya çift tıklanması yeterlidir. Diğer iki paketleme sistemindeki gibi AppImage uygulamarı da sanal güvenli alanda çalışmaktadır.

AppImage paketlerini mağaza ortamında görebileceğiniz resmi bir site yoktur. Onun yerine [bu sitede](https://appimage.github.io/apps/) bu formatta paylaşılan uygulamalar listelenmiştir.

AppImage biçimindeki uygulamalar içlerinde güncelleme için gerekli bilgileri tutsalar da kendi başlarına güncellenebilecek bir yapıya sahip değillerdir. Sisteminizde AppImage uygulamalarını kullanıyorsanız aşağıdaki iki araç işinize yarayabilir;

- [AppImageUpdate](https://github.com/AppImage/AppImageUpdate)
- [AppImage Launcher](https://github.com/TheAssassin/AppImageLauncher)

## Farkları

Aşağıdaki tabloda üç paket sisteminin/biçiminin önemli özelliklerinin karşılaştırması bulunmaktadır.

|Özellikler |Snap |Flatpak | AppImage |
|:----------|-----|--------|---------:|
|GUI veya CLI üzerinden izin kontrolleri|Var|Var|Yok|
|Güvenli (korumalı) depolama desteği|Var|Var|Var|
|Güvenli (korumalı) depolama zorunluluğu|Var|Var|Yok|
|Uygulama taşınabilirliği|Hayır|Hayır|Evet|
|Yerel tema desteği|Var (kısmi)|Var (kısmi)|Var (kısmi)|
|Tek, yürütülebilir dosya formatı|Hayır|Hayır|Evet|
|Uygulama mağazası|Var|Var|Var sayılır|
|Farklı sürümlerde paralel uygulama desteği|Var|Var|Var|
|Otomatik güncellemeler|Var|Var|Var (3.parti uygulamalar ile)|
|Chrome OS desteği|Var|Var|Var|
|Uygulama boyutları|Yüksek|Yüksek|Diğer ikisi kadar yüksek değil|
|Uygulama sayısı|Yüksek|Snap kadar yüksek değil|Arada bir yerde|
|Masaüstü uygulama mağazaları için eklenti|Var|Var|Yok|

## Sonuç

Gördüğünüz üzere *dağıtımdan bağımsız* paket biçimlerinin avantajları olduğu gibi dezavantajları da var. Her ne kadar geleneksel paket biçimleri ve sistemleri ile boy ölçüşecek durumda olmasalar da, benim şahsi görüşüm, bu konteynerize veya evrensel veya veya dağıtımdan bağımsız diyebileceğimiz paket sistemleri ve biçimleri gelecekte çok önemli yerlere gelecek gibi duruyor. Özellikle bu teknolojiler Linux ekosisteminin geleceği için büyük önem arz ediyor gibi.

Aslında [Fedora Silverblue](https://getfedora.org/tr/silverblue/), [openSUSE MicroOS](https://microos.opensuse.org/) gibi yenilikçi dağımtımlar için bu bahsettiğimiz paket sistemleri çok önemlidir. Şahsen çok hızlı evrilen Linux ekosisteminde bulunmak heyecan verici, umarım ileride daha ilginç gelişmelerle karşılaşırız.
