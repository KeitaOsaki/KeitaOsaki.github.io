+++
title = 'デキレーレット'
date = 2026-03-26T00:00:00+09:00
draft = false
tags = ["Web開発", "React", "TypeScript", "Vite", "Tailwind CSS", "Cloudflare Pages"]
description = "結果をこっそり決めておけるルーレットと順番決め"
image = "/images/products/roulette.svg"
+++

## 概要

「ルーレットで決めたことにしたい」というシーンのためのツールです。
回す前に当てたい項目を指定しておくと、見た目はランダムに回りながら、結果は必ずその項目に止まります。
ランダムではなく、**ユーザの意図を結果として演出する**ことがこのサービスのコンセプトです。

ごはん何を食べるか決めるときに自分が食べたいもの100%選びたいという筆者の悪意がこのサービスを生み出しました。

人に画面を見せながら回す状況を前提にしているため、**仕込めることが画面上から一切分からない**設計にしてあります。
盤面も操作も普通のルーレットそのもので、当たりの指定は隠しジェスチャからのみ行えます。

項目を並べ替えて順番を決める「順番決め」ページも用意しています。こちらは先頭と末尾だけを伏せたまま決めておけます。

<div style="display:flex;flex-wrap:wrap;gap:1rem;max-width:640px;margin:1.5rem auto;">
  <figure style="flex:1 1 220px;margin:0;display:flex;flex-direction:column;">
    <img src="/images/products/deki-roulette.png" alt="デキレーレットのルーレット画面" style="width:100%;height:auto;border-radius:8px;display:block;" />
    <figcaption style="margin-top:auto;padding-top:.5rem;text-align:center;">ルーレット</figcaption>
  </figure>
  <figure style="flex:1 1 220px;margin:0;display:flex;flex-direction:column;">
    <img src="/images/products/deki-roulette-order.png" alt="デキレーレットの順番決め画面" style="width:100%;height:auto;border-radius:8px;display:block;" />
    <figcaption style="margin-top:auto;padding-top:.5rem;text-align:center;">順番決め</figcaption>
  </figure>
</div>

## リンク

- [デキレーレット](https://roulette.basekeita.com/)
- [順番決め](https://roulette.basekeita.com/order/)

## 使い方

### ふつうに使う

項目を追加して「スピン」を押すだけです。項目は 2 個から 24 個まで登録できます。
何も指定しなければ、結果は本当にランダムです。

### 結果を決めておきたいとき

項目を **0.6 秒ほど長押し**すると、その項目が次のスピンで選ばれます。もう一度長押しすると解除されます。
キーボードの場合は項目にフォーカスして Enter を押しっぱなしにします。単純なクリックやタップでは何も起きません。

順番決めでは、長押しするたびに 先頭 → 末尾 → 解除 と切り替わります。
先頭と末尾はそれぞれ 1 項目までで、指定した項目以外の並びは常にランダムです。

### 指定した印の見え方

指定中の印は、リストのカラードットが中抜きのリングに変わるだけです。しかもこの印は以下の条件でしか出ません。

- リストにポインタまたはフォーカスがある間
- 指定した直後の約 1.6 秒間

スピン中と結果表示中は必ず伏せられ、フッターの「使い方」もスピンを押した瞬間に自動的に閉じます。

## デザイン

暗い紫を地色にした、少し縁日っぽい雰囲気のダークテーマでまとめています。

| 要素 | 内容 |
|---|---|
| 配色 | ダークな紫のインク色 (`#17111F` 〜 `#7D6D96`) にアイボリーの文字 |
| アクセント | 操作を促す `flare` (`#FF4E63`)、結果とフォーカスリングの `gold` (`#FFC94A`) |
| スライス | 彩度と明度を揃えた 10 色。暗色ラベルとのコントラストを 4.5:1 以上に確保 |
| 書体 | 丸ゴシック系 (`ui-rounded` / Zen Maru Gothic / M PLUS Rounded 1c ほか) |
| 盤面 | SVG で描画し、回転は CSS `transform` のトランジション |

色・書体・アニメーションは Tailwind のテーマに集約し、値をコードに直接書かないようにしています。
当たりの指定にも専用色は使わず、スライス色をそのまま流用することで、印が目立たないようにしています。

`prefers-reduced-motion` が有効な環境では、回転も結果の 1 件ずつの表示も短縮されます。

## 使用技術

| カテゴリ | 技術 |
|---|---|
| フレームワーク | React 19 |
| 言語 | TypeScript 5.7 |
| ビルドツール | Vite 6 (MPA + プリレンダリング) |
| スタイリング | Tailwind CSS 3 |
| CI/CD | Cloudflare Pages (Connect to Git) |
| ホスティング | Cloudflare Pages |

## 主な機能

1. 項目の追加・削除（2〜24 個）と、円グラフ状のルーレットへの反映
2. スピンボタンでルーレットを回転し、結果を表示
3. 長押しで次のスピンの結果を指定（画面上に痕跡を残さない）
4. 順番決めページで項目をランダムに並べ替え、1 位から順に表示・テキストとしてコピー
5. 順番決めでは長押しで先頭・末尾を指定
6. 日本語 / 英語の言語別 URL（ルーレット `/` `/en/`、順番決め `/order/` `/en/order/`）
