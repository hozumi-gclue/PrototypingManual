# プロジェクトの作成

## プロジェクトの作成

KeilのMenuから[Project]-[New uVision Project...]を選択。

![](../img/dev/nrf/install001.png)

nRF51822_xxACを選択。

![](../img/dev/nrf/install002.png)

CMSIS>CoreとDevice>Startupを選択。

![](../img/dev/nrf/install003.png)

## プロジェクトを整理する


![](../img/dev/nrf/install004.png)

Project Targetを"UART"、Groupsを"Sample1"にします。ここは、任意の名前でも問題ありません。

![](../img/dev/nrf/install005.png)

## main.c を作成

Sample1の付近で右クリックで、ショートカットメニューを表示し、[Add New Item to Group 'Sample1'を選択。

![](../img/dev/nrf/install006.png)

C File(.c)を選択し、Name:を"main"にて、main.cを作成。

![](../img/dev/nrf/install007.png)

main.c
```c
int main(){}
```

## Optionを設定

![](../img/dev/nrf/install008.png)

[Target]タブでは、Use MicroLIBにチェックをいれる。

| 項目 | 値 |
| -- | -- |
| Xtal | 16.0 |
| IROM1 Start | 0x18000 |
| IROM1 Size | 0x28000 |
| IRAM1 Start | 0x20002000 |
| IRAM1 Size | 0x6000 |

![](../img/dev/nrf/install009.png)

[Output]タブでは、Create HEX Fileにチェックマークをいれる。また、[Select Folder for Objects]を選択し、保存先フォルダ Outputディレクトリを新規作成し、Outputディレクトリを保存先にする。

![](../img/dev/nrf/nrf_uart009.png)

![](../img/dev/nrf/nrf_uart010.png)

[Output]タブでは、[Output]タブで作成したOutputディレクトリに保存先を設定する。

![](../img/dev/nrf/nrf_uart011.png)

![](../img/dev/nrf/nrf_uart012.png)

[C/C++]タブでは、DefineにNRF51を追記し、C99 Modeにチェックマークをいれる。

![](../img/dev/nrf/nrf_uart013.png)

[Asm]タブでは、DefineにNRF51を追記する。

![](../img/dev/nrf/nrf_uart014.png)

[Linker]タブでは、"Use Memory Layout from Target Dialog"にチェックマークをいれる。

![](../img/dev/nrf/nrf_uart015.png)

[Debug]タブでは、J-LINK/J-TRACE Cortexを選択し、[Settings]をクリックする。

![](../img/dev/nrf/nrf_uart016.png)

[Cortex JLink/JTrace Target Driver Setup]ダイアログが表示されるので、[Debug]タブで、Portを"SW"にし、[Scan]を選択する。J-LINK経由で、デバイスが認識されると、ARM CoreSight...の記述が表示される。

![](../img/dev/nrf/nrf_uart017.png)

[Flash Download]タブを選択し、"Reset and Run"にチェックマークをいれ、Sizeは0x2000にする。

![](../img/dev/nrf/nrf_uart018.png)


## Buildして転送

![](../img/dev/nrf/nrf_uart028.png)

![](../img/dev/nrf/nrf_uart029.png)