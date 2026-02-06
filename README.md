# 📊 Dados com Python — Alura

Projeto educacional focado em **Análise de Dados com Python**, desenvolvido durante os cursos da Plataforma Alura. Este repositório documenta a exploração, limpeza e análise de um dataset de salários da indústria de tecnologia.

## 🎯 Sobre o Projeto

Este projeto busca demonstrar as principais técnicas de análise de dados em Python, incluindo:
- Carregamento e exploração inicial de dados
- Limpeza e transformação de dados
- Análise exploratória de dados (EDA)
- Tratamento de valores ausentes
- Renomeação e padronização de colunas
- Visualização e interpretação de resultados

**Dataset utilizado**: Salários de profissionais da área de tecnologia, contendo informações como cargo, nível de senioridade, tipo de contrato, localização e estrutura de trabalho.

## 📁 Estrutura do Projeto

```
Dados-com-python---Alura/
├── Alura-Dados com python.ipynb    # Notebook principal com toda análise
└── README.md                         # Este arquivo
```

## 💻 Principais Tecnologias

- **Python 3.x**
- **Pandas** - Manipulação e análise de dados
- **NumPy** - Operações numéricas
- **Jupyter Notebook** - Ambiente interativo para análise

## 📊 Dataset - Informações Principais

O dataset contém **133.349 registros** com as seguintes características:

### Colunas do Dataset

| Coluna        | Tipo   | Descrição |
|---------------|------  |-----------|
| `ano`         | Float  | Ano do registro (2020-2025) |
| `senioridade` | String | Nível profissional (Junior, Pleno, Senior, Executivo) |
| `contrato`    | String | Tipo de contrato (FT, CT, PT, FL) |
| `cargo`       | String | Título da posição (390 cargos únicos) |
| `salario`     | Int    | Salário em moeda local |
| `moeda`       | String | Moeda do salário (26 tipos diferentes) |
| `usd`         | Int    | Salário convertido para USD |
| `residencia`  | String | País de residência do funcionário |
| `remoto`      | String | Modalidade (Presencial, Híbrido, Remoto) |
| `empresa`     | String | Localização da empresa (95 países) |
| `porte_empresa` | String | Tamanho (Pequeno, Médio, Grande) |

## 📈 Principais Descobertas dos Dados

### Distribuição por Senioridade
- **Senior**: 77.241 registros (57,9%)
- **Pleno**: 40.465 registros (30,3%)
- **Junior**: 12.443 registros (9,3%)
- **Executivo**: 3.200 registros (2,4%)

### Distribuição por Tipo de Contrato
- **Tempo Integral (FT)**: 132.563 (99,4%)
- **Contrato Temporário (CT)**: 394 (0,3%)
- **Meio Período (PT)**: 376 (0,3%)
- **Freelancer (FL)**: 16 (0,01%)

### Distribuição por Modalidade de Trabalho
- **Presencial**: 105.312 (78,9%)
- **Remoto**: 27.718 (20,7%)
- **Híbrido**: 319 (0,2%)

### Distribuição por Porte de Empresa
- **Médio**: 129.561 (97,1%)
- **Grande**: 3.574 (2,7%)
- **Pequeno**: 214 (0,2%)

### Salários (em USD)
- **Média**: $157.617
- **Mediana**: $146.206
- **Mínimo**: $15.000
- **Máximo**: $800.000

## 🛠️ Como Cada Parte Foi Feita

### **Aula 1 - Análise de Dados com Pandas**

#### 1.1 Carregamento do Dataset
```python
import pandas as pd
df = pd.read_csv("https://raw.githubusercontent.com/guilhermeonrails/data-jobs/main/salaries.csv")
```
- Dados importados de um repositório GitHub público
- Formato: CSV com 133.349 linhas e 11 colunas

#### 1.2 Exploração Inicial
- `.head()` - Visualização das primeiras 5 linhas
- `.shape` - Dimensões do dataset (133.349 linhas × 11 colunas)
- `.info()` - Tipos de dados e informações de não-nulos
- `.describe()` - Estatísticas descritivas das colunas numéricas

