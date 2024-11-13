# HANDS-ON-2
HANDS-ON-2 TAREA

Código C++

#include <iostream>
#include <vector>
using namespace std;

class SimpleLinearRegression {
private:
    vector<double> X;
    vector<double> Y;
    double B0, B1;

public:
    // Constructor: inicializa el conjunto de datos
    SimpleLinearRegression(vector<double> x, vector<double> y) : X(x), Y(y), B0(0), B1(0) {}

    // Método para calcular B0 y B1
    void calculateCoefficients() {
        double sumX = 0, sumY = 0, sumXY = 0, sumX2 = 0;
        int n = X.size();

        for (int i = 0; i < n; i++) {
            sumX += X[i];
            sumY += Y[i];
            sumXY += X[i] * Y[i];
            sumX2 += X[i] * X[i];
        }

        B1 = (n * sumXY - sumX * sumY) / (n * sumX2 - sumX * sumX);
        B0 = (sumY - B1 * sumX) / n;
    }

    // Método para imprimir la ecuación de regresión
    void printEquation() {
        cout << "\n\nEcuación de Regresión: [^y = " << B0 << " + " << B1 << " * x]" << endl;
    }

    // Método para hacer una predicción
    double predict(double x) {
        return B0 + B1 * x;
    }
};

int main() {
    // Dataset hardcoded
//    vector<double> X = {23, 26, 30, 34, 43, 48, 52, 57, 58};
    vector<double> X = {1, 2, 3, 4, 5, 6, 7, 8, 9};
//    vector<double> Y = {651, 762, 856, 1063, 1190, 1298, 1421, 1440, 1518};
    vector<double> Y = {2, 4, 6, 8, 10, 12, 14, 16, 18};
    SimpleLinearRegression model(X, Y);

    // Calcular coeficientes y mostrar la ecuación
    model.calculateCoefficients();
    model.printEquation();

    // Ingresar valor de x para predecir
    double x_value;
    cout << "\nIngrese el valor de [x] para predecir [y]: ";
    cin >> x_value;
    cout << "\nPredicción: " << model.predict(x_value) << endl;

    return 0;
}
