# Projeto 2 — Árvores Binárias de Busca (BST) e AVL com dados do IBGE

Projeto acadêmico em Python para **construção, análise e comparação de desempenho** entre **Árvore Binária de Busca (BST)** e **Árvore AVL**, utilizando bases do **IBGE** com informações de **renda por bairros** e **setores censitários**.

O foco do estudo é mostrar, na prática, como a **ordem de inserção**, a **altura da árvore** e o **balanceamento** afetam a eficiência de **inserção** e **busca**, além de discutir como a escolha da **chave de ordenação** altera a utilidade da estrutura para diferentes tipos de consulta.

---

## Visão geral

Neste projeto, foram implementadas estruturas de dados do tipo **BST** e **AVL** para indexar registros do IBGE e avaliar:

- o impacto da **ordem de inserção** (`aleatória`, `crescente` e `decrescente`);
- a relação entre **altura da árvore** e custo de busca;
- a diferença prática entre uma árvore **não balanceada** e uma árvore **auto-balanceada**;
- a influência da **chave escolhida** na eficiência das consultas;
- a geração de **gráficos, tabelas, mapas e dashboard analítico em HTML**.

---

## Objetivos do projeto

- Implementar árvores **BST** e **AVL** em Python;
- Comparar desempenho estrutural e temporal entre as duas abordagens;
- Medir **altura**, **profundidade**, **comparações na busca** e **latência**;
- Avaliar o comportamento das árvores em diferentes cenários de inserção;
- Discutir a modelagem das árvores com **outras chaves**, como `CD_SETOR` e `COD_MUNI`;
- Produzir visualizações analíticas para interpretação dos resultados.

---

## Bases utilizadas

O notebook trabalha principalmente com duas bases:

### 1) Base de bairros
- **Arquivo:** `Agregados_por_bairros_renda_responsavel_BR.xlsx`
- **Total de registros:** **17.378**
- **Municípios representados:** **895**
- **Campos centrais:** `CD_BAIRRO`, `COD_MUNI`, `MUNICIPIO`, `UF`, `BAIRRO`, `RENDA_MEDIA`

### 2) Base de setores censitários
- **Arquivo:** `Agregados_por_setores_renda_responsavel_BR.xlsx`
- **Total de registros:** **449.531**
- **Municípios representados:** **5.570**
- **Campos centrais:** `CD_SETOR`, `COD_MUNI`, `RENDA_MEDIA`

### 3) Base geográfica
- **Shapefile:** `BR_Municipios_2024.shp`

> **Observação:** no notebook original, alguns caminhos estão configurados com diretórios locais do Windows. Para executar em outro ambiente, ajuste os paths conforme a sua máquina.

---

## Estruturas implementadas

O projeto implementa e analisa:

- **BST (Binary Search Tree / Árvore Binária de Busca)**
- **AVL (árvore auto-balanceada por rotações)**

Também foram construídas variações de modelagem para consultas por outras chaves:

- árvore de **setores censitários por `CD_SETOR`**;
- árvore de **municípios por `COD_MUNI`**, em que cada nó agrega os bairros pertencentes ao município.

---

## Metodologia

A comparação foi feita com base em três cenários de inserção:

- **Aleatória**
- **Crescente**
- **Decrescente**

Para cada cenário, foram avaliados indicadores como:

- número total de nós;
- altura final da árvore;
- altura ótima teórica;
- profundidade média;
- tempo de inserção;
- comparações médias na busca;
- latência média da busca;
- robustez estrutural da BST e da AVL.

Além disso, o notebook inclui:

- visualização da montagem das árvores;
- gráficos comparativos em Plotly;
- análise municipal;
- mapas temáticos;
- exportação de **dashboard analítico final em HTML**.

---

## Principais resultados

Os resultados do notebook mostram com bastante clareza o efeito do balanceamento na eficiência da estrutura.

### Altura final das árvores (17.378 nós)

| Ordem de inserção | BST | AVL |
|---|---:|---:|
| Aleatória | 32 | 17 |
| Crescente | 17.378 | 15 |
| Decrescente | 17.378 | 15 |

### Tempo de construção

| Ordem de inserção | BST (s) | AVL (s) |
|---|---:|---:|
| Aleatória | 0.0909 | 0.1295 |
| Crescente | 0.0089 | 0.1248 |
| Decrescente | 0.0076 | 0.1202 |

### Busca: comparações médias

| Ordem de inserção | BST | AVL |
|---|---:|---:|
| Aleatória | 19.64 | 14.63 |
| Crescente | 8558.49 | 13.09 |
| Decrescente | 8820.51 | 13.15 |

### Busca: latência média

