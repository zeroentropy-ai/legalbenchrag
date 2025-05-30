# LegalBench-RAG

LegalBench-RAG is an information retrieval (IR) benchmark, whose purpose is to evaluate any retrieval system against complex legal contract understanding questions.
LegalBench-RAG allows the evaluator to deterministically compute precision and recall, even at the exact character level.

<div align="center">

[**ZeroEntropy**](https://www.zeroentropy.dev/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**Data**](https://www.dropbox.com/scl/fo/r7xfa5i3hdsbxex1w6amw/AID389Olvtm-ZLTKAPrw6k4?rlkey=5n8zrbk4c08lbit3iiexofmwg&st=0hu354cq&dl=0)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**Paper**](https://arxiv.org/abs/2408.10343)
</div>

# Download

To download the existing benchmark and corpus, please visit [this link](https://www.dropbox.com/scl/fo/r7xfa5i3hdsbxex1w6amw/AID389Olvtm-ZLTKAPrw6k4?rlkey=5n8zrbk4c08lbit3iiexofmwg&st=0hu354cq&dl=0). The data at that download link was generated using the code in this repository, usage details are below.

# Usage

1. Create a virtual environment

```bash
python3.12 -m venv .venv
source .venv/bin/activate
```

2. Install the dependencies

```bash
pip install pip-tools
pip-sync && pip install -e .
```

3. Create your credentials.toml and set your API keys

```bash
cp ./credentials/credentials.example.toml ./credentials/credentials.toml
vim ./credentials/credentials.toml
```

4. Download or Generate the dataset

You can download the data using the download link provided above. The directory structure from the root should have a `./data/corpus` folder and a `./data/benchmarks` folder. The corpus folder should be a set of raw text files, potentially with a directory hierarchy within itself. The benchmarks folder should be a set of benchmark json files. Each benchmark json has a set of test cases. Each test case has a query, and a ground truth array of snippets. Each snippet references a text file in the corpus via its file path within the corpus folder, and a character index range of that file.

If instead you would like to re-generate the benchmark from the source datasets, the entire code to do so is also provided in this repository. Please ensure you agree to the usage policies of ContractNLI, CUAD, MAUD, and PrivacyQA, before running this script. Once you have done that, simply execute the following:

```bash
python ./legalbenchrag/generate
```

Please note that LLMs are used in the process of creating the LegalBench-RAG benchmark. So, running this generate script will not generate exactly the same benchmark as was provided in the download link. However, the data in the download link itself was generated from the exact same process.


5. Run the benchmark script

```bash
python ./legalbenchrag/benchmark.py
```

# Citation

If you would like to use this work, please cite us!

```
@article{pipitone2024legalbenchrag,
  title={LegalBench-RAG: A Benchmark for Retrieval-Augmented Generation in the Legal Domain},
  author={Pipitone, Nicholas and Houir Alami, Ghita},
  journal={arXiv preprint arXiv:2408.10343},
  year={2024},
  url={https://arxiv.org/abs/2408.10343}
}
```

Additionally, here are citations for the datasets we use in this work:

```
@article{koreeda2021contractnli,
  title={ContractNLI: A dataset for document-level natural language inference for contracts},
  author={Koreeda, Yuta and Manning, Christopher D},
  journal={arXiv preprint arXiv:2110.01799},
  year={2021}
}
@article{hendrycks2021cuad,
  title={Cuad: An expert-annotated nlp dataset for legal contract review},
  author={Hendrycks, Dan and Burns, Collin and Chen, Anya and Ball, Spencer},
  journal={arXiv preprint arXiv:2103.06268},
  year={2021}
}
@article{wang2023maud,
  title={MAUD: An Expert-Annotated Legal NLP Dataset for Merger Agreement Understanding},
  author={Wang, Steven H and Scardigli, Antoine and Tang, Leonard and Chen, Wei and Levkin, Dimitry and Chen, Anya and Ball, Spencer and Woodside, Thomas and Zhang, Oliver and Hendrycks, Dan},
  journal={arXiv preprint arXiv:2301.00876},
  year={2023}
}
@inproceedings{ravichander-etal-2019-question,
    title = "Question Answering for Privacy Policies: Combining Computational and Legal Perspectives",
    author = "Ravichander, Abhilasha  and
      Black, Alan W  and
      Wilson, Shomir  and
      Norton, Thomas  and
      Sadeh, Norman",
    booktitle = "Proceedings of the 2019 Conference on Empirical Methods in Natural Language Processing and the 9th International Joint Conference on Natural Language Processing (EMNLP-IJCNLP)",
    month = nov,
    year = "2019",
    address = "Hong Kong, China",
    publisher = "Association for Computational Linguistics",
    url = "https://www.aclweb.org/anthology/D19-1500",
    doi = "10.18653/v1/D19-1500",
    pages = "4949--4959",
    abstract = "Privacy policies are long and complex documents that are difficult for users to read and understand. Yet, they have legal effects on how user data can be collected, managed and used. Ideally, we would like to empower users to inform themselves about the issues that matter to them, and enable them to selectively explore these issues. We present PrivacyQA, a corpus consisting of 1750 questions about the privacy policies of mobile applications, and over 3500 expert annotations of relevant answers. We observe that a strong neural baseline underperforms human performance by almost 0.3 F1 on PrivacyQA, suggesting considerable room for improvement for future systems. Further, we use this dataset to categorically identify challenges to question answerability, with domain-general implications for any question answering system. The PrivacyQA corpus offers a challenging corpus for question answering, with genuine real world utility.",
}
```
