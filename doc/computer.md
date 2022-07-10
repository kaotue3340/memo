```mermaid
flowchart TD
  A1["電源ボタンON"]-->B1
　subgraph UEFIフェーズ
  B1["UEFI起動"]-->
  B3{"POST(Power On Self Test)実行\nハードウェアが\n正常かどうか"} -->|Yes| C1[OK]
  B3 -->|No| B9[ビープ音を鳴らす] --> B9
  end
  subgraph ブートマネージャーフェーズ
  C1["ブートマネージャー(bootmgfw.efi)を検索\n起動優先順に物理ドライブを参照\n※一般的にはUSBメモリ→DVDドライブ→HDDorSSDの順"]-->
  C2["ブートマネージャー(bootmgfw.efi)起動"]-->
  C3["BCDファイルを参照\nブートローダーが保存されている物理ドライブを特定"]-->D1
  end
  subgraph カーネルフェーズ
  D1["ブートローダー(winload.efi)起動"]-->
  D2["カーネル起動"]--> 
  D3["サブシステムWindows起動"]-->
  D4["セッションマネージャー(smss.exe)起動"]
  D4-->DD1
  D4-->DD2
    direction TB
    subgraph セッション0
      DD1["セッション作成"]
      DD1-->DD1-1
      DD1-->DD1-2
      DD1-1["デバイス起動"]
      DD1-2["Windowsサービス起動"]
    end
    subgraph セッション1
      DD2["セッション作成"]-->
      DD2-1["ログオン準備処理"]--> 
      DD2-2["ログイン画面表示"]
    end
  end

```

## UEFI (Unified Extensible Firmware Interface)
* OSが起動する前にパソコンに搭載されているハードウェアを制御しOSを起動させるプログラム
* マザーボード上のUEFI専用のフラッシュメモリに格納されている
* UEFIで保存された情報は、メインメモリには保存されず、マザーボード上のUEFI専用のRAMに保存される（※ボタン電池で稼働している）
* BIOSとの違い：OSやハードウェアの技術進歩についていけなくなり進化したのがUEFI

## ブートマネージャー (bootmgfw.efi)
* UEFIから起動されるブートローダーを起動するためのプログラム

## ブートローダー (winload.efi)
* ブートマネージャーから起動されるカーネルを起動するためのプログラム

## BCDファイル (Boot Configuration Data ブート構成データ)
* ブートローダーを起動するために記載されている設定情報
* 例
```console
PS C:\WINDOWS\system32> bcdedit
Windows ブート マネージャー
--------------------------------
identifier              {bootmgr}
device                  partition=\Device\HarddiskVolume3
path                    \EFI\Microsoft\Boot\bootmgfw.efi
description             Windows Boot Manager
locale                  ja-JP
inherit                 {globalsettings}
default                 {current}
resumeobject            {********-****-****-****-***********}
displayorder            {current}
toolsdisplayorder       {memdiag}
timeout                 30
Windows ブート ローダー
--------------------------------
identifier              {current}
device                  partition=C:
path                    \WINDOWS\system32\winload.efi
description             Windows 10
locale                  ja-JP
inherit                 {bootloadersettings}
recoverysequence        {********-****-****-****-***********}
displaymessageoverride  Recovery
recoveryenabled         Yes
isolatedcontext         Yes
allowedinmemorysettings 0x15000075
osdevice                partition=C:
systemroot              \WINDOWS
resumeobject            {********-****-****-****-***********}
nx                      OptIn
bootmenupolicy          Standard
hypervisorlaunchtype    Auto
```

## カーネル
* OSのコア部分のプログラム
* ドライバからの命令を受けサブシステムへ命令を出す

## サブシステム
* ネットワークやハードウェアを操作するプログラム群

## セッションマネージャー (smss.exe)
* アプリケーションが動作するプロセス空間を分ける仕組み
  ※プロセス空間内ではアプリ間を跨いで同じメモリ空間を共有可能
* 元々は最初にログオンしたユーザもOS起動時のドライバやWindowsサービスも同一セッションで稼働していたが、
　WindowsVISTAから、より堅牢なセキュリティを考慮してセッションが分割された
※ プロセスエクスプローラーで確認可能
* 別ユーザがログオンすると新規セッションが作成される
