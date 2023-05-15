import java.util.*;
import java.util.Arrays;

import javax.imageio.plugins.tiff.ExifTIFFTagSet;
import javax.swing.text.AsyncBoxView;

import java.io.*;

class project{

    static double finalPrice;
    static String ItemName;
    static String[] ITEMS;
    static double[] PRICES;
    static double[] DISCOUNT;
    static List<String> selectedItems = new ArrayList<>();
    static List<Integer> selectedQuantities = new ArrayList<>();
    static List<Integer> newUser = new ArrayList<>();
    static Scanner input = new Scanner(System.in);
    static String[] usernames = new String[10]; // array to store usernames
    static String[] passwords = new String[10]; // array to store passwords
    static int userCount = 0; // variable to keep track of number of users

    static {
        try {
            ITEMS = readFile("items.txt").split(",");
            PRICES = Arrays.stream(readFile("prices.txt").split(",")).mapToDouble(Double::parseDouble).toArray();
            DISCOUNT = Arrays.stream(readFile("discounts.txt").split(",")).mapToDouble(Double::parseDouble).toArray();
        } catch (IOException e) {
            System.out.println("Error reading files: " + e.getMessage());
        }
    }

    public static String readFile(String fileName) throws IOException {
        StringBuilder sb = new StringBuilder();
        BufferedReader br = new BufferedReader(new FileReader(fileName));
        String line;
        while ((line = br.readLine()) != null) {
            sb.append(line);
        }
        br.close();
        return sb.toString();
    }

    public static void checkitem() {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter The Item Name To Check The Price : ");
        ItemName = sc.nextLine();

        boolean found = Arrays.stream(ITEMS).anyMatch(t -> t.equals(ItemName));

        if (found) {
            System.out.println(ItemName + " is found.");
            System.out.println("------------------------");
            showPrice(ItemName);
        } else {
            System.out.println(ItemName + " is not found.");
            System.out.println("------------------------");
            System.out.print("Re");
            checkitem();
        }
    }

    public static void showPrice(String ItemName) {
        Scanner input = new Scanner(System.in);
        for (int i = 0; i < ITEMS.length; i++) {
            if (ItemName.equals(ITEMS[i])) {
                System.out.println("The Prices of " + ItemName + " is :" + PRICES[i]);
                System.out.println("Discount of This Item is " + DISCOUNT[i] + "%");
                double Pr = PRICES[i] / DISCOUNT[i];
                finalPrice = PRICES[i] - Pr;
                System.out.println("After Discount The Price of " + ItemName + " " + finalPrice);
                System.out.println("------------------------");
            }
        }
        invalidbutton();

    }

    public static void invalidbutton(){

        System.out.println("Write 1 to Buy the Item");
        System.out.println("Write 2 Cancel the item and Check the price of another Item");
        System.out.println("Write 3 for checkout");
        System.out.println("------------------------");

        int buttonPressed = input.nextInt();

        if (buttonPressed == 1) {
            forbuyItem();
        } else if (buttonPressed == 2) {
            print_item_name();
            checkitem();
        } else if(buttonPressed == 3){
            generateBill(selectedItems, selectedQuantities, PRICES, DISCOUNT);
        }else {
            System.out.println("Invalid button selected Please select valid number");
            invalidbutton();
        }
    }

    public static void forbuyItem() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter the Quantity of the item: ");
        int numberOfItem = sc.nextInt();

        System.out.println(numberOfItem + " " + ItemName + " has been successfully added to your list");
        selectedItems.add(ItemName);
        selectedQuantities.add(numberOfItem);

        System.out.println("Write 1 to buy another item");
        System.out.println("Write 2 for checkout");

