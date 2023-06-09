<!--
title:   チャートギャラリー　Visual Basic
tags:    Python,VisualStudio2017,chart,matplotlib,チャートギャラリー
id:      8923dcff96edbae96df4
private: false
-->
#チャートギャラリーから株価データを取得する。
チャートギャラリーは素晴らしい株価分析ツール。
でもちょっと独自の分析をpythonを使ってしたいといったときに自由度がないので、手軽に使えるようにCSVにデータを抽出する。

#チャートギャラリーからデータを取得する理由
株価データを探しているが中々ネットに転がってないので、有料だがデータが整っているチャートギャラリーからデータを取得する。

#チャートギャラリーからデータを抽出する方法
チャートギャラリーは**ActiveMarket.Prices**を利用してVBAなんかで簡単にデータアクセスできるようになっている。Microsoft製品なら何でもいいようだが、今回はexe化してタスクスケジューラーで自動実行させたいので、Visual Basicを利用する。
VisualStudio2019 communityでは対応していないみたいなので、**VisualStudio2017 community**で開発する。

##実際のコード
株価データを所定のフォルダに、証券コード毎のCSVファイルを作成している。

```vb
Module Module1

    'Dim csvPath As String = "D:\Users\****\source\repos\ConsoleApp2\stock_data\"
    Dim csvPath As String = "C:\Users\****\source\repos\chart_gallery\stock_data\"

    Sub Main()
        'makeZip()
        'Exit Sub

        'getCmdParam()

        Dim securitiesCodes() As Integer = {
            9101, 9104, 9107, 9984
        }

        Dim Prices As New ActiveMarket.Prices
        Dim Calendar As New ActiveMarket.Calendar
        Dim hash As New Hashtable
        Dim date_position As Integer
        Dim date_range As Integer
        Dim output As String
        Dim csvFile As String

        For securitiesCode = 0 To UBound(securitiesCodes)
            Prices.Read(securitiesCodes(securitiesCode))
            date_position = 7900
            date_range = Prices.End - date_position
            Dim stock_array(date_range, 7) As String

            For i = 0 To date_range - 1
                date_position = date_position + 1
                If Prices.IsClosed(date_position) Then
                    Continue For
                End If
                stock_array(i, 0) = Format(Calendar.Date(date_position), "yyyy-MM-dd")
                stock_array(i, 1) = Prices.Open(date_position)
                stock_array(i, 2) = Prices.High(date_position)
                stock_array(i, 3) = Prices.Low(date_position)
                stock_array(i, 4) = Prices.Close(date_position)
                stock_array(i, 5) = Math.Floor(Prices.Volume(date_position) * 1000)
                stock_array(i, 6) = Prices.Close(date_position)
            Next

            Try
            Catch ex As Exception
            End Try

            hash.Add(securitiesCodes(securitiesCode), Prices.Name)

            csvFile = csvPath + CType(securitiesCodes(securitiesCode), String) + "_2019.csv"

            'ファイル削除
            System.IO.File.Delete(csvFile)

            'csvヘッダー表示
            outputCsv(CType(securitiesCodes(securitiesCode), String) + " " + Prices.Name + ",,,,," + vbCrLf _
                    + """date"",""open"",""hight"",""low"",""close"",""power"",""End""", csvFile)

            For i = 0 To date_range
                If IsNothing(stock_array(i, 0)) Then
                    Continue For
                End If

                output = """" + stock_array(i, 0) + """,""" + stock_array(i, 1) + """,""" + stock_array(i, 2) + """,""" + stock_array(i, 3) _
                     + """,""" + stock_array(i, 4) + """,""" + stock_array(i, 5) + """,""" + stock_array(i, 6) + """"
                'System.Diagnostics.Debug.WriteLine(output)
                outputCsv(output, csvFile)
            Next
        Next

    End Sub

    Sub outputCsv(output, csvFile)
        Dim enc As System.Text.Encoding = System.Text.Encoding.GetEncoding("Shift_JIS") 'CSVファイルのエンコードを指定（今回はShift_JIS）
        Dim sr As New System.IO.StreamWriter(csvFile, True, enc) '書き込むファイルを開く
        sr.Write(output)
        sr.Write(vbCrLf) '改行
        sr.Close()
    End Sub

    Sub getCmdParam()
        Console.WriteLine(System.Environment.CommandLine) 'コマンドライン引数を表示する
        Dim cmds As String() = System.Environment.GetCommandLineArgs() 'コマンドライン引数を配列で取得する
        Dim cmd As String 'コマンドライン引数を列挙する
        For Each cmd In cmds
            Console.WriteLine(cmd)
        Next
    End Sub

    Sub makeZip()
        'ZIP書庫を作成
        System.IO.Compression.ZipFile.CreateFromDirectory("C:\temp\test\dir", "C:\temp\test\1.zip", System.IO.Compression.CompressionLevel.Optimal, False, System.Text.Encoding.GetEncoding("shift_jis"))
    End Sub

End Module
```

#まとめ
株価データをCSV化できたので、pythonで扱えるようになった。
matplotlibでグラフ化もできる。
独自の分析や、投資戦略の検証にも使えます。

## データサイエンティストスクール 無料部分あります
PythonやRなどのプログラミングを学ぶなら、
さらに統計分野を学習してデータサイエンティストを目指すのがおすすめ！

ディープラーニングやビックデータ分析などの高額システム案件の受注にも有利になります。

システム開発より、分析がやりたい方向けですが、下記載せておきます。

https://hack-note.com/programming-schools/#toc17
 
