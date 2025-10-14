# Minicurso: Fundamentos de Python e IA Simbólica

## Material Didático para Nivelamento

---

## Módulo 1: Estruturas de Dados em Python

### 1.1 Listas

**O que são?** Coleções ordenadas e mutáveis (podem ser modificadas).

```python
# Criando listas
estados = ["AC", "AL", "AP", "AM", "BA"]
numeros = [1, 2, 3, 4, 5]

# Acessando elementos (índice começa em 0)
print(estados[0])   # AC (primeiro)
print(estados[-1])  # BA (último)

# Operações comuns
estados.append("CE")      # Adiciona no final
estados.remove("AL")      # Remove elemento
len(estados)              # Retorna quantidade
```

**Quando usar?** Para guardar sequências de dados que podem mudar.

---

### 1.2 Dicionários

**O que são?** Mapeamento de chaves para valores (como uma agenda).

```python
# Criando dicionário
pessoa = {
    "nome": "João",
    "idade": 25,
    "cidade": "São Paulo"
}

# Acessando valores
print(pessoa["nome"])        # João
print(pessoa.get("idade"))   # 25

# Adicionando/modificando
pessoa["profissao"] = "Engenheiro"
pessoa["idade"] = 26

# Verificando se existe
if "nome" in pessoa:
    print("Chave existe!")

# Iterando
for chave, valor in pessoa.items():
    print(f"{chave}: {valor}")
```

**Quando usar?** Para dados estruturados com identificadores únicos.

**Exemplo real no código:**
```python
# Base de conhecimento sobre doenças
doenca = {
    "nome": "Dengue",
    "sintomas": ["febre alta", "dor de cabeça"],
    "gravidade": "alta"
}
```

---

### 1.3 Sets (Conjuntos)

**O que são?** Coleções não-ordenadas de elementos únicos (sem duplicatas).

```python
# Criando sets
sintomas_paciente = {"febre", "dor de cabeça", "náusea"}
sintomas_dengue = {"febre", "dor de cabeça", "dor muscular"}

# Adicionando (não adiciona duplicatas)
sintomas_paciente.add("cansaço")
sintomas_paciente.add("febre")  # Não faz nada (já existe)

# OPERAÇÕES DE CONJUNTO
# Interseção: elementos em AMBOS
em_comum = sintomas_paciente & sintomas_dengue
# Resultado: {'febre', 'dor de cabeça'}

# União: TODOS os elementos
todos = sintomas_paciente | sintomas_dengue

# Diferença: só no primeiro
so_paciente = sintomas_paciente - sintomas_dengue

# Verificando tamanho
len(sintomas_paciente)
```

**Quando usar?** Para eliminar duplicatas e fazer operações matemáticas de conjuntos.

---

### 1.4 Tuplas

**O que são?** Como listas, mas IMUTÁVEIS (não podem ser modificadas).

```python
# Criando tuplas
fronteira = ("AC", "AM")
coordenadas = (10.5, 20.3)

# Acessando
print(fronteira[0])  # AC

# ERRO: Não pode modificar!
# fronteira[0] = "RO"  # Gera TypeError

# Desempacotamento
estado1, estado2 = fronteira
print(f"{estado1} faz fronteira com {estado2}")

# Lista de tuplas (comum)
fronteiras = [
    ("AC", "AM"),
    ("AC", "RO"),
    ("AL", "PE")
]

for e1, e2 in fronteiras:
    print(f"{e1} <-> {e2}")
```

**Quando usar?** Para dados que não devem mudar (mais seguro e rápido).

---

## Módulo 2: Funções e Programação Funcional

### 2.1 Definindo Funções

**O que são?** Blocos de código reutilizáveis.

```python
# Função simples
def saudacao(nome):
    return f"Olá, {nome}!"

resultado = saudacao("Maria")  # "Olá, Maria!"

# Função com múltiplos parâmetros
def calcular_score(sintomas_paciente, sintomas_doenca):
    em_comum = len(sintomas_paciente & sintomas_doenca)
    total = len(sintomas_doenca)
    
    if total == 0:
        return 0
    
    return em_comum / total

# Testando
paciente = {"febre", "dor de cabeça"}
dengue = {"febre", "dor de cabeça", "dor muscular"}
score = calcular_score(paciente, dengue)  # 0.67

# Função com valor padrão
def diagnosticar(sintomas, limiar=0.5):
    if len(sintomas) >= limiar * 10:
        return "Provável doença"
    return "Improvável"
```

