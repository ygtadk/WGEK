---
layout: post
title: İlginç HTML İpuçları ve Püf Noktaları 1
author:
  name: Yiğit Adak
  link: https://github.com/ygtadk
date: 2022-03-08 20:02 +0300
categories: [Web]
tags: [html]
---

## Yazdırılabilir İçerik Oluşturmak

Kullanıcıların web içeriğimizi nasıl tüketeceğini tahmin etmek bayağı zor. Kullanıcılar içeriği görmek ve tüketmek için çok farklı yollara farklı cihazlardan başvurabilmektedir. Bunlardan biri de kullanıcının içeriğimizi yazdırmasıdır.

Web sitemiz için bir yazdırılabilir stil kağıdı oluşturmak kullanıcı deneyimini olumlu şekilde etkileyebilir. Bu yöntemin günümüzde sık kullanıldığını pek sanmıyorum ancak web siteniz için yararlı olabileceği için bahsetmek istedim.

Buradaki önemli nokta web sitenizideki içeriğin asıl önemli bölümlerinin gerçek kağıda düzgün bir şekilde aktarıldığından emin olmaktır. 

Bunu, baskı için oluşturulmuş ayrı bir stil kağıdı sağlayarak ve onu HTML'ye ekleyerek veya stil kağıdımıza (yani CSS dosyamıza) bir `@media print` kuralı ekleyerek yapabiliriz.

Aşağıdaki örneklerde kullanımı gösterilmiştir.

```html
<!-- ayrı ayrı stil dosyaları olarak kullanımı -->
<link rel="stylesheet" href="style.css">
<link rel="stylesheet" href="print.css" media="print">
```

```css
/* tek stil dosyası içinde kullanımı */
@media print {
  body {
    font-size: 28px;
	 }
	@page {
    margin: 1cm;
  }
}
```

> Normalde `cm` `in` gibi mutlak ölçü birimlerini kullanmak mantıklı değildir, fakat baskı için oluşturulmuş stil kağıtlarında çok kullanışlı olabilir.
{: .prompt-note }

## Üstü Çizili Metinler

HTML üstü çizili metin tanımlamanın iki farklı yolunu sunar, `s` ve `del` öğeleri.

Bu öğeler gibi sadece görsel biçimlendirmeye yarayan HTML öğelerinin asıl kullanım nedeni sayfayı anlamlandırmaktır. Bildiğiniz gibi bu etiketlere anlamsal (semantic) etiketler diyoruz.

Peki `s` ile `del` arasındaki fark ne?

### `s` etiketi

Artık doğru olmayan veya alakasız olan içerikleri vurgulamak için `s` öğesini kullanılır. Aşağıda tipik bir örnek verilmiştir.

```html
<p><s>Fiyat: ₺ 199.99</s></p>
<p><strong>BUGÜNE ÖZEL TEKLİF: ₺ 159.99!</strong></p>
```
<div>
<p><s>Fiyat: ₺ 199.99</s></p>
<p><strong>BUGÜNE ÖZEL TEKLİF: ₺ 159.99!</strong></p>
</div>

> Bazı ekran okuyucuları `s` öğesini normal metin olarak duyurabilir, dikkatli kullanılmalıdır.
{: .prompt-warning }

### `del` etiketi

Belgeden kaldırılmış bir içeriği vurgulamak için `del` öğesi kullanılır. 

Düzenleme hakkında daha fazla bilgi vermek için `cite` niteliğini ve düzenlemenin tarihini (ve saatini) eklemek için `datetime` niteliğini kullanabilirsiniz.

```html
<p>
  En sevdiğim programlama dili <del datetime="2022-03-06T16:00:30">Pyhton</del> <ins datetime="2022-03-07T17:00:36">Python</ins> .
</p>
```

<div>
<p>
  En sevdiğim programlama dili <del datetime="2022-03-06T16:00:30">Pyhton</del> <ins datetime="2022-03-07T17:00:36">Python</ins> .
</p>
</div>

