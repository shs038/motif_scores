import numpy as np
import pandas as pd
from matplotlib import pyplot as plt
import seaborn as sns
import scipy
from scipy import stats
%matplotlib inline
#read file
motif_scores_df = pd.read_csv('/home/shs038/motif_scores/motif_scores_C57BL6J.tsv', sep='\t', index_col=0)
motif_scores_df=motif_scores_df.ix[:,2:-1]
#plot socre distribution
scores=motif_scores_df.values.flatten()
sns.distplot(scores)
plt.ylabel('Frequency')
plt.xlabel('scores')
plt.title('motifs_scores')
sns.distplot(scores[scores!=0])
plt.ylabel('Frequency')
plt.xlabel('scores')
plt.title('motifs_scores_nonezero')
#find max score of each motif and overall
max_for_each_motif=motif_scores_df.max(axis=0)
max_score=max_for_each_motif.max(axis=0)
max_id=max_for_each_motif.idxmax(axis=0)
#find min score of each motif and overall
min_for_each_motif=motif_scores_df.min(axis=0)
min_score=min_for_each_motif.min(axis=0)
min_id=min_for_each_motif.idxmin(axis=0)
#normalize by max
normalized_socre_df=motif_scores_df/max_for_each_motif
#remove negative value
normalized_socre_df[normalized_socre_df<0]=0
normalized_socre=normalized_socre_df.values.flatten()
#plot scores without zeros and negative
sns.distplot(normalized_socre[normalized_socre!=0])
plt.ylabel('Frequency')
plt.xlabel('scores')
plt.title('normalized_nonezero scores')
