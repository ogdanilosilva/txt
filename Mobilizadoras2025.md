# Metas Mobilizadoras


## Definições

As definições dos conceitos das metas são realizadas em conjunto com a área de planejamento e com envolvimento das unidades técnicas. Os scripts em **SQL** são construídos em conjunto com a UTC.
 
## Índice

- [Caminho da rede](#CaminhoRede)
- [Metas Mobilizadoras](#Metas)
  * [Clientes Atendidos com Foco em Resultados](#ClientesAtendidosFocoResultados)
  * [Faturamento (Sem Ali)](#FaturamentoSemAli)
  * [Faturamento](#Faturamento)
  * [Produtividade](#Produtividade)
  * [Receita Própria](#ReceitaPropria)
  * [Municípios Reconhecidos - Empreendedorismo e Inovação](#MuncipiosReconhecidos)
  * [Cobertura ME e EPP](#CoberturaMEEPP)
  * [Recorrência](#Recorrencia)
  * [Cobertura dos Grupos Sub-Representados](#GruposSubRepresentados)
  * [Cobertura de Estudantes](#Cobertura-Estudantes)
- [Metas de Monitoramento (Não é Meta Mobilizadora de SP)](#NaoMobilizadora)
  * [NPS](#NPS)
  * [FAMPE](#Fampe)
- [Painel De Metas Mobilizadoras](#PainelMetasMobilizadoras)



<br />
<br />

# Caminho da rede

- \\sp-sebrae
  * UGE
      + 06.Monitoramento Estratégico
        + 26 - Scripts SQL
          + Scripts 2025
            + Metas 2025 -  Mobilizadoras

<br>

## Execução do Script

Para execução do script se faz necessário a utilização do software Microsoft SQL Management Studio.

<br>

# METAS MOBILIZADORAS <a id='Metas'></a>

***
# Clientes atendidos com Foco em Resultados
<a id='ClientesAtendidosFocoResultados'></a>


## Definição da Meta

Somatório de clientes distintos atendidos com foco em resultados.

## Fórmula de Cálculo
Pequenos negócios (MEI + ME + EPP) distintos que concluíram em 2025 alguma iniciativa apontada no planejamento como geradoras de resultados
para os clientes. Esses clientes, devem ter concluído soluções com foco em aumento de faturamento de suas empresas.

Iniciativas consideradas: 
<b>
 * Impulsiona
 * Sebrae Delas (MEI)
 * Sebrae Comunidades - Lojas Colaborativas
 * Clube de Negócios
 * Transformação Digital e Negócios Digitais
 * Rodada e Encontro de Negócios
 * Feiras Estaduais e Regionais
 * Franquias
 * Pré-Aceleração
 * Aceleração
 * Crie Mercado
 * Conexões Corporativas
 * Jornada de Atendimento Estruturado
 * Sustentabilidade, Eficiência Empresarial e Soluções Tecnológicas
 * Projetos Especiais - Setores, Segmentos e Cadeias Produtivas
 * Projetos Especiais – Competitividade em CPL, IG e Rotas de Turismo e Rural.
 </b>


## Script 

Segue abaixo os scripts que compõem a Meta:


```SQL
SELECT SUM(qt_inscrito) as Inscritos, SUM(qt_participante) as Participantes, SUM(qt_cONcluinte_distinto) as ConcluintesDistintos, SUM(qt_concluinte_sem_ali) as ConcluintesDistintosSemALI, SUM(vl_executado) as Executado
FROM [dbo].[v_dim_execucao_meta_estadual]
where id_meta = 1
AND mes = MONTH(getdate())
group by mes
order by mes asc

SELECT COUNT(DISTINCT id_pessoa_juridica) as ConcluintesDistintos
FROM [dbo].[v_dim_execucao_meta_estadual]
where id_meta in ('46','47','48','49','50','51','52','53','54','55','56','57','58','59','60','61')
AND mes = MONTH(getdate())
AND qt_concluinte_distinto > 0

-- 1. Impulsiona --

-- 2. Sebrae Delas MEI --

-- 3. Sebrae Comunidades - Lojas Colaborativas --

-- 4. Clube de Negócios --

-- 5. Transformação Digital / Negócios Digitais --

-- 6. Rodada e Encontro de Negócios  --

-- 7. Feiras Estaduais e Regionais --

-- 8. Franquias --

-- 9. Pré-Aceleração --

-- 10. Aceleração --

-- 11. Crie Mercado --

-- 12. Conexões Corporativas --

-- 13. Jornada de Atendimento Estruturado --

-- 14. Sustentabilidade, Eficiência Empresarial e Soluções Tecnológicas --

-- 15. Projetos Especiais - Setores, Segmentos e Cadeias Produtivas --

-- 16. Projetos Especiais - Competividade em CPL, IG e Rotas de Turismo/Rural --


```

Resultado do indicador:

```
 Número
```

***
# Faturamento (Sem Ali)
<a id='FaturamentoSemAli'></a>

## Definição da Meta

Variação percentual do faturamento dos pequenos negócios atendidos nos projetos e processos executados pelo sistema Sebrae.

## Fórmula de Cálculo
Iniciativas consideradas para esse indicador: 
<b>
 * Impulsiona
 * Sebrae Delas (MEI)
 * Sebrae Comunidades - Lojas Colaborativas
 * Clube de Negócios
 * Transformação Digital e Negócios Digitais
 * Rodada e Encontro de Negócios
 * Feiras Estaduais e Regionais
 * Franquias
 * Pré-Aceleração
 * Aceleração
 * Crie Mercado
 * Conexões Corporativas
 * Jornada de Atendimento Estruturado
 * Sustentabilidade, Eficiência Empresarial e Soluções Tecnológicas
 * Projetos Especiais - Setores, Segmentos e Cadeias Produtivas
 * Projetos Especiais – Competitividade em CPL, IG e Rotas de Turismo e Rural.
</b>

<br />

A variação média do Faturamento:
![img1](image-1.png)

<br />
A média da UF é calculada:

![img2](image-2.png)

Onde:
-  j = 1, 2, 3....N (índice indicando cada projeto/processo)
-  i = 1, 2, 3.....n (índice indicando cada cliente da amostra)
-  n = Nº clientes com mensuração válida por Projeto ou Processo
-  N= Nº Projetos e Processos mensurados
-  c = Nº clientes prioritários dos projetos/processos


## Script

Segue abaixo os scritps que compõem a meta:

```SQL
SELECT *
FROM [dbo].[v_dim_execucao_meta_estadual]
where id_meta = 2
order by mes asc
```
<br />

**Observação: Neste indicador, temos apenas o valor consolidado no banco de metas, efetuado por uma empresa contratada**

<br />

Resultado do indicador:

```
Percentual(%)
```
***

# Faturamento
<a id='Faturamento'></a>

## Definição da Meta

Variação percentual do faturamento dos pequenos negócios atendidos nos projetos e processos executados pelo sistema Sebrae.

## Fórmula de Cálculo
Iniciativas consideradas para esse indicador: 
<b>
 * Impulsiona
 * Sebrae Delas (MEI)
 * Sebrae Comunidades - Lojas Colaborativas
 * Clube de Negócios
 * Transformação Digital e Negócios Digitais
 * Rodada e Encontro de Negócios
 * Feiras Estaduais e Regionais
 * Franquias
 * Pré-Aceleração
 * Aceleração
 * Crie Mercado
 * Conexões Corporativas
 * Jornada de Atendimento Estruturado
 * Sustentabilidade, Eficiência Empresarial e Soluções Tecnológicas
 * Projetos Especiais - Setores, Segmentos e Cadeias Produtivas
 * Projetos Especiais – Competitividade em CPL, IG e Rotas de Turismo e Rural.
</b>

<br />

A variação média do Faturamento:
![img1](image-1.png)

<br />
A média da UF é calculada:

![img2](image-2.png)

Onde:
-  j = 1, 2, 3....N (índice indicando cada projeto/processo)
-  i = 1, 2, 3.....n (índice indicando cada cliente da amostra)
-  n = Nº clientes com mensuração válida por Projeto ou Processo
-  N= Nº Projetos e Processos mensurados
-  c = Nº clientes prioritários dos projetos/processos


## Script

Segue abaixo os scritps que compõem a meta:

```SQL
SELECT *
FROM [dbo].[v_dim_execucao_meta_estadual]
where id_meta = 3
order by mes asc
```
<br />

**Observação: Neste indicador, temos apenas o valor consolidado no banco de metas, efetuado por uma empresa contratada**

<br />

Resultado do indicador:

```
Percentual(%)
```
***


# Receita Própria <a id='Receita'></a>

## Descrição da Meta

Captação de receita por meio da comercialização de produtos, serviços, espaços publicitários, mídias, merchandising, patrocínios, espaços de exposição e aluguéis.

## Fórmula de Cálculo
Fórmula de cálculo: receita líquida = <b>(A)− (B)  + (C)</b>, onde:

**(A)** Receita Total: Soma do valor bruto das vendas realizadas, deduzindo as devoluções, estornos, descontos e cancelamentos.
**(B)** Inadimplência Gerada: títulos vencidos que estão em aberto de 01/01/2024 até D-1, sendo D a data de apuração do indicador. 
**(C)** Recuperações de Créditos de anos anteriores: receita proveniente do pagamento de títulos vencidos em aberto de cinco anos anteriores à 2024. Dessa forma, o estoque de títulos que podem ser recuperados vai de 01/01/2019 até 31/12/2023.

Receita Líquida = Receita Total - Inadimplência Gerada + Recuperações de Créditos de anos anteriores.

<b>Observação: Não serão contabilizadas as receitas oriundas de alunos bolsistas.</b>

<br />

## Script
Segue abaixo os scripts que compõem a meta:

```SQL
SELECT *
FROM [Metas2024].[Execucao].[v_MetaEstadual]
WHERE IdMeta = 2
ORDER BY MES asc

-- Captação de Receita Própria -- 

SELECT FORMAT(sum(ValorReceitaBruta) - sum(ValorInadimplenciaGerada) + sum(ValorInadimplenciaRecuperada) - sum(valorbolsa), 'C', 'pt-br') as ReceitaLíquida
  FROM [Metas2024].[Execucao].[MetaReceita]

-- Receita Bruta Estadual --
SELECT FORMAT(SUM(ValorReceitaBruta), 'C', 'pt-br') as ReceitaBruta 
  FROM [Metas2024].[Execucao].[MetaReceita]

-- Receita Futura Estadual --
SELECT FORMAT(SUM(ValorReceitaFutura), 'C', 'pt-br') as ReceitaFutura
  FROM [Metas2024].[Execucao].[MetaReceita]

-- Inadimplência Gerada --
SELECT FORMAT(SUM(ValorInadimplenciaGerada), 'C', 'pt-br') as InadimplênciaGerada
  FROM [Metas2024].[Execucao].[MetaReceita]

-- Inadimplência Recuperada --
SELECT FORMAT(SUM(ValorInadimplenciaRecuperada), 'C', 'pt-br') as InadimplênciaRecuperada
  FROM [Metas2024].[Execucao].[MetaReceita]

-- Bolsistas e Anistias --
SELECT FORMAT(SUM(ValorBolsa), 'C', 'pt-br') as ValorBolsa
  FROM [Metas2024].[Execucao].[MetaReceita]

-- Receita Bruta Estadual (Consulta direta no RM pelo SQL) --
SELECT FORMAT(SUM(ValorContabil), 'C', 'pt-br') as ReceitaBruta
  FROM [HubDados].[CorporeRM].[VUtiEdwContabilizacaoAnaliticoNovo]
  where CodigoConta in ('4.1.2.1.01.001','4.1.2.1.01.002','4.1.2.1.01.003',
  '4.1.2.1.01.006','4.1.2.1.01.007','4.1.2.1.01.999','4.1.2.2.01.002',
  '4.1.2.1.01.010','4.1.2.1.01.011', '4.1.2.1.01.014', '4.1.2.1.01.008')  
  and anocontabil = '2024'

-- Receita Futura Estadual RAE (Aqui pedimos para a Mônica gerar o relatório no RM para batermos os valores) --
SELECT FORMAT(SUM(ValorReceitaFutura), 'C', 'pt-br') as ReceitaFutura
  FROM [Metas2024].[Execucao].[MetaReceita]
  where ValorReceitaFutura is not null
  and ValorReceitaFutura <> '0.0000'
  and GRANDES_CONTRATOS is null
  order by ReceitaFutura desc

-- Receita Futura Estadual Grandes Contratos (Aqui pedimos para a Mônica gerar o relatório no RM para batermos os valores) --
SELECT FORMAT(SUM(ValorReceitaFutura), 'C', 'pt-br') as ReceitaFutura
  FROM [Metas2024].[Execucao].[MetaReceita]
  where ValorReceitaFutura is not null
  and ValorReceitaFutura <> '0.0000'
  and GRANDES_CONTRATOS = 'X'
  order by ReceitaFutura desc

-- Inadimplência Gerada Estadual (Aqui pedimos para o Marcelo gerar o relatório no RM para batermos os valores) --
SELECT FORMAT(SUM(ValorInadimplenciaGerada), 'C', 'pt-br') as InadimplênciaGerada
  FROM [Metas2024].[Execucao].[MetaReceita]
  where ValorInadimplenciaGerada is not null
  and ValorInadimplenciaGerada <> '0.0000'
  order by InadimplênciaGerada desc

-- Inadimplência Recuperada Estadual (Aqui pedimos para o Marcelo gerar o relatório no RM para batermos os valores) --
SELECT FORMAT(SUM(ValorInadimplenciaRecuperada), 'C', 'pt-br') as InadimplênciaRecuperada
  FROM [Metas2024].[Execucao].[MetaReceita]
  where ValorInadimplenciaRecuperada is not null
  and ValorInadimplenciaRecuperada <> '0.0000'
  order by InadimplênciaRecuperada desc

-- Valor Bolsistas e Anistias Estadual (Consulta direta no RM pelo SQL) --
SELECT FORMAT(SUM(ValorBolsa), 'C', 'pt-br') as ValorBolsa
  FROM [Metas2024].[Execucao].[MetaReceita]
  where ValorBolsa is not null
  and ValorBolsa <> '0.0000'
  order by ValorBolsa desc


```
Resultado do indicador:

```
 Número
```



***
<br />


# Produtividade


## Descrição da Meta

Média das variações percentuais de produtividade do trabalho dos Pequenos Negócios atendidos pelo Sebrae.


## Fórmula de Cálculo

Programas considerados para esse indicador: 
 * ALI - Produtividade

![Calculo](image.png) <b>se compõe das variáveis:</b>

A mensuração da variação percentual de produtividade será obtida por meio da coleta de dados realizada pelos agentes do ALI. 


## Script


```SQL
SELECT *
FROM [Metas2024].[Execucao].[v_MetaEstadual]
WHERE IdMeta = 4
ORDER BY MES asc
```

<br />

**Observação: Neste indicador, temos apenas o valor consolidado no banco de metas, efetuado por uma empresa contratada**

<br />

Resultado do indicador:

```
Percentual (%)
```

# Cobertura no atendimento (ME + EPP)<a id='coberturaME-EPP'></a>



## Descrição da Meta

Percentual de microempresas (ME) e empresas de pequeno porte (EPP) distintas atendidas (market share) pelo Sebrae no ano.

## Fórmula de Cálculo

Pequenos negócios atendidos = <b>![img3](image-3.png)</b>

Contabilização do atendimento: será computado para o Sebrae de mesma UF do endereço do estabelecimento da empresa atendida, independentemente do Sebrae (Nacional ou UF) que realizou o atendimento. 

Ou seja, só serão contabilizadas as empresas atendidas com o endereço de estabelecimento de SP, independentemente do Sebrae (Nacional ou UF) que realizou o atendimento.

## Script


```SQL
SELECT *
FROM [Metas2024].[Execucao].[v_MetaEstadual]
WHERE IdMeta = 5
ORDER BY MES asc

63.393 / 2.726.705 = 2,32%

SELECT COUNT(distinct a.idPessoaJuridica) 
FROM [UAC].[dbo].[Atendimentos2024_RAE_Completa] a
INNER JOIN [HubDados].[RAE].[Contato] b ON a.idpessoajuridica = b.idpessoa
WHERE a.TipoCliente = 'PJ'
AND a.AtendimentoValido = 1
AND a.Instrumento NOT LIKE '%informação%'
AND a.Porte IN ('ME', 'EPP')
and a.Tipo_Atendimento not in ('Agendamento', 'Agendamento executado em Kit')
and a.Situacao_Atendimento in ('Concluído')
and a.Frequencia >= '75'
and a.idPessoaJuridica <> '0'
and b.UF = 'SP'
AND year(a.DataFimAtendimento) = 2024

```

Resultado do indicador:

```
Percentual (%)
```
***

# Cobertura de atendimentos a estudantes <a id='Estudantes'></a>


## Descrição da Meta

Percentual de estudantes distintos do ensino fundamental, médio e superior atendidos pelo Sebrae no ano.

## Fórmula de Cálculo
Cobertura de estudantes = ![img4](image-4.png)

O numerador é composto por:

  * Soma de alunos distintos do Ensino Fundamental beneficiados pelos programas da UCE e outras metodologias pedagógicas tanto presenciais quanto digitais (definidas pela Unidade Cultura Empreendedora) registrados no centro de custo do programa “00076.000004.017” e “00076.000005.017”. Também serão adicionados os alunos distintos do JEPP registrados no SAS.
 * Soma de alunos distintos do Ensino Médio beneficiados pelos programas da UCE e outras metodologias pedagógicas tanto presenciais quanto digitais (definidas pela Unidade Cultura Empreendedora) registrados no centro de custo programa “00076.000006.017” e “00076.000007.017”.
 * Soma de alunos distintos do Ensino Superior beneficiados pelos programas da UCE e outras metodologias pedagógicas tanto presenciais quanto digitais (definidas pela Unidade Cultura Empreendedora) registrados no centro de custo do programa “00076.000003.017”.

São contabilizados no denominador os estudantes matriculados nos ensinos fundamental, médio e superior, de acordo com os Censos da Educação Básica e Superior publicados pelo Instituto Nacional de Estudos e Pesquisas Educacionais (Inep) e o Ministério da Educação. A defasagem da disponibilidade da base de dados dos censos é uma limitação do indicador. Em anos em que não for possível obter as bases coincidentes com o ano de apuração, considerar-se-á as bases mais recentes disponíveis até o momento da apuração do indicador. Não são incluídos atendimentos a estudantes de ensino infantil, educação de jovens e adultos (EJA) e Ensino Especial.


## Script

```SQL
SELECT *
FROM [Metas2024].[Execucao].[v_MetaEstadual]
WHERE IdMeta = 6
ORDER BY MES asc

56 / 8.400.046 = 0,0007%

-- Alunos do Ensino Médio, Fundamental e Superior Registrados no RAE --
SELECT COUNT(distinct a.idPessoaFisica) 
FROM [UAC].[dbo].[Atendimentos2024_RAE_Completa] a
INNER JOIN [HubDados].[RAE].[Contato] b ON a.idPessoaFisica = b.idpessoa
WHERE a.TipoCliente = 'PF'
AND a.AtendimentoValido = 1
AND a.Instrumento NOT LIKE '%informação%'
and a.Tipo_Atendimento not in ('Agendamento', 'Agendamento executado em Kit')
and a.Situacao_Atendimento in ('Concluído')
and a.Frequencia >= '75'
and a.CentroCusto in ('00076.000004.017', '00076.000005.017', '00076.000006.017', '00076.000007.017', '00076.000003.017')
and b.UF = 'SP'

-- Alunos do Ensino Fundamental (JEPP) e Médio Registrados no SAS --
SELECT SUM(QuantidadeInscricoes) as QuantidadedeAlunos
FROM [HubDados].[SAS].[AtendimentoEducacao]

```

Resultado do indicador:

```
Percentual(%)
```

# Recomendação Sebrae (NPS)<a id='NPS'></a>


## Descrição da Meta

Indicador do grau de recomendação do Sebrae pelo cliente.

## Fórmula de Cálculo
NPS = **(% de clientes promotores − % de clientes detratores)**

Regras de contabilização: <b>
• Detratores: clientes que atribuem notas de 0 a 6;
• Neutros: clientes que atribuem notas de 7 a 8 
• Promotores: clientes que atribuem notas de 9 a 10 
</b>

• Pergunta realizada: Em uma escala de 0 a 10, o quanto o(a) Sr(a) recomendaria o SEBRAE para um amigo ou familiar? 

O resultado estadual é coletado após a publicação do Nacional no Painel de Metas Mobilizadoras organizacionais – Sebrae/NA. Para recortes regionais e demais analises o Sebrae/SP calcula a partir do cruzamento dos dados da pesquisa com os respectivos atendimentos identificados nas bases de dados do Sebrae/SP.

Alocação do Atendimento: para cada UF serão aferidos os atendimentos realizados pelo Sebrae/UF de acordo com o Sebrae Executor. 

Não são pesquisados clientes cujo atendimento é realizado pelos canais e-mail e redes sociais.


## Script


```SQL
SELECT *
FROM [Metas2024].[Execucao].[v_MetaEstadual]
WHERE IdMeta = 7
ORDER BY MES asc
```

<br />

**Observação: Neste indicador, temos apenas o valor consolidado no banco de metas, efetuado por uma empresa contratada**

<br />

Resultado do indicador:

```
Número
```
***

# Recorrência do Atendimento (NPS)<a id='Atendimento'></a>

## Descrição da Meta

Percentual de pequenos negócios distintos atendidos mais de uma vez em relação ao total de pequenos negócios distintos atendidos no ano-calendário.

## Fórmula de Cálculo
Recorrência do atendimento =  ![img5](image-5.png)

Contabilização do atendimento: será computado para o Sebrae de mesma UF do endereço do estabelecimento da empresa atendida, independentemente do Sebrae (Nacional ou UF) que realizou o atendimento. 

Ou seja, só serão contabilizadas as empresas atendidas com o endereço de estabelecimento de SP, independentemente do Sebrae (Nacional ou UF) que realizou o atendimento.


## Script


```SQL
SELECT *
FROM [Metas2024].[Execucao].[v_MetaEstadual]
WHERE IdMeta = 8
ORDER BY MES asc

-- Numerador -- 
SELECT COUNT(distinct a.idAtendimento) AS QuantidadedeAtendimentos, a.idPessoaJuridica
INTO #BASERECORR�NCIA
FROM [UAC].[dbo].[Atendimentos2024_RAE_Completa] a
INNER JOIN [HubDados].[RAE].[Contato] b ON a.idpessoajuridica = b.idpessoa
WHERE a.TipoCliente = 'PJ'
AND a.AtendimentoValido = 1
AND a.TipoCliente = 'PJ'
AND a.Instrumento NOT LIKE '%informação%'
AND a.porte in ('MEI', 'ME', 'EPP')
AND a.Tipo_Atendimento not in ('Agendamento', 'Agendamento executado em Kit')
AND a.Situacao_Atendimento in ('Concluído')
AND a.Frequencia >= '75'
AND a.idPessoaJuridica not in ('0')
and b.UF = 'SP'
AND year(a.DataFimAtendimento) = 2024
GROUP BY a.idPessoaJuridica
HAVING COUNT(distinct a.idAtendimento) >= 2;

SELECT COUNT(DISTINCT idpessoajuridica) ClientesDistintosNumerador
from #BASERECORR�NCIA

-- Denominador --
SELECT COUNT(distinct a.idPessoaJuridica) as ClientesDistintosDenominador
FROM [UAC].[dbo].[Atendimentos2024_RAE_Completa] a
INNER JOIN [HubDados].[RAE].[Contato] b ON a.idpessoajuridica = b.idpessoa
WHERE a.TipoCliente = 'PJ'
AND a.AtendimentoValido = 1
AND a.TipoCliente = 'PJ'
AND a.Instrumento NOT LIKE '%informação%'
AND a.porte in ('MEI', 'ME', 'EPP')
AND a.Tipo_Atendimento not in ('Agendamento', 'Agendamento executado em Kit')
AND a.Situacao_Atendimento in ('Concluído')
AND a.idPessoaJuridica not in ('0')
AND a.Frequencia >= '75'
and b.UF = 'SP'
AND year(a.DataFimAtendimento) = 2024

```

Resultado do indicador:

```
Percentual(%)
```
***

# Metas de Monitoramento (Não é Meta Mobilizadora de SP) <a id='Monitoramento'></a>

<br>

# Recursos na atividade Fim<a id='FIM'></a>

## Descrição da Meta

Percentual de recursos aplicados na atividade-fim do Sebrae.

## Fórmula de Cálculo
Recursos na atividade fim =  <b>![img6](image-6.png)</b>

Atividade-Fim corresponde a projetos e processos classificados nas finalidades: <b>
1) Atendimento Direto pelo Sebrae; 
2) Atendimento pela Rede Sebrae;
3) Desenvolvimento de Produtos e Serviços;
4) Articulação Institucional;
5) Inversão Financeira quando da aplicação de recursos em benefício dos Pequenos Negócios nas modalidades de crédito ou fundos (são 3.1.5.3 Transf. Externas Convênios com Outas Entidades, 5.1.5.1 FAMPE, 5.1.5.2 Fundo de Empresas Emergentes e 5.1.5.3 Microcrédito).</b> 

O valor resultante da somatória do numerador será dividido pela despesa orçamentária do Sebrae. São desconsideradas do denominador as despesas 3.1.4.1 Despesas tributárias, 3.1.7.1 Despesa com Provisão de I.R. sobre Aplicações Financeiras, 5.1.4.1 Depósitos Judiciais, 5.2.1.1 Reclamações Trabalhistas, 5.2.1.2 Ações Cíveis, 5.2.1.3 Autuações Fiscais e 5.2.1.4 Passivo Atuarial s/ Previ. Complementar. 

Como o repasse do Sebrae Nacional aos Sebrae/UF é registrado na origem e a aplicação deste recurso na atividade-fim ocorre no Sebrae/UF, para não haver duplicidade no cálculo do consolidado do Sistema Sebrae serão deduzidas as transferências intraSebrae, registradas nas contas 3.1.5.1 Interna CSO Lei 8.029/90 (45%), 3.1.5.2 Transf. Interna CSN Programas e Projetos Nacionais, 3.1.5.4 Transf. p/ Sebrae-UF Contr. Interno, 3.1.5.6 Transf. Interna CSN Agentes, 3.1.5.7 Transf. CSO Res. e CSN MP 907 CDN 20/92 (somente até 2022), 3.1.5.8 Transf. CSN - Res. CDN 20/92 (20%) e 3.1.5.9 Outras Transferências. 

O resultado estadual é coletado após a publicação do Nacional no Painel de metas mobilizadoras organizacionais – Sebrae/NA. 


## Script


```SQL
SELECT *
FROM [Metas2024].[Execucao].[v_MetaEstadual]
WHERE IdMeta = 9
ORDER BY MES asc
```

<br />

**Observação: Neste indicador, temos apenas o valor consolidado no banco de metas, sendo este calculado pelo SEBRAE Nacional**

<br />

Resultado do indicador:

```
Percentual(%)
```

***

# Volume de garantias de crédito contratadas<a id='volume'></a>

## Descrição da Meta

Variação percentual do volume de garantias de crédito contratadas pelas instituições financeiras conveniadas ao Fampe junto ao Sebrae.

## Fórmula de Cálculo

Garantias contratadas = <b>![img7](image-7.png)</b>

Serão computadas no somatório do indicador as garantias concedidas e registradas no SisFampe no período de análise e que não foram canceladas no período. Não serão consideradas as operações de transferência e renegociação, pois não alteram o volume de crédito contratado no período.

O resultado estadual é coletado após a publicação do Nacional no Painel de metas mobilizadoras organizacionais – Sebrae/NA. 

## Script


```SQL
SELECT *
FROM [Metas2024].[Execucao].[v_MetaEstadual]
WHERE IdMeta = 10
ORDER BY MES asc
```
<br />

**Observação: Neste indicador, temos apenas o valor consolidado no banco de metas, sendo este calculado pelo SEBRAE Nacional**

<br />

Resultado do indicador:

```
Percentual(%)
```

***
# Painel De Metas Mobilizadoras

Acessar:

<https://app.powerbi.com/groups/me/apps/818bd115-ccfe-40ba-b820-9aa4b11adc95/reports/c2569e43-a2d5-4639-bd65-6d76b0368fbc/ReportSection680013890a9fa2d1d4c4?experience=power-bi>

Para acessar a meta do ano
<a href='https://app.powerbi.com/groups/me/apps/818bd115-ccfe-40ba-b820-9aa4b11adc95/reports/c2569e43-a2d5-4639-bd65-6d76b0368fbc/ReportSection5e0de61f836e819a2e25?experience=power-bi'>- MOBILIZADORAS RESUMO</a>

Para acessas a meta mês a mês
<a href='https://app.powerbi.com/groups/me/apps/818bd115-ccfe-40ba-b820-9aa4b11adc95/reports/c2569e43-a2d5-4639-bd65-6d76b0368fbc/ReportSection6035af832781ad83031a?experience=power-bi'>- MOBILIZADORAS DETALHE</a>

## Contribuição

Todas as contribuições serão bem vindas!

Qualquer sugestão, melhoría ou dúvidas a melhor forma de contato é pelo email sp-monitoramento@sebraesp.com.br

Obrigado pela leitura!

