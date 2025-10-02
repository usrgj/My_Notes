---
tags: [Home]
title: log
created: '2025-09-19T07:37:21.186Z'
modified: '2025-09-19T11:57:51.962Z'
---

log

## 9.19
> 重新寻找开源的姿态识别项目无果，改为使用yolov8的pose模型对人体关节位置标定，判断关节位置来实现动作识别

### Idea
**挥手**
三个动作中只有挥手时手腕高于腕关节。故当手腕高于肩膀时，识别为挥手。
判断左腕与左肩或右腕与右肩
且一般正面挥手

**摔倒**

**躺下**
从侧面观察和正面观察的判断有很大不同，考虑到可以定点，先实现正面观察的识别
由于躺下时，收观察者下半身离相机可能较近，导致人在画面中占比仍较大；又人站里相机较远时可能占比本身较小，故使用多重判断
（下面中，鼻子改为两眼中间， 髋关节指两髋关节中间）
1. 计算鼻子到脚踝的距离，小于某值时可能为躺
2. 规定鼻子到髋关节与髋关节到脚踝的比例，判断是否站姿

### Question
1. 模型导出为onnx或tensorrt加速有什么优势?
2. 是否结合时序分析提高对动作的识别？
结合 时序分析（如 LSTM 或 MediaPipe 的姿势分类器）处理连续帧，实现复杂动作（如深蹲、跑步）：
```python
from collections import deque

# 存储最近N帧的关键点序列
pose_sequence = deque(maxlen=10)  

def classify_action(sequence):
    # 在此添加动作分类逻辑（例如：阈值判断或机器学习模型）
    pass

pose_sequence.append(keypoints)
if len(pose_sequence) == 10:
    action = classify_action(pose_sequence)
```
3. 假如人躺着时，头比脚靠近相机，可能会识别出wave
4. 如果人弯腰，可能会识别成躺？

### Todo
- [ ] 111
