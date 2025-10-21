# TPC5: Aplicação para gestão de alunos 

## Ana Teresa da Silva Ribeiro

## Resumo
O TPC5 consistiu no desenvolvimento do código de uma aplicação, em Python, para criar uma aplicação de gestão de gestão de alunos

### O programa 
Considere que o modelo do aluno e da turma têm a seguinte estrutura:

`aluno = (nome, id, [notaTPC, notaProj, notaTeste])`

`turma = [aluno]`

* Cria uma aplicação que coloca no monitor o seguinte menu de operações:
    - 1: Criar uma turma;
    - 2: Inserir um aluno na turma;
    - 3: Listar a turma;
    - 4: Consultar um aluno por id;
    - 8: Guardar a turma em ficheiro;
    - 9: Carregar uma turma dum ficheiro;
    - 0: Sair da aplicação
* No fim de executar a operação selecionada, a aplicação deverá colocar novamente o menu e pedir ao utilizador a opção para continuar;
* Utiliza a tua aplicação para criar uma turma com 5 alunos.

## Resultado
```python
def Menu():
    print("--------- Menú --------")
    print("1.Criar uma turma")
    print("2.Inserir um aluno na turma")
    print("3.Listar a turma")
    print("4.Consultar um aluno por id")
    print("5.Guardar a turma em ficheiro")
    print("6.Carregar a turma de um ficheiro")
    print("0.Sair da aplicação")
    print("----------------------")

def criarTurma():
    turma = []
    return turma

def inserirAluno():
    turma = []
    nome = input("Insira o nome de um aluno na turma:")
    id = input("ID do aluno:")
    notaTPC = float(input("Introduza a nota do TPC do aluno:"))
    notaProjeto = float(input("Introduza a nota do projeto do aluno:"))
    notaTeste = float(input("Introduza a nota do teste do aluno:"))

    aluno = (nome, id, [notaTPC, notaProjeto, notaTeste])
    turma.append(aluno)

    print(f"Aluno {nome} inserido na turma!")
    return turma

def listarTurma(turma):
    if turma == []:
        print("Ainda não existem alunos na turma.")
    else:
        print("---------- Listagem da Turma ----------")
        for aluno in turma:
            print(f"Nome: {aluno[0]} | ID: {aluno[1]} | Nota TPC: {aluno[2][0]} | Nota Projeto: {aluno[2][1]} | Nota Teste: {aluno[2][2]} ")
        print("--------------------")

def consultaralunoID(turma):
    consultarID = input("Introduza o ID do aluno")
    encontrado = False
    for aluno in turma:
        if consultarID == aluno[1]:
            encontrado = True
            print("Aluno encontrado")
            print(f"Nome: {aluno[0]} | ID: {aluno[1]} | Nota TPC: {aluno[2][0]} | Nota Projeto: {aluno[2][1]} | Nota Teste: {aluno[2][2]}")
    if not encontrado:
        print("O aluno não se encontra nesta turma")
    
def guardarFicheiro(turma):
    nomeFicheiro = input("Nome do ficheiro para guardar a turma (nomeficheiro.txt)")

    ficheiro = open(nomeFicheiro, "w", encoding = "utf-8")      # encoding = "utf-8" ----> para evitar erros com acentos, cedilhas, letras maiusculas....
    for aluno in turma:
        linha = f"Nome: {aluno[0]} | ID: {aluno[1]} | Nota TPC: {aluno[2][0]} | Nota Projeto: {aluno[2][1]} | Nota Teste: {aluno[2][2]}"
        ficheiro.write(f"{linha}\n")
    ficheiro.close()
    print(f"A turma foi guardada no ficheiro {nomeFicheiro}.")

def carregaFicheiro():
    nomeFicheiro = input("Introduza o nome do ficheiro que deseja carregar (nomeficheiro.txt):")
    turma = []

    ficheiro = open(nomeFicheiro, "r", encoding = "utf-8")
    for line in ficheiro:
       nome, id, notas = line.split("|")
       notaTPC, notaProjeto, notaTeste = notas.split(";")
       notasAluno = [float(notaTPC), float(notaProjeto), float(notaTeste)]
       turma.append((nome, id, notasAluno))
    ficheiro.close()

    print("Ficheiro carregado com sucesso!")
    print(turma)
    return turma

def Main():
    turma = []
    cond = True
    while cond:
        Menu()
        opcao = input("Introduza a opção pretnedida:")

        if opcao == "1":
            turma = criarTurma()
            print("Turma criada!")
        elif opcao == "2":
            turma = inserirAluno()
        elif opcao == "3":
            listarTurma(turma)
        elif opcao == "4":
            consultaralunoID(turma)
        elif opcao == "5":
            guardarFicheiro(turma)
        elif opcao == "6":
            turma = carregaFicheiro()
        elif opcao == "0":
            cond = False
            print("Até à próxima!")

Main()




