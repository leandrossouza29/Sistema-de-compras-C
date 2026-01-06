este código foi testado efeito através do compilador Programiz

#include <stdio.h>
#include <time.h>

int main() {

    int continuar;

    do {

        int qtdProdutos, i, produto, regiao;
        float precoProduto = 0, somaProdutos = 0, frete = 0, total = 0;

        int codigo;
        char nome[30];
        float peso, pesoTotal = 0;

        printf("================== Loja TechRJ =================\n");

        printf("\n=========== Produtos em promocao ===========\n");
        printf("1 - Mouse Gamer de R$110.00 por R$ 80.00\n");
        printf("2 - Teclado Mecanico de R$300.00 por R$ 250.00\n");
        printf("3 - notebook Dell  de R$1250.00 por R$ 800.00\n");
        printf("============================================\n");

        printf("\nQuantos produtos deseja comprar?: ");
        scanf("%d", &qtdProdutos);

        for (i = 1; i <= qtdProdutos; i++) {
            printf("\nEscolha o produto %d:\n", i);
            printf("1 - Mouse Gamer (R$ 80.00)\n");
            printf("2 - Teclado Mecanico (R$ 250.00)\n");
            printf("3 - notebook Dell (R$ 800.00)\n");
            printf("Digite sua opcao: ");
            scanf("%d", &produto);

            switch (produto) {
                case 1:
                    precoProduto = 80.00;
                    codigo = 101;
                    peso = 0.250;
                    sprintf(nome, "Mouse Gamer");
                    break;

                case 2:
                    precoProduto = 250.00;
                    codigo = 202;
                    peso = 0.850;
                    sprintf(nome, "Teclado Mecanico");
                    break;

                case 3:
                    precoProduto = 180.00;
                    codigo = 303;
                    peso = 2.120;
                    sprintf(nome, "notebook Dell");
                    break;

                default:
                    printf("Opcao invalida! Produto ignorado.\n");
                    continue;
            }

            printf("\n===== INFORMACOES DO PRODUTO %d =====\n", i);
            printf("Codigo: %d\n", codigo);
            printf("Nome: %s\n", nome);
            printf("Peso: %.3f kg\n", peso);
            printf("Preco: R$ %.2f\n", precoProduto);

            somaProdutos += precoProduto;
            pesoTotal += peso;  

            printf("Subtotal atual: R$ %.2f\n", somaProdutos);
        }

        printf("\nPeso total da compra: %.3f kg\n", pesoTotal);

        printf("\nAgora selecione a região para entrega:\n");
        printf("1 - Norte\n");
        printf("2 - Nordeste\n");
        printf("3 - Sudeste\n");
        printf("4 - Sul\n");
        printf("Digite sua opcao: ");
        scanf("%d", &regiao);

        if (pesoTotal > 2.0) {
            
            switch (regiao) {
                case 1: frete = 55.00; break; 
                case 2: frete = 60.00; break; 
                case 3: frete = 45.00; break; 
                case 4: frete = 50.00; break; 
                default:
                    printf("Opcao invalida! Frete definido como 0.\n");
                    frete = 0;
            }
            printf("\nFrete aplicado: PESO > 2KG\n");
        } 
        else {
            
            switch (regiao) {
                case 1: frete = 35.00; break; 
                case 2: frete = 40.00; break; 
                case 3: frete = 25.00; break; 
                case 4: frete = 30.00; break; 
                default:
                    printf("Opcao invalida! Frete definido como 0.\n");
                    frete = 0;
            }
            printf("\nFrete aplicado: PESO <= 2KG\n");
        }

        total = somaProdutos + frete;
        
        time_t t = time(NULL);
        struct tm compra = *localtime(&t);

        struct tm entrega = compra;
        entrega.tm_mday += 1; // entrega 1 dia depois
        mktime(&entrega); // ajusta o calendário

        printf("\n========= *RESUMO DO PEDIDO* =========\n");
        printf("Quantidade de produtos: %d\n", qtdProdutos);
        printf("Total dos produtos:     R$ %.2f\n", somaProdutos);
        printf("Valor do frete:         R$ %.2f\n", frete);
        printf("TOTAL A PAGAR:          R$ %.2f\n", total);

        printf("\nData e hora da compra:  %02d/%02d/%04d %02d:%02d\n",
               compra.tm_mday, compra.tm_mon + 1, compra.tm_year + 1900,
               compra.tm_hour, compra.tm_min);

        printf("Data prevista de entrega: %02d/%02d/%04d\n",
               entrega.tm_mday, entrega.tm_mon + 1, entrega.tm_year + 1900);
        // ----------------------------------------------------

        printf("\nDeseja realizar outra compra? (1 - Sim / 0 - Nao): ");
        scanf("%d", &continuar);

    } while (continuar == 1);

    return 0;
}