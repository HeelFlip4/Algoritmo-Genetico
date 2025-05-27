# Algoritmo Genético - Otimização de Indivíduos Inteiros

## 📌 Introdução

Este projeto é a implementação de um Algoritmo Genético em C++, utilizado para encontrar um número inteiro que satisfaça determinada equação polinomial:

```
a·x⁵ + b·x⁴ + c·x³ + d·x² + e·x + f
```

A técnica é inspirada em processos de melhoramento genético, aplicando conceitos como:
- **Seleção** de indivíduos com base em sua aptidão (valor da equação),
- **Cruzamento** (crossover) com manipulação de bits,
- **Mutação** aleatória,
- Evolução da população ao longo de diversas gerações.

O objetivo é encontrar um número inteiro `x` cujo resultado da equação esteja entre `-1` e `1`. Caso isso não seja possível, o algoritmo retorna o melhor indivíduo encontrado ao fim do número máximo de gerações.

---

## ⚙️ Funcionamento

### 1. Avaliação dos Indivíduos
- Cada indivíduo é um número inteiro.
- A equação `a*x^5 + b*x^4 + c*x^3 + d*x^2 + e*x + f` é usada como função de avaliação.
- O resultado é ordenado por **módulo**, aproximando os valores de zero (que é a solução ideal).

### 2. Inicialização da População
- Geração aleatória de indivíduos com valores entre -2000 e 2000.
- A população pode ter tamanho 10, 100 ou 1000 (limitado).

### 3. Seleção
- 50% dos indivíduos com melhor desempenho são selecionados.
- Se a quantidade for ímpar, um indivíduo extra é adicionado.

### 4. Cruzamento
- Indivíduos selecionados são cruzados por manipulação de bits.
- Cada par gera dois novos filhos.
- A nova população é preenchida com os filhos e parte da população selecionada, retornando ao tamanho original.

### 5. Mutação
- Ocorre com probabilidade definida pelo usuário.
- Apenas os **11 bits menos significativos (posições 0 a 10)** podem ser alterados, para evitar gerar números acima de 2000.

### 6. Parada
- O algoritmo para se encontrar um indivíduo com resultado da equação entre `-1` e `1`.
- Caso contrário, continua até o número máximo de gerações (máximo permitido: 1000).

---

## 📌 Restrições e Tratamentos

- Se um indivíduo ultrapassar os limites `[-2000, 2000]`, ele é substituído por um novo valor aleatório.
- O melhor indivíduo de cada geração é armazenado.
- Todos os vetores são estáticos.
- O algoritmo trata corretamente valores inválidos.

---

## 🚀 Compilação e Execução

### Compilação (Linux, WSL ou Windows com g++):
```bash
g++ driver.cpp -o algoritmoGenetico.exe
```

### Execução:
```bash
./algoritmoGenetico.exe
```

---

## 🧪 Casos de Uso

### 🔹 Caso 1
- População: 10
- Crossover: 0.8
- Mutação: 0.9
- Gerações: 50  
- Coeficientes: `a=1, b=2, c=3, d=4, e=5, f=6`

**Resultado:**
> Melhor indivíduo na geração 5: valor 1 → resultado da equação: 21

---

### 🔹 Caso 2
- População: 100
- Crossover: 0.5
- Mutação: 0.5
- Gerações: 100  
- Coeficientes: `a=1, b=0, c=0, d=0, e=0, f=250`

**Resultado:**
> Melhor indivíduo na geração 3: valor -2 → resultado da equação: 218

---

### 🔹 Caso 3
- População: 1000
- Crossover: 0.4
- Mutação: 0.7
- Gerações: 250  
- Coeficientes: `a=1, b=2, c=3, d=4, e=50, f=100`

**Resultado:**
> Melhor indivíduo na geração 159: valor 0 → resultado da equação: 100

---

### 🔹 Caso 4
- População: 1000
- Crossover: 0.7
- Mutação: 0.99
- Gerações: 1000  
- Coeficientes: `a=1, b=2, c=3, d=4, e=5, f=-115`

**Resultado:**
> Melhor indivíduo encontrado na geração 2: valor 2 → resultado da equação: -1
