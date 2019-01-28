# Hierarchical Clustering
```
  #데이터 선언
  x1 = c(1, 2, 3, ...)
  x2 = c(2, 3, 4, ...)
  ...
  
  data = rbind(x1, x2, ...)
  
  #거리계산
  distance = dist(data, method="euclidean"....)
  
  #Hierarchical Clustering
  cluster = hclust(distance, method="complete"....)
  plot(cluster)
```
