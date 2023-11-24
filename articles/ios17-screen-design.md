<!--
title: 【ios 17】画面デザインとユーザーインターフェースの変更点
tags: ios,ios17
id: 
private: false
-->

# 【ios 17】画面デザインとユーザーインターフェースの変更点

## モダンなデザインとアイコンのリフレッシュ
ios 17では、ユーザーインターフェースのデザインが大幅に変更され、よりモダンな印象を与えるデザインになりました。新しいアイコンは、よりフラットでシンプルなデザインになり、見た目が一新されています。また、従来のアプリケーションのアイコンもリフレッシュされ、よりアップデートされた印象を受けるようになりました。

### サンプルコード
```
class iconviewcontroller: uiviewcontroller {
    let iconimageview: uiimageview = {
        let imageview = uiimageview()
        imageview.image = uiimage(systemname: "square.and.arrow.up")
        imageview.tintcolor = .systemblue
        imageview.contentmode = .scaleaspectfit
        return imageview
    }()
    
    override func viewdidload() {
        super.viewdidload()
        
        view.addsubview(iconimageview)
        iconimageview.translatesautoresizingmaskintoconstraints = false
        
        nslayoutconstraint.activate([
            iconimageview.centerxanchor.constraint(equalto: view.centerxanchor),
            iconimageview.centeryanchor.constraint(equalto: view.centeryanchor),
            iconimageview.widthanchor.constraint(equaltoconstant: 100),
            iconimageview.heightanchor.constraint(equaltoconstant: 100)
        ])
    }
}
```


## 新しいウィジェットとホーム画面のカスタマイズ
ios 17では、新しいウィジェットが追加され、ホーム画面のカスタマイズがより充実しました。ウィジェットは、ホーム画面に追加して常に表示することができます。例えば、天気予報やカレンダーなどの情報を素早く確認することができます。また、ホーム画面のカスタマイズも容易になり、アプリのアイコンやウィジェットの配置を自由に変更することができます。

### サンプルコード
```
// ウィジェットの追加
let weatherwidget = weatherwidget(size: .large)
homescreen.addwidget(weatherwidget)

// ホーム画面のカスタマイズ
let appicon = appicon(image: uiimage(named: "app_icon"))
homescreen.setappicon(appicon)
```


## ダークモードの拡張とカラーテーマの選択肢
ダークモードは、ios 17においてさらに拡張され、より鮮明で快適な視認性を提供しています。ユーザーは、システムの設定に応じて自動的にダークモードを切り替えることができます。また、カラーテーマの選択肢も増え、ユーザーは自分の好みに合わせて色をカスタマイズすることができます。

### サンプルコード
```
// ダークモードの有効化
override func viewwillappear(_ animated: bool) {
    super.viewwillappear(animated)
    
    overrideuserinterfacestyle = .dark
}

// カラーテーマの選択
let themecolors = themecolors()
themecolors.primarycolor = .systemred
themecolors.secondarycolor = .systemblue
themecolors.backgroundcolor = .systemgray

thememanager.applycolors(themecolors)
```


## インタラクティブな通知と快適な操作性の向上
ios 17では、通知の扱いがよりインタラクティブになり、快適な操作性が向上しました。ユーザーは、通知をスワイプしてアクションを実行することができます。また、通知の種類に応じてプレビューや返信などの操作を行うこともできます。これにより、よりスムーズな作業フローが実現できるようになりました。

### サンプルコード
```
// インタラクティブな通知の設定
let content = unmutablenotificationcontent()
content.title = "新着メール"
content.body = "新しいメールが届きました。"

// 通知の追加
let request = unnotificationrequest(identifier: "new_mail_notification", content: content, trigger: nil)
notificationcenter.add(request) { (error) in
    if let error = error {
        print("failed to add notification request: \(error.localizeddescription)")
    }
}

// 通知のアクションの追加
let replyaction = untextinputnotificationaction(identifier: "reply", title: "返信", options: [])
let deleteaction = unnotificationaction(identifier: "delete", title: "削除", options: [.destructive])

let category = unnotificationcategory(identifier: "mail_notification_category", actions: [replyaction, deleteaction], intentidentifiers: [], options: [])
notificationcenter.setnotificationcategories([category])
```


## インテリジェントなナビゲーションとジェスチャー操作の追加
ios 17では、よりインテリジェントなナビゲーションが実現され、ジェスチャー操作が追加されました。例えば、特定のアプリを使用している際に、ホームボタンをダブルタップすると、最近使用したアプリの一覧が表示されます。また、ジェスチャー操作により、画面のスワイプやピンチイン・アウトなどの操作が容易になりました。

### サンプルコード
```
// ジェスチャー操作の追加
let swipegesturerecognizer = uiswipegesturerecognizer(target: self, action: #selector(handleswipegesture))
swipegesturerecognizer.direction = .right
view.addgesturerecognizer(swipegesturerecognizer)

let pinchgesturerecognizer = uipinchgesturerecognizer(target: self, action: #selector(handlepinchgesture))
view.addgesturerecognizer(pinchgesturerecognizer)

// ナビゲーションの設定
navigationcontroller?.interactivepopgesturerecognizer?.delegate = self

// ホームボタンのダブルタップ時の動作
@objc func handlehomebuttondoubletap() {
    let recentlyusedapps = appmanager.getrecentlyusedapps()
    // 最近使用したアプリの一覧を表示する処理
}

// スワイプジェスチャーの処理
@objc func handleswipegesture(gesturerecognizer: uiswipegesturerecognizer) {
    if gesturerecognizer.direction == .right {
        // 画面を右にスワイプしたときの処理
    }
}

// ピンチイン・アウトジェスチャーの処理
@objc func handlepinchgesture(gesturerecognizer: uipinchgesturerecognizer) {
    let scale = gesturerecognizer.scale
    // 画面をピンチイン・アウトしたときの処理
}
```


以上が、ios 17における画面デザインとユーザーインターフェースの変更点についての紹介でした。初心者のエンジニアの方でも理解しやすいように、各変更点に対してサンプルコードを用意しましたので、ぜひ参考にしてみてください。
より美しいデザイン、使いやすいインターフェースによって、ios 17はますます魅力的なバージョンとなっています。

　

## 【iOS 17】関連のまとめ
https://hack-note.com/summary/ios17-summary/

　

## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/

　

## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)