---

### 2.2 Funções Lambda (Anônimas)

**O que são?** Funções pequenas escritas em uma linha só.

```python
# Lambda básica
quadrado = lambda x: x ** 2
print(quadrado(5))  # 25

# Lambda com múltiplos parâmetros
soma = lambda a, b: a + b
print(soma(3, 7))  # 10

# USO PRINCIPAL: Restrições em CSP
adjacente = lambda pos1, pos2: abs(pos1 - pos2) == 1
print(adjacente(3, 4))  # True

a_esquerda = lambda a, b: a < b
print(a_esquerda(2, 5))  # True

exatamente_antes = lambda a, b: a == b - 1
print(exatamente_antes(3, 4))  # True

# Restrição "entre"
entre = lambda a, b, c: (a < b < c) or (c < b < a)
print(entre(2, 4, 6))  # True
```

**Exemplo real no quebra-cabeça:**
```python
# Pista: "Tênis está exatamente à esquerda de Verde"
problem.addConstraint(
    lambda tenis, verde: tenis == verde - 1, 
    ("Tênis", "Verde")
)
```

---

### 2.3 List Comprehensions

**O que são?** Forma elegante e rápida de criar listas.

```python
# FORMA TRADICIONAL
quadrados = []
for x in range(5):
    quadrados.append(x ** 2)

# COM COMPREHENSION
quadrados = [x**2 for x in range(5)]
print(quadrados)  # [0, 1, 4, 9, 16]

# Com condição (filtro)
pares = [x for x in range(10) if x % 2 == 0]
print(pares)  # [0, 2, 4, 6, 8]

# Transformando strings
estados = ["ac", "al", "ap"]
estados_upper = [e.upper() for e in estados]
print(estados_upper)  # ['AC', 'AL', 'AP']

# Dictionary comprehension
estados_ids = {estado: i for i, estado in enumerate(["AC", "AL", "AP"])}
print(estados_ids)  # {'AC': 0, 'AL': 1, 'AP': 2}

# Set comprehension
letras = {c.lower() for c in "Python"}
print(letras)  # {'p', 'y', 't', 'h', 'o', 'n'}
```

---

## Módulo 3: Conceitos de IA Simbólica

### 3.1 O que é CSP?

**Definição:** Constraint Satisfaction Problem - paradigma onde:
- Temos VARIÁVEIS (coisas que precisam receber valores)
- Cada variável tem um DOMÍNIO (valores possíveis)
- Temos RESTRIÇÕES (regras que devem ser satisfeitas)

**Objetivo:** Encontrar valores para as variáveis que satisfaçam TODAS as restrições.

**Exemplo: Colorir 3 estados**

```python
# 1. VARIÁVEIS
variaveis = ["AC", "AM", "RO"]

# 2. DOMÍNIO
dominio = ["vermelho", "verde", "azul"]

# 3. RESTRIÇÕES
# AC e AM são vizinhos → cores diferentes
# AC e RO são vizinhos → cores diferentes

# Solução: AC=vermelho, AM=verde, RO=azul
```

**Usando a biblioteca python-constraint:**

```python
from constraint import Problem, AllDifferentConstraint

problem = Problem()

# Define variáveis e domínios
estados = ["AC", "AL", "AP", "AM"]
cores = ["vermelho", "verde", "azul", "amarelo"]
problem.addVariables(estados, cores)

# Define restrições
fronteiras = [("AC", "AM"), ("AC", "RO")]

for estado1, estado2 in fronteiras:
    problem.addConstraint(
        AllDifferentConstraint(), 
        (estado1, estado2)
    )

# Resolve
solucao = problem.getSolution()
print(solucao)
```

---

### 3.2 Tipos de Restrições em CSP

**1. AllDifferent - Todos Diferentes**
```python
problem.addConstraint(AllDifferentConstraint(), ["X", "Y", "Z"])
# X, Y e Z devem ter valores diferentes
```

**2. Adjacência - Ao Lado**
```python
lambda pos1, pos2: abs(pos1 - pos2) == 1
# Exemplo: pos1=3, pos2=4 → True
```

**3. Ordem - À Esquerda/Direita**
```python
# "A está à esquerda de B"
lambda a, b: a < b

# "A está à direita de B"
lambda a, b: a > b
```

