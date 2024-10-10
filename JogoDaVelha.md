import random

def exibir_tabuleiro(tabuleiro):
    for linha in tabuleiro:
        print("|".join(linha))
        print("-" * 5)

def verificar_vencedor(tabuleiro, jogador):
    for linha in tabuleiro:
        if all([c == jogador for c in linha]):
            return True
    for col in range(3):
        if all([tabuleiro[linha][col] == jogador for linha in range(3)]):
            return True
    if tabuleiro[0][0] == tabuleiro[1][1] == tabuleiro[2][2] == jogador:
        return True
    if tabuleiro[0][2] == tabuleiro[1][1] == tabuleiro[2][0] == jogador:
        return True
    return False

def tabuleiro_cheio(tabuleiro):
    return all([all([coluna != " " for coluna in linha]) for linha in tabuleiro])

def jogada_maquina(tabuleiro):
    while True:
        linha = random.randint(0, 2)
        coluna = random.randint(0, 2)
        if tabuleiro[linha][coluna] == " ":
            tabuleiro[linha][coluna] = "O"
            break

def jogo_da_velha():
    tabuleiro = [[" " for _ in range(3)] for _ in range(3)]

    print("Jogo da Velha")
    exibir_tabuleiro(tabuleiro)

    jogador_atual = "X"
    while True:
        if jogador_atual == "X":
            linha = int(input("Digite a linha (0, 1, 2): "))
            coluna = int(input("Digite a coluna (0, 1, 2): "))
            if tabuleiro[linha][coluna] == " ":
                tabuleiro[linha][coluna] = "X"
            else:
                print("Essa posição já está ocupada. Tente novamente.")
                continue
        else:
            print("Jogada da máquina:")
            jogada_maquina(tabuleiro)

        exibir_tabuleiro(tabuleiro)

        if verificar_vencedor(tabuleiro, jogador_atual):
            print(f"O jogador {jogador_atual} venceu!")
            break

        if tabuleiro_cheio(tabuleiro):
            print("O jogo empatou!")
            break

        jogador_atual = "O" if jogador_atual == "X" else "X"

if __name__ == "__main__":
    jogo_da_velha()
