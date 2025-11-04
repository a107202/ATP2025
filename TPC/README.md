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
lista1 = [1, 2, 3, 4, 5]
lista2 = [4, 5, 6, 7, 8]  
ncomuns = [...]


naoComuns = [n for n in lista1 if n not in lista2] + [n for n in lista2 if n not in lista1]
print(naoComuns)
```

- b) Lista formada pelas palavras do texto compostas por mais de 3 letras:
```
texto = """Vivia há já não poucos anos algures num concelho do Ribatejo 
    um pequeno lavrador e negociante de gado chamado Manuel Peres Vigário"""
lista = [...]


lista = [palavra for palavra in texto.split() if len(palavra) > 3]
print(lista)
```

- c) Lista formada por pares do tipo (índice, valor) com os valores da lista dada:
```
lista = ['anaconda', 'burro', 'cavalo', 'macaco']
listaRes = [...]


listaRes = [(indice, valor) for indice, valor in enumerate(lista)]
print(listaRes)
```



tpc-2. À semelhança do que foi feito nas aulas, realize as seguintes tarefas:

- a) Especifique uma função que dada uma string e uma substring não vazia, calcula  o número de vezes em que a substring aparece na string, sem que haja sobreposição de substrings:
```
def strCount(s, subs):
    res = 0
    i = 0
    while i <= len(s) - len(subs):
        if s[i: i + len(subs)] == subs:
            res = res + 1
            i = i + len(subs)
        else: i = i + 1

    return res

strCount("catcowcat", "cat") 
strCount("catcowcat", "cow") 
strCount("catcowcat", "dog")
```

- b) Especifique uma função que recebe uma lista de números inteiros positivos e devolve o menor produto que for possível calcular multiplicando os 3 menores inteiros da lista:
```
def produtoM3(lista):
    lista.sort()
    return lista[0] * lista[1] * lista[2]

print(produtoM3([12,3,7,10,12,8,9]))
```

- c) Especifique uma função que dado um número inteiro positivo, repetidamente adiciona os seus dígitos até obter apenas um dígito que é retornado como resultado:
```
def reduxInt(n):
    while n >= 10:      
        soma = 0
        for digito in str(n):       
            soma = soma + int(digito)       
        n = soma

    return n

print(reduxInt(38))
```

- d) Especifique uma função que recebe duas strings, `string1` e `string2`, e devolve o índice da primeira ocorrência de `string2` em `string1`, caso não ocorra nenhuma vez a função deverá retornar `-1`:
```
def myIndexOf(s1, s2):
    i = 0
    while i <= (len(s1) - len(s2)):
        if s1[i: i + len(s2)] == s2:
            return i
        i = i + 1
    return -1

print(myIndexOf("Hoje está um belo dia de sol!", "belo"))
```



tpc-3. A Rede Social
```
MyFaceBook = [{
        'id': 'p1', 
        'conteudo': 'A tarefa de avaliação é talvez a mais ingrata das tarefas que um professor tem de realizar...', 
        'autor': 'jcr', 
        'dataCriacao': '2023-07-20', 
        'comentarios': [
            {
                'comentario': 'Completamente de acordo...',
                'autor': 'prh'
            },
            {
                'comentario': 'Mas há quem goste...',
                'autor': 'jj'
            }
        ]},
        {
            'id': 'p2',
        
        },
        ...
        ]
```

- a) `quantosPost`, que indica quantos posts estão registados:
```
def quantosPost(redeSocial):
    return len(redeSocial)

print(quantosPost(MyFaceBook))
```

- b)  `postsAutor`, que devolve a lista de posts de um determinado autor:
```
def postsAutor(redeSocial, autor):
    return [posts for posts in redeSocial if posts["autor"] == autor]

print(postsAutor(MyFaceBook, "jcr"))
```

- c) `autores`, que devolve a lista de autores de posts ordenada alfabeticamente:
```
def autores(redeSocial):
    listaAutores = [post["autor"] for post in redeSocial]
    return  sorted(listaAutores)

print(autores(MyFaceBook))
```

- d) `insPost`, que acrescenta um novo post à rede social a partir dos parâmetros recebidos e devolve a nova rede social. 
    O campo `id` devrá ser calculado a partir dos já existentes, por exemplo, se a rede tiver posts com id `p1`, `p2` e `p3`, o novo `id` deverá ser `p4`.
```
def insPost(redeSocial, conteudo, autor, dataCriacao, comentarios):
    if redeSocial:
        maxID = max(insPost(["id"][1:]))
        novoID = f"p{maxID + 1}"
    else:
        novoID = "p4"

    novoPost = {
        'id': novoID,
        "conteudo" : conteudo,
        "autor" : autor,
        "dataCriacao" : dataCriacao,
        "comentarios" : comentarios
   }

    redeSocial.append(novoPost)
    return redeSocial

print(MyFaceBook)
```

- e)  `remPost`, que remove um post da rede, correspondente ao `id` recebido.
```
def remPost(redeSocial, id):
    redeAtualizada = [post for post in redeSocial if post["id"] != id]
    return redeAtualizada

print(remPost(MyFaceBook, "p1"))
```

- f) `postsPorAutor`, que devolve uma distribuição de posts por autor (à semelhança do que foi feito nas aulas).
```
def postsPorAutor(redeSocial):
    distribuicao = {}
    for post in redeSocial:
        autor = post['autor']
        if autor not in distribuicao:
            distribuicao[autor] = -1
        else: 
            distribuicao[autor] = distribuicao[autor] + 1
    return distribuicao

print(postsPorAutor(MyFaceBook))
```

- g) `comentadoPor`, que recebe um autor e devolve a lista de posts comentados por esse autor.
```
def comentadoPor(redeSocial, autor):
    postsComentados = []
    for post in redeSocial:
        encontrado = False
        for comentario in post["comentarios"]:
            if comentario["autor"] == autor:
                rncontrado = True
            if encontrado:
                postsComentados.append(post)
    return postsComentados
```
