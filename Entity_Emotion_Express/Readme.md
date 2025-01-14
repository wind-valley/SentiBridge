# 情感表达组合获取系统

## 系统文件
1. Build_Candidate_Set.py候选集合获取程序
2. Pair_Patt_Sort.py二部图排序算法
3. Pair_Refine.py, pair_mine_n.py, pair_mine_s.py 提炼算法
4. 一个CCF_data的测试数据文件夹
5. POS-tagging文本转word2vec文本, file2wc.py
6. word2vec模型训练脚本, word2vec.py

---

## 配置要求
1. python2.7
2. python-jieba分词包
3. python-gensim包
4. 训练好的word2vec模型文件

---

## 使用方法
- 构建候选集合

1. python Build_Candidate_Set.py --path ./CCF_data

- 排序

1. python Pair_Patt_Sort.py --path ./CCF_data

- 提炼
1. python pair_mine_n.py --read_path ./CCF_data/Iterative_record/pair_sort_ns/99 --split_point 0.1 --word2vec ./CCF_data/word2vec.model.txt --result_path ./CCF_data/pair_mine_n_result
2. python pair_mine_s.py --read_path ./CCF_data/Iterative_record/pair_sort_ns/99 --split_point 0.1 --word2vec ./CCF_data/word2vec.model.txt --result_path ./CCF_data/pair_mine_s_result
3. python Pair_Refine.py --n_path ./CCF_data/pair_mine_n_result --s_path ./CCF_data/pair_mine_s_result --sim 0.3 --result_path ./CCF_data/pair_mine_result

---

## 系统说明
1. 候选集合构建中间中文进行保存
2. 待处理文本重命名为data.ori
3. 词性标注后，data.ori.pos
4. 文本切片后，data.ori.pos.seg
   - 需要使用file2wc.py将data.ori.pos转为data.ori.pos.w2c文本用来训练word2vec模型
   - 将上一步骤得到的w2c文件，通过word2vec.py训练相应的模型文件
5. 最终得到，pair_ns, pair_pt两个文本，pair_ns只保留pair信息，pair_pt保留pair和patt的映射关系
6. 排序后，迭代结果保存至Iterative_record文件夹中，默认迭代100次，保留了每一轮的迭代结果。
7. 提炼后，结果为pair_ming_n_result, pair_mine_s_result和pair_mine_result三个文件。pair_mine_result是我们提炼的最终结果。

