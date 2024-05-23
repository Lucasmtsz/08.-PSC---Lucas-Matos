Implemente uma classe Empregado com os seguintes atributos: nome, idade e salario. Crie os métodos promover(), aumentarSalario(), demitir() e fazerAniversario() com as seguintes regras:
Regras dos Métodos:
Todos os atributos devem ser privados e os métodos públicos.
 Você deve implementar métodos get e set para todos os atributos, independentemente do uso.
 Implementar método toString.
promover()
A promoção só poderá ser realizada se o funcionário tiver mais de 18 anos.
A promoção resultará em um aumento de 25% no salário, utilizando o método aumentarSalario().
aumentarSalario()
Deve receber um percentual de aumento como parâmetro.
Deve realizar o aumento do salário do funcionário de acordo com o percentual informado.
demitir()
Deve receber um motivo como parâmetro (1, 2 ou 3):
1: Justa causa.
2: Decisão do empregador.
3: Aposentadoria.
Se o motivo for decisão do empregador, o empregado deverá receber uma multa de 40% do salário (realizar este cálculo e informar).
Se o motivo for justa causa, o funcionário deverá cumprir aviso prévio.
Se o motivo for aposentadoria, o salário de aposentadoria deve ser calculado conforme a tabela do INSS abaixo:
Salário entre 1000 e 2000 reais: receberá 1500 reais.
Salário entre 2000 e 3000 reais: receberá 2500 reais.
Salário entre 3000 e 4000 reais: receberá 3500 reais.
Salário acima de 4000 reais: receberá 4000 reais.
fazerAniversario()
Aumenta a idade do empregado em 1 ano.
Crie uma classe Principal com um menu interativo para testar a classe Empregado. O menu deve permitir ao usuário escolher as seguintes opções para manipular uma lista de empregados:
Criar novo empregado
Promover empregado
Aumentar salário do empregado
Demitir empregado
Fazer aniversário do empregado
Mostrar detalhes dos empregados
Sair









import java.util.ArrayList;
import java.util.Scanner;

class Empregado {
    private String nome;
    private String cargo;
    private double salario;
    private int idade;
    private boolean ativo;

    public Empregado(String nome, String cargo, double salario, int idade) {
        this.nome = nome;
        this.cargo = cargo;
        this.salario = salario;
        this.idade = idade;
        this.ativo = true;
    }

    public String getNome() {
        return nome;
    }

    public String getCargo() {
        return cargo;
    }

    public double getSalario() {
        return salario;
    }

    public int getIdade() {
        return idade;
    }

    public boolean isAtivo() {
        return ativo;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public void setCargo(String cargo) {
        this.cargo = cargo;
    }

    public void setSalario(double salario) {
        this.salario = salario;
    }

    public void setIdade(int idade) {
        this.idade = idade;
    }

    public void setAtivo(boolean ativo) {
        this.ativo = ativo;
    }

    public String toString() {
        return String.format("Nome: %s, Cargo: %s, Salário: %.2f, Idade: %d, Ativo: %b",
                              nome, cargo, salario, idade, ativo);
    }

    public void promover(String novoCargo) {
        this.cargo = novoCargo;
        aumentarSalario(25); 
    }

    public void aumentarSalario(double percentual) {
        this.salario += this.salario * percentual / 100;
    }

    public void demitir(int motivo) {
        this.ativo = false;
        switch (motivo) {
            case 1:
                System.out.println("Demissão por justa causa. O empregado deverá cumprir aviso prévio.");
                break;
            case 2:
                double multa = this.salario * 0.40;
                System.out.printf("Demissão por decisão do empregador. O empregado receberá uma multa de 40%% do salário: R$ %.2f%n", multa);
                break;
            case 3:
                double salarioAposentadoria = calcularSalarioAposentadoria(this.salario);
                System.out.printf("Demissão por aposentadoria. O empregado receberá um salário de aposentadoria de: R$ %.2f%n", salarioAposentadoria);
                break;
            default:
                System.out.println("Motivo inválido.");
        }
    }

    public void fazerAniversario() {
        this.idade++;
    }

    public String getDetalhes() {
        return toString();
    }

    private double calcularSalarioAposentadoria(double salario) {
        if (salario >= 1000 && salario < 2000) {
            return 1500;
        } else if (salario >= 2000 && salario < 3000) {
            return 2500;
        } else if (salario >= 3000 && salario < 4000) {
            return 3500;
        } else if (salario >= 4000) {
            return 4000;
        } else {
            return salario;
        }
    }
}

public class Main {
    private static ArrayList<Empregado> empregados = new ArrayList<>();
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        while (true) {
            mostrarMenu();
            int opcao = scanner.nextInt();
            scanner.nextLine();

            switch (opcao) {
                case 1:
                    criarEmpregado();
                    break;
                case 2:
                    promoverEmpregado();
                    break;
                case 3:
                    aumentarSalarioEmpregado();
                    break;
                case 4:
                    demitirEmpregado();
                    break;
                case 5:
                    fazerAniversarioEmpregado();
                    break;
                case 6:
                    mostrarDetalhesEmpregados();
                    break;
                case 7:
                    System.out.println("Saindo...");
                    scanner.close();
                    return;
                default:
                    System.out.println("Opção inválida. Tente novamente.");
            }
        }
    }

