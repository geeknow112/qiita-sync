<!--
title:   【ios 17】カメラと写真機能の進化
tags:    iOS,iOS17
id:      2e9e0819bba64ed115e5
private: false
-->


## 新たなカメラ機能と写真撮影のクオリティ向上

こんにちは。今回は、ios 17について初心者エンジニアに向けて、新たなカメラ機能と写真撮影のクオリティ向上についてご紹介します。

ios 17では、カメラ機能がさらに進化し、写真をより美しく鮮明に撮影することができるようになりました。これにより、ユーザーはより高品質な写真を撮影し、思い出をより美しく残すことができます。

具体的には、画質向上や低光環境での撮影の向上など、さまざまな機能が強化されています。カメラの起動が速くなり、被写体の動きによるブレやノイズを少なくすることができます。また、デュアルカメラ搭載の機種では、より広い範囲を撮影することができるようになりました。

以下に、新たなカメラ機能と写真撮影のクオリティ向上に関するサンプルコードを示します。

```swift
import uikit
import avfoundation

class cameraviewcontroller: uiviewcontroller, avcapturephotocapturedelegate {

    var capturesession: avcapturesession!
    var cameraoutput: avcapturephotooutput!
    var previewlayer: avcapturevideopreviewlayer!

    override func viewdidload() {
        super.viewdidload()

        capturesession = avcapturesession()
        cameraoutput = avcapturephotooutput()

        guard let device = avcapturedevice.default(for: .video) else { return }

        do {
            let input = try avcapturedeviceinput(device: device)

            if capturesession.canaddinput(input) && capturesession.canaddoutput(cameraoutput) {
                capturesession.addinput(input)
                capturesession.addoutput(cameraoutput)

                previewlayer = avcapturevideopreviewlayer(session: capturesession)
                previewlayer.frame = view.bounds
                previewlayer.videogravity = .resizeaspectfill
                view.layer.addsublayer(previewlayer)

                capturesession.startrunning()
            }
        } catch {
            print(error.localizeddescription)
        }
    }

    // ボタンが押された時のアクション
    @ibaction func capturebuttontapped(_ sender: uibutton) {
        let settings = avcapturephotosettings()
        cameraoutput.capturephoto(with: settings, delegate: self)
    }

    func photooutput(_ output: avcapturephotooutput, didfinishprocessingphoto photo: avcapturephoto, error: error?) {
        if let imagedata = photo.filedatarepresentation() {
            let image = uiimage(data: imagedata)
            // 撮影した写真の処理や表示などを行う
        }
    }
}
```

上記のコードは、カメラの起動や写真の撮影を行うために必要なコードです。avcapturesessionクラスを使ってカメラのセッションを作成し、avcapturephotooutputクラスを使って写真の出力を設定しています。

カメラの起動と写真の撮影は、capturebuttontappedメソッド内で行われています。avcapturephotosettingsを使って写真の設定を行い、capturephotoメソッドを呼び出すことによって写真の撮影が行われます。撮影が完了すると、photooutput(_:didfinishprocessingphoto:error:)メソッドが呼ばれ、撮影した写真のデータを取得することができます。

## プロフェッショナルな編集ツールと写真補正機能

ios 17では、プロフェッショナルな編集ツールと写真補正機能も進化しました。これにより、写真編集の幅が広がり、ユーザーはより美しい写真を作成することができます。

編集ツールの中でも特に注目すべきは、フィルターやエフェクトの追加が容易になった点です。例えば、写真に美しい背景を追加したり、カラーバランスや明度を調整したりすることができます。また、様々なエフェクトを追加することで、写真にアート的な雰囲気を演出することも可能です。

以下に、プロフェッショナルな編集ツールと写真補正機能に関するサンプルコードを示します。

