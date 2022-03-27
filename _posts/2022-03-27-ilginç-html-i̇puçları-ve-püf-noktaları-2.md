---
layout: post
title: İlginç HTML İpuçları ve Püf Noktaları 2
author:
  name: Yiğit Adak
  link: https://github.com/ygtadk
date: 2022-03-27 12:18 +0300
categories: [Web]
tags: [html]
---

## Dosya İndirme Bağlantıları

Bir bağlantıya `download` niteliğini ekleyerek onu indirme bağlantısına dönüştürebilirsiniz. Böyle yapıldığında tarayıcılar bağlantıya gitmek yerine, kullanıcılardan dosyayı disklerine kaydetmelerini ister.

```html
<a href="/media/Da_Vinci_Vitruve_Luc_Viatour.jpg" download>
  Vitruvius Adamı
</a>
```

Ayrıca `download` niteliğine atadığınız değer, indireceğiniz dosyanın ismini belirlemenizi sağlar.

```html
<a href="/media/Da_Vinci_Vitruve_Luc_Viatour.jpg" download="vitruvian_adam.jpg">
  Vitruvius Adamı
</a>
```

<a href="/blogum/media/posts/2022-03-27-ilginç-html-i̇puçları-ve-püf-noktaları-2/Da_Vinci_Vitruve_Luc_Viatour.jpg" download>&#10145; Vitruvius Adamı</a>

> `download` niteliği sadece aynı kökenli ([same-origin](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)) bağlantılarda veya `blob:` ve `data:` şemalarında çalışır.
{: .prompt-warning }

## Düzenlenebilir İçerikler

HTML’de neredeyse her içeriği düzenlenebilir yapabiliriz. Tek yapmamız gereken `contenteditable` niteliğine `true` değerini vermek.

Aşağıda bir örnek verilmiştir.

```html
<div contenteditable="true">
  Bu düzenlenebilir bir metin.
</div>
```

<div contenteditable="true" spellcheck="false">
Bu düzenlenebilir bir metin. (Tıkla)
</div>

## Duyarlı (Responsive) Görseller

`picture` etiketi ile ekran boyutuna göre duyarlı görsel grubu oluşturabiliriz.

```html
<picture>
  <source media="(min-width:1200px)" srcset="https://upload.wikimedia.org/wikipedia/commons/thumb/6/62/Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg/837px-Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg">
  <source media="(min-width:992px)" srcset="https://upload.wikimedia.org/wikipedia/commons/thumb/6/62/Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg/628px-Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg">
  <source media="(min-width:768px)" srcset="https://upload.wikimedia.org/wikipedia/commons/thumb/6/62/Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg/392px-Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg">
  <source media="(max-width:767px)" srcset="https://upload.wikimedia.org/wikipedia/commons/thumb/6/62/Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg/196px-Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg">
  <img src="https://upload.wikimedia.org/wikipedia/commons/6/62/Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg" alt="Vincent van Gogh Otoportre" style="width:auto">
</picture>
```

<div style="border: 2px solid gray; border-radius: 5px; padding: 5px;">
<picture>
<source media="(min-width:1200px)" srcset="https://upload.wikimedia.org/wikipedia/commons/thumb/6/62/Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg/837px-Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg">
<source media="(min-width:992px)" srcset="https://upload.wikimedia.org/wikipedia/commons/thumb/6/62/Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg/628px-Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg">
<source media="(min-width:768px)" srcset="https://upload.wikimedia.org/wikipedia/commons/thumb/6/62/Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg/392px-Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg">
<source media="(max-width:767px)" srcset="https://upload.wikimedia.org/wikipedia/commons/thumb/6/62/Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg/196px-Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg">
<img src="https://upload.wikimedia.org/wikipedia/commons/6/62/Vincent_van_Gogh_-_Self-portrait_with_pipe_-_Google_Art_Project.jpg" alt="Vincent van Gogh Otoportre" style="width:auto">
</picture>
</div>
<br>

> Tarayıcınızın geliştirici araçlarını kullanarak bu resmin duyarlı olduğunu görebilirsiniz.
{: .prompt-note }

## Giriş Önerileri

`input` elementinde giriş önerileri sunmak için `datalist` elementi kullanabilirsiniz.

Yapılması gereken şey `input` elementine bir `list` niteliği yerleştirmek ve `list` niteliğinin değerini `datalist` için oluşturduğumuz `id` ile aynı yapmak. En iyisi örnek üzerinde göstermek

```html
<label for="araba">Arabanın markası ve modeli:</label>
<input list="arabalar" name="araba">
  <datalist id="arabalar">
    <option value="1985 Alpine A310 V6 Pack GT Boulogne">
    <option value="1986 Koenig-Specials Countach Turbo">
    <option value="2000 Spoon Civic Type-R">
    <option value="2004 Amuse S2000 GT1 Turbo">
    <option value="2005 TVR Sagaris">
    <option value="2002 Tofaş Doğan SLX 1.6 i.e.">
    <option value="198x Anadol A9 (Prototip)">
  </datalist>
```

<div>
<label for="araba">Arabanın markası ve modeli:</label>
<input list="arabalar" name="araba">
<datalist id="arabalar">
  <option value="1985 Alpine A310 V6 Pack GT Boulogne">
  <option value="1986 Koenig-Specials Countach Turbo">
  <option value="2000 Spoon Civic Type-R">
  <option value="2004 Amuse S2000 GT1 Turbo">
	<option value="2005 TVR Sagaris">
	<option value="2002 Tofaş Doğan SLX 1.6 i.e.">
</datalist>
</div>
