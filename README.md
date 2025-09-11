📦 Sistema_de_Hortifruti
 ┣ 📂 src/     

 # Código-fonte
 
#include <stdio.h>
#include <string.h>
#include <locale.h>

#define MAX_PRODUTOS 100
#define MAX_FUNCIONARIOS 50

// Estrutura para Produtos

typedef struct {
    int id;
    char nome[50];
    float preco;
    int quantidade;
} Produto;

// Estrutura para Funcionários

typedef struct {
    int id;
    char nome[50];
    char cargo[50];
} Funcionario;

// Funções de Estoque

void adicionarProduto(Produto estoque[], int *numProdutos);
void listarProdutos(Produto estoque[], int numProdutos);
void atualizarQuantidade(Produto estoque[], int numProdutos);
void buscarProduto(Produto estoque[], int numProdutos);

// Funções de Caixa

void realizarVenda(Produto estoque[], int numProdutos);
void relatorioVendas();

// Funções de Funcionários

void cadastrarFuncionario(Funcionario funcionarios[], int *numFuncionarios);
void listarFuncionarios(Funcionario funcionarios[], int numFuncionarios);

int main() {
    setlocale(LC_ALL, "Portuguese");
    Produto estoque[MAX_PRODUTOS];
    Funcionario funcionarios[MAX_FUNCIONARIOS];
    int numProdutos = 0;
    int numFuncionarios = 0;
    int opcao;

    do {
        printf("\nMenu Principal:\n");
        printf("1. Gerenciar Estoque\n");
        printf("2. Caixa\n");
        printf("3. Gerenciar Funcionários\n");
        printf("0. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);

        switch(opcao) {
            case 1:
                printf("\n1. Adicionar Produto\n");
                printf("2. Listar Produtos\n");
                printf("3. Atualizar Quantidade\n");
                printf("4. Buscar Produto\n");
                printf("Escolha uma opção: ");
                scanf("%d", &opcao);

                switch(opcao) {
                    case 1: adicionarProduto(estoque, &numProdutos); break;
                    case 2: listarProdutos(estoque, numProdutos); break;
                    case 3: atualizarQuantidade(estoque, numProdutos); break;
                    case 4: buscarProduto(estoque, numProdutos); break;
                    default: printf("Opção inválida.\n");
                }
                break;
            case 2:
                printf("\n1. Realizar Venda\n");
                printf("2. Relatório de Vendas\n");
                printf("Escolha uma opção: ");
                scanf("%d", &opcao);

                switch(opcao) {
                    case 1: realizarVenda(estoque, numProdutos); break;
                    case 2: relatorioVendas(); break;
                    default: printf("Opção inválida.\n");
                }
                break;
            case 3:
                printf("\n1. Cadastrar Funcionário\n");
                printf("2. Listar Funcionários\n");
                printf("Escolha uma opção: ");
                scanf("%d", &opcao);

                switch(opcao) {
                    case 1: cadastrarFuncionario(funcionarios, &numFuncionarios); break;
                    case 2: listarFuncionarios(funcionarios, numFuncionarios); break;
                    default: printf("Opção inválida.\n");
                }
                break;
            case 0:
                printf("Saindo...\n");
                break;
            default:
                printf("Opção inválida.\n");
        }
    } while(opcao != 0);

    return 0;
}

// Funções de Estoque

void adicionarProduto(Produto estoque[], int *numProdutos) {
    if (*numProdutos >= MAX_PRODUTOS) {
        printf("Estoque cheio.\n");
        return;
    }

    Produto p;
    printf("Digite o ID do produto: ");
    scanf("%d", &p.id);
    printf("Digite o nome do produto: ");
    scanf(" %49[^\n]", p.nome);
    printf("Digite o preço do produto: ");
    scanf("%f", &p.preco);
    printf("Digite a quantidade do produto: ");
    scanf("%d", &p.quantidade);

    estoque[*numProdutos] = p;
    (*numProdutos)++;
    printf("Produto adicionado com sucesso.\n");
}

void listarProdutos(Produto estoque[], int numProdutos) {
    if (numProdutos == 0) {
        printf("Nenhum produto no estoque.\n");
        return;
    }
    printf("Produtos em estoque:\n");
    for (int i = 0; i < numProdutos; i++) {
        printf("ID: %d, Nome: %s, Preço: %.2f, Quantidade: %d\n",
               estoque[i].id, estoque[i].nome, estoque[i].preco, estoque[i].quantidade);
    }
}

void atualizarQuantidade(Produto estoque[], int numProdutos) {
    int id, novaQuantidade;
    printf("Digite o ID do produto para atualizar a quantidade: ");
    scanf("%d", &id);

    for (int i = 0; i < numProdutos; i++) {
        if (estoque[i].id == id) {
            printf("Digite a nova quantidade: ");
            scanf("%d", &novaQuantidade);
            estoque[i].quantidade = novaQuantidade;
            printf("Quantidade atualizada com sucesso.\n");
            return;
        }
    }
    printf("Produto não encontrado.\n");
}

void buscarProduto(Produto estoque[], int numProdutos) {
    int id;
    printf("Digite o ID do produto para buscar: ");
    scanf("%d", &id);

    for (int i = 0; i < numProdutos; i++) {
        if (estoque[i].id == id) {
            printf("Produto encontrado: ID: %d, Nome: %s, Preço: %.2f, Quantidade: %d\n",
                   estoque[i].id, estoque[i].nome, estoque[i].preco, estoque[i].quantidade);
            return;
        }
    }
    printf("Produto não encontrado.\n");
}

// Funções de Caixa

void realizarVenda(Produto estoque[], int numProdutos) {
    int id, quantidade;
    printf("Digite o ID do produto para venda: ");
    scanf("%d", &id);

    for (int i = 0; i < numProdutos; i++) {
        if (estoque[i].id == id) {
            printf("Digite a quantidade a ser vendida: ");
            scanf("%d", &quantidade);
            if (quantidade > estoque[i].quantidade) {
                printf("Quantidade insuficiente em estoque.\n");
                return;
            }
            estoque[i].quantidade -= quantidade;
            printf("Venda realizada com sucesso. Total: %.2f\n", estoque[i].preco * quantidade);
            return;
        }
    }
    printf("Produto não encontrado.\n");
}

void relatorioVendas() {
    // Implementar um relatório de vendas real conforme necessário
    printf("Relatório de vendas não disponível neste momento.\n");
}

// Funções de Funcionários

void cadastrarFuncionario(Funcionario funcionarios[], int *numFuncionarios) {
    if (*numFuncionarios >= MAX_FUNCIONARIOS) {
        printf("Número máximo de funcionários alcançado.\n");
        return;
    }

    Funcionario f;
    printf("Digite o ID do funcionário: ");
    scanf("%d", &f.id);
    printf("Digite o nome do funcionário: ");
    scanf(" %49[^\n]", f.nome);
    printf("Digite o cargo do funcionário: ");
    scanf(" %49[^\n]", f.cargo);

    funcionarios[*numFuncionarios] = f;
    (*numFuncionarios)++;
    printf("Funcionário cadastrado com sucesso.\n");
}

void listarFuncionarios(Funcionario funcionarios[], int numFuncionarios) {
    if (numFuncionarios == 0) {
        printf("Nenhum funcionário cadastrado.\n");
        return;
    }
    printf("Funcionários:\n");
    for (int i = 0; i < numFuncionarios; i++) {
        printf("ID: %d, Nome: %s, Cargo: %s\n",
               funcionarios[i].id, funcionarios[i].nome, funcionarios[i].cargo);
    }
}


 ┣ 📂 docs/                 # Documentação extra (diagramas, especificações etc.)
 ┣ 📂 tests/                # Testes automatizados
 ┣ 📄 README.md         
 
 # Documentação principal
 
# Sistema_de_Hortifruti

## 📖 Descrição

Sistema feito para gerenciamento de estoque e vendas de um Hortifruti. Este projeto tem como objetivo desenvolver um sistema de hortifrúti para controle de estoque e vendas.

---

## 🚀 Funcionalidades
- [x] Cadastro de clientes
- [x] Controle de estoque
- [x] Vendas
- [ ] Relatórios financeiros
- [ ] Dashboard com gráficos

---

## 🛠️ Tecnologias Utilizadas
- Linguagem: C / C# /
- Banco de Dados:
- Frameworks:

---

## 📂 Estrutura do Projeto


 
 ┣ 📄 .gitignore            # Arquivos a serem ignorados
 ┣ 📄 LICENSE               # Licença do projeto

