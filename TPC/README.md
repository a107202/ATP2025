# TPC7: Aplicação para gestão da meteorologia

## Ana Teresa da Silva Ribeiro

## Resumo
O TPC7 consistiu em resolver um teste de aferição sobre os conhecimentos adquiridos.

### O programa
- Listas em compreensão;
- Funções;
- Dicionários.

## Resultados
tpc-1. Especifique as seguintes listas em compreensão:

- a) Lista formada pelos elementos que não são comuns às duas listas:
```
naoComuns = [n for n in lista1 if n not in lista2] + [n for n in lista2 if n not in lista1]
print(naoComuns)
```
- b) Lista formada pelas palavras do texto compostas por mais de 3 letras:
```
lista = [palavra for palavra in texto.split() if len(palavra) > 3]
print(lista)
```