```swift
import uikit
import coreimage

class photoeditviewcontroller: uiviewcontroller {

    @iboutlet weak var imageview: uiimageview!

    override func viewdidload() {
        super.viewdidload()

        // 編集前の写真を表示する
        let originalimage = uiimage(named: "original.jpg")
        imageview.image = originalimage
    }

    // ボタンが押された時のアクション
    @ibaction func editbuttontapped(_ sender: uibutton) {
        guard let originalimage = imageview.image else { return }

        let context = cicontext(options: nil)
        let ciimage = ciimage(image: originalimage)

        // エフェクトやフィルターの追加
        let filter = cifilter(name: "ciphotoeffectnoir")
        filter?.setvalue(ciimage, forkey: kciinputimagekey)
        let filteredimage = uiimage(ciimage: (filter?.outputimage)!)

        // 画像の明度調整
        let adjustedimage = filteredimage.adjustbrightness(value: 0.5)

        imageview.image = adjustedimage
    }
}

extension uiimage {
    func adjustbrightness(value: cgfloat) -> uiimage? {
        guard let ciimage = ciimage(image: self) else { return nil }
        let filter = cifilter(name: "cicolorcontrols")
        filter?.setvalue(ciimage, forkey: "inputimage")
        filter?.setvalue(value, forkey: "inputbrightness")
        let outputimage = filter?.outputimage
        let context = cicontext(options: nil)
        guard let cgimage = context.createcgimage(outputimage!, from: outputimage!.extent) else { return nil }
        return uiimage(cgimage: cgimage)
    }
}
```

上記のコードでは、写真の編集や補正を行うためのメソッドが追加されています。editbuttontappedメソッド内では、cifilterを使用してエフェクトやフィルターを追加し、写真の明度を調整しています。

また、uiimageの拡張機能として、adjustbrightnessメソッドが追加されています。このメソッドを使用することで、画像の明度を指定の値に調整することができます。上記のコードでは、inputbrightnessというキーに明度の値を設定しています。

## モード切替とフィルター効果の拡大

ios 17では、異なるモードやフィルターの切り替えが容易になり、ユーザーは様々なシーンに合った撮影設定を選ぶことができます。

ios標準のカメラアプリでは、モード切替やフィルターの選択がスムーズに行えるようになっています。たとえば、ポートレートモードでは、被写体をクリアに写し、背景をぼかすことができます。また、モノクロモードでは、写真をモノクロームに変換することができます。

以下に、モード切替とフィルター効果の拡大に関するサンプルコードを示します。

```swift
import uikit
import avfoundation

class cameraviewcontroller: uiviewcontroller, avcapturephotocapturedelegate {

    @iboutlet weak var cameramodebutton: uibutton!

    var capturesession: avcapturesession!
    var cameraoutput: avcapturephotooutput!
    var previewlayer: avcapturevideopreviewlayer!
    var currentmode: cameramode = .normal

    enum cameramode {
        case normal
        case portrait
        case monochrome
    }

    override func viewdidload() {
        super.viewdidload()

        capturesession = avcapturesession()
        cameraoutput = avcapturephotooutput()

        guard let device = avcapturedevice.default(for: .video) else { return }

        do {
            let input = try avcapturedeviceinput(device: device)

            if capturesession.canaddinput(input) && capturesession.canaddoutput(cameraoutput) {
                capturesession.addinput(input)
                capturesession.addoutput(cameraoutput)

                previewlayer = avcapturevideopreviewlayer(session: capturesession)
                previewlayer.frame = view.bounds
                previewlayer.videogravity = .resizeaspectfill
                view.layer.addsublayer(previewlayer)

                capturesession.startrunning()
            }
        } catch {
            print(error.localizeddescription)
        }
    }

    // ボタンが押された時のアクション
    @ibaction func cameramodebuttontapped(_ sender: uibutton) {
        switch currentmode {
        case .normal:
            cameramodebutton.setimage(uiimage(named: "portrait_icon"), for: .normal)
            currentmode = .portrait
        case .portrait:
            cameramodebutton.setimage(uiimage(named: "monochrome_icon"), for: .normal)
            currentmode = .monochrome
        case .monochrome:
            cameramodebutton.setimage(uiimage(named: "normal_icon"), for: .normal)
            currentmode = .normal
        }
    }

    @ibaction func capturebuttontapped(_ sender: uibutton) {
        let settings = avcapturephotosettings()

        switch currentmode {
        case .normal:
            break
        case .portrait:
            settings.isportraiteffectmattedeliveryenabled = true
        case .monochrome:
            let filter = cifilter(name: "cicolormonochrome")
            filter?.setvalue(1.0, forkey: kciinputintensitykey)
            settings.photofilters = [ciimage(image: uiimage(ciimage: (filter?.outputimage)!))!]
        }

        cameraoutput.capturephoto(with: settings, delegate: self)
    }

    func photooutput(_ output: avcapturephotooutput, didfinishprocessingphoto photo: avcapturephoto, error: error?) {
        if let imagedata = photo.filedatarepresentation() {
            let image = uiimage(data: imagedata)
            // 撮影した写真の処理や表示などを行う
        }
    }
}
```