**4. Posição Exata**
```python
# "A está EXATAMENTE à esquerda de B"
lambda a, b: a == b - 1
```

**5. Entre**
```python
# "B está entre A e C"
lambda a, b, c: (a < b < c) or (c < b < a)
```

**6. Posição Fixa**
```python
from constraint import ExactSumConstraint
problem.addConstraint(ExactSumConstraint(1), ["A"])
# A está na posição 1
```

**7. Conjunto de Posições**
```python
from constraint import InSetConstraint
problem.addConstraint(InSetConstraint([1, 5]), ["A"])
# A está na posição 1 ou 5
```

---

### 3.3 Sistemas Especialistas

**O que são?** Programas que simulam conhecimento de especialistas usando regras IF-THEN.

**ESTRUTURA:**
1. Base de Conhecimento - Regras
2. Base de Fatos - Informações atuais
3. Motor de Inferência - Aplica regras

**Exemplo Simples:**

```python
# BASE DE CONHECIMENTO
regras = {
    "regra1": {
        "se": ["febre alta", "dor de cabeça", "dor muscular"],
        "então": "Dengue provável"
    },
    "regra2": {
        "se": ["Dengue provável"],
        "então": "Recomendar hidratação"
    }
}

# BASE DE FATOS
fatos = ["febre alta", "dor de cabeça", "dor muscular"]

# MOTOR DE INFERÊNCIA
def aplicar_regras(fatos, regras):
    mudou = True
    while mudou:
        mudou = False
        for regra in regras.values():
            if all(condicao in fatos for condicao in regra["se"]):
                conclusao = regra["então"]
                if conclusao not in fatos:
                    fatos.append(conclusao)
                    mudou = True
    return fatos
```

---

### 3.3.1 Biblioteca Experta - Conceitos Fundamentais

**Fact (Fato):** Representa uma informação conhecida no sistema.

```python
from experta import *

# Fact é a classe BASE para criar tipos de fatos
# Pense em Fact como um "molde" para criar informações

# Exemplo 1: Fato simples (sem campos específicos)
class Sintoma(Fact):
    """Representa que um sintoma foi observado"""
    pass

# Exemplo 2: Fato com campos OBRIGATÓRIOS
class Sintoma(Fact):
    """Sintoma com nome obrigatório"""
    # Field define um campo (atributo) do fato
    # str = tipo do dado (texto)
    # mandatory=True = campo é OBRIGATÓRIO (não pode criar sem ele)
    nome = Field(str, mandatory=True)

# Exemplo 3: Fato com múltiplos campos
class Paciente(Fact):
    """Informações sobre o paciente"""
    nome = Field(str, mandatory=True)      # Nome obrigatório
    idade = Field(int, mandatory=False)    # Idade opcional
    tem_febre = Field(bool, mandatory=True) # Booleano obrigatório

# CRIANDO fatos (instâncias)
sintoma1 = Sintoma(nome="febre alta")
sintoma2 = Sintoma(nome="dor de cabeça")
paciente = Paciente(nome="João", idade=30, tem_febre=True)
```

**Field:** Define os atributos (campos) que um Fato pode ter.

```python
# Sintaxe: Field(tipo, mandatory=True/False, default=valor)

class Diagnostico(Fact):
    # Campo obrigatório do tipo string
    doenca = Field(str, mandatory=True)
    
    # Campo obrigatório do tipo float (número decimal)
    probabilidade = Field(float, mandatory=True)
    
    # Campo opcional com valor padrão
    confianca = Field(str, mandatory=False, default="baixa")
    
# Criando diagnósticos
diag1 = Diagnostico(doenca="Dengue", probabilidade=0.85)
# confianca será "baixa" automaticamente

diag2 = Diagnostico(doenca="Zika", probabilidade=0.70, confianca="média")
# confianca foi especificada
```

**KnowledgeEngine:** Motor que aplica as regras.

```python
# KnowledgeEngine é a "inteligência" do sistema
# Ele guarda os fatos e aplica as regras automaticamente

class MeuSistema(KnowledgeEngine):
    """Sistema que herda de KnowledgeEngine"""
    
    def __init__(self):
        # Inicializa o motor
        super().__init__()
        # Você pode adicionar atributos próprios
        self.diagnosticos_encontrados = []
```

**@Rule:** Decorador que define uma regra IF-THEN.

