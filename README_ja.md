[English](/README.md) | [ 简体中文](/README_zh-Hans.md) | [繁體中文](/README_zh-Hant.md) | [日本語](/README_ja.md) | [Deutsch](/README_de.md) | [한국어](/README_ko.md)

<div align=center>
<img src="/doc/image/logo.svg" width="400" height="150"/>
</div>

## LibDriver MAX31865

[![MISRA](https://img.shields.io/badge/misra-compliant-brightgreen.svg)](/misra/README.md) [![API](https://img.shields.io/badge/api-reference-blue.svg)](https://www.libdriver.com/docs/max31865/index.html) [![License](https://img.shields.io/badge/license-MIT-brightgreen.svg)](/LICENSE)

MAX31865は、白金測温抵抗体（RTD）用に最適化された使いやすい抵抗-デジタルコンバータです。 外部抵抗は使用されているRTDの感度を設定し、高精度のデルタシグマADCはRTD抵抗と基準抵抗の比をデジタル形式に変換します。 MAX31865の入力は、Q45Vまでの過電圧障害から保護されています。 RTDおよびケーブルのオープンおよびショート状態のプログラム可能な検出が含まれています。 MAX31865は、産業機器、機器、医療機器に使用されています。

LibDriver MAX31865は、LibDriverによって起動されたMAX31865の全機能ドライバーです。PT温度連続モード読み取り、PT温度シングルモード読み取りなどの機能を提供します。LibDriverはMISRAに準拠しています。

### 目次

  - [説明](#説明)
  - [インストール](#インストール)
  - [使用](#使用)
    - [example basic](#example-basic)
    - [example shot](#example-shot)
  - [ドキュメント](#ドキュメント)
  - [貢献](#貢献)
  - [著作権](#著作権)
  - [連絡して](#連絡して)

### 説明

/ srcディレクトリには、LibDriver MAX31865のソースファイルが含まれています。

/ interfaceディレクトリには、LibDriver MAX31865用のプラットフォームに依存しないSPIバステンプレートが含まれています。

/ testディレクトリには、チップの必要な機能を簡単にテストできるLibDriver MAX31865ドライバーテストプログラムが含まれています。

/ exampleディレクトリには、LibDriver MAX31865プログラミング例が含まれています。

/ docディレクトリには、LibDriver MAX31865オフラインドキュメントが含まれています。

/ datasheetディレクトリには、MAX31865データシートが含まれています。

/ projectディレクトリには、一般的に使用されるLinuxおよびマイクロコントローラー開発ボードのプロジェクトサンプルが含まれています。 すべてのプロジェクトは、デバッグ方法としてシェルスクリプトを使用しています。詳細については、各プロジェクトのREADME.mdを参照してください。

### インストール

/ interfaceディレクトリにあるプラットフォームに依存しないSPIバステンプレートを参照して、指定したプラットフォームのSPIバスドライバを完成させます。

/ srcディレクトリ、/ interfaceディレクトリ、および/exampleディレクトリをプロジェクトに追加します。

### 使用

#### example basic

```C
#include "driver_max31865_basic.h"

uint8_t res;
uint8_t i;
float temp;

res = max31865_basic_init(MAX31865_WIRE_4, MAX31865_RESISTOR_1000PT, 430.f);
if (res != 0)
{
    return 1;
}

...

for (i = 0; i < 3; i++)
{
    res = max31865_basic_read((float *)&temp);
    if (res != 0)
    {
        (void)max31865_basic_deinit();

        return 1;
    }
    max31865_interface_debug_print("max31865: temperature is %0.4fC.\n", temp);
    max31865_interface_delay_ms(1000);
    
    ...
    
}

...

(void)max31865_basic_deinit();

return 0;
```

#### example shot

```C
#include "driver_max31865_shot.h"

uint8_t res;
uint8_t i;
float temp;

res = max31865_shot_init(MAX31865_WIRE_4, MAX31865_RESISTOR_1000PT, 430.f);
if (res != 0)
{
    return 1;
}

...

for (i = 0; i < 3; i++)
{
    res = max31865_shot_read((float *)&temp);
    if (res != 0)
    {
        (void)max31865_shot_deinit();

        return 1;
    }
    max31865_interface_debug_print("max31865: temperature is %0.4fC.\n", temp);
    max31865_interface_delay_ms(1000);
    
    ...
    
}

...

(void)max31865_shot_deinit();

return 0;
```

### ドキュメント

オンラインドキュメント: [https://www.libdriver.com/docs/max31865/index.html](https://www.libdriver.com/docs/max31865/index.html)。

オフラインドキュメント: /doc/html/index.html。

### 貢献

CONTRIBUTING.mdを参照してください。

### 著作権

著作権（c）2015-今 LibDriver 全著作権所有

MITライセンス（MIT）

このソフトウェアおよび関連するドキュメントファイル（「ソフトウェア」）のコピーを取得した人は、無制限の使用、複製、変更、組み込み、公開、配布、サブライセンスを含む、ソフトウェアを処分する権利を制限なく付与されます。ソフトウェアのライセンスおよび/またはコピーの販売、および上記のようにソフトウェアが配布された人の権利のサブライセンスは、次の条件に従うものとします。

上記の著作権表示およびこの許可通知は、このソフトウェアのすべてのコピーまたは実体に含まれるものとします。

このソフトウェアは「現状有姿」で提供され、商品性、特定目的への適合性、および非侵害の保証を含むがこれらに限定されない、明示または黙示を問わず、いかなる種類の保証もありません。 いかなる場合も、作者または著作権所有者は、契約、不法行為、またはその他の方法で、本ソフトウェアおよび本ソフトウェアの使用またはその他の廃棄に起因または関連して、請求、損害、またはその他の責任を負わないものとします。

### 連絡して

お問い合わせくださいlishifenging@outlook.com。