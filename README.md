# =========================================
# Clinical Trial Phase Distribution
# Nature/SCI风格柱状图（光谱色阶版）
# 600 dpi TIFF输出
# =========================================

library(ggplot2)

# 数据
df <- data.frame(
  Phase = factor(
    c("I", "II", "III", "IV", "I/II", "II/III"),
    levels = c("I", "II", "III", "IV", "I/II", "II/III")
  ),
  Count = c(13, 26, 35, 37, 17, 3)
)

# 绘图
p <- ggplot(df, aes(x = Phase, y = Count, fill = Count)) +

  geom_col(
    width = 0.70,
    color = NA
  ) +

  geom_text(
    aes(label = Count),
    vjust = -0.5,
    size = 5,
    fontface = "bold"
  ) +

  # 光谱色阶
  scale_fill_gradientn(
    colours = c(
      "#5E4FA2",  # 紫
      "#3288BD",  # 蓝
      "#66C2A5",  # 青绿
      "#ABDDA4",  # 浅绿
      "#E6F598",  # 黄绿
      "#FEE08B",  # 浅黄
      "#FDAE61",  # 橙
      "#F46D43",  # 橙红
      "#D53E4F"   # 红
    ),
    guide = "none"
  ) +

  labs(
    x = "Clinical Phase",
    y = "Number of Studies"
  ) +

  expand_limits(y = max(df$Count) * 1.15) +

  theme_classic(base_size = 14) +

  theme(
    axis.title = element_text(
      face = "bold",
      size = 14
    ),
    axis.text = element_text(
      size = 12,
      color = "black"
    ),
    axis.line = element_line(
      linewidth = 0.8,
      color = "black"
    ),
    axis.ticks = element_line(
      linewidth = 0.8,
      color = "black"
    ),
    plot.margin = margin(15, 15, 15, 15)
  )

# 显示图形
print(p)

# 保存600 dpi TIFF
ggsave(
  filename = "Phase_Barplot_Spectrum.tiff",
  plot = p,
  width = 7,
  height = 5,
  units = "in",
  dpi = 600,
  compression = "lzw"
)
