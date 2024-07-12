 # Explorando Padrões de Projetos com Java

Para criar uma solução que explore os conceitos de padrões de design Singleton, Strategy e Facade, utilizamos o contexto de um sistema de abertura de conta bancária para dar continuidade aos desafios propostos acima, podemos seguir a seguinte estrutura em Java:

### 1. Singleton
O padrão Singleton garante que uma classe tenha apenas uma instância e fornece um ponto global de acesso a essa instância.
 

    public class Banco {
    private static Banco instance;

    private Banco() {
        // Construtor privado para evitar múltiplas instâncias
    }

    public static Banco getInstance() {
        if (instance == null) {
            instance = new Banco();
        }
        return instance;
    }

    public void criarConta(String tipoConta) {
        // Lógica para criar uma conta
    }

    public void exibirContas() {
        // Lógica para exibir as contas
    }
    }



### 2. Strategy
O padrão Strategy permite definir uma família de algoritmos, encapsular cada um deles e os torne intercambiáveis. Vamos usar este padrão para definir diferentes estratégias de criação de contas (ex. Conta Corrente, Conta Poupança).

    // Interface Strategy
    public interface ContaStrategy {
    void criarConta();
    }

    // Implementação de Conta Corrente
    public class ContaCorrenteStrategy implements ContaStrategy {
    @Override
    public void criarConta() {
        System.out.println("Conta Corrente criada com sucesso.");
    }
    }

    // Implementação de Conta Poupança
    public class ContaPoupancaStrategy implements ContaStrategy {
    @Override
    public void criarConta() {
        System.out.println("Conta Poupança criada com sucesso.");
    }
    }

    // Contexto que utiliza as estratégias
    public class ContaContext {
    private ContaStrategy strategy;

    public void setStrategy(ContaStrategy strategy) {
        this.strategy = strategy;
    }

    public void criarConta() {
        this.strategy.criarConta();
    }
    }


### 3. Facade
O padrão Facade fornece uma interface unificada para um conjunto de interfaces em um subsistema. Vamos usar este padrão para criar uma fachada que simplifique as interações com as estratégias de criação de contas.

    public class BancoFacade {
    private ContaContext contaContext;

    public BancoFacade() {
        contaContext = new ContaContext();
    }

    public void criarContaCorrente() {
        contaContext.setStrategy(new ContaCorrenteStrategy());
        contaContext.criarConta();
    }

    public void criarContaPoupanca() {
        contaContext.setStrategy(new ContaPoupancaStrategy());
        contaContext.criarConta();
    }
    }


### 4. Exemplo de Uso
Aqui está um exemplo de como usar os padrões de projeto mencionados acima em um programa principal:

    public class Main {
    public static void main(String[] args) {
        Banco banco = Banco.getInstance();

        BancoFacade bancoFacade = new BancoFacade();
        bancoFacade.criarContaCorrente();
        bancoFacade.criarContaPoupanca();

        banco.exibirContas();
    }
    }


## Explicação
- Singleton: Garantimos que a classe Banco tenha apenas uma instância para centralizar a criação e o gerenciamento das contas.

- Strategy: Definimos diferentes estratégias de criação de contas (ContaCorrenteStrategy e ContaPoupancaStrategy) e permitimos que sejam intercambiáveis.

- Facade: Criamos uma fachada (BancoFacade) que simplifica a interação com as estratégias de criação de contas, oferecendo métodos fáceis de usar (criarContaCorrente e criarContaPoupanca).

Este exemplo demonstra como os padrões de projeto podem ser aplicados em conjunto para resolver problemas comuns no design de software, promovendo flexibilidade, reutilização de código e um design mais limpo e modular.

