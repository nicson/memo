# bootcampでwindows10をインストールまとめ

## 1. windows10を購入
エディションさえ間違えなければ、購入形態はdvdでもusbでもオンラインコードでも
なんでもよい。プロダクトキーさえ取得できればよい。

## 1. ISOイメージファイルを取得
MicrosoftのHPから手に入れるのが一番楽。
usb版のwindows10をdisk utilityを使ってisoを作成したら、なぜか
15GBもサイズアップしてしまい。usb16Gでは容量おーばになったorz

## キーボード設定

* Cmd <=> ctrl の設定
以下の内容を"mac_cmd_ctr_exchange.reg"で保存し、ダブルクリックすると
レジスタの内容を書き換えてくれる。

>Windows Registry Editor Version 5.00
>
>[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]
>"Scancode >Map"=hex:00,00,00,00,00,00,00,00,04,00,00,00,5b,e0,1d,00,1d,00,5b,e0,1d,e0,5c,e0,00,00,00,00

再起動後、commandとcontrolが交換される

 * Command + Space で日本語入力
 Commandとcontrolを交換したあとで、IMEを右クリック>プロパティ>詳細設定>編集操作_変更
 でcontrol + Space の入力/変換を　IME-オン/オフに設定
 
