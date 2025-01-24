# CODE-REFACTORING-AND-PERFORMANCE-OPTIMIZATION
*COMPANY*: CODTECH IT SOLUTIONS
*NAME*: KHUSHI ANAND YADAV
*INTERN ID*: CT08GKA
*DOMAIN*: SOFTWARE DEVELOPMENT
*DURATION*: 4 WEEKS
*MENTOR*: NEELA SANTHOSH KUMAR

# DESCRIPTION

Refactoring an open-source project like the given code can significantly improve its readability and performance. Let's break down the provided Java code, analyze its current state, and make necessary improvements.

 Original Code Structure

The original code consists of two classes: Product and Store.

1. Product Class:
    Fields: Contains fields such as name, price, shippingCost, and quantity.
    Constructor: Initializes these fields.
    Getters: Provides getter methods for each field.
    Methods: Includes a getTotalCost() method to calculate the total cost of the product, considering quantity discounts.

2. Store Class:
    Fields: Contains a list of Product objects.
    Methods: Includes methods to add a product (addAProduct) and calculate the cost of all products (getCostOfProducts). The main method creates instances of Store and Product and prints the cost details.

 Issues and Improvements

1. Encapsulation and Readability:
    The Product class fields should be private, and only accessible through getters and setters. This ensures better encapsulation and data protection.
    The getTotalCost() method has complicated logic that can be simplified for better readability.

2. Performance:
    The calculation of discounts and total costs can be optimized by avoiding redundant computations.
    Avoid unnecessary use of global variables in the Store class.

3. Code Comments:
    Remove the commented-out "BAD CODE" sections to avoid clutter.
    Add meaningful comments that explain the code logic where necessary.

 Refactored Code

Here is the refactored version of the code with improved readability and performance:

java
public class Product {
    private String name;
    private double price;
    private double shippingCost;
    private int quantity;

    public Product(String name, double price, double shippingCost, int quantity) {
        this.name = name;
        this.price = price;
        this.shippingCost = shippingCost;
        this.quantity = quantity;
    }

    public String getName() { return name; }
    public double getPrice() { return price; }
    public double getShippingCost() { return shippingCost; }
    public int getQuantity() { return quantity; }

    public double getTotalCost() {
        double quantityDiscount = getQuantityDiscount();
        double discount = ((quantity - 1) * quantityDiscount) * price;
        return (quantity * price) + (quantity * shippingCost) - discount;
    }

    private double getQuantityDiscount() {
        if (quantity > 50 || (quantity * price) > 500) {
            return 0.10;
        } else if (quantity > 25 || (quantity * price) > 100) {
            return 0.07;
        } else if (quantity >= 10 || (quantity * price) > 50) {
            return 0.05;
        } else {
            return 0.0;
        }
    }
}

import java.util.ArrayList;

public class Store {
    private ArrayList<Product> products;

    public Store() {
        this.products = new ArrayList<>();
    }

    public void addProduct(Product product) {
        products.add(product);
    }

    public void displayProductCosts() {
        for (Product product : products) {
            int numOfProducts = product.getQuantity();
            String prodName = product.getName();
            double totalCost = product.getTotalCost();
            double costPerProduct = totalCost / numOfProducts;
            double costWithoutDiscount = product.getPrice() + product.getShippingCost();

            System.out.println("Total cost for " + numOfProducts + " " + prodName + "(s) is $" + totalCost);
            System.out.println("Cost per product: $" + costPerProduct);
            System.out.println("Savings per product: $" + (costWithoutDiscount - costPerProduct));
            System.out.println();
        }
    }

    public static void main(String[] args) {
        Store cornerStore = new Store();
        cornerStore.addProduct(new Product("Pizza", 10.00, 1.00, 52));
        cornerStore.addProduct(new Product("Pizza", 10.00, 1.00, 26));
        cornerStore.addProduct(new Product("Pizza", 10.00, 1.00, 10));
        cornerStore.displayProductCosts();
    }
}


 Explanation of Refactoring

1. Encapsulation: 
    The fields in Product are now private, and accessor methods (getters) are provided for external access.
    Introduced a private method getQuantityDiscount() in Product to simplify the getTotalCost() method.

2. Readability:
    The discount logic is separated into a distinct method, making the main cost calculation more readable.
    Simplified the `Store` class by using meaningful method names and removing unnecessary global variables.

3. Performance:
    The refactored code avoids redundant calculations by computing discounts once and reusing the computed values.

By refactoring the code, we achieve cleaner, more maintainable, and efficient code, enhancing both its readability and performance. This approach ensures that the code is easier to understand, extend, and debug, ultimately leading to better software development practices.