```python
class SistemaDiagnostico(KnowledgeEngine):
    
    # @Rule define: SE (condições) ENTÃO (executar função)
    # Cada parâmetro dentro de @Rule é uma CONDIÇÃO
    
    @Rule(Sintoma(nome="febre alta"))
    def regra_simples(self):
        """SE existe sintoma 'febre alta' ENTÃO executa isso"""
        print("Paciente tem febre!")
    
    # Múltiplas condições: TODAS devem ser verdadeiras (E lógico)
    @Rule(Sintoma(nome="febre alta"),
          Sintoma(nome="dor de cabeça"),
          Sintoma(nome="dor muscular"))
    def regra_dengue(self):
        """SE febre E dor de cabeça E dor muscular ENTÃO Dengue"""
        print("Diagnóstico: Dengue provável")
        # Pode declarar novos fatos aqui
        self.declare(Diagnostico(doenca="Dengue", probabilidade=0.85))
```

**OR:** Operador lógico OU.

```python
class SistemaDiagnostico(KnowledgeEngine):
    
    # OR significa: pelo menos UMA das condições deve ser verdadeira
    @Rule(Sintoma(nome="febre alta"),
          Sintoma(nome="dor de cabeça"),
          OR(Sintoma(nome="dor atrás dos olhos"),
             Sintoma(nome="manchas vermelhas")))
    def regra_dengue_completa(self):
        """
        SE febre alta E dor de cabeça E 
        (dor atrás dos olhos OU manchas vermelhas)
        ENTÃO Dengue
        """
        self.declare(Diagnostico(doenca="Dengue", probabilidade=0.85))
```

**AS e MATCH:** Capturar valores de fatos.

```python
class SistemaDiagnostico(KnowledgeEngine):
    
    def __init__(self):
        super().__init__()
        self.diagnosticos = []
    
    # AS captura o fato inteiro em uma variável
    # MATCH captura valores específicos dos campos
    @Rule(AS.diagnostico << Diagnostico(doenca=MATCH.doenca,
                                        probabilidade=MATCH.prob,
                                        confianca=MATCH.conf))
    def capturar_diagnostico(self, doenca, prob, conf):
        """
        Esta regra dispara quando QUALQUER Diagnostico é declarado
        
        AS.diagnostico << : captura o fato completo na variável 'diagnostico'
        MATCH.doenca : captura o valor do campo 'doenca' no parâmetro 'doenca'
        MATCH.prob : captura 'probabilidade' no parâmetro 'prob'
        MATCH.conf : captura 'confianca' no parâmetro 'conf'
        
        Útil para processar diagnósticos que outras regras criaram
        """
        self.diagnosticos.append({
            'doenca': doenca,
            'probabilidade': prob,
            'confianca': conf
        })
        print(f"✓ Capturado: {doenca} ({prob*100:.0f}%)")
```

**@DefFacts:** Define fatos iniciais.

```python
class SistemaDiagnostico(KnowledgeEngine):
    
    @DefFacts()
    def _initial_facts(self):
        """
        Fatos que SEMPRE existem no início
        yield é como return, mas retorna múltiplos valores
        """
        yield Fact(sistema="ativo")
        yield Fact(versao="1.0")
        # Esses fatos são adicionados automaticamente
```

**Ciclo de Uso Completo:**

```python
from experta import *

# 1. DEFINIR OS TIPOS DE FATOS
class Sintoma(Fact):
    nome = Field(str, mandatory=True)

class Diagnostico(Fact):
    doenca = Field(str, mandatory=True)
    probabilidade = Field(float, mandatory=True)

# 2. CRIAR O SISTEMA COM REGRAS
class SistemaDiagnostico(KnowledgeEngine):
    
    def __init__(self):
        super().__init__()
        self.resultados = []
    
    @Rule(Sintoma(nome="febre alta"),
          Sintoma(nome="dor de cabeça"),
          Sintoma(nome="dor muscular"))
    def diagnosticar_dengue(self):
        """Regra: sintomas típicos de dengue"""
        self.declare(Diagnostico(doenca="Dengue", probabilidade=0.85))
    
    @Rule(AS.d << Diagnostico(doenca=MATCH.doenca, probabilidade=MATCH.prob))
    def capturar(self, doenca, prob):
        """Captura qualquer diagnóstico criado"""
        self.resultados.append({'doenca': doenca, 'prob': prob})

# 3. USAR O SISTEMA
# Criar instância
engine = SistemaDiagnostico()

# Resetar (limpar memória) - SEMPRE fazer antes de usar
engine.reset()

# Declarar fatos (observações)
engine.declare(Sintoma(nome="febre alta"))
engine.declare(Sintoma(nome="dor de cabeça"))
engine.declare(Sintoma(nome="dor muscular"))

# Executar motor de inferência (aplica TODAS as regras)
engine.run()

# Ver resultados
print("Diagnósticos:", engine.resultados)
# Saída: Diagnósticos: [{'doenca': 'Dengue', 'prob': 0.85}]
```

