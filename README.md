// Piggy bank

// Inicio do trabalho de Cofrinho


package Trabalho;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.Scanner;

abstract class Moeda {
    protected double valor;

    public Moeda(double valor) {
        this.valor = valor;
    }
//Conversor
    public abstract double converterParaReal();
    public abstract String getTipo();
    public double getValor() {
        return valor;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Moeda moeda = (Moeda) obj;
        return Double.compare(moeda.valor, valor) == 0 && getTipo().equals(moeda.getTipo());
    }
}

class Dolar extends Moeda {
    public Dolar(double valor) {
        super(valor);
    }

    @Override
    public double converterParaReal() {
        return valor * 5.14;
    }

    @Override
    public String getTipo() {
        return "Dólar";
    }
}

class Euro extends Moeda {
    public Euro(double valor) {
        super(valor);
    }

    @Override
    public double converterParaReal() {
        return valor * 5.54;
    }

    @Override
    public String getTipo() {
        return "Euro";
    }
}

class Real extends Moeda {
    public Real(double valor) {
        super(valor);
    }

    @Override
    public double converterParaReal() {
        return valor;
    }

    @Override
    public String getTipo() {
        return "Real";
    }
    //Lista de moedas
}

class Cofrinho {
    private ArrayList<Moeda> moedas;

    public Cofrinho() {
        moedas = new ArrayList<>();
    }

    public void adicionarMoeda(Moeda moeda) {
        moedas.add(moeda);
        System.out.println(moeda.getTipo() + " adicionado(a): " + moeda.getValor());
    }
// remover moeda
    public void removerMoeda(Moeda moeda) {
        Iterator<Moeda> iterator = moedas.iterator();
        while (iterator.hasNext()) {
            Moeda m = iterator.next();
            if (m.equals(moeda)) {
                iterator.remove();
                System.out.println(moeda.getTipo() + " removido(a): " + moeda.getValor());
                return;
            }
        }
        System.out.println("Moeda não encontrada no cofrinho.");
        // listagem da moeda com o conversor 
    }

    public void listarMoedas() {
        if (moedas.isEmpty()) {
            System.out.println("Cofrinho vazio.");
        } else {
            System.out.println("Moedas no cofrinho:");
            for (Moeda moeda : moedas) {
                System.out.println(moeda.getTipo() + ": " + moeda.getValor());
            }
        }
    }

    public double calcularTotal() {
        double total = 0;
        for (Moeda moeda : moedas) {
            total += moeda.converterParaReal();
        }
        return total;
    }
    // Iniciando o cofrinho
}

public class Principal {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Cofrinho cofrinho = new Cofrinho();
        boolean executando = true;

        while (executando) {
            System.out.println("\nOpções:");
            System.out.println("1. Adicionar dinheiro");
            System.out.println("2. Remover dinheiro");
            System.out.println("3. Listar moedas");
            System.out.println("4. Total no cofrinho");
            System.out.println("5. Encerrar");
            System.out.print("Escolha uma opção: ");

            int opcao = scanner.nextInt();

            switch (opcao) {
                case 1:
                    System.out.println("Escolha o tipo de moeda para adicionar:");
                    System.out.println("1. Dólar");
                    System.out.println("2. Euro");
                    System.out.println("3. Real");
                    int tipoMoeda = scanner.nextInt();
                    System.out.print("Digite o valor: ");
                    double valor = scanner.nextDouble();

                    switch (tipoMoeda) {
                        case 1:
                            cofrinho.adicionarMoeda(new Dolar(valor));
                            break;
                        case 2:
                            cofrinho.adicionarMoeda(new Euro(valor));
                            break;
                        case 3:
                            cofrinho.adicionarMoeda(new Real(valor));
                            break;
                        default:
                            System.out.println("Tipo de moeda inválido.");
                    }
                    break;

                case 2:
                    System.out.println("Escolha o tipo de moeda para remover:");
                    System.out.println("1. Dólar");
                    System.out.println("2. Euro");
                    System.out.println("3. Real");
                    tipoMoeda = scanner.nextInt();
                    System.out.print("Digite o valor: ");
                    valor = scanner.nextDouble();

                    Moeda moedaRemover = null;

                    switch (tipoMoeda) {
                        case 1:
                            moedaRemover = new Dolar(valor);
                            break;
                        case 2:
                            moedaRemover = new Euro(valor);
                            break;
                        case 3:
                            moedaRemover = new Real(valor);
                            break;
                        default:
                            System.out.println("Tipo de moeda inválido.");
                    }

                    if (moedaRemover != null) {
                        cofrinho.removerMoeda(moedaRemover);
                    }
                    break;

                case 3:
                    cofrinho.listarMoedas();
                    break;

                case 4:
                    double total = cofrinho.calcularTotal();
                    System.out.printf("Total no cofrinho em reais: R$%.2f%n", total);
                    break;

                case 5:
                    executando = false;
                    System.out.println("Programa encerrado.");
                    break;

                default:
                    System.out.println("Opção inválida.");
            }
        }

        scanner.close();
    }
}

