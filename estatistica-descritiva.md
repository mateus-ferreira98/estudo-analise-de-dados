# Parte I: Estatística Descritiva

## 1.1: Introdução a Estatística
### Uma visão geral da Estatística
#### Uma definição de estatística
- Dados: consistem em informações provenientes de observações, contagens, medições ou respostas.
- Estatística: é a ciência que trata da coleta, organização, análise e interpretação dos dados para tomada de decisões.

#### Conjunto de dados
Há dois tipos de conjuntos de dados e são chamados de população e amostra.
- População: é a coleção de todos os resultados, respostas, medições ou contagens que são de interesse. <br>
  Exemplo: Coletar a média de idade de todas os estudantes de uma Universidade.
- Amostra: é um subconjunto ou parte de uma população. <br>
  Exemplo: Coleta a média de idade de todos os estudantes de um curso especifíco. <br>

  Uma amostra deve ser representativa de uma população, para que com os dados conseguimos tirar conclusões sobre aquela população.
  E devem ser coletados usando métodos apropriados, tal como a amostragem aleátoria. <br>

 #### Usando os conceitos de População e Amostra na prática. Dados da Universidade Federal de Goiás, dados de até 2018

   Exemplo de População, a média de idade de todos os estudantes da UFG

 ```
  # Usando 'coerce' para lidar com datas inválidas
df['DATA_NASC.'] = pd.to_datetime(df['DATA_NASC.'], errors='coerce') 

# Corrija a data problemática na linha 393
df.loc[393, 'DATA_NASC.'] = pd.to_datetime('1987-07-01')

# Calcule a idade com base no ano de referência 2018
df['idade'] = 2018 - df['DATA_NASC.'].dt.year

# Exiba as colunas 'DATA_NASC.' e 'idade'
print(df[['DATA_NASC.', 'idade']])
 
# Calcule a média da idade e converta para um número inteiro
media_idade = int(df['idade'].mean())

# Exiba a média da idade como um número inteiro
print(f'A média da idade é: {media_idade} anos.')

A média da idade é: 24 anos.
  ```
  Exemplo de Amostra, a média de idade de todos os estudantes do curso de Gestão da Informação

```
# Filtrar o DataFrame para incluir apenas as pessoas do curso "GI"
curso_gi = df[df['CURSO'] == 'GESTÃO DA INFORMAÇÃO']

# Calcular a média da idade para as pessoas do curso "GI"
media_idade_gi = int(curso_gi['idade'].mean())

# Exibir a média da idade das pessoas do curso "GI"
print(f'A média da idade das pessoas do curso GI é: {media_idade_gi} anos')

A média da idade é: 23 anos.
```

  Dois termos importantes que também são utilizados, chamados de parâmetro e estatística.
  - Parâmetro: é a descrição numérica de uma característica populacional.
  - Estatística: é a descrição numérica de uma característica amostral.
 
 #### Ramos da estatística
  
  O estudo da estatística tem dois ramos principais, estatística descritiva e estatística inferencial.
  - Estatística Descritiva: é o ramo da estatística que envolve a organização, o resumo e a representação dos dados.
  - Estatística Inferencial: é o ramo da estatística que envolve o uso de uma  amostra para chegar a conclusões sobre uma população.
Conceitos de Probabilidade é muito usado nessa parte.

### Classificação dos dados
#### Tipos de dados

Os conjuntos de dados consistem em dois tipos: qualitativo e quantitativo
- Dados qualitativos: consistem em atributos, rótulos ou entradas não numéricas.
- Dados quantitativos: consistem em medidas numéricas ou contagens.

#### Níveis de mensuração

  O nível de mensuração determina quais operações estatísticas são apropriadas. Existem 4 tipos: nominal, ordinal, intervalar e de razão.

  - Dados de mensuração nominal: são apenas qualitativos. Dados 
nesse nível são categorizados usando-se nomes, rótulos ou qualidades. Não 
é possível realizar cálculos matemáticos nesse nível.
 - Dados de mensuração ordinal: são qualitativos ou quantitativos. 
Dados nesse nível podem ser postos em ordem ou classificados, mas as 
diferenças entre as entradas de dados não têm sentido matemático.
 - Dados de mensuração intervalar: podem ser ordenados e é 
possível calcular diferenças que tenham sentido matemático entre as 
entradas de dados. No nível intervalar, um registro zero simplesmente 
representa uma posição em uma escala; a entrada não é um zero natural.
 - Dados de mensuração de razão: são similares aos dados no nível 
intervalar, com a propriedade adicional de que, nesse nível, um registro 
zero é um zero natural.

##### Operações apropriadas nos níveis de mensuração.