**Fluxo de Execução:**

```
1. engine.reset()
   └─> Limpa toda memória de fatos anteriores
   └─> Adiciona fatos definidos em @DefFacts()

2. engine.declare(Sintoma(...))
   └─> Adiciona fato na memória de trabalho
   └─> NÃO executa regras ainda

3. engine.run()
   └─> Varre TODAS as regras
   └─> Para cada regra, verifica se condições são satisfeitas
   └─> Se SIM, executa a função da regra
   └─> Se a função declarar novos fatos, processa novamente
   └─> Continua até não haver mais regras para disparar
```

**Exemplo Completo do Código:**

```python
from experta import *

# TIPOS DE FATOS
class Sintoma(Fact):
    """Um sintoma observado no paciente"""
    nome = Field(str, mandatory=True)

class Vetor(Fact):
    """Vetor de transmissão (mosquito, carrapato, etc)"""
    tipo = Field(str, mandatory=True)

class Viagem(Fact):
    """Se o paciente viajou recentemente"""
    realizada = Field(bool, mandatory=True)

class Diagnostico(Fact):
    """Diagnóstico gerado pelo sistema"""
    doenca = Field(str, mandatory=True)
    probabilidade = Field(float, mandatory=True)
    confianca = Field(str, mandatory=True)

# SISTEMA ESPECIALISTA
class SistemaDiagnostico(KnowledgeEngine):
    
    def __init__(self):
        # Chama construtor da classe pai (KnowledgeEngine)
        super().__init__()
        # Lista para armazenar diagnósticos encontrados
        self.diagnosticos = []
    
    @DefFacts()
    def _initial_facts(self):
        """Fatos sempre presentes no início"""
        yield Fact(sistema="ativo")
    
    # REGRAS DE DIAGNÓSTICO
    
    @Rule(Sintoma(nome="febre alta"),
          Sintoma(nome="dor de cabeça"),
          Sintoma(nome="dor muscular"),
          OR(Sintoma(nome="dor atrás dos olhos"),
             Sintoma(nome="manchas vermelhas na pele")))
    def diagnosticar_dengue(self):
        """
        SE: febre alta E dor de cabeça E dor muscular E
            (dor atrás dos olhos OU manchas vermelhas)
        ENTÃO: Declara diagnóstico de Dengue
        """
        self.declare(Diagnostico(
            doenca="Dengue",
            probabilidade=0.85,
            confianca="alta"
        ))
    
    @Rule(Sintoma(nome="febre alta"),
          Sintoma(nome="calafrios"),
          Sintoma(nome="suor intenso"),
          Viagem(realizada=True))
    def diagnosticar_malaria(self):
        """
        SE: febre E calafrios E suor E viajou recentemente
        ENTÃO: Declara diagnóstico de Malária
        """
        self.declare(Diagnostico(
            doenca="Malária",
            probabilidade=0.80,
            confianca="alta"
        ))
    
    # REGRA DE CAPTURA
    @Rule(AS.diagnostico << Diagnostico(
              doenca=MATCH.doenca,
              probabilidade=MATCH.prob,
              confianca=MATCH.conf))
    def capturar_diagnostico(self, doenca, prob, conf):
        """
        Esta regra SEMPRE dispara quando um Diagnostico é declarado
        Captura os valores e salva na lista
        
        AS.diagnostico: captura o fato completo
        MATCH.doenca: extrai o valor do campo 'doenca'
        MATCH.prob: extrai o valor do campo 'probabilidade'
        MATCH.conf: extrai o valor do campo 'confianca'
        """
        self.diagnosticos.append({
            'doenca': doenca,
            'probabilidade': prob,
            'confianca': conf
        })

# USANDO O SISTEMA
engine = SistemaDiagnostico()
engine.reset()  # Limpa memória

# Adiciona sintomas observados
engine.declare(Sintoma(nome="febre alta"))
engine.declare(Sintoma(nome="dor de cabeça"))
engine.declare(Sintoma(nome="dor muscular"))
engine.declare(Sintoma(nome="dor atrás dos olhos"))

# Executa motor de inferência
engine.run()

# Mostra resultados
print("Diagnósticos encontrados:")
for diag in engine.diagnosticos:
    print(f"  - {diag['doenca']}: {diag['probabilidade']*100:.0f}%")
```

