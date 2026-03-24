# bank-system
package assignment1;

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Bank bank = new Bank();
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\n--- BANK MENU ---");
            System.out.println("1. Create Account");
            System.out.println("2. Deposit");
            System.out.println("3. Withdraw");
            System.out.println("4. Balance Enquiry");
            System.out.println("5. Transfer");
            System.out.println("6. Search Customer");
            System.out.println("7. Display All");
            System.out.println("0. Exit");
            System.out.print("Enter choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter Acc Num: ");
                    int acc = scanner.nextInt();
                    scanner.nextLine(); 
                    System.out.print("Enter Name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter Balance: ");
                    double bal = scanner.nextDouble();
                    scanner.nextLine();
                    System.out.print("Enter Type: ");
                    String type = scanner.nextLine();
                    System.out.print("Enter Email: ");
                    String email = scanner.nextLine();
                    bank.createAcc(acc, name, bal, type, email);
                    break;

                case 2:
                    System.out.print("Acc Num: ");
                    int dAcc = scanner.nextInt();
                    System.out.print("Amount: ");
                    double dAmt = scanner.nextDouble();
                    bank.deposit(dAcc, dAmt);
                    break;

                case 3:
                    System.out.print("Acc Num: ");
                    int wAcc = scanner.nextInt();
                    System.out.print("Amount: ");
                    double wAmt = scanner.nextDouble();
                    bank.withdraw(wAcc, wAmt);
                    break;

                case 4:
                    System.out.print("Acc Num: ");
                    int eAcc = scanner.nextInt();
                    bank.enquiryBal(eAcc);
                    break;

                case 5:
                    System.out.print("From Acc: ");
                    int from = scanner.nextInt();
                    System.out.print("To Acc: ");
                    int to = scanner.nextInt();
                    System.out.print("Amount: ");
                    double tAmt = scanner.nextDouble();
                    bank.transfer(from, to, tAmt);
                    break;

                case 6:
                    System.out.print("Acc Num: ");
                    int sAcc = scanner.nextInt();
                    Customer found = bank.searchCus(sAcc);
                    System.out.println(found != null ? found : "Not found.");
                    break;

                case 7:
                    bank.displayAll();
                    break;
            }
        } while (choice != 0);
        
        scanner.close();
    }
}

package assignment1;
import java.util.*;

public class Bank {
	
	    private ArrayList<Customer> customers = new ArrayList<>();

	    public void createAcc(int accNum, String name, double balance, String accType, String email) {
	        Customer newCustomer = new Customer(accNum, name, balance, accType, email);
	        customers.add(newCustomer);
	        System.out.println("Account created successfully.");
	    }

	    public Customer searchCus(int accNum) {
	        for (Customer c : customers) {
	            if (c.getAccNum() == accNum) {
	                return c;
	            }
	        }
	        return null;
	    }

	    public void deposit(int accNum, double amount) {
	        Customer c = searchCus(accNum);
	        if (c != null) {
	            c.setBalance(c.getBalance() + amount);
	        }
	    }

	    public void withdraw(int accNum, double amount) {
	        Customer c = searchCus(accNum);
	        if (c != null && c.getBalance() >= amount) {
	            c.setBalance(c.getBalance() - amount);
	        }
	    }

	    public void enquiryBal(int accNum) {
	        Customer c = searchCus(accNum);
	        if (c != null) {
	            System.out.println("Balance: " + c.getBalance());
	        }
	    }

	    public void transfer(int fromAcc, int toAcc, double amount) {
	        Customer sender = searchCus(fromAcc);
	        Customer receiver = searchCus(toAcc);
	        if (sender != null && receiver != null && sender.getBalance() >= amount) {
	            sender.setBalance(sender.getBalance() - amount);
	            receiver.setBalance(receiver.getBalance() + amount);
	        }
	    }

	    public void displayAll() {
	        for (Customer c : customers) {
	            System.out.println(c);
	        }
	    }
	}

package assignment1;

public class Customer {

    private int accNum;
    private String name;
    private double balance;
    private String accType;
    private String email;

    public Customer(int accNum, String name, double balance, String accType, String email) {
        this.accNum = accNum;
        this.name = name;
        this.balance = balance;
        this.accType = accType;
        this.email = email;
    }

    public int getAccNum() {
        return accNum;
    }

    public void setAccNum(int accNum) {
        this.accNum = accNum;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        this.balance = balance;
    }

    public String getAccType() {
        return accType;
    }

    public void setAccType(String accType) {
        this.accType = accType;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    @Override
    public String toString() {
        return "AccNum: " + accNum + " | Name: " + name + " | Balance: " + balance + " | Type: " + accType + " | Email: " + email;
    }
}