#### 1.3 Análise de Frequências
Uso de `.value_counts()` para entender a distribuição:
```python
df['senioridade'].value_counts()  # Contagem por nível
df['contrato'].value_counts()     # Tipos de contrato
df['remoto'].value_counts()       # Modalidades de trabalho
df['porte_empresa'].value_counts() # Tamanho das empresas
```

#### 1.4 Renomeação de Colunas
As colunas originais foram traduzidas para português:
```python
df.columns = ['ano', 'senioridade', 'contrato', 'cargo', 'salario', 
              'moeda', 'usd', 'residencia', 'remoto', 'empresa', 'porte_empresa']
```

#### 1.5 Codificação e Transformação de Dados
Mapeamento de valores abreviados para descrições completas:

**Senioridade**:
- SE → Senior
- MI → Pleno
- EN → Junior
- EX → Executivo

**Tipo de Contrato**:
- FT → Tempo_Integral
- CT → Contrato_Temporario
- PT → Meio_Periodo
- FL → Freelancer

**Modalidade de Trabalho**:
- 0 → Presencial
- 50 → Híbrido
- 100 → Remoto

**Porte de Empresa**:
- M → Médio
- L → Grande
- S → Pequeno

### **Aula 2 - Preparação e Limpeza dos Dados**

#### 2.1 Verificação de Valores Ausentes
```python
df.isnull().sum()
df.isnull().any(axis=1)
```
- **10 valores ausentes** identificados na coluna `ano`
- Detectados em 10 linhas do dataset
- Cargos afetados: Product Manager, Engineer, Data Scientist, Software Engineer, Machine Learning Engineer, etc.

#### 2.2 Tratamento de Dados Faltantes
```python
df[df.isnull().any(axis=1)]
```
- Linhas com NaN identificadas e analisadas
- Decisão: Podem ser removidas ou imputadas dependendo da análise

#### 2.3 Verificação de Integridade
- Confirmação de que não há valores ausentes (NaN) nas demais colunas
- Todos os dados categóricos e numéricos foram validados

## 🚀 Como Executar

### Pré-requisitos
- Python 3.7 ou superior
- Jupyter Notebook
- pip (gerenciador de pacotes Python)

### Instalação

1. Clone o repositório:
```bash
git clone https://github.com/YamSantosGX/Dados-com-python---Alura.git
cd Dados-com-python---Alura
```

2. Crie um ambiente virtual (recomendado):
```bash
python -m venv venv
source venv/bin/activate  # No Windows: venv\Scripts\activate
```

3. Instale as dependências:
```bash
pip install pandas numpy jupyter matplotlib seaborn
```

4. Abra o Jupyter Notebook:
```bash
jupyter notebook
```

5. Abra o arquivo `Alura-Dados com python.ipynb` no navegador que abrir

## 📚 Conceitos Aprendidos

- ✅ Importação de dados com Pandas
- ✅ Exploração e inspeção de dados
- ✅ Renomeação de colunas
- ✅ Transformação e codificação de variáveis
- ✅ Detecção de valores ausentes (NaN)
- ✅ Análise descritiva e estatística
- ✅ Uso de `.value_counts()` para análise de frequências
- ✅ Mapeamento de valores com dicionários
- ✅ Visualização básica de distribuições

## 🔗 Links Úteis

- [Documentação Pandas](https://pandas.pydata.org/docs/)
- [Documentação NumPy](https://numpy.org/doc/)
- [Alura - Cursos de Python e Dados](https://www.alura.com.br/)
- [Dataset Original](https://github.com/guilhermeonrails/data-jobs)

## 📝 Notas Importantes

- O dataset original contém dados internacionais de salários em tecnologia
- Algumas análises podem estar sujeitas a desvios devido aos 10 valores ausentes na coluna `ano`
- Os salários variam significativamente por país, moeda e nível de experiência
- A maioria dos dados refere-se a profissionais Sênior em contratos de Tempo Integral
- Trabalho remoto está em crescimento, mas presencial ainda é predominante

## 🎓 Desenvolvido por

**Yam Santos** - [@YamSantosGX](https://github.com/YamSantosGX)

## 📄 Licença

Este projeto está sob licença MIT. Veja o arquivo LICENSE para mais detalhes.

---

**Última atualização**: Fevereiro de 2026
