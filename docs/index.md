---
layout: default
title: home
permalink: /
---

# AkaiKKR

- AkaiKKRはKorringa, Kohn, Rostoker[1, 2]によって提案された密度汎関数に
  基づくグリーン関数法であるKKR法を用いた第一原理計算ソフトウェアである。

- KKR法には不規則合金を扱うための手法であるCPA
  (コヒーレントポテンシャル近似、Coherent potential approximation)法[3]を
  自然に適用する事が可能であり、これらを組み合わせたKKR-CPA法[4]を
  用いる事で、他の第一原理計算ソフトウェアでは計算が大変な
  合金系、不純物系に関しても高速に計算を実行出来る。

## 機能について

- KKR-CPA法を用いた電子状態計算。SCF計算、状態密度、エネルギー分散を計算可能。

- 位置ごとに原子の割合を指定できる。合金系、空孔を含んだ系、不純物系の計算が可能となる。

- 相対論（スカラー相対論、スピン軌道相互作用）や磁性の取り扱い。

- 交換相関ポテンシャルはMorruzi-Janak-Williams[5]、von Barth-Hedin[6]、Vosko-Wilk-Nusair[7]、
  generalized gradient approximation 91[8]、Perdew-Burke-Ernzerhof[9]
  の中から選択する。

## 導入方法

- [Linuxでintelコンパイラを使う場合](./md/linux_intel.md)

- [Linuxでgfortranを使う場合](./md/linux_gfortran.md)

- [Macでintelコンパイラを使う場合](./md/mac_intel.md)

- [Macでgfortranを使う場合](./md/mac_gfortran.md)

- [WindowsのWSLを使う場合](./md/wsl.md)

## 使用方法

- [インプットの解説](./md/input.md)

- [アウトプットの解説](./md/output.md)

- [状態密度計算のチュートリアル](./md/tutorial_DOS.md)

- [cifファイルから作成したインプットの確認方法](./md/input_cif.md)

- [原子空孔を入れた計算](./md/input_vc.md)

## 拡張機能

拡張機能をご使用になりたい場合はアカデメイアまで[お問い合わせ](https://www.academeia15.co.jp/akaikkrform)下さい。

- [電気伝導度](./md_proprietary/conductivity.md)

- [磁気相互作用](./md_proprietary/jij.md)

- [有限温度におけるフォノン及びマグノンによる電子散乱](./md_proprietary/temperature.md)

- [FPKKR](./md_proprietary/fpkkr.md)

- [遮蔽KKR](./md_proprietary/screenedkkr.md)

## 参考資料（PDF）

- [KKR法（AkaiKKR講習会2022/11/17）](./pdf/AkaiKKR_RIST2022_8jpn.pdf)

- [KKRグリーン関数法（AkaiKKR講習会2022/11/17）](./pdf/beginner2022_5jpn.pdf)

- [KKR-Green関数法によるバンド計算（外部リンク）](http://kkr.issp.u-tokyo.ac.jp/jp/document/akaikkr_j.pdf)

- [Machikaneyama2000の使用に関するメモ（外部リンク）](http://kkr.issp.u-tokyo.ac.jp/jp/document/machikaneyama2000_memo.pdf)

- [Korringa-Kohn-Rostoker Method（外部リンク）](http://kkr.issp.u-tokyo.ac.jp/jp/document/kkrnote.pdf)

## 参考文献

[1] J. Korringa, Physica, **13** (1947) 3

[2] W. Kohn and N. Rostoker, Phys. Rev., **94** (1954) 1111

[3] P. Soven, Phys. Rev., **156** (1967) 809

[4] H. Ehrenreich and L. M. Schwartz, in Solid State Physics, Vol. 31, edited by H. Ehrenreich, F. Seitz, and D. Turnbull (Academic,  New York, 1976)

[5] V. L. Moruzzi, A. R. Williams, and J. F. Janak, Phys. Rev. B, **15** (1977) 2854 

[6] U. von Barth and L. Hedin, J. Phys. C: Solid State Phys., **5** (1972) 1629

[7] S. H. Vosko, L. Wilk and M. Nusair, Can. J. Phys., **58** (1980) 80

[8] J. P. Perdew, J. A. Chevary, S. H. Vosko, K. A. Jackson, M. R. Pederson, D. J. Singh, and C. Fiolhais,  Phys. Rev. B, **46** (1992) 6671

[9] J. P. Perdew, K. Burke, and M. Ernzerhof, Phys. Rev. Lett., **77** (1996) 3865

## リリース情報

- AkaiKKR最新版 2024/9/26リリース

- GPU(Nvidia)対応版 2024/9/26リリース

- [リリース履歴](./md/release_log.md)

## アカデメイアホームページ

- [AkaiKKRホームページ](https://www.academeia15.co.jp/akaikkr)

- [お問い合わせ](https://www.academeia15.co.jp/akaikkrform)