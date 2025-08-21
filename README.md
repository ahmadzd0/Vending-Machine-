import java.util.HashMap;
import java.util.Scanner;

public class VendingMachine {

    static class Item {
        String name;
        double price;

        public Item(String name, double price) {
            this.name = name;
            this.price = price;
        }
    }

    public static void main(String[] args) {
        // Initialize the vending machine inventory
        HashMap<Integer, Item> items = new HashMap<>();
        items.put(1, new Item("Chips", 1.50));
        items.put(2, new Item("Soda", 2.00));
        items.put(3, new Item("Candy", 1.00));
        items.put(4, new Item("Cookies", 2.50));

        Scanner scanner = new Scanner(System.in);
        double totalMoneyInserted = 0.0;

        System.out.println("Welcome to the Vending Machine!");

        // Display available items
        System.out.println("Available items:");
        for (Integer key : items.keySet()) {
            Item item = items.get(key);
            System.out.printf("%d. %s - $%.2f\n", key, item.name, item.price);
        }

        // Ask user to select an item
        System.out.print("Please select an item by entering its number: ");
        int itemNumber = scanner.nextInt();

        if (!items.containsKey(itemNumber)) {
            System.out.println("Invalid selection. Please restart the machine.");
            return;
        }

        Item selectedItem = items.get(itemNumber);
        System.out.printf("You selected %s, which costs $%.2f.\n", selectedItem.name, selectedItem.price);

        // Ask user to insert money
        while (totalMoneyInserted < selectedItem.price) {
            System.out.printf("Please insert money (current balance: $%.2f): ", totalMoneyInserted);
            double insertedMoney = scanner.nextDouble();
            if (insertedMoney > 0) {
                totalMoneyInserted += insertedMoney;
            } else {
                System.out.println("Invalid amount. Please insert positive money.");
            }
        }

        // Dispense item and calculate change
        System.out.printf("Dispensing %s...\n", selectedItem.name);
        double change = totalMoneyInserted - selectedItem.price;

        if (change > 0) {
            System.out.printf("Please collect your change: $%.2f\n", change);
        }

        System.out.println("Thank you for using the vending machine. Have a great day!");
    }
}
