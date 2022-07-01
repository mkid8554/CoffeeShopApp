/**
 * CS160 Lab - Summer 2022
 * @author Michael Kidane
 * Coffe Shop App
 */

import java.io.*;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Scanner;
import java.util.Stack;
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.BufferedReader;
import java.util.Date;

public class Main {
    static int[] inventory = inventoryReader();

    public static void main(String[] args) throws FileNotFoundException {

        Coffee cof = new BlackCoffee(new BasicCoffee());
        int[] inventory = inventoryReader();
        Scanner CafeApplication = new Scanner(System.in);
        System.out.println("Cafe Application is Running... \nPress 1: Read Inventory \nPress 2: Create Coffee Order" +
                "\nPress 3: Update Inventory \nPress 4: Update log file \nPress 5: Exit the application");
        int input = 0;
        ArrayList<String> Temp;
        Stack<String> stack = new Stack<>();


        while(input != 1){
            switch(CafeApplication.nextLine()) {
                case "1":
                    System.out.println("Current items in the inventory:");
                    inventoryReader();
                    try{

                        File file = new File("Inventory.txt");
                        BufferedReader in = new BufferedReader(new FileReader(file));
                        Scanner scan = new Scanner(in);
                        String line;

                        while(scan.hasNextLine()) {
                            line = scan.nextLine();
                            System.out.println(line);


                        }

                    }catch(IOException e){
                        e.printStackTrace();
                    }
                    System.out.println("Press 1: Read Inventory \nPress 2: Create Coffee Order" +
                            "\nPress 3: Update Inventory \nPress 4: Update log file \nPress 5: Exit the application");
                    break;
                case "2":
                    if(inventory[0] != 0){
                        System.out.println("Coffee order created. Select toppings for the coffee.");
                        CreateOrder(cof);
                    }else{
                        System.out.println("Out of coffee. Visit us later.");
                    }
                    System.out.println("Press 1: Read Inventory \nPress 2: Create Coffee Order" +
                            "\nPress 3: Update Inventory \nPress 4: Update log file \nPress 5: Exit the application");
                    break;
                case "3":
                    inventoryWriter(inventory);
                    break;
                case "4":
                    //logWriter(stack);
                    break;
                case "5":
                    input = 1;
                    break;
                default:
                    System.out.println("Invalid selection, please try again");
            }

        }

        Coffee coffee = new BlackCoffee(new BasicCoffee());
        Temp = CreateOrder(cof);
        ArrayList<Double> price = new ArrayList<> ();


        stack.push(PrintOrder(Temp,price));




        try {
            File file = new File("coffeeshop.txt");
            if(file.createNewFile()){
                System.out.println("File: " + file.getName());
            }else{
                System.out.println("Already exists");
            }
        }catch (IOException e){
            System.out.println("Error");
        }
        try {
            FileWriter writer = new FileWriter("coffeeshop.txt");
            //writer.write(Temp.toString());
            writer.close();
        }catch (IOException e){
            System.out.println("Error");
        }



    }

    /**
     * This method takes in the arraylists that hold the names of the orders and the prices of them and returns a receipt
     * This receipt says what the customer got and how much each item costed
     * @param Item
     * @param price
     * @return receipt
     */
    public static String PrintOrder(ArrayList<String> Item, ArrayList<Double> price){
        StringBuilder receipt = new StringBuilder("RECEIPT:\n");

        double total = 0;
        for (int i=1; i<=Item.size(); i++){
            receipt.append("Item "+ i +": " + Item.get(i-1) + " | cost:" + price.get(i-1) + "\n");

            total = total + price.get(i-1);
        }
        receipt.append("TOTAL COST OF ORDER:" + total);
        System.out.println(receipt);
        return receipt.toString();
    }

