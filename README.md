# 30nichi_os
## naskとNASMの違いについて
[ここ](http://hrb.osask.jp/wiki/?tools/nask)を参考

## day1

- やったこと
  - hello.imgを作成,qemuで実行
  - helloos.asmの作成,アセンブル
- アセンブラについて
    - DB命令
        - ファイルの内容を1byteだけ直接書く命令

## day2

- アセンブラについて
    - ORG命令
        - 機械語を実行した時に読み込み始めるメモリの場所を指定する命令
        - ORG 0x7c00で0x7c00地点から読み込み始める
    - JMP命令
        - JMP hoge で hoge と記述されている部分に飛ぶ
    - MOV命令
        - 代入の命令。MOV AX,0でAX=0;という代入文
    - ADD命令
        - ADD SI,1 ⇔ SI=SI+1;
    - CMP命令
        - CMP AL,0 ⇔ compare AL with 0
    - JE命令
        - CMP命令と合わせて使う
        - CMP AL,0 JE fin ⇔ if(AL==0){goto fin};
    - INT命令
        - ソフトウェア割り込みの命令(詳しく勉強するのはあとで)
- レジスタ
    - CPUにある記憶装置(16bit)
        - AX accumulator
        - CX counter
        - DX data
        - BX base
        - SP stack pointer
        - BP base pointer
        - SI source index
        - DI destination index
    - AXレジスタのうち、下位8bitをAL,上位8bitをAHという
        - CX,DX,BXも同様
        - SP,BP,SI,DIは8bitずつに分けられない
    - 32bitのレジスタはEAXなど頭文字にEがつく
    - セグメントレジスタ → 次回
    - entryやmsgなどのラベルはただの数字らしい
        - よく分からない(？)
- メモリ
    - CPU外部の記憶装置
    - MOV AX,[SI]などと書くとき[]はメモリの場所を指定している
    - MOV BYTE [678],123:メモリ678に数値123を覚えてもらう
        - BYTEだと8bit
        - MOV WORD [678],123 と書くと16bitで覚えてくれる
            - "データの大きさ [番地]"で指定
        - DWORDで4バイト(32bit)
    - MOV AL,[SI] = MOV AL,BYTE [SI]　(SIの番地にあるメモリの内容をALに読み込め)