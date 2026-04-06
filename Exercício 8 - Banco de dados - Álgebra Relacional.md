


**Nome:** Gabriel Augusto de Lima Maia

Seja o banco de dados de uma cinemateca representado pelo seguinte esquema relacional:

Estúdio (~~CodEst~~, NomeEst)
Filme (~~CodFilme~~, Título, Diretor, Genero, AnoProd, CodEst)
	Filme [CodEst] → Estudio [CodEst]
Ator (~~CodAtor~~, Nome)
Elenco (~~CodFilme~~, ~~CodAtor~~, Salário)
	Elenco [CodAtor] → Ator [CodAtor]
	Elenco [CodFilme] → Filme [CodFilme]
	
Expresse, com operadores da Álgebra Relacional, as seguintes consultas:

1) Liste o título e o gênero dos filmes produzidos pelo estúdio Paramount Pictures neste ano.

	$\pi_{Titulo,Genero}(\sigma_{AnoProd=2025}(Filme)\bowtie \sigma_{NomeEst='Paramount Pictures'}(Estudio) )$

2)  Liste o nome e o salário dos atores que atuaram no filme Matrix Revolutions.
   
	$\pi_{Nome,Salário}(Ator \bowtie (Elenco \bowtie \sigma_{Titulo='Matrix Revolutions}Filme))$
   
   
3)  Liste o título e o ano de produção de todos os filmes cujos diretores também fizeram parte do elenco.

	$\pi_{Título,AnoProd}(\sigma_{Filme.Diretor=Ator.Nome}(Filme \bowtie_{Filme.CodFilme=Elenco.CodFilme}(Elenco \bowtie Ator))$
	
4) Liste o nome dos atores que já atuaram em algum filme dirigido por Clint Eastwood.

	 $\pi_{Nome}(Ator \bowtie(Elenco \bowtie \sigma_{Diretor='Clint Eastwood'}(Filme)))$
	 
5)  Liste o nome dos atores que já atuaram em filmes produzidos pela MGM, mas nunca foram dirigidos por Clint Eastwood.
	
	$\text{ElencoClint} \leftarrow  \pi_{CodAtor}(Elenco \bowtie \sigma_{Diretor='ClintEastwood'}(Filme))$
	$ElencoEstMGM \leftarrow \pi_{CodAtor}(Elenco \bowtie Filme \bowtie \sigma_{NomeEst='MGM'}(Estudio))$
	$\pi_{Nome}(Ator \bowtie (ElencoEstMGM - ElencoClint))$
	
6) Liste o nome dos atores que na década de 90 atuaram em filmes produzidos pela MGM e pela Universal.

   $$
\begin{aligned}
\text{FilmesMGM} &\leftarrow \sigma_{\text{NomeEst}='MGM'}(\text{Estúdio}) \bowtie \sigma_{1990 \leq \text{AnoProd} \leq 1999}(\text{Filme}) \\
\text{FilmesUniversal} &\leftarrow \sigma_{\text{NomeEst}='Universal'}(\text{Estúdio}) \bowtie \sigma_{1990 \leq \text{AnoProd} \leq 1999}(\text{Filme}) \\
\\
\text{AtoresMGM} &\leftarrow \pi_{\text{CodAtor}} (\text{Elenco} \bowtie \text{FilmesMGM}) \\
\text{AtoresUniversal} &\leftarrow \pi_{\text{CodAtor}} (\text{Elenco} \bowtie \text{FilmesUniversal}) \\
\\
\text{AtoresComuns} &\leftarrow \text{AtoresMGM} \cap \text{AtoresUniversal} \\
\\
\pi_{\text{Nome}} &(\text{Ator} \bowtie \text{AtoresComuns})
\end{aligned}
$$


7) Apresente a quantidade de filmes já produzidos pelo estúdio MGM, por ano. Ano e o nome do estúdio devem aparecer no resultado.
   
  
$\text{FilmesMGM} \leftarrow \sigma_{NomeEst='MGM'}(Estudio) \bowtie Filme$
$\text{AnosMGM} \leftarrow \pi_{AnoProd,NomeEst}(\text{FilmesMGM})$
$\gamma_{AnoProd,NomeEst;count(codFilme)\to QtdFilmes}(FilmesMGM)$