| Ordem de inserção | BST (µs) | AVL (µs) |
|---|---:|---:|
| Aleatória | 6.77 | 4.46 |
| Crescente | 3621.68 | 7.30 |
| Decrescente | 3956.52 | 5.06 |

### Leitura crítica dos achados

- A **BST** pode ter custo de inserção menor no curto prazo, mas é **muito sensível à ordem de entrada**.
- Em inserções ordenadas, a BST se torna praticamente **linear**, com altura igual ao número de nós.
- A **AVL** mantém a altura próxima da ideal mesmo em cenários desfavoráveis.
- O ganho da AVL aparece com força principalmente na **busca**, que permanece estável e rápida.
- A **altura da árvore** explica boa parte do comportamento observado nos tempos experimentais.

---

## Discussão conceitual

Um ponto central do projeto é que a eficiência da árvore depende não apenas da estrutura (**BST ou AVL**), mas também da **chave escolhida para organizá-la**.

Em termos práticos:

- uma árvore organizada por **renda** é ótima para consultas sobre **faixas e comparações socioeconômicas**;
- essa mesma árvore **não é a melhor escolha** para buscar rapidamente um `COD_MUNI` ou um `CD_SETOR`;
- se o objetivo da busca muda, a **chave de ordenação também deve mudar**.

Por isso, o projeto também explora a reconstrução das árvores com:

- `CD_SETOR` como chave, para indexação cadastral por setor censitário;
- `COD_MUNI` como chave, para agregação e recuperação municipal.

---

## Tecnologias e bibliotecas

- **Python**
- **pandas**
- **numpy**
- **matplotlib**
- **plotly**
- **geopandas**
- **pathlib**
- **Jupyter Notebook**

---

## Estrutura sugerida do repositório

```bash
.
├── projeto_arvores_binarias_ibge_final_otimizado_compacto.ipynb
├── dashboard_arvores_ibge.html
├── data/
│   ├── Agregados_por_bairros_renda_responsavel_BR.xlsx
│   ├── Agregados_por_setores_renda_responsavel_BR.xlsx
│   └── BR_Municipios_2024/
├── imagens/
│   ├── grafico_alturas.png
│   ├── grafico_busca.png
│   └── mapa_ganho_avl.png
└── README.md
```

> Você pode adaptar essa estrutura para o seu repositório real. Se quiser, também vale criar pastas como `notebooks/`, `data/`, `outputs/` e `docs/`.

---

## Como executar

### 1. Clone o repositório
```bash
git clone <URL_DO_SEU_REPOSITORIO>
cd <NOME_DO_REPOSITORIO>
```

### 2. Crie um ambiente virtual
```bash
python -m venv .venv
```

### 3. Ative o ambiente

**Windows**
```bash
.venv\Scripts\activate
```

**Linux / macOS**
```bash
source .venv/bin/activate
```

### 4. Instale as dependências
```bash
pip install pandas numpy matplotlib plotly geopandas openpyxl jupyter
```

### 5. Abra o notebook
```bash
jupyter notebook
```

Depois, execute o arquivo:

```bash
projeto_arvores_binarias_ibge_final_otimizado_compacto.ipynb
```

---

## Saídas geradas

Ao longo da execução, o projeto pode gerar:

- tabelas analíticas de desempenho;
- gráficos comparativos entre BST e AVL;
- visualizações estruturais das árvores;
- mapas temáticos por município;
- **dashboard final em HTML**:
  - `dashboard_arvores_ibge.html`

---

## Conclusões

Os resultados mostram que a **AVL é estruturalmente mais robusta e mais estável para busca**, especialmente quando a ordem de inserção é desfavorável. Já a **BST**, embora simples e em alguns casos mais barata para construir, pode sofrer degradação severa e perder eficiência quando cresce sem balanceamento.

Além disso, o projeto reforça que a boa performance não depende apenas de escolher entre **BST** e **AVL**, mas também de definir uma **chave coerente com o tipo de consulta que se deseja realizar**.

---

## Possíveis melhorias futuras

- transformar as implementações em módulos `.py`;
- adicionar testes automatizados;
- separar a camada de visualização da camada de estrutura de dados;
- incluir métricas adicionais de memória;
- publicar o dashboard em GitHub Pages;
- criar uma versão com interface interativa para exploração dos resultados.

---

## Autor

**Mateus Pasquali**

Se este projeto te ajudou ou foi interessante, fique à vontade para deixar uma estrela no repositório.

---

## Licença

Este projeto pode ser disponibilizado sob a licença de sua preferência, como **MIT**.

> Caso queira, basta substituir esta seção pela licença oficial escolhida para o repositório.