        int buttonPressed = sc.nextInt();
        if (buttonPressed == 1) {
            print_item_name();
            checkitem();
        } else if (buttonPressed == 2) {
            generateBill(selectedItems, selectedQuantities, PRICES, DISCOUNT);
        } else {
            System.out.println("Invalid button selected");
        }
    }

    public static void generateBill(List<String> items, List<Integer> quantities, double[] prices, double[] discounts) {
        System.out.print("\033[H\033[2J");
        System.out.flush();

        double totalAmount = 0;
        System.out.println("***********************");
        System.out.println("        BILL           ");
        System.out.println("***********************");
        System.out.println("Item\tQuantity\tPrice");
        for (int i = 0; i < items.size(); i++) {
            String itemName = items.get(i);
            int quantity = quantities.get(i);
            double price = prices[Arrays.asList(ITEMS).indexOf(itemName)];
            double discount = discounts[Arrays.asList(ITEMS).indexOf(itemName)];
            double discountedPrice = price - (price * (discount / 100));
            double amount = discountedPrice * quantity;
            System.out.println(itemName + "\t" + quantity + "\t\t" + amount);
            totalAmount += amount;
        }
        System.out.println("-----------------------");
        System.out.println("Total amount:\t\t" + totalAmount);
        System.out.println("Thank you for shopping!");
        System.out.println("-----------------------");

        System.out.println("Write 1 for edit the bill ");
        System.out.println("Write 2 for print the bill");
        int button = input.nextInt();

        if(button == 1){
            editQuantity();
        }
        else{
           return;
        }
    }

    public static void editQuantity() {
        System.out.println(" _________________________________________");
        System.out.println("Sno.\tItem\tQuantity");
        for (int i = 0; i < selectedItems.size(); i++) {
            System.out.println(i + 1 + ".\t" + selectedItems.get(i) +"\t"+ selectedQuantities.get(i) );
        }
        System.out.print("Enter the Serial number of the item you want to edit the quantity of: ");
        int itemIndex = input.nextInt() - 1;
        if (itemIndex < 0 || itemIndex >= selectedItems.size()) {
            System.out.println("Invalid item number.");
            return;
        }
        String itemName = selectedItems.get(itemIndex);
        System.out.print("Enter the new quantity of " + itemName + ": ");
        int newQuantity = input.nextInt();
        if (newQuantity <= 0) {
            System.out.println("Invalid quantity.");
            return;
        }
        selectedQuantities.set(itemIndex, newQuantity);
        System.out.print("\033[H\033[2J");
        System.out.flush();
        System.out.println("The final Bill is :");  
          generateBill(selectedItems, selectedQuantities, PRICES, DISCOUNT);
        
    }

    public static void main(String[] args) {
        boolean exit = false;

        while (!exit) {
            System.out.println("1. Register new user\n2. Login\n3. Exit");
            int choice = input.nextInt();

            switch (choice) {
                case 1:
                    
                    newuser();
                    break;
                case 2:
                    alreadyuser();
                    break;
                case 3:
                    exit = true;
                    break;
                default:
                    System.out.println("Invalid choice. Please enter a number between 1 and 3.");
                    break;
            }
        }
    }

    public static void alreadyuser() {
       

        System.out.print("Enter username: ");
        String user = input.next();
        System.out.print("Enter password: ");
        String pass = input.next();

        for (int i = 0; i < userCount; i++) {
            if (usernames[i].equals(user) && passwords[i].equals(pass)) {
                System.out.print("\033[H\033[2J");
                System.out.flush();
                System.out.println("THANK YOU " + user + " LOGIN SUCCESSFULLY");
                print_item_name();
                checkitem();
                return;
            }
        }

        System.out.println("Incorrect username or password.");
        alreadyuser();
    }

    public static void newuser() {
        System.out.print("\033[H\033[2J");
        System.out.flush();
        if (userCount >= 10) {
            System.out.println("Maximum number of users reached.");
            return;
        }

        System.out.print("Enter username: ");
        String user = input.next();
        System.out.print("Enter password: ");
        String pass = input.next();

        System.out.println("Thankyou for Registration Now you Login With your username and password");
        for (int i = 0; i < userCount; i++) {
            if (usernames[i].equals(user) && passwords[i].equals(pass)) {

                System.out.println("You have already registered Please login!");
            }
        }
        usernames[userCount] = user;
        passwords[userCount] = pass;
        userCount++;

    }

    public static void print_item_name(){
        System.out.println("List of Items:");
        for (String item : ITEMS) {
            System.out.println("- " + item);
        }
        
    }
}
