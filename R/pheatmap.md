# Making Heatmap and Clustering

The pheatmap package can plot heatmaps and annotate clusterings.

## Clustering

Clustering can be done with the [hclust](hclust.md) package, and the cluster membership can be supplied to pheatmap as a data.frame. Multiple cluster memberships can be supplied.

Visualize the dendrograms with the *dendextend* package.

> [!code]
> my_clust <- hclust(dist(data_matrix))
> as.dendrogram(my_clust) %>% plot(horiz=TRUE)
> clust_df <- cutree(tree=as.dendrogram(my_clust),k=2) %>% data.frame(colname=factor(.)) %>% dplyr::select(!".")

To do clustering in the other direction, transpose the original matrix.

## Making heatmap

> [!code]
> heat <- pheatmap(data_vec,
>                  cutree_rows = 3,
>                  cutree_cols = 4,
>                  annotation_row = row_clust,
>                  annotation_col = col_clust,
>                  show_rownames = T,
>                  angle_col = 45,
>                  main = "Title")

- cutree_rows, cutree_columns: break rows and columns into sections and add gap in between;
- annotation_row, annotation_column: row and column cluster membership;
- angle_col: slant the row labeling to an angle;
- main: plot title.


[Source](https://davetang.org/muse/2018/05/15/making-a-heatmap-in-r-with-the-pheatmap-package/)