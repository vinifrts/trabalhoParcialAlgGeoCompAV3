import java.util.Arrays;
import java.util.Comparator;
import java.util.stream.IntStream;

public class questaoCinco {
    public static double[][] transpor(double[][] matriz) {
        double[][] transposta = new double[matriz[0].length][matriz.length];
        for (int i = 0; i < matriz.length; i++) {
            for (int j = 0; j < matriz[0].length; j++) {
                transposta[j][i] = matriz[i][j];
            }
        }
        return transposta;
    }

    public static double[][] multiplicarMatrizes(double[][] m1, double[][] m2) {
        int linhasM1 = m1.length;
        int colunasM2 = m2[0].length;
        int colunasM1 = m1[0].length;

        double[][] resultado = new double[linhasM1][colunasM2];

        for (int i = 0; i < linhasM1; i++) {
            for (int j = 0; j < colunasM2; j++) {
                for (int k = 0; k < colunasM1; k++) {
                    resultado[i][j] += m1[i][k] * m2[k][j];
                }
            }
        }

        return resultado;
    }

    public static double norma(double[] vetor) {
        return Math.sqrt(Arrays.stream(vetor)
                .map(val -> val * val)
                .sum());
    }

    public static double[] normalizar(double[] vetor) {
        double normalizacao = norma(vetor);
        return Arrays.stream(vetor)
                .map(val -> val / normalizacao)
                .toArray();
    }

    public static double[] multiplicarMatrizVetor(double[][] matriz, double[] vetor) {
        return Arrays.stream(matriz)
                .mapToDouble(linha -> {
                    double soma = 0;
                    for (int j = 0; j < linha.length; j++) {
                        soma += linha[j] * vetor[j];
                    }
                    return soma;
                })
                .toArray();
    }

    public static double[] calcularAutoridade(double[][] A, int iteracoes, double tolerancia) {
        double[][] At = transpor(A);
        double[][] AtA = multiplicarMatrizes(At, A);

        double[] a_k = new double[AtA.length];
        Arrays.fill(a_k, 1.0);
        a_k = normalizar(a_k);

        double[] a_k1;
        for (int i = 0; i < iteracoes; i++) {
            a_k1 = multiplicarMatrizVetor(AtA, a_k);
            a_k1 = normalizar(a_k1);

            boolean convergiu = true;
            for (int j = 0; j < a_k.length; j++) {
                if (Math.abs(a_k[j] - a_k1[j]) >= tolerancia) {
                    convergiu = false;
                    break;
                }
            }

            if (convergiu) break;
            a_k = a_k1;
        }

        return a_k;
    }

    public static void main(String[] args) {
        double[][] A = {
                {0, 0, 1, 0},
                {1, 0, 0, 0},
                {1, 1, 0, 0},
                {0, 1, 0, 0}
        };

        double[] vetorAutoridade = calcularAutoridade(A, 10, 1e-6);

        Integer[] indices = IntStream.range(0, vetorAutoridade.length)
                .boxed()
                .sorted(Comparator.comparing(i -> -vetorAutoridade[i]))
                .toArray(Integer[]::new);

        System.out.println("Vetor de Autoridade:");
        imprimirVetor(vetorAutoridade);

        System.out.println("\nSites Ranqueados:");
        for (int indice : indices) {
            System.out.printf("Site %d: %.6f%n", indice + 1, vetorAutoridade[indice]);
        }
    }

    private static void imprimirVetor(double[] vetor) {
        for (double valor : vetor) {
            System.out.printf("%.6f ", valor);
        }
        System.out.println();
    }
}
