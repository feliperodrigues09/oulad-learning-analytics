# Um panorama educacional da maior universidade do Reino Unido - Dataset OULAD.

**Python version** - 3.12
**Status** - Em Desenvolvimento (Fase 2)

## Principais Insights

(EM DESENVOLVIMENTO)

## Visão Geral

A Open University é uma universidade pública britânica que possui o maior número de alunos de graduação no Reino Unido. É a maior instituição acadêmica do Reino Unido (e uma das maiores da Europa), com dois milhões de alunos matriculados desde sua fundação em 1969. Como o próprio nome indica, a Open University é composta majoritariamente por alunos fora do campus (off-campus).

O dataset OULAD se apresenta como um caso de análise relevante, com a tabela de Estudantes retornando um número de 32.593 observações e muitas possibilidades de relações a serem observadas a partir do conjunto de sete tabelas diferentes. Também foi possível notar que é um caso com oportunidades de limpeza e tratamento de dados. É um cenário de múltiplas facetas que se aproxima de uma operação do mundo real e torna o caso interessante.

A intenção desta análise será tratar e analisar os dados, porém visando um retorno de inteligência para a operação. Logo, o outcome desejado é um conjunto de instruções para que a operação possa considerar melhorias futuras nos indicadores.

## Objetivos

- Realizar a limpeza e normalização dos dados;
- Promover a análise exploratória dos dados (EDA) da Open University;
- Gerar insights sobre a operação educativa da Open University;
- Propor ações de melhorias com base nos dados.

### Perguntas para a análise:

- Influência de fatores socioeconômico:

  1. Grupos com menor imd_band e menor highest_education apresentam taxas de reprovação superiores à média?;
  2. Grupos PcD's possuem taxas de evasão maiores do que a média?;
  3. Existe relação entre imd_band e o grupo de alunos que realiza novas tentativas de inscrição no curso reprovado (num_of_prev_attempts)?
- Quais cursos apresentam maior taxa de Distinction e quais os de maior taxa de evasão?
- No curso de maior evasão:

  1. é possível identificar o momento no semestre em que estes casos se concentram?;
  2. O comportamento se repete nos semestres seguintes?
- A amplitude de engajamento nos primeiros 30 dias — medida pelo número de recursos distintos acessados no VLE e pelo número de assessments submetidos — prediz Distinction ou evasão?
- Existe correlação entre o número de créditos cursados no semestre (studied_credits) e a performance do aluno (final_result)?

## Dataset

Este conjunto de dados pertence à Plataforma de Aprendizagem Online da Open University (também chamada de "Ambiente Virtual de Aprendizagem (VLE)"), que os alunos utilizam para acessar o conteúdo dos cursos, discussões em fóruns, envio de avaliações, consulta de notas, etc. O dataset consiste em 7 arquivos CSV e contemplam o universo de 7 cursos selecionados. Diferentes períodos letivos são indicados pelas letras "B" e "J" após o ano, representando o segundo e o primeiro semestre, respectivamente.
Abaixo estão as descrições de cada coluna para os 7 datasets que compõem o ecossistema **OULAD**.

#### **assessments.csv**

| Coluna                | Descrição                                                                                         |
| :-------------------- | :-------------------------------------------------------------------------------------------------- |
| `code_module`       | ID do curso (identificador).                                                                        |
| `code_presentation` | ID para turma, composto de ANO + PERÍODO (ex: "2013B" para Fevereiro, "2013J" para Julho).         |
| `id_assessment`     | ID da avaliação.                                                                                  |
| `assessment_type`   | Tipo de avaliação: Tutor Marked Assessment (TMA), Computer Marked Assessment (CMA) ou Final Exam. |
| `date`              | Data final para submissão (número de dias desde o início do curso).                              |
| `weight`            | Peso da avaliação em %. Exames geralmente valem 100%; já a soma das outras avaliações é 100%. |

#### **courses.csv**

| Coluna                         | Descrição                                                                                 |
| :----------------------------- | :------------------------------------------------------------------------------------------ |
| `code_module`                | ID do curso (identificador).                                                                |
| `code_presentation`          | ID para turma, composto de ANO + PERÍODO (ex: "2013B" para Fevereiro, "2013J" para Julho). |
| `module_presentation_length` | Duração do curso em dias.                                                                 |

#### **studentAssessment.csv**

| Coluna             | Descrição                                                                                            |
| :----------------- | :----------------------------------------------------------------------------------------------------- |
| `id_assessment`  | ID da avaliação.                                                                                     |
| `id_student`     | ID único do estudante.                                                                                |
| `date_submitted` | Data de submissão da avaliação (número de dias desde o início do curso).                          |
| `is_banked`      | Flag indicando se o resultado da avaliação foi transferido de um curso anterior.                     |
| `score`          | Nota do estudante nesta avaliação (0-100). Notas abaixo de 40 são consideradas Reprovação (Fail). |

#### **studentInfo.csv**

