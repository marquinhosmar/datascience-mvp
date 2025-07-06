## Introdução

Este trabalho faz parte do MVP Análise de Dados e Boas Práticas do curso de Ciências de Dados e Analytics da PUC-RIO.

  O objetivo do MPV é escolher um dataset preferencialmente em algum repositário de dados públicos, e a partir dele aplicar as técnicas vistas nas 
disciplinas de:
  - Análise Exploratória e Pré-Processamento de Dados.
  - Visualização de Informação
  - Engenharia de Software para Ciência de Dados

  O dataset escolhido foi o do SICONFI (Sistema de Informações Contábeis e Fiscais do Setor Público Brasileiro) que é uma plataforma do Tesouro 
Nacional que recebe, processa e divulga informações contábeis, financeiras e estatísticas de todos os entes federativos. É uma ferramenta essencial
para a transparência e o acompanhamento da gestão fiscal do país.

## Descrição do Problema

  O conjunto de dados do Siconfi é um conjunto de dados multivariado que consiste em medidas que permitem analisar várias situações financeiras dos 
estados brasieliros, tais como: evolução da Receita e Despesa Pública, capacidade de Investimento dos estados, situação da responsabilidade fiscal, 
depência de transferências federais, comparativos entre regiões, qualidade do gasto público, entre outros.O investimento público é universalmente 
reconhecido como um pilar para o desenvolvimento econômico e social. 

  Por meio da formação de capital em infraestrutura, educação e saúde, ele não apenas estimula a atividade econômica no curto prazo, mas também eleva 
a produtividade e a competitividade no longo prazo, sendo um instrumento essencial para a redução das desigualdades. Em um país de dimensões 
continentais e com profundas disparidades regionais como o Brasil, a alocação de investimentos pelos governos estaduais assume um papel ainda mais 
crítico, sendo fundamental para promover a convergência de renda e garantir o acesso equitativo a serviços públicos de qualidade.

  O presente trabalho tem como objetivos principais analisar os investimentos públicos dos entes estaduais durante o período de 2018 a 2024. Bem como a
relação investimento sobre a despesa total. O investimento público é uma depesa de capital. Incluí obras públicas (escolas, hospitais, estradas), compra 
de equipamentos e imóveis permanentes. Seu objetivo é o desenvolvimento econômico e social (infraestrutura, serviços, geração de ativos)

## Hipóteses do Problema

As hipóteses que tracei são as seguintes:

- O **Investimento** público segue um padrão uniforme durante um determinado período de tempo ou apresenta variações?

- Avaliar se a maior **Receita Total** ou maior **Despesa Total** está associada a maior capacidade de investimento.

-  Estados com maiores gastos brutos são os que mais realizam investimentos em termos percentuais?

- Prioridade em Investimentos, avaliar a tendência da alocação orçamentária. Estados priorizam despesas correntes em detrimento dos investimentos ao longo do tempo?


## Tipo de Problema

  Este é um problema de **classificação supervisionada**. Dado um conjunto de características como despesa total, depesa corrente e receita total o 
objetivo é classificar se um estado está em com dificuldades orçamentárias com base em seus indicadores de investimento público.

## Seleção de Dados

  O dataset do **siconfi** é um conjunto de dados de domínio público, amplamente disponível e frequentemente incluído em bibliotecas de aprendizado de máquina. 
É  utilizado para diversas finalidades de pesquisas econômicas, bem como no meio acadêmico. É necessária uma etapa de seleção de dados externa, pois o dataset  
possui muitos dados e de acordo com a finalidade é importante definir o que será filtrado.

  O dataset poderia ser carregado diretamente da **api** do **tesouro nacional**, porém para acelerar o processo de importação de dados e garantir que o dataset possa 
ser importado diretamente do github através de um arquivo csv foi rodado alguns códigos até a geração de um arquivo final csv que foi hospedado no github.


## Importação das Bibliotecas Necessárias e Carga de Dados

  Esta seção consolida todas as importações de bibliotecas necessárias para a análise, visualização e pré-processamento dos dados, bem como o carregamento inicial 
do dataset dfsiconfi_resultados_brutos.csv que estar alocado no github.

# Análise de Dados

