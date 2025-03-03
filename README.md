# IMPROVEDATMSYSTEM
import java.util.*;

class User {
    String userID;
    String password;
    double balance;

    User(String userID, String password) {
        this.userID = userID;
        this.password = password;
        this.balance = 0.0;
    }
}
public class Main {
    static ArrayList<User> users = new ArrayList<>();
    static Scanner scanner = new Scanner(System.in);
    static User currentUser = null;

    public static void main(String[] args) {
        while (true) {
            System.out.println("\n**WELCOME TO Otyp's BANK**\n");
            System.out.println("1. Register");
            System.out.println("2. Login");
            System.out.println("3. Exit");
            System.out.print("Enter Choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1:
                    registerUser();
                    break;
                case 2:
                    loginUser();
                    break;
                case 3:
                    System.out.println("Byebye!");
                    return;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }

    public static void registerUser() {
        System.out.print("Enter Accoount Number: ");
        String userID = scanner.nextLine();
        System.out.print("Enter PIN: ");
        String password = scanner.nextLine();


        for (User user : users) {
            if (user.userID.equals(userID)) {
                System.out.println("User ID already exists. Try another one.");
                return;
            }
        }

        users.add(new User(userID, password));
        System.out.println("Account Successfully Registered.");
    }

    public static void loginUser() {
        System.out.print("Enter Accoount Number: ");
        String userID = scanner.nextLine();
        System.out.print("Enter PIN: ");
        String password = scanner.nextLine();

        for (User user : users) {
            if (user.userID.equals(userID) && user.password.equals(password)) {
                System.out.println("Login Successful.");
                currentUser = user;
                bankingMenu();
                return;
            }
        }
        System.out.println("\nInvalid credentials. Please try again.");
    }
    public static void bankingMenu() {
        while (true) {
            System.out.println("\n1. Check Balance");
            System.out.println("2. Deposit");
            System.out.println("3. Withdraw");
            System.out.println("4. Logout");
            System.out.print("Enter Choice: ");
            int option = scanner.nextInt();
            scanner.nextLine(); // consume newline

            switch (option) {
                case 1:
                    System.out.println("Current Balance: ₱" + currentUser.balance);
                    break;
                case 2:
                    deposit();
                    break;
                case 3:
                    withdraw();
                    break;
                case 4:
                    System.out.println("Logged out.");
                    currentUser = null;
                    return;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }
    public static void deposit() {
        System.out.print("Enter amount to deposit: ₱");
        double amount = scanner.nextDouble();
        if (amount > 0) {
            currentUser.balance += amount;
            System.out.println("₱" + amount + " deposited successfully.");
        } else {
            System.out.println("Invalid amount.");
        }
    }
    public static void withdraw() { 
        System.out.print("Enter amount to withdraw: ₱");
        double amount = scanner.nextDouble();
        if (amount > 0 && amount <= currentUser.balance) {
            currentUser.balance -= amount;
            System.out.println("₱" + amount + " withdrawn successfully.");
        } else {
            System.out.println("Insufficient balance or invalid amount.");
        }
    }
}
