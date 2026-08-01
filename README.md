from typing import Callable


def soma(a: float, b: float) -> float:
    return a + b


def subtracao(a: float, b: float) -> float:
    return a - b


def multiplicacao(a: float, b: float) -> float:
    return a * b


def divisao(a: float, b: float) -> float:
    if b == 0:
        raise ZeroDivisionError("Não é possível dividir por zero.")
    return a / b


OPERACOES: dict[str, tuple[str, Callable[[float, float], float]]] = {
    "1": ("Soma", soma),
    "2": ("Subtração", subtracao),
    "3": ("Multiplicação", multiplicacao),
    "4": ("Divisão", divisao),
}


def ler_numero(mensagem: str) -> float:
    while True:
        try:
            return float(input(mensagem).replace(",", "."))
        except ValueError:
            print("Entrada inválida. Digite um número válido.\n")


def exibir_menu() -> None:
    print("=" * 40)
    print("        CALCULADORA PROFISSIONAL")
    print("=" * 40)

    for codigo, (nome, _) in OPERACOES.items():
        print(f"{codigo} - {nome}")

    print("0 - Sair")
    print("=" * 40)


def main() -> None:
    while True:
        exibir_menu()

        opcao = input("Escolha uma opção: ").strip()

        if opcao == "0":
            print("\nPrograma encerrado.")
            break

        if opcao not in OPERACOES:
            print("\nOpção inválida.\n")
            continue

        numero1 = ler_numero("Primeiro número: ")
        numero2 = ler_numero("Segundo número: ")

        nome_operacao, funcao = OPERACOES[opcao]

        try:
            resultado = funcao(numero1, numero2)
            print(f"\n{nome_operacao}")
            print(f"Resultado: {resultado:.2f}\n")
        except ZeroDivisionError as erro:
            print(f"\nErro: {erro}\n")


if __name__ == "__main__":
    main()
