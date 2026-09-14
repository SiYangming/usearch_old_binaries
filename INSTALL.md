# USEARCH 简介、安装与许可

## 简介

USEARCH 是一款功能强大的序列分析工具，由 Robert C. Edgar 开发。它提供了序列聚类、嵌合体检测、序列比对、OTU 挑选等多种功能，是 QIIME 1.x 中 OTU 聚类（uclust 方法）的核心引擎。

- 官网：`https://www.drive5.com/usearch/`

## 安装方式

- 官网下载二进制文件：需注册后下载
- QIIME 1.x 内置部分功能：通过 `pick_otus.py -m uclust` 调用 uclust 算法
- 直接取用本仓库内的旧版二进制：`bin/` 下文件名即版本与平台，例如 `bin/usearch8.1.1861_i86linux32`（对应 `usearch v8.1.1861_i86linux32`）

### 安装示例

```bash
# 将下载（或从本仓库 bin/ 取用）的 usearch 二进制复制到 ~/bin/ 目录
cp ~/software/usearch8.1.1861_i86linux32 ~/bin/usearch
chmod 755 ~/bin/usearch
```

> ⚠️ 注意：USEARCH 是商业软件，学术使用免费但需遵守许可协议。
> 本仓库内 v5–v11 的旧版**二进制**系由作者捐赠为公有领域（CC0-1.0，见 `LICENSE`），但**新版 USEARCH/USEARCH12 等**仍受 drive5 许可条款约束。

## UCHIME（嵌合体检测）

UCHIME 是一款用于检测核糖体 RNA 基因序列中嵌合体（chimera）的工具。嵌合体是 PCR 扩增过程中产生的人工产物，会导致 OTU 数量高估，因此在微生物组分析中必须进行嵌合体检测和去除。

- 官网：`https://www.drive5.com/usearch/manual/uchime_algo.html`

**安装方式**

- 作为 USEARCH 的一部分发布（推荐）：下载 USEARCH 后即可使用（本仓库 `bin/` 内 9/10/11 各版本提供 `-uchime_ref`、`-uchime_denovo`、`-uchime2_ref`、`-uchime3_denovo` 等子命令）
- QIIME 1.x 内置：通过 `parallel_identify_chimeric_seqs.py -m blast_fragments` 调用
- QIIME 2.x 内置：DADA2 和 Deblur 去噪过程中自动进行嵌合体检测

## 仓库内容

- `bin/`：usearch `5.2.32` → `11.0.667` 共 65 个可执行文件（linux / osx / win × 32/64 位）；各文件 MD5 见上游 `README.md` 清单（本仓库为 `rcedgar/usearch_old_binaries` 的 fork）
- Release `variant-usearch8.1.1861_i86linux32`：一份来源不明的**改动版**（基于 `bin/usearch8.1.1861_i86linux32`）——与 `bin/` 内原件同版本、同平台、同 BuildID（`b4e46286…`），差异为末尾被追加 1 字节 `0x0a` 且 `2203076–2203895` 区间 789 字节不同；仅供依赖该改动版的流水线取用，需要可校验的原件请用 `bin/usearch8.1.1861_i86linux32`（MD5 `1fc7b91bad6eba3518d719e74d018007`）

## 相关工具（QIIME 1.x 时代）

- 嵌合体检测：`ChimeraSlayer`（microbiomeutil，见 `SiYangming/microbiomeutil`）
- 双端拼接：`fastq-join`（ea-utils，见 `SiYangming/ea-utils` 的 `INSTALL.md`）
- 本仓库的 `usearch_old_binaries` 为旧版本留存；USEARCH 9/10/11 的 `-uchime*`、`-cluster_otus`、`-unoise3` 等子命令可替代部分 QIIME 1.x 流程中的 uclust/uchime