| Coluna                   | Descrição                                                                                                                         |
| :----------------------- | :---------------------------------------------------------------------------------------------------------------------------------- |
| `code_module`          | ID do curso (identificador).                                                                                                        |
| `code_presentation`    | ID para turma, composto de ANO + PERÍODO (ex: "2013B" para Fevereiro, "2013J" para Julho).                                         |
| `id_student`           | ID único do estudante.                                                                                                             |
| `gender`               | Gênero do estudante.                                                                                                               |
| `region`               | Região geográfica onde o estudante vivia durante o curso.                                                                         |
| `highest_education`    | Nível de escolaridade mais alto ao ingressar.                                                                                      |
| `imd_band`             | Índice de Privação Múltipla que categoriza a população em decis. É uma estatística oficial que mede a pobreza de uma área. |
| `age_band`             | Faixa etária do estudante.                                                                                                         |
| `num_of_prev_attempts` | Número de vezes que o estudante tentou este curso anteriormente.                                                                   |
| `studied_credits`      | Número total de créditos dos cursos que o estudante está cursando atualmente.                                                    |
| `disability`           | Indicação se o aluno está dentro do grupo PcD (pessoa com deficiência).                                                         |
| `final_result`         | Informação sobre o resultado final alcançado pelo aluno na turma inscrita.                                                       |

#### **studentRegistration.csv**

| Coluna                  | Descrição                                                                                 |
| :---------------------- | :------------------------------------------------------------------------------------------ |
| `code_module`         | ID do curso (identificador).                                                                |
| `code_presentation`   | ID para turma, composto de ANO + PERÍODO (ex: "2013B" para Fevereiro, "2013J" para Julho). |
| `id_student`          | ID único para o estudante.                                                                 |
| `date_registration`   | Data do registro do estudante no curso (relativo ao início do curso).                      |
| `date_unregistration` | Data do cancelamento do registro (evasão), relativa ao início do curso.                   |

#### **studentVle.csv**

| Coluna                | Descrição                                                                                 |
| :-------------------- | :------------------------------------------------------------------------------------------ |
| `code_module`       | ID do curso (identificador).                                                                |
| `code_presentation` | ID para turma, composto de ANO + PERÍODO (ex: "2013B" para Fevereiro, "2013J" para Julho). |
| `id_student`        | ID único para o estudante.                                                                 |
| `id_site`           | ID do material do VLE (Ambiente Virtual de Aprendizagem).                                   |
| `date`              | Data da interação do estudante com o material (número de dias desde o início).          |
| `sum_click`         | Número de vezes que o estudante interagiu com o material naquele dia.                      |

#### **vle.csv**

| Coluna                | Descrição                                                                                 |
| :-------------------- | :------------------------------------------------------------------------------------------ |
| `id_site`           | ID do material do VLE.                                                                      |
| `code_module`       | ID do curso (identificador).                                                                |
| `code_presentation` | ID para turma, composto de ANO + PERÍODO (ex: "2013B" para Fevereiro, "2013J" para Julho). |
| `activity_type`     | Tipo de atividade associada ao material do curso.                                           |
| `week_from`         | Semana a partir da qual o material está planejado para ser usado.                          |
| `week_to`           | Semana até a qual o material está planejado para ser usado.                               |

Agradecimentos:

- Kuzilek J., Hlosta M., Zdrahal Z. Open University Learning Analytics dataset Sci. Data 4:170171 doi: 10.1038/sdata.2017.171 (2017).
- Anil (https://www.kaggle.com/anlgrbz)

Dataset:
https://www.kaggle.com/datasets/anlgrbz/student-demographics-online-education-dataoulad/data

## Estrutura do Repositório

├── Dataset/
│   ├── csv/            # Raw Datasets & .gitkeep
│   └── parquet/        # Tabelas Gold exportadas (saída do pipeline)
├── Images/             # Schema OULAD
├── Notebooks/
│   └── ETL_OULAD.ipynb # Pipeline de dados (Bronze → Silver → Gold)
├── Presentation/       # Apresentação de Análise & .gitkeep
├── environment.yml     # Ambiente Conda para projeto
├── .gitignore          # Arquivos ignorados
└── README.md           # Este arquivo

##### Versionamento de Notebook

⚠️ Este projeto está em desenvolvimento ativo. Os notebooks estão versionados sem outputs (uso de nbstripout). A versão renderizada com gráficos e tabelas será publicada ao final da Fase 5. Para executar localmente, ver "Como Reproduzir".

## Análises Planejadas

## Como Reproduzir

1. **Clone o repositório:**

```bash
   git clone https://github.com/feliperodrigues09/oulad-learning-analytics.git
   cd oulad-learning-analytics
```

2. **Crie o ambiente a partir do arquivo YAML:**

```bash
   conda env create -f environment.yml
```

3. **Ative o ambiente:**

```bash
   conda activate portfolio_oulad
```

4. **Dados:** Baixe o dataset no [Kaggle](https://www.kaggle.com/datasets/anlgrbz/student-demographics-online-education-dataoulad/data) e extraia os CSVs na pasta `Dataset/csv/`.
5. **Execute o pipeline:**
   Abra e execute o `Notebooks/ETL_OULAD.ipynb` na ordem. As tabelas Gold serão exportadas automaticamente para `Dataset/parquet/`.

- [ ] Fase 1: Business Understanding
- [ ] Fase 2: Data Understanding
- [ ] Fase 3: Data Preparation
- [ ] Fase 4: EDA - Univariada, Bivariada, Multivariada
- [ ] Fase 5: Evaluation - Insights e Conclusões

## Tecnologias

- Python, Pandas, NumPy, Matplotlib, Seaborn, VS Code, Jupyter, nbstripout

## Autor

- Felipe Rodrigues
- LinkedIn: [[link](https://www.linkedin.com/in/felipe-rodrigues-a551864b/)]
- GitHub: [[link](https://github.com/feliperodrigues09)]

## Licença

- MIT License
- Como citar este projeto
