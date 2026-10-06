---
title: "Acer Predator M.2 SSD 2TB"
---

![image](https://scrapbox.io/files/6ac397f903edf2395a418749.png)
- Acer Predator M.2 SSD 2TB GM7 NVMe2.0 2280 PCIe Gen4×4 超高速(最大読み取り：7400MB/s、最大書き込み：6500MB/s) 内蔵SSD 高耐久 3D NAND TLC PS5/PS5 Pro動作確認済み メーカー5年保証
- [Amazon](https://link.amazon/B0gkRQIsl)

2026-10-05
- AIちゃんが「これが欲しい〜」とねだって来たので買いましたw

2026-10-06
- もう届いた
- ![image](https://scrapbox.io/files/6ac50be703edf2395a462e1e.jpeg)
    - どこにつけるんだ？
- とClaude Codeに聞いたら図解してくれた、親切
    - ![image](https://scrapbox.io/files/6ac50d3203edf2395a46391c.png)
- ![image](https://scrapbox.io/files/6ac50bee03edf2395a462e2c.jpeg)
    - あー、ここか
    - 前にタワーPCにストレージを追加したのはSATAの時代のHDDだと思うので、こんなちっさい端子にメモリみたいなペラい板を刺して2TBあるというのは隔世の感があるな
    - 手先不器用だと装着できないw
- なんとか装着した
- Dドライブとして認識するようにした、あとはAIの仕事
:

```
増設SSD（Acer Predator GM7 2TB）を M2_2 に取り付け、D: としてNTFSでフォーマットした（2026-10-06、所有者作業）。
C:（1TB）が9/15・9/18・9/23に枯渇していた問題を解くための増設。以下を順に進めて、各段で結果を報告して。

1. 確認: D: の容量、CrystalDiskInfo か Get-PhysicalDisk 等で PCIe 4.0 x4 接続であること、C: の現在の空き。
2. C: の大口の現状を測る: AI\models、private、Docker の vhdx、WSL distro の vhdx、その他 50GB 超のもの。
3. 移設計画を提案（実行は私の OK 後）。方針:
   - Docker Desktop のディスクイメージは Settings → Resources → Disk image location で D: へ。
   - 大型 GGUF は、Windows 側から bind mount で読むと実効 ~46MB/s しか出ない（mnt-c-performance）。D: に置いた WSL の ext4 側へ入れる案を比較対象に含める。
   - 移した後は元を消す前に動作確認。削除は一覧を見せてから。
4. 終わったら galleria-wiki に file back（local-ai-machine-profile の SSD 行、local-ai-data-layout、log.d）。マニュアルは raw/2026-10-06-asrock-b850-tw-manual.pdf にある。先に ~/forest で pull すること。
```

- 比較実験の立案がきた
    - ![image](https://scrapbox.io/files/6ac50e7f03edf2395a46454a.png)
- 結果
    - ![image](https://scrapbox.io/files/6ac52a3903edf2395a46cdcc.png)

- 全部終わりました。C: の空きは 79.7GB → 414.5GB
- D: は総容量 1907.7GB のうち 347.6GB を使用、空き 1560.1GB です。

よーし、これで実験のたびにモデルを消したりしなくてよくなったぞ
