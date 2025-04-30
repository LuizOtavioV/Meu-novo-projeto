/* projeto de validador de CPF pelos 2 ultimos digitos */


#include <iostream>
using namespace std;

int main() {
    int d1, d2, d3, d4, d5, d6, d7, d8, d9; 
    int soma1, resto1, dv1, soma2, resto2, dv2;
    
    // Solicita ao usuário os 8 ou 9 primeiros dígitos do CPF
    long cpf;
    cout << "Digite os 8 ou 9 primeiros dígitos do CPF (entre 10000000 e 999999999): ";
    cin >> cpf;

    // Preenche com zero à esquerda se tiver apenas 8 dígitos
    if (cpf >= 10000000 && cpf < 100000000) {
        cpf = cpf + 1000000000; // Adiciona um 0 à esquerda virtualmente (ver abaixo)
    }

    // Verifica se o número digitado tem exatamente 9 dígitos agora
    if (cpf < 100000000 || cpf > 9999999999) {
        cout << "Valor inválido! O número deve ter 8 ou 9 dígitos." << endl;
        return 1; // Encerra o programa com erro
    }

    // Extração dos 9 dígitos individualmente (sem uso de arrays)
    if (cpf > 999999999) {
        cpf = cpf % 1000000000; // Remove o 1 "falso" que foi somado para simular o 0 à esquerda
        d1 = 0;
    } else {
        d1 = cpf / 100000000;
    }

    d2 = (cpf / 10000000) % 10;
    d3 = (cpf / 1000000) % 10;
    d4 = (cpf / 100000) % 10;
    d5 = (cpf / 10000) % 10;
    d6 = (cpf / 1000) % 10;
    d7 = (cpf / 100) % 10;
    d8 = (cpf / 10) % 10;
    d9 = cpf % 10;

    // Cálculo do primeiro dígito verificador
    soma1 = d1 * 10 + d2 * 9 + d3 * 8 + d4 * 7 + d5 * 6 + d6 * 5 + d7 * 4 + d8 * 3 + d9 * 2;
    resto1 = soma1 % 11;

    if (resto1 < 2) {
        dv1 = 0;
    } else {
        dv1 = 11 - resto1;
    }

    // Cálculo do segundo dígito verificador
    soma2 = d1 * 11 + d2 * 10 + d3 * 9 + d4 * 8 + d5 * 7 + d6 * 6 + d7 * 5 + d8 * 4 + d9 * 3 + dv1 * 2;
    resto2 = soma2 % 11;

    if (resto2 < 2) {
        dv2 = 0;
    } else {
        dv2 = 11 - resto2;
    }

    // Exibição do CPF completo no formato correto
    cout << "CPF completo: " << d1 << d2 << d3 << "." << d4 << d5 << d6 << "." << d7 << d8 << d9 << "-" << dv1 << dv2 << endl;

    return 0;
}
