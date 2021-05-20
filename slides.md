---
# try also 'default' to start simple
theme: default
# theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
---

# React NativeとExpoを<br>１ヶ月触ってみてわかったこと

ひじり（@hijiri408）

---

# 自己紹介

<br>
<br>

- **名前** - ひじり
- Javaでバックエンド開発を主にしています（していました）
  - 昨年からフロントエンドの開発もやってます
- 登壇は初ではないですが、LTは初です

---

# 今日話すこと

<br>

React経験者が初めてのアプリ開発にReact NativeとExpoを1ヶ月くらい使ってみて感じたこと

---


# React NativeとExpoに触れるきっかけ

<br>
<br>

- お仕事でアプリ開発をすることになり、React NativeとExpoを使うことになった
- そのときの自分の状態は↓
  - アプリ開発経験は**無し**
  - Reactの経験は1年（たまに触る）

---

# 1ヶ月でやったこと

<br>
<br>

- 会社の教材で学習する
- React NativeやExpo、ライブラリのチュートリアルをやる & ドキュメントを読む
- React Native Japanのハンズオンイベントに参加する
- トライ＆エラーの繰り返し

---
layout: center
class: text-center
---

# 1ヶ月間いろいろとやってみてわかったこと

---

# Reactでの開発経験をそのまま活かせる

<br>

**当たり前だけどやっぱり一番インパクトがある**

React Nativeでのコンポーネント開発にはReactの知識をそのまま活かせるため、楽に書くことができた。

新しいことばかりで考えることもかなり多かったため、ある程度知っているものの上で開発できるというのは、気持ち的にもかなり楽だった。

最初にアプリのコードを見た時は「あ、Reactだ」と思った。

```ts
export default function App() {
  return (
    <View style={styles.container}>
      <Text>Open up App.tsx to start working on your app!</Text>
      <StatusBar style="auto" />
    </View>
  );
}
```

---

# Reactで使っていたライブラリが使える（制限付き）

<br>

React QueryやFormikのようなReact用のライブラリを、React Nativeでも使うことができた。

ただ、ブラウザ依存の機能が使われていると使えなかったり、何かしらの制限はあったりする。<br>React Nativeで使えるかどうかは、ドキュメントに記載があったり誰かがIssueで聞いていたりする。

React Queryの場合だと以下のように「開発用ツールを除いてすぐに使える」 とドキュメントに記載があり、実際にまったく同じように使えたので、かなり助かった。

> React Query is designed to work out of the box with React Native, with an exception to the devtools, which are only supported with React DOM at this time.

Storybookなんかも使えるのかなと思って調べたりしたのだが、こちらは制限が多くてWebと同じようには使えなさそうだったので、踏み込むのはやめた。

---

# JavaScript(TypeScript)でライブラリのコードが読める

<br>

ライブラリについても、ネイティブのコンポーネントを使わない部分であればJavaScript（TypeScript）で書かれているため、気軽にコードを読むことができた。

おかげで、ライブラリのバージョンアップ時にバグを踏んだ時にもすぐに原因を特定できるときがあり、プルリクエストを送ったりもできた。<br>（このときはreact-native-elementsをバージョンアップしたら表示が崩れた）

---

# Expoを使うと実機で簡単に確認できる

<br>

アプリ開発中に実機で確認するのってどうやるんだろうと思っていたら、Expoを使って簡単に確認することができて、体験がとても良かった。

1. Expoで起動
2. 表示されたQRコードを実機で読む（端末にはExpo Goをインストールしておく）
3. Expo Goが起動されてJavaScriptなどをロードしてくれる
4. 動作確認ができる

（はじめて使ったときは思わず声が出た）

---

# Expoだと起動が速い（使わないと遅い）

<br>

自分の端末だとReact Native CLI（Expo無し）でiOS用にビルドすると30分くらいかかり、その間はマシンパワーが持っていかれて（ファンも全開）でほとんど作業できなくなってしまう。

一度起動するとFast Refreshでコード変更を即時反映してくれるが、たまにうまくいかなかったり、ライブラリをいろいろと試しているときは使えなかったりした。

それに比べると、Expoでの起動はかなり速く、検証時の効率がとてもよかった。

---

# Expoとライブラリのバージョン関係に気をつける

<br>

Expoではライブラリの最新バージョンに対応しているわけではないので、単純に最新版を入れると動かなくなったりもする。（実際にハマった）

Expoのinstallコマンドを使うことで、使用しているExpoのバージョンと互換性のあるバージョンをインストールすることができるので、こちらを使うと余計なトラブルを避けられる。

❌ ダメなときがある
```
npm install xxx
```

⭕️ こっちが確実
```
expo install xxx
```

ちなみに互換性がないバージョンを使っていると、Expo起動時に警告メッセージを出してくれる。

---

# エラーメッセージからの原因特定が難しい

<br>

動作確認中にエラーが発生するとエラーメッセージと該当箇所のコード情報（スタックトレース）が出力されるが、大体が自分で書いたコードではなく内部のコードとメッセージが表示されたりもして、読んでも何が原因なのかよく分からないことが多かった。

がんばって読むしかない。

---

# バージョンアップがつらい

<br>

ExpoのBere Workflowで開発していたが、Expoをバージョンアップしたら次から次へとエラーが発生して、めちゃくちゃつらかった。

Expoにはupgradeコマンドが用意されているがそれだけではうまく動かず、ググったりIssueを見ながらエラーを順番に解決していくことになった。（おかげでExpoの設定まわりについて理解は進んだが）

React Native自体もまだバージョンアップで破壊的変更が普通に発生するようなので、バージョンアップするときはある程度の覚悟が必要になりそう。

（バージョンアップがつらかったとき、色々なIssueで「バージョンアップしたら動かなくなった！」みたいなのが出てくるので、みんな大変なんだなぁと思うとちょっと気持ちが安らいだ）

---

# 日本語の情報はそれほど多くない（と感じた）

<br>

うまく動かないときやこういうのどう実現するんだろうと思って調べたりすると、解決の糸口になるのはリポジトリのIssueや海外の記事であることが多かった。

---
layout: center
class: text-center
---

# まとめ

---

# まとめ

<br>
<br>

- React経験者であれば、アプリ開発でReact Nativeはかなり魅力的な選択肢
- Expoは便利だったので、使えない理由が無いなら使った方がいい
- バージョンアップする時はがんばる

---
layout: center
class: text-center
---

# ご清聴ありがとうございました