| Nível de mensuração   | Categorizar os dados | Ordenar os dados | Substrair os dados | Determinar se um  dado é múltiplo de outro |
| --------------------- | -------------------- | ---------------- | ------------------ | ------------------------------------------ |                      
| Nominal               | Sim                  | Não              | Não                | Não                                        |
| Ordinal               | Sim                  | Sim              | Não                | Não                                        |
| Intervalar            | Sim                  | Sim              | Sim                | Não                                        |
| Razão                 | Sim                  | Sim              | Sim                | Sim                                        |


  #### Colocando em prática

  ```
  # Crie um dicionário com os nomes das colunas e os tipos de dados correspondentes
data = {
    'Coluna': ['TURNO', 'AÇÃO AFIRMATIVA PARTICIPAÇÃO', 'ANO INGRESSO', 'idade'],
    'Tipo de Dado': ['Nominal', 'Ordinal', 'Intervalar', 'Razão']
}

# Crie um DataFrame com esses dados
tabela_tipos_dados = pd.DataFrame(data)

# Exiba a tabela de tipos de dados
print(tabela_tipos_dados)
  ```
 | Nome                         | Tipo de dado |
 |----------------------------- | ------------ | 
 | TURNO                        | Nominal      |
 | AÇÃO AFIRMATIVA PARTICIPAÇÃO | Ordinal      |
 | ANO INGRESSO                 | Intervalar   |
 | IDADE                        | Razão        |

Turno é um dado nominal, pois não tem uma ordem intrínseca. (Matutino, Vespertino, Integral, Noturno). <br>
Ação Afirmativa participação é um dado Ordinal, pois existe uma ordem para o aluno ingressar. (sem cotas ou com cotas, e dentro da cotas tem uma ordem). <br>
Ano ingresso é um dado Intervalar, pois podemos colocar eles em um intervalo. (Qual intervalo de ano teve mais trancamentos). <br>
Idade é um dado de Razão, pois podemos fazer vários cálculos matématicos com ele. (média, se um é múltiplo por outro). <br>


## 1.2: Estatística Descritiva

### Distribuições de frequência e seus gráficos

#### Distribuições de frequência

Definição: É uma tabela que mostra classes ou intervalos dos valores com a contagem do número de ocorrências em cada classe ou intervalo.
Cada classe tem um limite inferior e superior, onde o inferior é o menor número que pode pertencer à classe e o superior que é o maior número
que pode pertencer a classe.
A amplitude de classe é a distância entre os limites inferiores e superiores.
O código abaixo vai mostrar isso. Utilizando dados da idade de Estudantes da UFG do curso Gestão da Informação.

```
# Determine o número de classes
num_classe = 5

# Determine o valor mínimo e máximo
valor_minimo = df['idade'].min()
valor_maximo = df['idade'].max()

# Determine a amplitude da classe
amplitude = (valor_maximo - valor_minimo) / num_classe

# Arredonde a amplitude para baixo
amplitude_arredondada = math.floor(amplitude)

print('Idade mínima: ', valor_minimo)
print('Idade máxima: ', valor_maximo)
print('A amplitude é: ' , valor_maximo , '-' , valor_minimo , '=' , amplitude_arredondada)

Idade mínima: 18
Idade máxima: 54
A amplitude é: 54 - 18 = 7
```
O valor mínimo é um limite inferior conveniente para a primeira 
classe. Para encontrar os limites inferiores das 5 classes restantes, 
adicione a amplitude de classe, 7, ao limite inferior de cada classe precedente. Logo, os limites inferiores das demais classes são: 18+ 7 = 25, 25 + 7 = 32, e assim por diante. A tabela abaixo vai mostrar como fica a frequência de idades dos estudantes de Gestão da Informação da UFG.
Observação: Dados de até 2018.

```
# Crie os intervalos de classe
intervalos = [valor_minimo + i * amplitude_arredondada for i in range(num_classe + 1)]

# Use pd.cut() para criar as classes e atribuir cada idade a uma classe
df['classe_idade'] = pd.cut(df['idade'], bins=intervalos, include_lowest=True)

# Use value_counts() para contar a frequência de cada classe
tabela_frequencia = df['classe_idade'].value_counts().sort_index().reset_index()

# Renomeie as colunas para "Classe de Idade" e "Frequência"
tabela_frequencia.columns = ['Classe de Idade', 'Frequência']

# Exiba a tabela de frequência
print(tabela_frequencia)

```
 | Classe de Idade              | Frequência   |
 |----------------------------- | ------------ | 
 | (17, 25]                     | 121          |
 | (25, 32]                     | 19           |
 | (32, 39]                     | 6            |
 | (39, 46]                     | 5            |
 | (46, 53]                     | 0            |
<br>
 Essa é uma distruibuição de frequência padrão, mas tem como adicionar outras características. E são elas, <b>ponto médio</b>, <b>frequência relativa</b> e <b>frequência acumulada</b>.
 Vamos para as definições.
 
 - <b>Ponto médio</b>: É a soma dos limites inferiores e superiores da classe dividido por 2.
  Exemplo: Pegando a classe de idade, a primeira classe (17, 25] = 17 + 25 / 2 = 29.5
- <b>Frequência relativa</b>: É a fração ou proporção de dados que está na classe. Para calcular, basta dividir a frequência pelo tamanho total da amostra.
  Exemplo: Pegando a primeira frequência que é 121, dividindo pelo total da amostra que é 151 = 121 / 151 = 0.80
- <b>Frequência acumulada</b>: E a soma das frequências dessa classe com todas as anteriores.
     Exemplo: A primeira frequência acumulada é 121 pois não tem nada antes dela, mas a segunda já é 121+19 = 140
    
 