---

### 3.4 NLP - Processamento de Linguagem Natural

**O que é?** Extrair informações estruturadas de texto livre.

**Técnicas Básicas:**

**1. Normalização**
```python
texto = "Paciente com FEBRE"
texto_normalizado = texto.lower()  # "paciente com febre"
```

**2. Busca de Padrões**
```python
sintomas_conhecidos = ["febre", "dor de cabeça", "náusea"]
texto = "paciente com febre e náusea"

sintomas_encontrados = []
for sintoma in sintomas_conhecidos:
    if sintoma in texto:
        sintomas_encontrados.append(sintoma)
```

**3. Sinônimos**
```python
sinonimos = {
    "febre": ["temperatura alta", "febril"],
    "dor de cabeça": ["cefaleia"]
}

def normalizar_sintoma(texto):
    texto_lower = texto.lower()
    for sintoma_oficial, variacoes in sinonimos.items():
        for variacao in variacoes:
            if variacao in texto_lower:
                return sintoma_oficial
    return None
```

**4. Expressões Regulares**
```python
import re

texto = "Sintomas começaram há 5 dias"
padrao = r'há (\d+) dias'
resultado = re.search(padrao, texto)

if resultado:
    dias = resultado.group(1)
    print(f"Há {dias} dias")
```

**Exemplo Completo:**

```python
import re

class ProcessadorNLP:
    def __init__(self):
        self.sintomas_conhecidos = [
            "febre", "febre alta", "dor de cabeça", 
            "dor muscular", "náusea", "vômito"
        ]
        self.sinonimos = {
            "febre": ["temperatura alta", "febril"],
            "dor de cabeça": ["cefaleia"],
            "náusea": ["enjoo"]
        }
    
    def extrair_sintomas(self, texto):
        texto_lower = texto.lower()
        sintomas = set()
        
        for sintoma in self.sintomas_conhecidos:
            if sintoma in texto_lower:
                sintomas.add(sintoma)
        
        for sintoma, variacoes in self.sinonimos.items():
            for variacao in variacoes:
                if variacao in texto_lower:
                    sintomas.add(sintoma)
        
        return sintomas
    
    def extrair_tempo(self, texto):
        padrao = r'há (\d+) dia'
        match = re.search(padrao, texto.lower())
        return match.group(1) if match else None
    
    def detectar_viagem(self, texto):
        palavras = ['viagem', 'viajou', 'voltou de']
        return any(p in texto.lower() for p in palavras)

# Usando
processador = ProcessadorNLP()
texto = "Paciente com cefaleia há 3 dias. Voltou de viagem."

sintomas = processador.extrair_sintomas(texto)
tempo = processador.extrair_tempo(texto)
viagem = processador.detectar_viagem(texto)
```

---

## Resumo dos Conceitos Principais

### Python Básico
- **Listas**: mutáveis, ordenadas
- **Dicionários**: pares chave-valor
- **Sets**: únicos, operações matemáticas
- **Tuplas**: imutáveis
- **Funções**: código reutilizável
- **Lambda**: funções anônimas
- **Comprehensions**: criação elegante

### IA Simbólica
- **CSP**: Variáveis + Domínios + Restrições
- **Restrições**: Adjacência, ordem, entre, posição
- **Sistema Especialista**: Regras IF-THEN + Motor
- **NLP**: Extração de informação de texto

### Bibliotecas Usadas
- `python-constraint`: Resolver CSPs
- `experta`: Sistemas especialistas
- `spacy`: NLP
- `geopandas`: Dados geográficos
- `matplotlib`: Visualização

---

## Dicas para o Minicurso

1. Comece pelo básico: listas e dicionários
2. Pratique com exemplos reais
3. Conecte os conceitos aos projetos
4. Use analogias simples
5. Mostre erros comuns

**Boa sorte com o minicurso!**