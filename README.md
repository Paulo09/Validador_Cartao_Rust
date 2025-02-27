﻿# Validador_Cartao_Rust
Para criar um validador de cartão de crédito em Rust, vamos implementar o algoritmo de Luhn. O algoritmo de Luhn é uma forma simples de validação de número de cartão de crédito, que verifica se a sequência de números é válida.

Passo a Passo
Criar um Novo Projeto Rust

Primeiro, crie um novo projeto Rust:

bash
Copiar código
cargo new card_validator
cd card_validator
Implementar o Algoritmo de Luhn

Abra o arquivo src/main.rs e substitua o conteúdo com a implementação do validador de cartão de crédito:

rust
Copiar código
fn main() {
    let card_number = "4532015112830366";
    if is_valid_credit_card(card_number) {
        println!("O número do cartão {} é válido.", card_number);
    } else {
        println!("O número do cartão {} é inválido.", card_number);
    }
}

fn is_valid_credit_card(card_number: &str) -> bool {
    let card_number = card_number.replace(" ", "");
    if card_number.chars().any(|c| !c.is_digit(10)) {
        return false;
    }

    let mut sum = 0;
    let mut alternate = false;

    for c in card_number.chars().rev() {
        let mut n = c.to_digit(10).unwrap();

        if alternate {
            n *= 2;
            if n > 9 {
                n -= 9;
            }
        }

        sum += n;
        alternate = !alternate;
    }

    sum % 10 == 0
}
Explicação do Código
Função main:

let card_number = "4532015112830366";: Definimos um número de cartão de crédito para testar.
if is_valid_credit_card(card_number) { ... }: Chamamos a função is_valid_credit_card para verificar se o número do cartão é válido e imprimimos a mensagem apropriada.
Função is_valid_credit_card:

let card_number = card_number.replace(" ", "");: Remove espaços em branco do número do cartão, se houver.
if card_number.chars().any(|c| !c.is_digit(10)) { return false; }: Verifica se todos os caracteres são dígitos.
let mut sum = 0; let mut alternate = false;: Inicializa a soma e a flag alternada.
for c in card_number.chars().rev() { ... }: Itera pelos dígitos do cartão de trás para frente.
let mut n = c.to_digit(10).unwrap();: Converte o caractere em um dígito.
if alternate { ... }: Se alternate for verdadeiro, dobra o valor do dígito e subtrai 9 se o resultado for maior que 9.
sum += n; alternate = !alternate;: Adiciona o valor à soma e alterna a flag.
sum % 10 == 0: Retorna verdadeiro se a soma for divisível por 10, indicando que o número do cartão é válido.
Executar a Aplicação
Para executar a aplicação, use o comando:

bash
Copiar código
cargo run
Você deve ver uma saída indicando se o número do cartão é válido ou inválido:

arduino
Copiar código
O número do cartão 4532015112830366 é válido.
Isso completa a implementação de um validador de cartão de crédito em Rust usando o algoritmo de Luhn.

