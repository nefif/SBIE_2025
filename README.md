# Suporte à Elaboração de Matrizes Curriculares com IA Generativa e Grafos

Este repositório contém os artefatos computacionais (dados, códigos e configurações) do artigo **"Suporte à Elaboração Matriz Curricular e Disciplinas com Inteligência Artificial Generativa e Grafos para Cursos de Graduação"**. O trabalho apresenta um método que integra Inteligência Artificial Generativa (IAGen) e Análise de Grafos para apoiar a criação, validação e organização de matrizes curriculares para cursos de graduação.

O objetivo é fornecer todos os elementos necessários para garantir a total reprodutibilidade dos resultados apresentados no estudo.

---

## Ambiente e Dependências

Para recriar o ambiente de execução e garantir a reprodutibilidade dos resultados, recomenda-se a criação de um ambiente virtual e a instalação das bibliotecas listadas no arquivo `requirements.txt`.

Execute o seguinte comando para instalar todas as dependências:

```bash
pip install -r requirements.txt
```

### Conteúdo do `requirements.txt`

```
pandas==2.2.2
scipy==1.14.0
scikit-learn==1.5.1
numpy==2.0.0
matplotlib==3.9.1
seaborn==0.13.2
requests==2.32.3
networkx==3.3
python-louvain==0.16
leidenalg==0.10.2
```

---

## Artefatos de Reproducibilidade

Esta seção detalha os principais artefatos utilizados para a execução do método, incluindo os prompts e os parâmetros dos modelos de IAGen.

### Prompts e Parâmetros

A seguir, são apresentados os prompts estruturados no método RTF (Role, Task, Format) e os parâmetros utilizados para interagir com os modelos de linguagem.

#### 1. Prompt para Extração de Keywords

- **Modelo:** deepseek-chat v3
- **Parâmetros:**
  - `stream=False`
  - `max_tokens=3000`
  - `temperature=0.0`

**Role (System):**

> Você é um especialista em educação que ajuda a extrair palavras-chave precisas e relevantes para disciplinas acadêmicas.

**Task & Format (Content):**

> Analise a ementa da disciplina e extraia as 10 principais palavras-chave que melhor representam o conteúdo da disciplina. As palavras-chave devem ser extraídas diretamente da ementa ou ser termos altamente relevantes para o conteúdo descrito. Evite palavras genéricas ou que não estejam diretamente relacionadas ao texto da ementa. Forneça as palavras-chave em formato de lista, separadas por vírgula, e todas em letras minúsculas.

**Exemplo de Estrutura:**

```
administracao, brasileiro, classicos, contexto, critica, cultura, estilo, global, organizacoes, pensamento
```

#### 2. Prompt para Criação de Novas Disciplinas

- **Modelo:** deepseek-chat v3
- **Parâmetros:**
  - `stream=False`
  - `max_tokens=300`
  - `temperature=0.5`

**Role:**

> Você é um especialista em educação e currículo acadêmico.

**Tasks & Formats:**

- **Para gerar o Nome:**
  - Analise as disciplinas a seguir e gere um novo nome de disciplina que represente uma fusão dessas áreas de conhecimento. Apenas retorne o nome da nova disciplina.
- **Para gerar a Ementa:**
  - Analise as ementas das disciplinas a seguir e crie uma nova ementa que englobe os principais tópicos. Apenas retorne a ementa no formato conciso e padronizado.
- **Para gerar as Keywords:**
  - Analise as palavras-chave das disciplinas abaixo e gere um novo conjunto de palavras-chave representando o conhecimento principal. Apenas retorne a lista de palavras-chave no mesmo formato.

#### 3. Prompt para Validar Aderência ao Documento de Referência

- **Modelo:** deepseek-chat v3
- **Parâmetros:**
  - `stream=False`
  - `max_tokens=100`
  - `temperature=0.0`

**Role:**

> Você é um coordenador de curso de graduação que precisa avaliar um documento de referência para determinar se determinada disciplina é alinhada ou não ao curso proposto no documento de referência.

**Task & Format (Content):**

> Para determinar a aderência seja direto. Se for aderente coloque **Sim**, porém se a disciplina não for aderente coloque apenas **Não**. Não justifique a resposta. Seja direto na resposta.

#### 4. Prompt para Selecionar a Lista Final de Disciplinas

- **Modelo:** deepseek-reasoner v1
- **Parâmetros:**
  - `stream=False`
  - `max_tokens=8000`
  - `temperature=0.0`

**Role:**

> Você é um coordenador de curso de graduação que precisa analisar uma lista de disciplinas e selecionar as 40 que mais se alinham com o documento de referência para criar um matriz curricular de um curso de graduação.

**Task & Format (Content):**

> Analise a lista de disciplinas extraídas e monte uma matriz acadêmica com as disciplinas que mais se alinham com o curso de graduação em Ciência de Dados apresentado no contexto do Documento Fornecido. Retorne as disciplinas mais coerentes com o contexto. A matriz curricular deverá ter 40 disciplinas, apenas 40 disciplinas, pois o curso terá 8 semestres e cada semestre terá 5 disciplinas para serem cursadas. Não selecione nenhuma disciplina de Trabalho de Conclusão de Curso ou Estágio. Retorne apenas a lista, sem justificativas ou formatações extras, e garanta que cada disciplina esteja em uma linha separada. Também garanta que não seja colocada na lista disciplinas repetidas ou muito semelhantes.

