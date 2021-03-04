# Instructions to evaluate a test collection

In order to evaluate the results obtained by an IR system on the REGIS test collection (or in any other IR test collection), you can use [trec_eval](https://trec.nist.gov/trec_eval/). TREC is the standard tool used by the TREC community for evaluating an ad hoc retrieval run and it calculates several retrieval quality metrics.

Trec_eval is a command line tool, which takes two inputs -- the results file and a file with the relevance assessments (commonly known as ?qrels? file).  The qrels file for REGIS is available here.

## Results file

The results file is the output of an information retrieval system such as Solr, Elastic Search, Anserini, Terrier, etc. It should be formatted as
`query-id Q0 document-id rank score run_id`
where

- `query-id`: Query num, from `queries.xml` file;
- `Q0`: Default value for all rows. Is currently ignored by trec_eval;
- `document-id`: Document identifier, which is also the file name;
- `rank`: Ranking order, starting in zero;
- `score`: Document score for the query;
- `run_id`: String of your choice to identify the run.

## Evaluating the results

The command to calculate the retrieval quality metrics is:

```
$ ./trec_eval [-q] [-m measure] [-l<num>] qrel_file results_file
```

- `-q`: In addition to summary evaluation, give an evaluation for each query;
- `-m <measure>`: Add 'measure' to the lists of measures to calculate and print. There can be multiple occurrences of the -m flag. '-m ndcg' is idicated to multi-relevance scale, '-m all_qrels' prints all qrels measures, '-m official' is the default, the main measures often used by TREC.
- `l<num>`: Used for multi-relevance scale. Num indicates the minimum relevance judgment value needed for a document to be called relevant;

## Main retrieval quality metrics

- `num_ret`: Total number of retrieved documents;
- `num_rel`: Total number of relevant documents;
- `num_rel_ret`: Total number of relevant documents retrieved;
- `map`: Mean average precision;
- `gm_map`: Average precision, geometric mean;
- `Rprec`: Precision of the first R documents, where R are the number of relevants;
- `bpref`: Binary preference
- `P_<K>`: Precision of the K first documents, where the predefined K is 5, 10, 15, 20, 30, 100, 200, 500, 1000;
- `ndcg`: Normalized discounted cumulative gain.

## REFERENCES

If you need more details, please refer to

- https://trec.nist.gov/trec_eval/
- https://www-nlpir.nist.gov/projects/trecvid/trecvid.tools/trec_eval_video/A.README
- http://www.rafaelglater.com/en/post/learn-how-to-use-trec_eval-to-evaluate-your-information-retrieval-system