> `del` öğesi de ekran okuyucular için problem olabilmektedir, `s` öğesi gibi dikkatli kullanılmalıdır.
{: .prompt-warning }

> Her iki öğe de ekran okuyucuları için sorun teşkil edebildiği için veya istenilen sonucu vermediği için sahte öğeler (pseudo-elements) kullanılması tavsiye edilir.
{: .prompt-note }

## Yazım Denetimi Kontrolü

Giriş alanları, metin alanı ve düzenlenebilir içerik alanlarında yazım denetimini devre dışı bırakabilirsiniz. Aşağıda bir örnek verilmiştir.

```html
<label for="lbl">Etiket</label>
<textarea spellcheck="false" id="lbl">I looove coding.</textarea>
```

`spellcheck` niteliği için bir değer vermek zorundayız, `true` veya `false`.

Eğer nitelik yoksa, öğenin yazım hataları için kontrol edilip edilmeyeceğine tarayıcı karar verir.

### Örnekler

```html
<div>
  <label for="label1">Etiket</label>
  <input value="I looove coding." id="label1">
</div>

<div>
  <label for="label2">Etiket</label>
  <textarea id="label2">I looove coding.</textarea>
</div>

<div>
  <strong>Etiket:</strong>
  <div contenteditable>I looove coding.</div>
</div>
```

Aşağıdaki alanlardan birine tıklarsanız (bazı tarayıcılarda içeriğe tıklamanız veya bir şeyler yazmanız gerekebilir), "**looove**" kelimesinin doğru yazılmadığını belirten dalgalı, kesikli veya noktalı kırmızı bir çizgi görmelisiniz.

<div>
<div>
  <label for="label1">Etiket</label>
  <input value="I looove coding." id="label1">
</div>

<div>
  <label for="label2">Etiket</label>
  <textarea id="label2">I looove coding.</textarea>
</div>

<div>
  <strong>Etiket:</strong>
  <div contenteditable>I looove coding.</div>
</div>
</div>

> Sonuçlar tarayıcınıza ve varsayılan dilinize bağlı olarak farklılık gösterebilir. `spellcheck` niteliği yalnızca bir ipucu olarak kullanılır, tarayıcıların yazım hatalarını kontrol etmesi zorunlu değildir.
{: .prompt-note }

Şimdi `spellcheck` niteliğini `false` değeri ile kullanalım;

```html
<div>
  <label for="label1">Etiket</label>
  <input spellcheck="false" value="I looove coding." id="label1">
</div>

<div>
  <label for="label2">Etiket</label>
  <textarea spellcheck="false" id="label2">I looove coding.</textarea>
</div>

<div>
  <strong>Etiket:</strong>
  <div spellcheck="false" contenteditable>I looove coding.</div>
</div>
```

Aşağıdaki alanlarda bu sefer yazım denetiminin yapılmadığını göreceksiniz.

<div>
<div>
  <label for="label1">Etiket</label>
  <input spellcheck="false" value="I looove coding." id="label1">
</div>

<div>
  <label for="label2">Etiket</label>
  <textarea spellcheck="false" id="label2">I looove coding.</textarea>
</div>

<div>
  <strong>Etiket:</strong>
  <div spellcheck="false" contenteditable>I looove coding.</div>
</div>
</div>

> Örneklerin çalışma ihtimalini arttırmak için metinleri İngilizce yazdım.
{: .prompt-note }

## Sadece HTML ile Renk Seçici Oluşturmak

Sadece HTML kullanarak renk seçici oluşturabileceğinizi biliyor muydunuz?

`input` etiketimizin `type` niteliğine `color` değerini yerleştirirsek güzel bir renk seçici elde etmiş oluruz. Aşağıda bir örnek verilmiştir.

```html
<input type="color" id="renk-secici" value="#e66465">
<label for="renk-secici">Bir Renk Seç</label>
```

<div>
<input type="color" id="renk-secici" value="#e66465">
<label for="renk-secici">Bir Renk Seç</label>
</div>


