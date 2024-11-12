1. PCA
	1. take n number of features, pass it through PCA pipeline to get m < n final features (prinicipal components) where each $Variation_{PC_{i}}$ > $Variation_{PC_{i+1}}$
	2. hence the PC are ordered in term of variability of data explained by them
	3. that's why we are using PCA for dimensionality reduction
	4. the proportion of each feature added in each PC is called loading score.
	5. next PC is perpendicular every other PC before him
	6. the most difficult task is creating the $PC_{i}$
	7. the worst case for PC in dimensionality reduction would be when every PC variability is same, hence variation explained by each PC is identical so we wont be able to reduce the data.
	8. *Method for Selection of Principal Components*
		1. selection any n number of PCs
		2. selection of number of

|        | Mouse1 | Mouse 2 | Mouse 3 | Mouse 4 | Mouse 5 | Mouse 6 |
| ------ | ------ | ------- | ------- | ------- | ------- | ------- |
| Gene 1 | 10     | 11      | 8       | 3       | 2       | 1       |
| Gene2  | 6      | 4       | 5       | 3       | 2.8     | 1       |