上記のコードでは、カメラのモード切替やフィルター効果の追加が行われています。cameramodebuttontappedメソッド内では、currentmodeの値に応じてボタンの画像が切り替わり、capturebuttontappedメソッドでは、currentmodeに応じて撮影時の設定が行われます。

写真の撮影時には、avcapturephotosettingsクラスのisportraiteffectmattedeliveryenabledプロパティを使用してポートレートモードを有効にすることができます。また、monochromeモードでは、cifilterを使って写真をモノクロームに変換しています。

## ライブフォトとメモリー機能の魅力的な活用法

ios 17では、ライブフォトとメモリー機能がさらに進化し、より魅力的な写真活用が可能となりました。

ライブフォトは、写真を撮影する際に同時に動画も撮影する機能です。これにより、静止画だけでは捉えきれない瞬間や表情をより豊かに残すことができます。また、メモリー機能では、複数の写真や動画をまとめて、自動的に編集してくれる機能です。これにより、ユーザーは思い出の一時をより鮮明に保つことができます。

具体的な活用法としては、ライブフォトを使って人物の動きや笑顔を捉え、より自然な表情を残すことが挙げられます。また、メモリー機能を使って旅行やイベントの思い出をまとめることで、より鮮明な記憶と共に楽しい思い出を振り返ることができます。

以下に、ライブフォトとメモリー機能の魅力的な活用法に関するサンプルコードを示します。

```swift
import uikit
import photosui

class photoviewcontroller: uiviewcontroller, phpickerviewcontrollerdelegate {

    @iboutlet weak var livephotoview: phlivephotoview!

    override func viewdidload() {
        super.viewdidload()

        livephotoview.contentmode = .scaleaspectfit
    }

    // ボタンが押された時のアクション
    @ibaction func pickerbuttontapped(_ sender: uibutton) {
        var configuration = phpickerconfiguration()
        configuration.filter = .livephotos
        configuration.selectionlimit = 1

        let picker = phpickerviewcontroller(configuration: configuration)
        picker.delegate = self
        present(picker, animated: true, completion: nil)
    }

    // phpickerviewcontrollerdelegate

    func picker(_ picker: phpickerviewcontroller, didfinishpicking results: [phpickerresult]) {
        picker.dismiss(animated: true, completion: nil)

        guard !results.isempty else { return }

        let itemprovider = results.first!.itemprovider
        if itemprovider.canloadobject(ofclass: phlivephoto.self) {
            itemprovider.loadobject(ofclass: phlivephoto.self) { [weak self] (livephoto, error) in
                if let livephoto = livephoto as? phlivephoto {
                    dispatchqueue.main.async {
                        self?.livephotoview.livephoto = livephoto
                        self?.livephotoview.startplayback(with: .hint)
                    }
                }
            }
        }
    }
}
```

上記のコードでは、ライブフォトを表示するためのメソッドが追加されています。pickerbuttontappedメソッド内では、phpickerviewcontrollerを使用してライブフォトの選択を行い、didfinishpickingメソッド内でライブフォトの表示を行っています。

phpickerviewcontrollerdelegateのpicker(_:didfinishpicking:)メソッド内では、phlivephotoのインスタンスを取得し、そのデータをlivephotoviewに設定しています。また、ライブフォトの再生を開始するために、livephotoviewのstartplayback(with:)メソッドを呼び出しています。

## クラウドストレージと写真バックアップの最適化




## 【iOS 17】関連のまとめ
https://hack-note.com/summary/ios17-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