    private static void mostrarMenu() {
        System.out.println("Menu:");
        System.out.println("1. Criar novo empregado");
        System.out.println("2. Promover empregado");
        System.out.println("3. Aumentar salário do empregado");
        System.out.println("4. Demitir empregado");
        System.out.println("5. Fazer aniversário do empregado");
        System.out.println("6. Mostrar detalhes dos empregados");
        System.out.println("7. Sair");
        System.out.print("Escolha uma opção: ");
    }

    private static void criarEmpregado() {
        System.out.print("Nome: ");
        String nome = scanner.nextLine();
        System.out.print("Cargo: ");
        String cargo = scanner.nextLine();
        System.out.print("Salário: ");
        double salario = scanner.nextDouble();
        System.out.print("Idade: ");
        int idade = scanner.nextInt();
        scanner.nextLine();

        empregados.add(new Empregado(nome, cargo, salario, idade));
        System.out.println("Empregado criado com sucesso!");
    }

    private static void promoverEmpregado() {
        Empregado empregado = selecionarEmpregado();
        if (empregado != null && empregado.isAtivo()) {
            if (empregado.getIdade() > 18) {
                System.out.print("Novo cargo: ");
                String novoCargo = scanner.nextLine();
                empregado.promover(novoCargo);
                System.out.println("Empregado promovido com sucesso! Salário aumentado em 25%.");
            } else {
                System.out.println("A promoção só pode ser realizada para funcionários com mais de 18 anos.");
            }
        }
    }

    private static void aumentarSalarioEmpregado() {
        Empregado empregado = selecionarEmpregado();
        if (empregado != null && empregado.isAtivo()) {
            System.out.print("Percentual de aumento: ");
            double percentual = scanner.nextDouble();
            scanner.nextLine();
            empregado.aumentarSalario(percentual);
            System.out.println("Salário aumentado com sucesso!");
        }
    }

    private static void demitirEmpregado() {
        Empregado empregado = selecionarEmpregado();
        if (empregado != null && empregado.isAtivo()) {
            System.out.print("Motivo da demissão (1: Justa causa, 2: Decisão do empregador, 3: Aposentadoria): ");
            int motivo = scanner.nextInt();
            scanner.nextLine();
            empregado.demitir(motivo);
            System.out.println("Processo de demissão concluído.");
        }
    }

    private static void fazerAniversarioEmpregado() {
        Empregado empregado = selecionarEmpregado();
        if (empregado != null && empregado.isAtivo()) {
            empregado.fazerAniversario();
            System.out.println("Aniversário registrado com sucesso!");
        }
    }

    private static void mostrarDetalhesEmpregados() {
        for (Empregado emp : empregados) {
            System.out.println(emp.getDetalhes());
        }
    }

    private static Empregado selecionarEmpregado() {
        mostrarDetalhesEmpregados();
        System.out.print("Selecione o número do empregado: ");
        int index = scanner.nextInt();
        scanner.nextLine();

        if (index >= 1 && index <= empregados.size()) {
            return empregados.get(index - 1);
        } else {
            System.out.println("Empregado inválido.");
            return null;
        }
    }
}