    /**
     * This method takes in a coffee object that was created and allows the customer to add toppings to it. Once the
     * customer adds the toppings they want, that order is made a string and put into the string arraylist that is
     * returned in the end (called order).
     * @param coffee
     * @return order
     */
    public static ArrayList<String> CreateOrder(Coffee coffee) {
        Scanner scan = new Scanner(System.in);
        int in = 0;
        String userFeedback;
        ArrayList<String> order = new ArrayList<> ();
        ArrayList<Double> price = new ArrayList<>();

        while (in != 1) {
            System.out.println("Enter the following values to add toppings:\n1.) Milk\n2.) Hot Water\n3.) Espresso\n4.) Sugar\n5.) Whipped Cream\n6.) Nutmeg\ne - to complete order");
            userFeedback = scan.nextLine();
            switch (userFeedback) {
                case "1":
                    if(inventory[1] != 0){
                        inventory[1] = inventory[1] -1;
                        coffee = new Milk(coffee);
                    }else{
                        System.out.println("Out of milk. Try a different topping.");
                    }
                    break;
                case "2":
                    if(inventory[2] != 0){
                        inventory[2] = inventory[2] -1;
                        coffee = new HotWater(coffee);
                    }else{
                        System.out.println("Out of hot water. Try a different topping.");
                    }
                    break;
                case "3":
                    if(inventory[3] != 0){
                        inventory[3] = inventory[3] -1;
                        coffee = new Espresso(coffee);
                    }else{
                        System.out.println("Out of espresso. Try a different topping.");
                    }
                    break;
                case "4":
                    if(inventory[4] != 0){
                        inventory[4] = inventory[4] -1;
                        coffee = new Sugar(coffee);
                    }else{
                        System.out.println("Out of sugar. Try a different topping.");
                    }
                    break;
                case "5":
                    if(inventory[5] != 0){
                        inventory[5] = inventory[5] -1;
                        coffee = new WhippedCream(coffee);
                    }else{
                        System.out.println("Out of whipped cream. Try a different topping.");
                    }
                    break;
                case "6":
                    if(inventory[6] != 0){
                        inventory[6] = inventory[6] -1;
                        coffee = new Nutmeg(coffee);
                    }else{
                        System.out.println("Out of nutmeg. Try a different topping.");
                    }
                    break;
                case "e":
                    inventory[0] = inventory[0] - 1;
                    in = 1;
                    System.out.println("Do you want to add another coffee to this order? - yes or no");
                    Scanner scnr = new Scanner(System.in);
                    if(scnr.nextLine().equalsIgnoreCase("yes")){
                        if(inventory[0] > 0){
                            CreateOrder(coffee);
                        }else{
                            System.out.println("Out of coffee. Visit us later.");
                        }
                    }else{
                        System.out.println("Order completed");
                    }
                    break;
                default:
                    System.out.println("Invalid Input");
            }
        }
        order.add(coffee.printCoffee());
        price.add(coffee.cost());
        System.out.println(coffee.cost());

        return order;
    }

    /**
     * This method reads the file that tells us what is available in the inventory. After reading this file, the method
     * passes the integer values from the text file into the corresponding indexes of array "list." The array is returned.
     * @return list
     */
    public static int[] inventoryReader(){
        int[] list = new int[7];
        int i = 0;

        try{

            File file = new File("Inventory.txt");
            BufferedReader in = new BufferedReader(new FileReader(file));
            Scanner scan = new Scanner(in);
            String line;

            while(scan.hasNextLine()) {
                line = scan.nextLine();

                String numberOnly= line.replaceAll("[^0-9]", "");
                int num = Integer.parseInt(numberOnly);
                list[i] = num;
                i++;

            }

        }catch(IOException e){
            e.printStackTrace();
        }
        return list;

    }

    /**
     * This method takes the text file "Inventory" rewrites the file by writing all the toppings followed by the updated
     * number of items available.
     * @param arr
     */
    public static void inventoryWriter(int[] arr){
        try{

            FileWriter writer = new FileWriter("Inventory.txt",false);

            writer.write("Black Coffee = "+ arr[0] + "\n");
            writer.write("Milk = " + arr[1]+ "\n");
            writer.write("HotWater = " + arr[2]+ "\n");
            writer.write("Espresso = " + arr[3]+ "\n");
            writer.write("Sugar = "+ arr[4]+ "\n");
            writer.write("WhippedCream = " + arr[5]+ "\n");
            writer.write("Nutmeg = " + arr[6] + "\n");
            writer.flush();
            writer.close();
            System.out.println("Successfully updated the inventory.");

        }catch(IOException e){
            e.printStackTrace();
        }

    }

    /**
     * This method reads the stack that has the orders. After reading the stack, it adds the order to the log file.
     * @param stack
     */
    public static void logWriter(Stack<String> stack){
        try{
            FileWriter myWriter = new FileWriter("LogFile.txt", true);
            SimpleDateFormat formatter = new SimpleDateFormat("yyyy-MM-dd 'at' HH:mm:ss z");
            Date date = new Date(System.currentTimeMillis());
            myWriter.write("\n\nWriting orders from stack" + formatter.format(date));
            int i = 0;
            if(stack.isEmpty()){
                System.out.println("Nothing to log - stack is empty");
            }else{
                while(!stack.isEmpty()){
                    myWriter.write(stack.get(i));
                    i++;
                }
                System.out.println("Successfully updated the log file.");
            }

        }catch(IOException e){
            e.printStackTrace();
        }
    }
}
