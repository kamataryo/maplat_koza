# Maplat koza

## ファイル構成

```
.
├── LICENSE
├── README.md
├── apps               // アプリの定義ファイル
├── css
├── fonts
├── img                // POIで使われる画像
├── index.html
├── js
├── locales            // 言語ファイル
├── maps               // ジオリファレンス情報
├── package-lock.json
├── package.json
├── parts              // システム画像
├── rjs_config.js
├── tiles              // 地図画像のタイル化画像
└── tmbs               // 地図画像のサムネイル
```

## アプリの定義

Maplat では、複数の地図の集まりを「アプリ」として定義でき、サイト上で複数のアプ
リを使用することができます。 `./apps/{{ アプリ ID }}.json`という JSON ファイルを
追加するとアプリが作成されます。アプリはアプリ ID によって識別されます。以下はア
プリの定義の例です。

```json
{
  "app_name": "古座",
  "fake_gps": true,
  "fake_center": "古座",
  "fake_radius": 10,
  "home_position": [135.821305, 33.519444],
  "default_zoom": 17,
  "sources": [
    {
      "mapID": "koza",
      "label": "古座"
    },
    "gsi",
    "osm"
  ],
  "pois": [
    {
      "name": "第五福竜丸の地",
      "lat": 33.51486,
      "lng": 135.824681,
      "address": "和歌山県東牟婁郡串本町西向",
      "desc": "第五福竜丸の地です。",
      "image": "daigo_fukuryu_maru.jpg"
    },
    {
      "name": "古座川",
      "lat": 33.517383,
      "lng": 135.825283,
      "address": "東牟婁郡串本町古座",
      "url": "https://ja.m.wikipedia.org/wiki/%E5%8F%A4%E5%BA%A7%E5%B7%9D"
    }
  ]
}
```

定義したアプリは、 `https://{{ ホスト名 }}/?appid={{ アプリ ID }}` からアクセス
できます。 `sample.json` はデフォルト選択のアプリとして扱われ、appid パラメータ
なしでアクセスできます。

また、クリックすると吹き出しがでるポイントマーカー (POI) を `pois: object[]`プロ
パティとして定義できます。なお、 `poi.url`プロパティを指定すると、他のプロパティ
は表示されず、iframe 要素のみがポップアップします。

## ベースマップへのオーバーレイ

ブラウザからアクセスするときに、 クエリストリングスに `overlay=true` の値を追加
すると、地図を表示したときにベースマップの上に地図画像が表示されるようになります
。

http://example.com/

![no-overlay](https://user-images.githubusercontent.com/6292312/33160707-cd4722c6-d061-11e7-99ac-01146a7eb490.png)

http://example.com/?overlay=true

![overlay](https://user-images.githubusercontent.com/6292312/33160717-f036a93c-d061-11e7-9ea2-00ae46094830.png)
