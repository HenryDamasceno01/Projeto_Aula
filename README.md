 # Documentação extra (diagramas, especificações etc.) <br>
 ┣ 📂 docs/  <br>              
  # Backlog <br>
 ┣ 📂 Backlog   <br>            
 ┣ 📄 README.md  <br> 
 
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
- Linguagem: C#
- Banco de Dados: 
- Frameworks: .NET

---

## 📂 Estrutura do Projeto
 # Código-fonte
 
    #include <stdio.h> <br>
    #include <string.h> <br>
    #include <locale.h> <br>

    #define MAX_PRODUTOS 100 <br>
    #define MAX_FUNCIONARIOS 50 <br>

// Estrutura para Produtos

    typedef struct {
    int id; <br>
    char nome[50]; <br>
    float preco; <br> 
    int quantidade; <br>
    } Produto;

// Estrutura para Funcionários

    typedef struct {
    int id; <br>
    char nome[50]; <br> 
    char cargo[50]; <br>
    } Funcionario;

// Funções de Estoque

    void adicionarProduto(Produto estoque[], int *numProdutos); <br>
    void listarProdutos(Produto estoque[], int numProdutos); <br> 
    void atualizarQuantidade(Produto estoque[], int numProdutos); <br> 
    void buscarProduto(Produto estoque[], int numProdutos); <br>

// Funções de Caixa

    void realizarVenda(Produto estoque[], int numProdutos); <br> 
    void relatorioVendas(); <br>

// Funções de Funcionários

    void cadastrarFuncionario(Funcionario funcionarios[], int *numFuncionarios); <br> 
    void listarFuncionarios(Funcionario funcionarios[], int numFuncionarios); <br>

    int main() {
    setlocale(LC_ALL, "Portuguese"); <br>
    Produto estoque[MAX_PRODUTOS]; <br> 
    Funcionario funcionarios[MAX_FUNCIONARIOS]; <br> 
    int numProdutos = 0; <br> 
    int numFuncionarios = 0; <br> 
    int opcao; <br>

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

    void adicionarProduto(Produto estoque[], int *numProdutos) <br> {
    if (*numProdutos >= MAX_PRODUTOS) <br> {
        printf("Estoque cheio.\n"); <br>
        return; <br>
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

    void listarProdutos(Produto estoque[], int numProdutos) <br> {
    if (numProdutos == 0) <br> {
        printf("Nenhum produto no estoque.\n"); <br>
        return; <br>
    }
    printf("Produtos em estoque:\n"); <br> 
    for (int i = 0; i < numProdutos; i++) <br> { 
        printf("ID: %d, Nome: %s, Preço: %.2f, Quantidade: %d\n", <br>
               estoque[i].id, estoque[i].nome, estoque[i].preco, estoque[i].quantidade); <br>
    }
    }

    void atualizarQuantidade(Produto estoque[], int numProdutos) <br> {
    int id, novaQuantidade; <br>
    printf("Digite o ID do produto para atualizar a quantidade: "); <br>
    scanf("%d", &id); <br>

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

    void buscarProduto(Produto estoque[], int numProdutos) <br> {
    int id; <br> 
    printf("Digite o ID do produto para buscar: "); <br> 
    scanf("%d", &id); <br>

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

    void realizarVenda(Produto estoque[], int numProdutos) <br> {
    int id, quantidade; <br> 
    printf("Digite o ID do produto para venda: "); <br>
    scanf("%d", &id); <br>

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

    void cadastrarFuncionario(Funcionario funcionarios[], int *numFuncionarios) <br> {
    if (*numFuncionarios >= MAX_FUNCIONARIOS) <br> {
        printf("Número máximo de funcionários alcançado.\n"); <br>
        return; <br>
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

    void listarFuncionarios(Funcionario funcionarios[], int numFuncionarios) <br> {
    if (numFuncionarios == 0) <br> {
        printf("Nenhum funcionário cadastrado.\n"); <br>
        return; <br>
    }
    printf("Funcionários:\n"); <br>
    for (int i = 0; i < numFuncionarios; i++) <br> {
        printf("ID: %d, Nome: %s, Cargo: %s\n", <br>
               funcionarios[i].id, funcionarios[i].nome, funcionarios[i].cargo); <br>
    }
    }
   
 # Licença do projeto
 ┣ 📄 LICENSE 
 MIT License
