#Expense tracker (console based)

import java.util.ArrayList;
import java.util.Scanner;

public class ExpenseTracker {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        double balance = 0;
        int choice;

        ArrayList<Transaction> history = new ArrayList<>();

        do {
            System.out.println("\n1. Add Money");
            System.out.println("2. Expense");
            System.out.println("3. Withdraw");
            System.out.println("4. Show Balance");
            System.out.println("5. Show History");
            System.out.println("6. Exit");
            System.out.print("Enter choice: ");
            choice = sc.nextInt();

            if (choice == 1) {
                System.out.print("Enter amount: ");
                double amt = sc.nextDouble();
                balance += amt;
                history.add(new Transaction("Added", amt, "Income"));
            }

            else if (choice == 2) {
                System.out.print("Enter expense: ");
                double exp = sc.nextDouble();
                sc.nextLine();

                System.out.print("Enter category: ");
                String cat = sc.nextLine();

                if (exp <= balance) {
                    balance -= exp;
                    history.add(new Transaction("Expense", exp, cat));
                } else {
                    System.out.println("Not enough balance!");
                }
            }

            else if (choice == 3) {
                System.out.print("Enter withdraw: ");
                double w = sc.nextDouble();

                if (w <= balance) {
                    balance -= w;
                    history.add(new Transaction("Withdraw", w, "Cash"));
                } else {
                    System.out.println("Insufficient balance!");
                }
            }

            else if (choice == 4) {
                System.out.println("Balance: " + balance);
            }

            else if (choice == 5) {
                System.out.println("\nTransaction History:");
                if (history.isEmpty()) {
                    System.out.println("No transactions yet.");
                } else {
                    for (Transaction t : history) {
                        System.out.println(t);
                    }
                }
            }

        } while (choice != 6);

        sc.close();
    }
}

class Transaction {
    String type;
    double amount;
    String category;

    Transaction(String type, double amount, String category) {
        this.type = type;
        this.amount = amount;
        this.category = category;
    }

    public String toString() {
        return type + " " + amount + " [" + category + "]";
    }
}
