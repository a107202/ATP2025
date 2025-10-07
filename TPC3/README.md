# TPC3: Aplicação para manipulação de listas de inteiros

## Ana Teresa da Silva Ribeiro

## Resumo
O TPC3 consistiu no desenvolvimento do código de uma aplicação, em Python, para manipulação de listas de inteiros:

### O programa 

- Crie uma aplicação em Python que coloca no monitor o seguinte menu:
    * (1) Criar Lista 
    * (2) Ler Lista
    * (3) Soma
    * (4) Média
    * (5) Maior
    * (6) Menor
    * (7) estaOrdenada por ordem crescente
    * (8) estaOrdenada por ordem decrescente
    * (9) Procura um elemento
    * (0) Sair
- O utilizador irá escolher uma das opções introduzindo o número correspondente;
- Se a opção não for sair, a aplicação executa a operação pretendida, apresenta o resultado e a seguir apresenta de novo o menu;
- Se a opção for sair, a aplicação termina colocando uma mensagem no monitor.

* No desenvolvimento da aplicação deverá ter em atenção o seguinte:
    - A aplicação terá uma variável interna para guardar uma lista de números;
    - Na opção 1, deverá ser criada uma lista de números aleatórios entre 1 e 100 que será guardada na variável interna;
    - Na opção 2, deverá ser criada uma lista com números introduzidos pelo utilizador, que será guardada na variável interna;
    - Nestas primeiras opções, se a variável interna já tiver uma lista, esta será sobreposta/apagada pela nova lista;
    - Na opção 3, será calculada a soma dos elementos na lista no momento;
    - Na opção 4, será calculada a média dos elementos na lista no momento;
    - Na opção 5, será calculado o maior elemento da lista no momento;
    - Na opção 6, será calculado o menor elemento da lista no momento;
    - Na opção 7, a aplicação deverá indicar (Sim/Não) se a lista está ordenada por ordem crescente;
    - Na opção 8, a aplicação deverá indicar (Sim/Não) se a lista está ordenada por ordem decrescente;
    - Na opção 9, a aplicação irá procurar um elemento na lista, se o encontrar deverá devolver a sua posição, devolverá -1 se o elemento não estiver na lista;
    - Se o utilizador selecionar a opção 0, a aplicação deverá terminar mostrando a lista que está nesse momento guardada.
## Resultados
```python
def Menu():
    print("--------MENU--------")
    print("(1)Criar lista")
    print("(2) Ler lista")
    print("(3) Soma")
    print("(4) Média")
    print("(5) Maior")
    print("(6) Menor")
    print("(7) Está ordenada por ordem crescente")
    print("(8) Está ordenada por ordem decrescente")
    print("(9) Procura um elemento")
    print("(10) Sair")
    print("--------------------")

def Criar_Lista():
    import random
    N = int(input("Quantos números deseja que tenha a sua lista?"))
    lista = []
    i = 0
    while i < N:
        x = random.randint(1,100)
        lista.append(x)
        i = i + 1
    return lista

def Ler_Lista():
    lista = []
    entrada = input("Introduza um número da sua lista. Escreva <<fim>> quando não quiser introduzir mais números.")
    while entrada != "fim":
        x = int(entrada)
        lista.append(x)
        entrada = input("Introduza um número da sua lista. Escreva <<fim>> quando não quiser introduzir mais números.")
    return lista

def Soma_Lista(lista):
    soma = 0
    i = 0
    while i < len(lista):
        soma = soma + lista[i]
        i = i + 1
    return soma

def Media_Lista(lista):
    soma = Soma_Lista(lista)
    media = 0
    if len(lista) != 0:
        media = soma/len(lista)
    return media

def Maior_Lista(lista):
    maior = lista[0]
    i = 1
    while i < len(lista):
        if lista[i] > maior:
            maior = lista[i]
        i = i + 1
    return maior

def Menor_Lista(lista):
    menor = lista[0]
    i = 1
    while i < len(lista):
        if lista[i] < menor:
            menor = lista[i]
        i = i + 1
    return menor

def Esta_Ordenada_Por_Ordem_Crescente(lista):
    for i in range(len(lista) - 1):
        if lista[i] > lista[i + 1]:
            return "Não"
    return "Sim"

def Esta_Ordenada_Por_Ordem_Decrescente(lista):
    for i in range(len(lista) - 1):
        if lista[i] < lista[i + 1]:
            return "Não"
    return "Sim"

def Procurar_Elemento(lista):
    x = int(input("Qual é o elemento que pretende encontrar na lista?"))
    if x in (lista):
        return lista.index(x)
    else: return "-1"

def Main():
    lista = []
    cond = True

    while cond:
        Menu()
        opção = input("Introduza a opção desejada.")

        if opção == "1":
            lista = Criar_Lista()
            print(lista)
        elif opção == "2":
            lista = Ler_Lista()
            print(lista)
        elif opção == "3":
            res = Soma_Lista(lista)
            print(res)
        elif opção == "4":
            res = Media_Lista(lista)
            print(res)
        elif opção == "5":
            res = Maior_Lista(lista)
            print(res)
        elif opção == "6":
            res = Menor_Lista(lista)
            print(res)
        elif opção == "7":
            res = Esta_Ordenada_Por_Ordem_Crescente(lista)
            print(res)
        elif opção == "8":
            res = Esta_Ordenada_Por_Ordem_Decrescente(lista)
            print(res)
        elif opção == "9":
            res = Procurar_Elemento(lista)
            print(res)
        elif opção == "10":
            cond = False
            print ("Até à próxima!")

Main()
