# Sina-Khodarahmi
CyberAI-Lab
#ifndef LINEAR_REGRESSION_HPP
#define LINEAR_REGRESSION_HPP

#include <vector>
#include <iostream>

// A simple implementation of Linear Regression in C++
// This can predict target values (like salary) from features (like years of experience)
class LinearRegression {
private:
    double slope;
    double intercept;

public:
    LinearRegression() : slope(0), intercept(0) {}

    // Train model using Least Squares method
    void fit(const std::vector<double>& X, const std::vector<double>& y) {
        if(X.size() != y.size() || X.empty()) {
            std::cerr << "Invalid training data.\n";
            return;
        }

        double x_mean = 0, y_mean = 0;
        for(size_t i=0; i<X.size(); ++i){
            x_mean += X[i];
            y_mean += y[i];
        }
        x_mean /= X.size();
        y_mean /= X.size();

        double numerator = 0, denominator = 0;
        for(size_t i=0; i<X.size(); ++i){
            numerator += (X[i]-x_mean)*(y[i]-y_mean);
            denominator += (X[i]-x_mean)*(X[i]-x_mean);
        }

        slope = numerator / denominator;
        intercept = y_mean - slope * x_mean;
    }

    // Predict target value for a new input
    double predict(double x) {
        return slope * x + intercept;
    }

    void printModel() {
        std::cout << "Linear Regression Model: y = " << slope << " * x + " << intercept << "\n";
    }
};

#endif // LINEAR_REGRESSION_HPP
