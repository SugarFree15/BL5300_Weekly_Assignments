# Volcano Plot

ggplot(res)+
  geom_point(aes(x=log2FoldChange, y=-log10(padj), color=ifelse(log2FoldChange < 0, "blue", "red")))+
  scale_color_manual(values=c("red","blue"))

> This created a volcano plot with control points in blue and mutant ones in red using the fact that control fold changes are always positive.

# Box Plot of Highest Positive Fold Change Gene

plotCounts(dds=WA8, gene="Solyc09g089500.2.1", intgroup="dex", returnData=TRUE) %>%
  ggplot(aes(dex,count))+
  geom_boxplot(aes(fill=dex))+
  scale_y_log10()+
  ggtitle("Solyc09g089500.2.1")
  
> This creates a box plot of the gene as found by sorting my results via log2FoldChange with a y-axis in log10 scale for ease of interpretation.

# Box Plot of Highest Negative Fold Change Gene

plotCounts(dds=WA8, gene="Solyc11g028040.1.1", intgroup="dex", returnData=TRUE) %>%
  ggplot(aes(dex,count))+
  geom_boxplot(aes(fill=dex))+
  scale_y_log10()+
  ggtitle("Solyc11g028040.1.1")
  
> This creates a box plot of the gene as found by sorting my results via log2FoldChange with a y-axis in log10 scale for ease of interpretation.

# MA Plot

ggplot(res)+
  geom_point(aes(x=baseMean, y=log2FoldChange))+
  scale_x_log10()+
  ggtitle("WA9-MA")
  
> Creates the MA plot by pulling the needed columns from the res dataframe and scaling the x-axis by log10.
