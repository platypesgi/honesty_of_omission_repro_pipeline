# consistency_reproducible_pipeline_1409b2f3

（模型文档的来源标注场景）空白的诚实性的分数该怎么读才不会被误用？用口径一致性比对标注它能说明什么、不能说明什么。

## 要回答的问题

- 子问题：空白的诚实性
- 提问角度：explainability
- 测量方式：口径一致性比对（指标字段 `consistency_rate`，单位 比例）
- 实验协议：可复现性 —— 记录输入指纹与顺序敏感性，核对重复测量是否一致
- 重点排查的失败模式：评测泄漏

## 快速开始

仅依赖 Python 标准库。

```bash
python consistency_reproducible_pipeline_1409b2f3.py --help
python consistency_reproducible_pipeline_1409b2f3.py --input sample.txt
python consistency_reproducible_pipeline_1409b2f3.py --input sample.txt --json
```

输入文件按行解析。协议「可复现性」使用分隔符 `|` 区分标签与载荷。

## 用法

| 参数 | 说明 | 默认值 |
| --- | --- | --- |
| `--input` | 输入文件路径 | 无（必填） |
| `--limit` | 只处理前 N 行 | 0 表示不限 |
| `--json` | 以 JSON 输出结果 | 关闭 |
| `--threshold` | 判定阈值 | 0 |
| `--budget` | 预算条数 | 50 |
| `--bins` | 分桶数量 | 10 |
| `--components` | 组件列表（逗号分隔） | 无 |

## 输出

```text
读取 1 个文件，共 3 条记录
处理完成，耗时 0.002s
```

## 判定规则

同一事实在不同表述间的一致率低于 95% 即判定口径不一致。

报告冲突事实对，便于定位分歧来源。

## 复现步骤

1. 按上面的分隔符准备输入文件，每行一条样本；
2. 运行 `python consistency_reproducible_pipeline_1409b2f3.py --input sample.txt --json`；
3. 记录运行环境、输入文件与完整输出；
4. **未运行的指标不要引用**：本仓库只提供测量方法与判定规则，
   不预填任何实测数字。填入实测值前请确认对应命令与输入一致。

## 适用与不适用

- 适用：需要可脚本化、可离线复核的「空白的诚实性」测量。
- 不适用：需要真实线上流量回放或分布式压测的场景。

## 与同类方案的区别

同类脚本通常只输出一个总数，无法回答「哪一段出的问题」。
这个实现把 consistency_rate 拆成可核对的分量，并明确给出判定规则与反例，
让人能追问结论是怎么来的，而不是接受一个无法追问来源的数字。

## 来源与参考

- Python 官方文档 argparse：<https://docs.python.org/3/library/argparse.html>
- Python 官方文档 statistics：<https://docs.python.org/3/library/statistics.html>