Nesta etapa de Análise de Dados Exploratória (EDA) sobre o dataset do Siconfi, visamos entender a distribuição, as relações e as características das variáveis,
o que é crucial para as etapas subsequentes de pré-processamento e modelagem.

## Total e Tipo das Instâncias

O dataset `df` possui 470.990 instâncias (observações), e 14 colunas. As características de medição são do tipo`float64` (ou ponto flutuante de 64 bits) é um tipo 
numérico usado para representar números decimais (com casas após a vírgula). Temos também o `int64` (ou inteiro de 64 bits) que é um tipo numérico usado para 
representar números inteiros (sem casas decimais). E por fim o tipo `object` que é um tipo de dados mais genérico, geralmente ele é usado para armazenar texto (strings).
Não existe valores nulos e nem dados faltantes.

## Atributos do Dataset

O dataset `df` contém 470.990 instâncias com 14 colunas:

- ***exercicio*** : o ano em que os fatos contábeis ocorreram e foram registrados.
- ***instituicao*** : descrição do nome do Estado.
- ***cod_ibge*** : código do estado segundo a classificação do IBGE.
- ***uf*** : sigla do estado.
- ***anexo*** :  indica em qual anexo dos demonstrativos contábeis ou fiscais aquela conta aparece ou deve ser demonstrada, conforme exigências da contabilidade pública brasileira.
- ***rotulo*** : é o nome oficial e padronizado da conta contábil, definido pela autoridade competente (como o Tesouro Nacional no caso do PCASP).
- ***coluna*** : dia, mês e ano (coincide com o exercício).
- ***cod_conta*** : número da conta do plano de contas.
- ***conta*** : nome da conta.
- ***valor*** : representa o montante financeiro associado àquela conta contábil.
- ***populacao*** : população do estado.
- ***UF*** : repete novamente a UF do estado.
- ***Codigo_UF*** : código IBGE da UF.
- ***Ano*** : coincide com o ano de exercício.

## Tratamento dos dados

Foram feitos alguns procedimentos até chegar ao DataFrame final. Alguns dos procedimentos feitos foram:
- limpeza removendo linhas e colunas;
- criação de novas colunas a partir de informações financeiras que estavam em uma determinada coluna;
- deflacionar os valores a partir de um dos índices oficais de inflação;
- transformação numérica de numéros para outra notação;

## Estatísticas Descritivas

 Nesta seção pode-se visualizar através de tabelas e gráficos estatísticas descritivas que fornecem um resumo das características numéricas, incluindo média, desvio padrão,
mínimo, máximo e quartis.

 Através dos gráficos são feitas algumas descobertas interessantes sobre os estados que mais gastam em valores brutos, como também os que mais investem em valores brutos.
Descobrimos que os estados que mais investem levando em consideração a relação investimento/despesa total estão fora da lista dos dos que tem as maiores receitas.

Pode-se perceber em meio a análise que determinados estados apresentam dificuldade para investir devido a relação depesa corrente/despesa total estar em patamares elevados.

## Pré-Processamento de Dados

  O pré-processamento de dados é uma etapa crucial para preparar os dados para modelagem, garantindo que estejam no formato correto e otimizados para o desempenho do
algoritmo. A escolha pela Normalização, Padronização ou por ambos será efetivada quando forem feitos testes posteriores. O objetivo é que o modelo preveja que baseado 
nos indicares de Despesa_Total, Despesa_Corrente e Receita_Total preveja o Investimento. E com base no investimento realizado por um ente em determinado ano pode ser
deduzido crise fiscal.

## Conclusão

As quatro hipóteses levantadas foram respondidas:

O Investimento público segue um padrão uniforme durante um determinado período de tempo ou apresenta variações?
- Descobrimos que o investimento público não é unfiforme ao longo do tempo. Apresenta períodos de crescimento e outros de queda.

Eficiência fiscal: avaliar se a maior Receita Total ou maior Despesa Total está associada a maior capacidade de investimento.
- Os estados que mais têm receita bruta, ou depesa bruta não são os que mais investem do ponto de vista percentual.

Estados com maiores gastos brutos são os que mais realizam investimentos em termos percentuais?
- Novamente descobrimos que os estados que mais investem em termos brutos estão abaixo da média nacional de investimento em termos percentuais.

