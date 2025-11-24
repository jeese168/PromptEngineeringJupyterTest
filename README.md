# PromptEngineeringJupyterTest

建议配合个人面试笔记项目（interview_questions_jeese）中的大模型应用开发.md的提示词工程那一章节配合使用


# Qwen3 系列模型 - Colab 部署参考指南
## 模型规格与硬件需求对照表

| 模型名称 | 参数量 | 默认量化 | 模型大小 | 最低显存 | 推荐显存 | Colab GPU | 下载命令 | 适用场景 |
|---------|--------|---------|---------|---------|---------|-----------|----------|---------|
| **Qwen3-0.6B** | 0.6B | Q4_K_M | ~400MB | 2GB | 3GB | T4 ✅ | `ollama pull qwen3:0.6b` | 轻量级测试、学习入门 |
| **Qwen3-1.7B** | 1.7B | Q4_K_M | ~1.2GB | 3GB | 4GB | T4 ✅ | `ollama pull qwen3:1.7b` | 快速原型开发 |
| **Qwen3-4B** | 4B | Q4_K_M | ~2.5GB | 4GB | 6GB | T4 ✅ | `ollama pull qwen3:4b` | 日常对话、代码生成 |
| **Qwen3-8B** | 8B | Q4_K_M | ~5.2GB | 6GB | 8GB | T4 ✅ | `ollama pull qwen3:8b` | 通用推理、复杂对话 |
| **Qwen3-14B** | 14B | Q4_K_M | ~8.5GB | 10GB | 12GB | T4 ✅ | `ollama pull qwen3:14b` | 高质量推理 |
| **Qwen3-32B** | 32B | Q4_K_M | ~19GB | 20GB | 24GB | L4 ✅<br>A100-40GB ✅ | `ollama pull qwen3:32b` | 专业级应用 |
| **Qwen3-30B-A3B** | 30B (MoE) | Q4_K_M | ~18GB | 20GB | 24GB | L4 ✅<br>A100-40GB ✅ | `ollama pull qwen3:30b-a3b` | MoE架构、高效推理 |
| **Qwen3-235B-A22B** | 235B (MoE) | Q4_K_M | ~130GB | 140GB | 160GB | A100-80GB ✅<br>(双卡) | `ollama pull qwen3:235b` | 旗舰级性能 |

## 量化版本对比

| 量化类型 | 精度 | 大小(8B为例) | 质量损失 | 速度 | 推荐使用 |
|---------|------|-------------|---------|------|---------|
| **Q2_K** | 2-bit | ~3.0GB | 较高 | 最快 | 极限显存环境 |
| **Q3_K_M** | 3-bit | ~3.8GB | 中等 | 很快 | 平衡性能 |
| **Q4_0** | 4-bit | ~4.8GB | 较低 | 快 | 默认推荐 |
| **Q4_K_M** | 4-bit | ~5.2GB | 低 | 快 | **最佳平衡** ⭐ |
| **Q5_K_M** | 5-bit | ~6.0GB | 很低 | 中等 | 高质量需求 |
| **Q6_K** | 6-bit | ~7.0GB | 极低 | 较慢 | 接近原始精度 |
| **Q8_0** | 8-bit | ~8.5GB | 几乎无 | 慢 | 生产环境 |

### 量化版本切换示例
```bash
# 默认 Q4_K_M
ollama pull qwen3:8b

# 更高精度
ollama pull qwen3:8b-q8_0

# 更小体积
ollama pull qwen3:8b-q2_k
```

## Colab 环境配置建议

### T4 GPU (16GB VRAM)
**推荐模型**: Qwen3-0.6B / 1.7B / 4B / 8B / 14B
```python
# Colab 安装命令
!curl -fsSL https://ollama.com/install.sh | sh
!nohup ollama serve &
!sleep 3

# 下载并运行模型
!ollama pull qwen3:8b
!ollama run qwen3:8b "你好，请介绍一下自己"
```

**显存使用建议**:
- 8B 模型: 占用 ~6GB，推理速度流畅 ✅
- 14B 模型: 占用 ~11GB，接近上限但可用 ⚠️

---

### L4 GPU (24GB VRAM)
**推荐模型**: Qwen3-14B / 32B / 30B-A3B
```python
# 适合运行中大型模型
!ollama pull qwen3:32b
```

**显存使用建议**:
- 32B 模型: 占用 ~20GB，流畅运行 ✅
- 30B-A3B (MoE): 激活参数少，推理更快 ⭐

---

### A100-40GB GPU
**推荐模型**: Qwen3-32B / 30B-A3B (可尝试更高量化版本)
```python
# 可以用更高精度量化
!ollama pull qwen3:32b-q8_0
```

---

### A100-80GB GPU (或双卡配置)
**推荐模型**: Qwen3-235B-A22B
```python
# 旗舰模型
!ollama pull qwen3:235b
```

## 特殊版本说明

### Thinking 模式
Qwen3 支持**思维链推理模式**，适合复杂数学和逻辑问题：
```bash
# 启用 Thinking 模式
ollama run qwen3:8b
/set think

# 禁用 Thinking 模式（更快响应）
/set nothink
```

### Code 专用版本
针对代码任务优化：
```bash
ollama pull qwen3-coder:8b
ollama pull qwen3-coder:30b
```

### VL 多模态版本
支持图像理解：
```bash
ollama pull qwen3-vl:8b
ollama pull qwen3-vl:32b
```

## 性能对比参考

| 模型 | 数学推理 | 代码生成 | 多语言 | 推理速度 (T4) | 综合评分 |
|------|---------|---------|--------|--------------|---------|
| Qwen3-4B | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | ~40 tokens/s | 适合入门 |
| Qwen3-8B | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ~25 tokens/s | **最推荐** |
| Qwen3-14B | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ~15 tokens/s | 高质量 |
| Qwen3-32B | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ~8 tokens/s | 专业级 |

## 快速开始示例
```python
# 1. 安装 Ollama
!curl -fsSL https://ollama.com/install.sh | sh
!nohup ollama serve > ollama.log 2>&1 &
!sleep 5

# 2. 下载模型（根据 GPU 选择）
# T4 用户推荐
!ollama pull qwen3:8b

# L4/A100 用户推荐
# !ollama pull qwen3:32b

# 3. 测试运行
!ollama run qwen3:8b "写一个Python快速排序算法"
```

## 注意事项

⚠️ **重要提示**:
1. Ollama 默认使用 **Q4_K_M** 量化，已经是质量和速度的最佳平衡
2. Colab T4 免费版有**12小时运行限制**，注意保存进度
3. 模型首次下载需要时间，建议使用 Colab Pro 获得更快的下载速度
4. MoE 模型（如 30B-A3B）激活参数少，推理速度比同等大小的密集模型更快

## 为什么选择 Qwen3？

✅ **完全开源**: 所有规格都开放下载，不像其他模型只开源旗舰版  
✅ **丰富的小模型**: 从 0.6B 到 235B 全覆盖，适合学习和实验  
✅ **优秀的中文支持**: 中文表现业界领先  
✅ **活跃的社区**: 文档完善，问题解决快  
✅ **多模态支持**: 提供 VL 版本支持图像理解  

---

**推荐配置**: Colab T4 + Qwen3-8B (Q4_K_M) ⭐⭐⭐⭐⭐